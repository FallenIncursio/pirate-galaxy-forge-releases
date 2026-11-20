# Alpha.17: Zielanzeigen und UI-/Audio-Diagnose

Core und Enhanced, Spielbasis 1002133, Starter 17. Die im ersten Sandbox-Test
gemeldete Namensregression wurde nachgebessert. Der Nutzer hat den neuen
Enhanced-Sandbox-Stand bestätigt und alpha.17 zur Veröffentlichung freigegeben.

## Ursache und gemeinsame Korrektur

Die untersuchte normale alpha.16-Sitzung enthielt zwei NullPointerExceptions in
`com.splitscreen.awa.PQ`. Die Klasse entspricht vor dieser Änderung bytegenau
dem Original der Spielbasis 1002133. Ihre Lebensbalken-Aktualisierung prüft den
Lebensbalken, greift aber ungeprüft auf den optionalen Schildbalken zu. Der
benachbarte Schildpfad setzt umgekehrt einen vorhandenen Lebensbalken voraus.
Bei abgebauten oder unvollständigen Zielanzeigen ist das nicht garantiert.

`TargetDisplayFixes` korrigiert beide Zugriffe unabhängig voneinander. Eine
Zielanzeige wird vor ihrem Abbau als geschlossen markiert. Bereits eingereihte
PropertyMap-Callbacks bearbeiten keine geschlossenen Anzeigen. Vor fertigem
Layout werden ausschließlich native Lebens-/Schildzugriffe zurückgehalten;
initiale Zustandsmeldungen für Namen, Symbole und Layout bleiben erhalten.
Initiale direkte Balkenupdates während des Layoutaufbaus bleiben möglich.
Die vier Änderungen an `awa` und die weiteren Diagnosehooks sind durch
Eingabehashes und erwartete Änderungszahlen in `patches/edition-fixes.tsv`
abgesichert. Core und Enhanced erhalten dieselben gemeinsamen Klassen.

Zwei reine Existenzprüfungen in `gm` verwenden die bereits vorhandene native
Widget-Registry. Ein erwartungsgemäß fehlendes Widget erzeugt dadurch keine
MyGUI-Fehlermeldung mehr. Erforderliche Widgetzugriffe und echte native Fehler
werden nicht pauschal unterdrückt.

## Sandbox-Nachbesserung: abgeschnittene Namen vor der Zielauswahl

Der erste private alpha.17-Kandidat verwarf mit seiner Bereitschaftsprüfung
auch `rank`, `selected`, `pvpactive`, `forcedpvp`, `inconquest`, `battlemode`,
`fleet` und `squadron`. Diese ursprünglichen Callbackzweige greifen gar nicht
auf native Widgets zu, sondern setzen nur das Änderungsflag `awa.cnM`.
Dadurch fehlten im ersten sichtbaren Frame `eS` (Symbole) und `eT` (Breite).
Das spätere Einblenden setzte zwar den Text über `eQ`, beließ aber die kleine
Vorlagenbreite und die Standardsymbole. Erst ein Klick setzte das Flag erneut.
Die übermittelten Bilder zeigen entsprechend abgeschnittene gelbe Namen und
übrig gebliebene Standardsymbole; nach Auswahl sind die Namen vollständig.

Der isolierte Vergleich führt dieselben acht Original-Callbacks vor dem
Layoutaufbau aus: Spielbasis 1002133 erhält **8/8** Änderungen, der verworfene
alpha.17-Kandidat **0/8**. Die Korrektur beschränkt die Bereitschaftsprüfung
auf `hitpoints`/`power`; der Schutz bereits geschlossener Anzeigen gilt
weiter für alle Callbackzweige. Keine künstlichen Klicks, kein ständiges
Neuberechnen der Namen und keine zusätzlichen Serverabfragen.

Die gemeinsame Klasse verwaltet Schiffsbeschriftungen allgemein. Auch Clan-,
Staffel-, Freund-, PvP- und NPC-Anzeigen können vom fehlenden ersten Layout
betroffen sein; die Allianz ist kein eigener fehlerhafter Serverdatenpfad.
Die Namens-/Beziehungslogik, Farben und Spielserverantworten werden nicht
umgeschrieben. Tests prüfen beide Callback-Einstiege in drei Aufbauphasen,
späte Änderungen und geschlossene Anzeigen. Native Tests laden das originale
`targetinfo.layout` und prüfen lange/farbige Namen, Umlaute, Symbolbereinigung,
NPC-/Spieler-Sichtbarkeit und stabile Breiten vor/nach einer Auswahl.
Die Tests isolieren die Anzeige; eine reale Allianz-/Clan-/Staffelsitzung
bleibt eine gesonderte Gameplay-Abnahme. Der Nachfix besteht 62 Editionssuites
und sechs Negativkontrollen, mit 93 Zielanzeigenchecks je Edition und nativen
Namenslayouts unter D3D9/D3D11. Beleg:
`distribution/tests/target-name-regression-alpha17.json`.

## Diagnose und Bedienung

Im Starter über **Live-Logs** beziehungsweise **Diagnose** öffnen; während des
Spiels bleibt der Zugang über das vorhandene Taskleistensymbol erreichbar.
Ein Export enthält nun zusätzlich zusammengefasste UI-/Audio-Ereignisse:

| Ereignis | Bedeutung |
| --- | --- |
| `ui-missing` | Ein tatsächlicher Widgetzugriff lieferte kein Objekt; bekannte strukturelle Namen werden zusammengefasst. |
| `ui-probe-failed` | Die native Registry konnte für eine Existenzprüfung nicht gelesen werden. |
| `target-stale` | Eine Aktualisierung wurde für eine geschlossene/unfertige Zielanzeige verworfen. Das ist ein Diagnosezähler, kein Absturz. |
| `audio-create-failed` | Der native Soundlader lieferte keinen Sound; enthalten sind Dateiname, Effekt/Stream und Schleife/einmalig. |
| `diagnostic-overflow` | Weitere unterschiedliche Ereignisse wurden in einem Sammelzähler begrenzt. |

Beispiel: `audio-create-failed · autodetect.effect.once.laser.ogg · 45`.
`autodetect` bezeichnet die tatsächlich verwendete automatische Ressourcensuche,
nicht eine angeblich bekannte Fehlergruppe. Ob eine Datei fehlt, die Dekodierung
scheitert oder ein anderes Audioproblem besteht, muss anschließend geprüft werden.
Diese Version ändert die Soundwiedergabe und die ursprüngliche Fehlerbehandlung
des Soundladers nicht.

Die Hooks führen keine Datei- oder Netzoperationen aus. Der vorhandene Watchdog
übermittelt alle zwei Sekunden nur veränderte Gesamtzähler. Höchstens 64
verschiedene Schlüssel und 192 kombinierte Starterereignisse bleiben erhalten.
Zähler verdrängen weder die gespeicherte Fehlerphase noch den gesamten
Startverlauf und gelten nicht als Ladefortschritt. Der Starter akzeptiert nur
das bestehende sitzungsgebundene Protokoll. Schema 4 bleibt kompatibel.

Widgetnummern werden normalisiert; unbekannte Namen werden `other`. Soundpfade
und URLs werden `external-or-unknown`. Keine Rohlogs, Chat- oder Anmeldedaten,
keine zusätzlichen Spielserverabfragen, kein automatischer Berichtversand.
Die Diagnose benötigt Starter 17; deshalb gehört der neue Starter zum Kandidaten.

## Materialprüfung: Befunde, keine vorgetäuschte Behebung

Die sieben protokollierten Parserfehler gehören zu bereits dokumentierten
Originaldateien. Ihre Cachehashes stimmen mit der vorhandenen Legacy-Policy
überein; das ist kein Nachweis für einen beschädigten Download.

Für `Skyscraper.ground` wurde dagegen ein konkreter Parserunterschied reproduziert:

| Prüfung derselben Originaldeklaration | Techniken / unterstützte Techniken |
| --- | --- |
| D3D9 | 9 / 9 |
| D3D11 mit aktuellem Legacy-Listener | 0 / 0 |
| D3D11, isolierte Kopie mit Leerzeichen nach dem Vererbungsdoppelpunkt | 9 / 9 |

Die Deklaration in `spacestation_gemini_02.material` verwendet
`Skyscraper.ground :Abstract.Material_SkyScraperSimple`. Die bestehende
Normalisierung in `LegacyMaterials14.cpp` behandelt diese Schreibweise bisher
nur bei Shop-Icons. Der isolierte Gegenversuch ändert ausschließlich diese
Schreibweise und den Testnamen, keine Originaldatei auf der Platte. Die
Elternmaterialien waren in beiden D3D11-Versuchen vorhanden (jeweils 9 / 9).

Empfohlener separater Rendererfix: zusammengezogene Vererbungsdoppelpunkte für
Materialdeklarationen allgemein normalisieren, bevor die Eltern gesammelt werden;
anschließend Originalskripte unter beiden Renderern und die Stationsszene prüfen.
Alpha.17 tauscht dafür noch keine native Renderer-DLL aus. Der Befund beweist
keine Ursache der weiterhin offenen kamerabhängigen Planetenhelligkeit.

Für `Spacestation.gemini.groundfog`, `Spacestation.gemini02.groundfog` und
`lava_flow` fand die Suche im verfügbaren Cache keine Materialdefinition.
Auch die isolierte Probe findet sie nicht. Das beweist keine globale Abwesenheit
auf dem Spielserver: weitere Ressourcen und dynamische Gruppen bleiben möglich.
Keine geratenen Ersatzmaterialien oder globalen Aliasänderungen eingebaut.

## Prüfungen und anschließender Sandbox-Test

Automatisch geprüft werden Original-gegen-Fix-Negativkontrolle, tatsächliche
MyGUI-Balken mit jeweils fehlendem Gegenstück, verspätete Callbacks, begrenzte
und parallele Zähler, Datenschutz, Export und Schema-4-Annahme. Der native
Audiotest erzeugt dreimal eine absichtlich fehlende Ressource und erwartet den
Gesamtzähler 3, mit Null-Audiotreiber in einem eigenen Prozess.

Für den anschließenden Spieltest: häufig zwischen Zielen mit/ohne Schild wechseln,
Ziele zerstören/aus der Reichweite fliegen und den Planeten wechseln. Lebens- und
Schildbalken müssen unabhängig korrekt bleiben. Anschließend im Starter den
Diagnoseexport prüfen. Die fehlenden Sounds der realen Sitzung lassen sich erst
mit den neuen Ressourcennamen gezielt zuordnen; es wird nicht behauptet, dass
alle bisherigen 45 Soundmeldungen bereits behoben seien.

Der normale Nutzerclient wird für diese Vorbereitung weder beendet noch
überschrieben. Authentifizierte Gameplay-Tests und eine visuelle Prüfung der
betroffenen Stationsszene stehen noch aus. [Prüfstand](RELEASE-STATUS-0.2-alpha.17.md).
