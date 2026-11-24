> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Enhanced alpha.18: mögliche Baupläne im Scanner

Enhanced-Update für Spielbasis **1002133**, ausgehend von alpha.17.
Veröffentlichung am 21.11.2026 beauftragt. Core bleibt alpha.17; die neue Funktion
gehört vollständig zu Enhanced. Der Enhanced-Kanal erhält Sequenz 99.

## Bedienung

Nach einem erfolgreichen NPC-Scan zeigt die rechte Spalte des vorhandenen
Scanfensters mögliche Baupläne und den eigenen Sammelstand. Native PG-Widgets,
ursprüngliche Vorschau, Fenstergröße und Schließen-Funktion bleiben erhalten.
Enthält der Originalscanner Informationen, bleiben diese im zweiten Reiter
„Informationen“ erreichbar. Die Liste ist mit dem Mausrad scrollbar.
Lange Namen werden mit der tatsächlichen Schriftbreite umgebrochen, auch an
Bindestrichen und innerhalb überlanger Wörter. Jede Zeile wächst mit ihrem
Text; die Teilezahl steht mit Abstand darunter. Es werden keine Namensbestandteile
gekürzt und keine globalen Schrift-/HUD-Einstellungen geändert.
Einzelne und kurze Listen beginnen direkt unter der Überschrift. Ihre Zeilen
nutzen die volle verfügbare Breite; Platz für einen Scrollbalken wird erst bei
wirklichem Überlauf berücksichtigt. Längere Listen bleiben scrollbar.
Einzelne und kurze Listen beginnen direkt unter der Überschrift. Ihre Zeilen
nutzen die volle verfügbare Breite; Platz für einen Scrollbalken wird erst bei
wirklichem Überlauf berücksichtigt. Längere Listen bleiben scrollbar.

Unter **Forge → Anzeige → HUD & Grafik**:

- **Scanner: mögliche Baupläne** — standardmäßig ein.
- **Scanner: nur fehlende Baupläne** — standardmäßig aus; verbirgt ausschließlich
  nachweislich vollständige Baupläne.

Einstellungen werden erst mit „Übernehmen“ gespeichert. „Verwerfen“ und Schließen
verwerfen den Entwurf. Unbekannter Besitz erscheint als **—/N**, nicht als 0/N.
Bekannte Teilezahlen stammen aus dem eigenen Profil und haben Vorrang vor der
Referenz. Vollständige Baupläne sind grün markiert. Die Liste beschreibt mögliche
Drops; sie enthält weder Dropchancen noch eine serverseitige Dropgarantie.

## Zuordnung und Quellen

4.553 geprüfte Zuordnungsregeln für 1.288 Referenzbaupläne aus dem bereits
gepinnten Prelude-Snapshot vom 31.10.2026. Die Fakten werden beim Bauen mitgeliefert;
während des Spiels gibt es keinen Webseitenabruf. Quellenhashes, ausgenommene
Zeilen und nicht eindeutig zuordenbare Fälle stehen in
`project/client-scan-drops/catalog-provenance.json`.

Normale Zuordnung: kanonischer Planet, native Gegnerkennung/Faktion und sichtbarer
Rang (`tO()+1`). Kein Vergleich mit übersetzten Anzeigenamen. Sirius verwendet
zusätzlich die Gegnerklasse und die für den aktuellen Planeten empfangenen
Blueprint-Schlüssel. Es werden nur deren Schnittmenge und passende Ränge gezeigt.
Grundlage der Sirius-Klassen ist die
[Prelude-Klassentabelle](https://www.c3709203.myzen.co.uk/PG/Sirius_drop.html);
Grundlage der Einzelregeln sind die in der Provenienz aufgeführten
[Prelude-Bauplanseiten](https://prelude-myzen.co.uk/).

**Giza, Soris und Amarna sind ausgeschlossen**, auch wenn eine andere sichtbare
Identität gesetzt ist. Spieler, Remnant-Träger sowie nicht eindeutig zuordenbare
Event-, Missions- und Sonderbedingungen werden nicht als normale Dropquelle
geraten. Death-Squad-Sonderrollen lassen sich aus der Typkennung allein nicht
sicher von normalen starken Einheiten unterscheiden; solche Sonderregeln sind
noch nicht zugeordnet. Die normalen schwachen/mittleren/starken Sirius-Klassen
und die eindeutig bezeichneten großen Kommandanten sind enthalten. Fehlende
Zuordnung bedeutet nicht, dass ein Gegner nichts fallen lässt.

## Laufzeit und Abfragen

- Scanner-Hook ausschließlich in Enhanced: `aox.do(ee,aeo,nm)` ruft die unveränderte
  Originalmethode und danach die Zusatzanzeige auf; die Wrapper-Argumente bleiben
  dabei gültig. Native `aix`-Ziele werden auch für die Zusatzanzeige aufgelöst.
  Dazu Aufräumen in `aox.bM(ee)`. Original-/Eingabehash und exakt zwei
  Änderungen sind in `patches/scan-drops.tsv` gesperrt. Die vorhandenen Schutzprüfungen
  für verspätete Scannerantworten und die Lebensdauer der Modellvorschau bleiben
  erhalten. Unerwartete Eingaben brechen den Build ab.
- Besitzabfrage: derselbe `ComfortBlueprints`-Cache und dieselbe Warteschlange wie
  im Bauplanfenster. Nur bei geöffnetem, aktiviertem Scan mit zugeordneten Drops;
  ein laufender Auftrag, automatisch frühestens fünf Sekunden nach dessen Abschluss erneut.
  Keine Abfrage pro Listeneintrag. Antworten und Cache sind an den Piloten gebunden.
- Sirius: zuerst bereits empfangener `aik`-Datensatz für exakt die aktuelle Zone.
  Sonst die originale `getSingularityPlanetDescriptionArgs`-Abfrage für die Zone
  des eigenen Piloten. Höchstens eine erfolgreiche Abfrage pro Besuch, maximal
  drei Versuche mit mindestens 30 Sekunden Abstand nach Fehlschlägen. Keine neue
  Abfrage bei ausgeschalteter Anzeige oder unbekannter/ausgeschlossener Klasse.
  Späte Antworten nach Zonen-/Pilotenwechsel werden verworfen. Keine NPC-/Loot-
  Serverabfrage und keine automatischen Scans oder Spielaktionen.
- UI-Arbeit nur im vorhandenen GUI-Thread. Profile werden nur bei neuer Revision
  aufbereitet. Reine Zählerupdates erhalten Scrollposition und Reiter; native
  Zeiger werden nicht über Frames aufbewahrt. Fehler der optionalen Anzeige
  stellen die ursprüngliche Scanner-Spalte wieder her.

## Sandbox-Abnahme

Automatische Prüfungen und Paketbeleg: siehe
[Prüfstand](../verification/RELEASE-STATUS-0.2-alpha.18.md). Normale Gegner, echte BP-Namen und
Teilezahlen sind in den vom Nutzer gezeigten D3D11-Scans sichtbar. Die letzte
Ausrichtung wird in nativen D3D9-/D3D11-Proben geprüft; der laufende Spielclient
bleibt beim vorherigen Namensfix. Eine vollständige Sirius-Abnahme ist offen.
Der erste private Start deckte einen `VerifyError` im Scanner-Hook auf.
Der korrigierte Wrapper erhält die Original-Stackframes; `ScanDropTests` lädt
die echte Scannerklasse unter `-Xverify:all`. Der erste Kandidat wird abgelehnt.

Die folgende Liste bleibt der weiterführende manuelle Testplan:

1. Normalen Gegner scannen; zwei Ränge und zwei Planeten vergleichen. Beispiel:
   Avenger Rang 23 auf Lustra gegenüber angrenzendem Rang und Terasa.
2. Blaue, goldene und antike Baupläne mit unbekanntem, teilweisem und vollständigem
   Besitz prüfen; Filter und Übernehmen/Verwerfen einschließlich Neustart testen.
3. Auf Sirius unterschiedliche Klassen und zwei Planeten mit verschiedenen
   Angeboten scannen. Kurz vor einer Antwort Fenster schließen, Gegner wechseln
   und Orbit betreten: keine alten Daten im nächsten Fenster.
4. Giza, Soris, Amarna, Spieler und Remnant-Träger: originale Scanneransicht,
   keine neue Dropabfrage. Sonderrollen ohne gesicherte Zuordnung nicht als
   vollständig unterstützt bewerten.
5. Lange Liste scrollen, ursprüngliche Informationen öffnen, HUD-Größe ändern;
   Komponenten-Tasten müssen nach der Bedienung weiter funktionieren.

Gegenüber dem 32-Bit-Client ist dies eine optionale Forge-Zusatzanzeige. Es wird
keine geänderte Dropmechanik, höhere Droprate oder Splitscreen-Freigabe behauptet.
