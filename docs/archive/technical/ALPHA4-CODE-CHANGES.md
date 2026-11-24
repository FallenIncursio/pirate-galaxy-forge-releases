> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Alpha.4 — Implementierung und Patchvertrag

Basis: gepinnte Alpha-73-Spielklassen und gemeinsamer Core/Enhanced-Quellstand.
`tools/forge/java/EditionFixes.java` läuft unmittelbar nach `EditionCompose`.
`patches/edition-fixes.tsv` enthält pro Zielklasse den vollständigen SHA-256 der
Originalklasse und der komponierten Eingabe sowie die erwartete Zahl der Eingriffe.
Unbekannte Eingaben und abweichende Trefferzahlen brechen ab. Negative Tests verändern
beide Hashspalten und die Editzahl. Alle gemeinsamen Helfer stammen ausschließlich
aus `editions/sources.json`; Core enthält keine Energiekugelklassen/-DLL.

### Korrektur nach dem ersten vollständigen Spielstart

Der erste alpha.4-Teststart blieb mit `VerifyError: Bad local variable type` in
`aol$14.go` am Ladebildschirm stehen. Der Original-Stackmap-Eintrag hatte vor
`RETURN` den nicht mehr benötigten Empfänger verworfen; der neue Abschlusshook
griff wieder darauf zu. `EditionFixes` berechnet deshalb sowohl Stackgrößen als
auch sämtliche Frames neu, mit den gepinnten Spiel-/Bibliotheksklassen im
Generator-Klassenpfad. Originalhashes und Eingriffszahlen bleiben verbindlich.

`EditionLoadProbe` prüft jetzt neben den Forge-Helfern alle zehn im Korrekturledger
deklarierten Spielklassen einschließlich Methoden, Konstruktoren und Feldern mit
JVM-Verifikation. Die vorherige Prüfung erfasste diese Klassen nicht. Der alte
Kandidat scheitert reproduzierbar an dieser erweiterten Prüfung, der korrigierte
besteht. Frühere alpha.4-Paket-/Installationsbelege gelten nicht für die neuen Bytes.

## Rangliste — beide Editionen

### Clan-Antworten und Divisionswechsel nach dem Sandbox-Test

Die laufende Sitzung bestätigte den eigentlichen Clan-Datenfehler:
`getLeagueRankingItemsFromTo` antwortete mit `Arrays$ArrayList` in den Eigenschaften
einer `amx`-Zeile. JBoss konnte `AbstractList` unter Java 27 nicht zugänglich machen;
die Antwort wurde verworfen und die Anfrage lief in den Timeout. Es handelt sich
um Java-/Protokollkompatibilität, nicht um einen D3D11-Zeichenfehler.

`LegacyCollectionCodec` und `LegacyEnumMetadata` erhalten den Java-8-Feldaufbau
dieser festen Array-Liste. Der dedizierte Reader registriert das Objekt vor dem
Einlesen des ursprünglichen, typisierten Arrays; geteilte Referenzen und Zyklen
bleiben erhalten. Für diesen Zugriff öffnet ausschließlich die Spiel-JVM
`java.base/java.util` zum unbenannten Spiel-/Serializer-Modul. System-Java und andere
Pakete bleiben unverändert. Die vorhandene Freigabe für finale Serialisierungsfelder
bleibt erforderlich. Nur das Öffnen des Pakets genügt nicht: neuere private
JDK-Serialisierungsmethoden würden das alte Drahtformat verändern. Der zusätzliche,
hashgebundene Eingriff in `ClassMetaDataSlot.explorePrivateMethod(Class)` überspringt
solche Methoden ausschließlich für die drei explizit unterstützten Collection-Typen
und den bereits vorhandenen Date-Codec. Der zusätzliche Date-Fall verhindert eine
durch die Paketfreigabe sonst wieder aktivierte, abweichende JDK-Schreibroutine.

`RankingWireTests` liest und schreibt sieben synthetische Pakete des gepinnten
Originalclients mit Java 8 bytegleich, einschließlich tatsächlicher `amx`-Zeilen,
leerer Listen, Nullwerten, typisierter/geteilter Arrays und Zyklen. Ohne die gezielte
JVM-Freigabe scheitert die Negativkontrolle. Bestehende Protokollvektoren werden auch
mit den tatsächlichen Spiel-JVM-Optionen geprüft. Keine echten Serverpakete im Repo.

Die Ladesteuerung hält die aktive Auftragskette bis zur Zustandsauswertung fest;
ein freigegebener WeakHashMap-Schlüssel gilt nicht mehr irrtümlich als Fehler.
Ein Tabwechsel löst den vorherigen Fehlerzustand. Bei mehreren Divisions-/Seiten-
Auswahlen bleibt nur die letzte Anfrage vorgemerkt, bis der bestehende Worker endet.
Alle ursprünglichen Ranking-Scheduler-Einstiege laufen durch dieselbe Einreihung.
Veraltete Antworten dürfen keine UI-Daten mehr anwenden; die 15-Sekunden-Frist beginnt
erst bei tatsächlicher Einreihung. Bereits geladene Kategorieauswahlen werden beim
Zurückwechseln nicht erneut angehängt. Der bislang nicht eingereihte periodische
Refresh wird im bisherigen Zehn-Sekunden-Takt korrekt angemeldet. Die gemeinsame
Workergrenze bleibt eins; es gibt keine automatische Wiederholung nach Fehlern.

Interne Folgeaufträge des ursprünglichen Divisionshandlers gehören zur selben
Anfrage wie ihre Elternkette. Sie werden nach deren Zeilenaufbau seriell ausgeführt,
ohne den eigenen Elternauftrag als vermeintlich veraltete Auswahl abzubrechen.
Eine neue Nutzerauswahl verwirft dagegen die gesamte alte Gruppe einschließlich
noch wartender Navigationsaufträge. Ein Regressionstest stellt genau diesen
verschachtelten Ablauf mit dem ursprünglichen Spiel-Scheduler nach.

Die alten Bytes scheitern am gezielten nativen Lebensdauertest. Neue Tests umfassen
Fehler-/Timeout-Erholung, rasche Tab-/Divisionswechsel, tatsächliche Ausführung durch
den Spiel-Scheduler sowie die Unterdrückung alter Antworten. Die abschließende
Live-Abnahme aller Clanlisten, Pilotendivisionen und Seiten bleibt separat.

`aol.bi(ee)` reihte bisher 14 Kategorieladevorgänge vor die Fensterfreigabe ein.
Jetzt bleiben Layout-/Listenaufbau und Fensterfreigabe erhalten; die 14 anhand ihrer
Methodendeskriptoren erkannten Aufrufe werden entfernt. `RankingLoad` lädt über die
ursprünglichen privaten Controllerfunktionen nur die ausgewählte Kategorie:
Metadaten, erste Seite, Anzahl und bei Spieler/Clan Auswertungszeit. Das sind je nach
Kategorie höchstens vier ursprüngliche Abfrageschritte statt aller Kategorien.
Es gibt keinen neuen Serverendpunkt und keinen zusätzlichen Threadpool.

`aol.bk(ee)` wird als `pgForgeRankingTick(ee)` erhalten; ein neuer Eingang ruft den
Helfer auf. Nach der ersten Kategorienladung bleiben ursprüngliche Seiten-/Eigenrang-
Abfragen und Auswertungstimer aktiv. Bestehende Folgeabfragen verwenden weiterhin
den ursprünglichen Aktualisierungstakt. Ein Timeout startet keine Wiederholung.

Alle Ranking-Aufrufe von `ayz.do` und `ayz.int` laufen durch lebensdauergebundene
`azb`-Wrapper. Sie übernehmen echte Ergebnisse, prüfen Generation und 15-Sekunden-
Frist und unterdrücken verspätete UI-Aktionen. Ein noch blockierter Worker wird
gezählt; Wiederöffnen erzeugt keine weiteren wartenden RPCs. Es wird kein harter
Netzwerkabbruch vorgetäuscht. Nullantworten oder Nullzeilen gelten als Fehler,
eine echte leere Antwort bleibt gültig. `aol$17.go`, `$14.go`, `reset` und
`CoreLifecycle.close` verbinden Öffnen und Schließen mit der Lebensdauer.
Die zwischenzeitlich eingeführte Statusfußzeile wurde nach dem Sandbox-Test entfernt.
Fenster und Listen behalten ihre originale Geometrie. Bei Timeout wird der originale
Ladezustand beendet; Fehler bleiben im Diagnoseprotokoll, ohne zusätzliche Leiste.

Tests: Original-Aufgabenketten mit Ergebnisweitergabe, Fehler, Timeout, verspäteter
Antwort und blockiertem Worker; echte originale MyGUI-Ranglistenoberfläche unter
D3D9/D3D11. Keine erfolgreich vom Live-Server geladene Rangliste behaupten.

## HUD-Größe — beide Editionen

Im laufenden Enhanced-Client wurde die Auswahl 115 % korrekt gespeichert, während
das HUD unverändert blieb. Ein nativer Regressionstest reproduziert dieses Verhalten
nach dem Wechsel auf ein anders benanntes Renderfenster: `Gui::windowResized` ersetzte
den Fensterzeiger, behielt aber den alten Namen für die Lebensdauerprüfung. Dadurch
war das neue Fenster für die Skalierungsabfrage nicht verfügbar. Die Zuordnung wird
jetzt gemeinsam aktualisiert; die Prüfung geschlossener Fenster bleibt erhalten.

Die D3D11-MyGui.dll wird aus den gepinnten Quellen neu gebaut. Exportnamen und
Klassenlayout bleiben gleich; Beleg: `editions/native-builds/mygui-hud-window.json`.
Enhanced liest die zulässigen Stufen direkt aus derselben nativen Abfrage wie Core,
statt die physische Auflösung aus gerundeten logischen Abmessungen zurückzurechnen.
Tests bedienen die native Auswahl und Übernehmen, prüfen Speicherung und erneutes
Laden in beiden Editionen. Der alte DLL-Stand scheitert am Fensterwechseltest.
Die abschließende Nutzerprüfung im Spiel steht noch aus.

## Kantenglättung — beide Editionen

`at.return(int)` fragt jetzt `GraphicsCapabilities.supportsFsaa` ab. D3D11/Ogre 14
bietet `FSAA` mit numerischen Stufen an; D3D9 verwendet `Anti aliasing` und `Level N`.
Die alte Suche erkannte die D3D11-Stufen nicht. Der Helfer liest die angebotenen
Werte über die tatsächlich vorhandene JNI-Schnittstelle und gibt native Vektoren
frei. Coverage-Modi wie `4f8` werden nicht als einfache 4x-Stufe ausgegeben.

Die vorhandene Grafikoption und deren Speicherung/Neuerzeugung bleiben zuständig.
Kein Schärfefilter, keine pauschale Texturunschärfe und kein Überschreiben bestehender
Benutzereinstellungen. Native Tests erzeugen Fenster mit 0/4/0/4 Samples und prüfen
die tatsächlich realisierten Werte auf der Test-GPU. Andere Hardware bleibt offen.

## Shopvorschau — beide Editionen

Die Antriebsspurvorschau verwendet eine 3D-Szene, keine Videodatei. In der isolierten
Originalszene bleiben die aktivierten Animationen ohne Fortschreibung bei Zeit 0.
`PreviewAnimation` registriert nur diese Präsentation nach
`aov.lambda$setupEngineTrailRenderBox$4`. Der Eingang `screens.if.int(nf)` bewegt
`ShipMovementNode`, `ShipAttachment` und `CameraAttachment` mit begrenztem Frame-Delta.
`extends(boolean)` und `release()` lösen die Registrierung. Andere Weltszenen oder
Animationszustände werden nicht global beschleunigt.

Der Sandbox-Test zeigte zusätzlich einen Fehler beim zweiten Artikel: Der originale
Szenen-Clear entfernte die Knoten, ließ aber die Animationszustände bestehen.
`State for animation named 'ShipMovementNode' already exists` brach den nächsten
Aufbau ab. `PreviewAnimation.reset` entfernt vor dem erneuten Aufbau die
Präsentationsanimationen und ihre Zustände aus dieser isolierten Szene über den
in D3D9 und D3D11 vorhandenen Export `destroyAllAnimations`. Der Welt-SceneManager
wird dabei nicht berührt; die originale Präsentation enthält drei Animationen.
Die Bereinigung erfasst auch einen vorher abgebrochenen Teilaufbau. Der originale
Clear und die übrigen Auswahl-/Ladeaktionen bleiben erhalten. Der Patchvertrag für
`aov` umfasst deshalb vier statt drei Eingriffe.

Die native Regression reproduziert zunächst den Fehler des originalen Clear und
prüft danach sechs aufeinanderfolgende Wechsel zwischen zwei Antriebskonfigurationen
mit tatsächlich gerenderten Pixeln und neu aufgebauten RibbonTrail-Elementen.

Die beiden erzeugten verzögerten Aktionen für Antriebs-/erweiterte Shopvorschau
werden zusätzlich durch `PreviewRequest.guard` an Widgetgeneration und Auswahl
gebunden. Alte Antworten dürfen weder die neue Auswahl noch zerstörte Widgets nutzen.

Native D3D11-Prüfung: Originalszene, Originalschiff und originale Engine-Konfiguration;
Negativkontrolle bleibt unbewegt, korrigierte Kamera-/Schiffsspuren ändern GPU-Pixel
und bauen echte RibbonTrail-Elemente auf. Die Prüfszene nutzt ein diagnostisches
Material zur eindeutigen Sichtbarkeit. Das belegt Bewegung und Lebensdauer, nicht
sämtliche originalen Shopfarben, Skins oder Live-Shopabläufe. Der Test erzeugt Root
selbst und ersetzt nur fixturebedingt fehlende globale Initialisierung; die
Produktions-JARs und -DLLs werden dabei nicht ersetzt.

## Energiekugel — nur Enhanced

`EnergyPriority.bind` behält Registrierungen vor Anlage des nativen Knotens.
`frame` löst den Knoten später auf; Auswahl, Sammelreichweite und manuelles Sammeln
bleiben unverändert. Fehler pausieren mit Backoff und nach drei Versuchen; Szenen-
wechsel, Schließen und Speichern der Option ermöglichen einen neuen Versuch.
Lokale Diagnosen nennen Auswahl-/Zeichenphase; keine zusätzliche Serverabfrage.

`ForgeEnergy.cpp` erzeugt D3D11-Material und Shader transaktional. Unvollständige
Materialien werden verworfen, Fehlversuche räumen Teilressourcen auf. Die neue DLL
ist mit Quellen-/Artefakthashes in `enhanced-energy-recovery.json` gepinnt; ihre zwei
JNI-Exporte bleiben gleich. D3D9 behält die bisherige DLL und erhält die Java-Fixes.

Tests: Auswahlregressionen plus kompletter Java/JNI/D3D11-Pfad mit späterem Knoten,
defektem Material, sichtbaren Markerpixeln, Einsammeln und Planet/Orbit-Lebensdauer.
Das synthetische Szenario ersetzt keine Bestätigung auf sämtlichen Live-Planeten.
