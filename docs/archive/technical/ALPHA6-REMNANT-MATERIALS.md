> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Remnant-Auftritte und Partikelmaterialien — alpha.6

Privater Teststand vom 16.11.2026. Keine Veröffentlichung oder Kanalaktivierung.

## Enhanced: Auftritte nur für große Remnant-Träger

`BossTargets.carrier` erkennt empfangene Träger anhand von `skullCarrierType` oder
`skullCarrierID`. Diese Erkennung gilt auch für MN und DL und bleibt für deren
Bossleiste und Effektanzeige erhalten. Bisher wählte `BossIntroStyle.forBoss` für
jeden solchen Träger den Remnant-Auftritt.

`BossIntroStyle.appearanceAllowed` lässt bei Remnants jetzt ausschließlich die
Präfixe `XC-` und `SC-` mit einem nachfolgenden Namen zu. Der empfangene Remnant-Typ
bleibt Voraussetzung; ein gleichnamiger Spieler wird dadurch kein Boss. Unbekannte,
leere und noch nicht aufgelöste Remnant-Namen erhalten keinen Auftritt.
Die Regel gilt für die Titel-/Musiksequenz, die HUD-Ankunftsanimation und den
älteren 3D-Ersatzimpuls in `BossAppearance`. Königin und Sirius behalten ihre Regeln.
Sichtbarkeit, Tarnung, erneutes Erscheinen und die Auswahl der Bossleiste bleiben erhalten.

Das ist eine Korrektur einer Enhanced-Zusatzfunktion, keine Funktion des
Original32-Clients. Core enthält weiterhin keine Bossauftrittsklassen oder -Hooks.

## Beide Editionen: Materialnamen bis zum tatsächlichen Laden erhalten

Im untersuchten Spielprotokoll fehlte beim Anlegen von `beacon.aggro.buff` das
Material `buff.taunt.icon`, obwohl Materialskript und Originaltextur im Cache
vorhanden waren. Dieselbe Meldung betraf `smoke.partial01`, `laser.projectile03`
und `lava.specles` in anderen Partikeleffekten.

Der ältere Enginepfad speichert den gewünschten Namen und lädt das Material beim
Einrichten des Renderers. OGRE 14 ersetzte einen zu früh aufgelösten Namen sofort
durch `BaseWhiteNoLighting`. Beim Kopieren der Partikelvorlage wurde anschließend
dieser Ersatzname weitergegeben. Der spätere Materialimport konnte das nicht
mehr reparieren; statt des Icons erschien die eingefärbte, untexturierte Fläche.

Der gepinnte OGRE-Patch korrigiert `OgreParticleSystem.cpp`:

- Der gewünschte Name und die Ressourcengruppe bleiben auch in kopierten Vorlagen erhalten.
- Bereits eingerichtete Renderer binden das Material nach dem Laden neu.
- Solange es fehlt, wird der Partikeleffekt nicht in die Renderwarteschlange gestellt.
  Simulation und Lebensdauer laufen weiter; es wird kein Ersatzrechteck gezeichnet.
- Wiederholte Suche und Prüfung auf entfernte/neu erzeugte Materialien sind auf
  einen Versuch je 250 ms pro aktivem System begrenzt, unabhängig von der Bildrate.
  Es gibt keine zusätzlichen Serverabfragen.
- Erst bei tatsächlicher Verwendung wird gewarnt, einmal pro fehlendem Material
  und Instanz bis zur erfolgreichen Wiederherstellung. Vorlagen erzeugen keine
  voreilige Warnung. Neue Zuweisungen werden sofort aufgelöst.
- Der Zustand wird über die bereits vorhandenen `UserObjectBindings` besessen.
  Das exportierte Klassenlayout und die DLL-Exports bleiben unverändert.

Zusätzlich kopiert `Entity::clone` in `OgreEntity.cpp` die tatsächliche
`MaterialPtr` eines Subobjekts statt nur den Namen erneut nachzuschlagen.
Damit bleiben Materialgruppe und dynamische Schiffsfärbung erhalten, auch wenn
das bereits verwendete Material nicht mehr in der Namensliste steht. Das behebt
auch die beobachteten Materialwarnungen beim Erzeugen der Bossauftritt-Kopie.

Die Änderungen betreffen den gemeinsamen D3D11-Enginepfad. D3D9-DLLs bleiben
bytegleich zur alpha.5. Originaltexturen, Materialskripte, Farben, Blending und
Spielwerte werden nicht ersetzt. Der ursprüngliche Ladevertrag wurde am älteren
Enginequelltext verglichen; eine neue Original32-Spielsitzung wurde nicht durchgeführt.

## Prüfung und Grenzen

Der neue native Test `regressions/particle-materials/ParticleMaterialsProbe.cpp`
prüft echte Partikelvorlagen, Billboard-Bildausgabe, Ressourcengruppen, verspätetes
Laden, Neuzuweisungen, Ressourcen-/Renderer-Neuerzeugung, dynamische Schiffskopien
und acht Szenenwechsel. 45 Prüfungen bestehen; die unveränderte alpha.5 schlägt
in derselben Gegenprobe bei 39 Prüfungen fehl. Die Bilder verwenden selbst
erstellte Testtexturen, keine veröffentlichten Originalassets.

76 Bossprüfungen einschließlich XC/SC, MN/DL, unbekannter Namen und unveränderter
HP-/Effektberechtigung bestehen. Beide Editionen bestehen die 40 gemeinsamen,
Java- und nativen Oberflächenprüfungen sowie sechs Negativkontrollen. Zusätzlich
bestehen 160 Material-/Shader-Bereinigungszyklen und 49 Overlayprüfungen;
elf Calon-Himmelsbilder und fünf Wasserbilder bleiben gegenüber dem Referenztest gleich.

Belege mit Quell-, DLL- und Testhashes: `distribution/tests/remnant-materials-alpha6.json`
und `distribution/tests/editions-0.2-alpha.6-readiness.json` in der Quellrepo.
Die Live-Abnahme von Aggrobeacon und Remnant-Auftritten steht noch aus.
Andere ursprüngliche Skriptwarnungen (z. B. Wolken-/Hangarsyntax) sind damit
nicht pauschal als behoben eingestuft. Weitere GPUs, Wine und lange Spielsitzungen
sind gesonderte Tests. Es gibt keine neue Sicherheitsfunktion oder FPS-/RAM-Zusage.
