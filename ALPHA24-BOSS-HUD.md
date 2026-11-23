# Enhanced alpha.24 – Remnant-Bossleisten

Veröffentlicht nach bestätigtem Enhanced-Sandbox-Test, Spielversion 1002133.
Core bleibt alpha.17 / Sequenz 16. Der laufende Nutzerclient blieb bei der
Veröffentlichung geöffnet.

## Darstellung und Einstellungen

- Zentrierter Name; symmetrischer Platz für die vorhandene Bossauswahl. Lange
  Namen werden zunächst verkleinert und nötigenfalls mit Auslassung gekürzt.
- Bekannte Itemklasse kleiner unter dem Namen. Der Platz bleibt bei noch
  unbekannter Klasse frei, damit später eintreffende Informationen nichts verschieben.
- Blaue Umhüllung für bekannte Schild-/Schutzreserven, von rechts nach links
  abnehmend und unabhängig von HP. Die bisherige Aktiv-Meldung entfällt; Icons bleiben.
- Bei mehreren Schutzschichten gilt dieselbe verbrauchs- und erneuerungssichere
  Summierung wie in der Staffel. Ohne bekannte Kapazität keine scheinbar volle Leiste.
- XC erhält standardmäßig einen kupferroten, SC einen violetten Rahmen. Die
  Rahmenfarbe ist je Typ aus fünf Farben wählbar; HP bleibt rot und Schutz blau.
- Dezente Randanimation; optional Klassenstil. Sechs wiederverwendete native
  Elemente, maximal etwa 30 Aktualisierungen pro Sekunde, nur an sichtbaren XC/SC.
  Keine neuen Shader, Partikel, Materialien oder Hintergrund-Threads.
- Bestätigter Landeschutz/Unverwundbarkeit verwendet das goldene Originalsymbol
  mit Ring aus `shop_icon_hitprotection.png` (dritte 32×32-Kachel), wie vom Nutzer
  ausgewählt; während des Texturladens eine einfache Schutzkontur.
  Das ist ein vorhandenes Schutzsymbol, kein gesondert belegtes Landeschutz-Icon.
  Der Effekt wird nicht als verbrauchbare Schildreserve gezählt.
- Ein Linksklick auf Name oder Lebensbalken wählt den angezeigten Boss direkt aus.
  Effektsymbole öffnen weiterhin Details, die Bossauswahl schaltet nur die Anzeige um.
  Keine automatische Zielauswahl oder Komponentenaktivierung; kein Tastaturfokus
  auf der Klickfläche. Verschwundene, tote oder nicht mehr sichtbare Ziele sowie
  Klicks über einen Ziel-/Szenenwechsel hinweg werden verworfen.

Unter **Forge → Anzeige → Bossleisten**: Bossauswahl, bisherige Treffer-/Auftritts-
animationen und Musik, Schutzmodus (aus/Umhüllung/mit Prozent), Itemklasse,
Randanimation (aus/dezent/Klassenstil), XC- und SC-Farben. Übernehmen/Verwerfen
gilt für alle Optionen. Reduzierte Bossanimationen unterdrücken auch die Randanimation.
Die Staffel hat weiterhin ihre eigene unabhängige Schutzeinstellung.

## Daten und Grenzen

Keine zusätzlichen Hintergrund-Datenabfragen. `ain.JD()` liest in der geprüften Originalbasis
1002133 direkt `skullItemDropCategory` vom empfangenen NPC. Nur die neun bekannten
nativen Kategorien werden angezeigt. Keine Herleitung aus Namen, Effekten oder
Ausrüstung, kein Aufruf von `ach.getSkullCarrierContainer()` und kein Öffnen des
Informationsfensters. Fehlende Daten bleiben unsichtbar, auch nach Ziel-/Szenenwechsel.

Ein ausdrücklicher Klick verwendet die vorhandene Zielauswahl des Originalclients
(`tools.try.do(aeo, ee)`). Deren übliche Meilensteinmeldungen bleiben erhalten.
Der Helfer liest ausschließlich bereits empfangene Objekte und ruft weder
Komponenten noch einen Angriffs- oder Datenlade-Endpunkt auf.

Schutz verwendet den bestehenden `OpsEffects.shields`-Pool und die bestätigten
`uu`-Reservefelder. Landeschutz/Unverwundbarkeit wird ausschließlich für `uw`
mit übereinstimmenden Visuals `StatusEffectInvulnerability` oder
`buff_invulnerable_loop_FX.model` erkannt. Diese Namen sind in Originalclient bzw.
Originalressourcen belegt. Zusätzlich ist seit 23.11.2026 die tatsächlich empfangene
XC-Anteer-Signatur bestätigt: `uw`, Producer `propertyAIAction_protection`, Level 0,
Visual `StatusEffectInvulnerability`, fehlendes/leeres Enemy-Visual. Nur diese exakte einseitige
Variante wird ebenfalls erkannt. Abweichende Producer, Level, Visuals oder Klassen
bleiben ungeklärt; keine pauschale Umdeutung von E. Restzeiten bleiben ohne bestätigten lokalen Timer unbekannt.

`bossbar.json` im manuell exportierten Forge-Diagnosebericht zählt fehlende Klassen,
unbekannte Schutzreserven und erkannte/unzugeordnete Effekte. Maximal 32 technische
Effektsignaturen; keine Pilotennamen, Konto-IDs, Positionen oder automatische Übertragung.
Die Zähler zählen Beobachtungen, nicht einzigartige Aktivierungen.

## Sandbox-Prüfung

1. XC/SC mit und ohne bekannte Klasse; Klasse trifft nachträglich ein, Zielwechsel.
2. Schild/Schutz voll, halb, verbraucht, neu angewendet, mehrere Schichten und
   fehlende Kapazität; HP unabhängig davon beschädigt/geheilt.
3. Landeschutz am betroffenen XC: bestätigte einseitige AI-Signatur zeigt die
   goldene PG-Schildsymbol; nach Entfernen und Ersetzen des Effekts keine alten Iconteile.
   Weitere unbekannte Signaturen erst nach lokalem Nachweis ergänzen.
4. Name/HP anklicken: genau dieser Boss wird anvisiert. Effekte und Überlauf
   öffnen nur Details, Bossauswahl wechselt nur die Anzeige. Maustaste außerhalb
   loslassen, Rechtsklick, Despawn und Szenenwechsel dürfen keine Auswahl auslösen.
   Lange Namen und HUD-Skalierung prüfen.
5. Alle neuen Einstellungen übernehmen/verwerfen und erneut öffnen.
6. Randanimation reduzieren/abschalten, Fenster/Szene wechseln; MN/DL weiterhin
   ohne Bossintro, Queen/Sirius behalten ihre eigene Identität.

Der Nutzer hat den R3-Sandbox-Stand mit D3D11 bestätigt. Die obige Liste bleibt
eine Anleitung für weitere Zustandsprüfungen; nicht jeder Punkt wurde einzeln
als live geprüft bestätigt. 62 Editionsgates, 22 Negativkontrollen, 61 Stil- und
32 Zielauswahlprüfungen sowie je 3163 native UI-Prüfungen mit D3D9/D3D11 bestanden.
Dieses Enhanced-Feature ist kein Fix der noch offenen Terrainhelligkeit oder
anderer nativer Absturzursachen und enthält keine neue FPS-/RAM-Zusage.
