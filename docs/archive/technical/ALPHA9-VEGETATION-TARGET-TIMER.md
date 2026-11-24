> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# alpha.9: Vegetation, Zielanzeigen und Timer

Privater Folgestand für Core und Enhanced; keine Veröffentlichung. Grundlage ist
die letzte [Calon-Auswertung](ALPHA9-CALON-PLANET-ANALYSIS.md), nicht eine neue
Behauptung, sämtliche Mini-Ruckler seien behoben.

## Gemeinsame Änderungen

### D3D11-Vegetation

`BatchedGeometry::prepareStaticSource` bereitet statische Prototypen beim ersten
Registrieren im TreeLoader vor. Vertex- und Indexpuffer erhalten eine vom Mesh
besessene CPU-Schattenkopie. Spätere Seiten und Windbatches verwenden dadurch
aktuelle CPU-Daten statt wiederholter synchroner GPU-Lesevorgänge. Schreibzugriffe
auf die neuen Puffer aktualisieren weiterhin die Schattenkopie. Animierte Meshes,
Skelette, dynamische und gesperrte Puffer werden nicht umgewandelt.

Grenzen: 64 MiB vorbereitete Quellpuffer insgesamt, höchstens 8 MiB pro Puffer;
bei ausgeschöpftem Budget bleibt der bisherige Lesepfad erhalten. Die Verwaltung
hält keine starken Pufferreferenzen. Beim Entladen eines Meshes werden auch die
schwachen Referenzen vor dem Entladen des Renderers entfernt. Registrierungen,
Wiederverwendung, Schreibzugriffe, Budget und geordnetes Ende sind geprüft.
Die gemeinsame Vertexdaten-Extraktion bleibt die bestehende Forests-Operation.

Optionales Vorladen wählt Seiten nach der Entfernung zu einer begrenzten
Halbsekunden-Vorausschau in Bewegungsrichtung. Nach zwei Millisekunden Arbeit
im Seitenmanager wird kein zusätzlicher Vorladeaufbau begonnen. Sichtbare,
benötigte Seiten werden weiterhin unmittelbar aufgebaut. **Dies ist kein hartes
2-ms-Framebudget:** ein einzelner großer Aufbau bleibt synchron. Dichte, Meshwahl,
Sichtweite, ursprüngliche Seitenradien und LOD-Distanzen werden nicht reduziert.
Ein leerer Vorladevorrat führt nicht mehr zur Division durch seine Größe.

### Zielanzeigen

`ResourceManager::_loadImplement` verwendet für exakte Layoutnamen den OGRE-
Ressourcenindex. Die bisherige Suche über sämtliche Archiveinträge pro Zielanzeige
entfällt. Der begrenzte XML-Cache prüft weiterhin bei jedem Laden die tatsächlichen
Dateibytes; gleich große Änderungen und Ressourcenwechsel bleiben sichtbar.
Wildcard- und andere Ressourcentypen behalten die bisherige Auflösung.

Nach dem ursprünglichen Lade-Layout wird eine private `targetinfo.layout`-Instanz
ohne Spielerdaten/Listener erzeugt und sofort zerstört. Damit werden vorhandene
Skin-/Schrift-/Texturressourcen vor der ersten sichtbaren Zielanzeige angefasst.
Fehlen sie zu diesem frühen Zeitpunkt, bleibt der normale Ladepfad verfügbar.
Auch ein fehlgeschlagener Layoutaufbau entfernt bereits erzeugte Wurzelwidgets.
Es gibt keinen Pool wiederverwendeter Gegnerwidgets, keine zurückgehaltenen
Spieleridentitäten und keine verzögerte Aktualisierung sichtbarer Gegnerdaten.

## Enhanced-Timer

Die ursprüngliche Java-Layoutgrenze ruft nach dem Ladebild die neutrale
Editionsschnittstelle auf. Nur Enhanced bindet darüber die nativen Timermethoden
und bereitet die benötigten Schriften sowie die aktuell gewählten Kreisatlanten
vor. Core besitzt weder diese Klasse noch die zusätzliche DLL-Abhängigkeit.
Die klassische Ansicht benötigt keine Kreisatlanten; für einen gewählten
Kreisstil werden nur dessen aktive und ablaufende Variante vorbereitet, nicht
beide Intensitäten. Die bisherige bedarfsgesteuerte Darstellung bleibt als
Fallback erhalten. Das Muster zum Entfernen von Farbcodes wird wiederverwendet.

## Genauere Diagnose

Die lokale, explizit gestartete 30-s-Aufnahme hat jetzt 62 Spalten. Die bisherigen
33 bleiben an derselben Position. Hinzu kommen Timer-Vorbereitung/Update und
native Unterphasen: Gras, Bäume, Seitenaufbau/Abbau, Höhenabfragen, Quellenlesen,
sofortige Seiten/Vorladen, Instanzen, Quellbytes, Schattenbestand, vertagtes
Vorladen, Layoutressourcen/XML, Widgeterzeugung/Eigenschaften, Schriftwahl,
Texturauflösung und Zielanzeigen. `component_mask` kennzeichnet die tatsächlich
vorhandenen Messmodule (1 Forests, 2 MyGUI).

Die Werte sind verschachtelte CPU-Wandzeiten, keine exklusiven GPU-Zeiten.
`unshadowed_reads` zählt Leseversuche ohne CPU-Schatten und beweist für sich allein
keinen GPU-Stall. `source_shadow_bytes` ist ein Bestand, keine Allokationssumme.
Ohne Aufnahme bleiben die Phasenzähler deaktiviert. Keine Serverabfragen,
automatischen Uploads, Spieler-/Objektnamen oder Anmeldedaten im Bericht.

## Reproduzierbare lokale Prüfung

- 49 echte Quellmeshes aus den lokal vorhandenen Ressourcen: 43 Calon, sechs
  Venar. Je Mesh dieselben 16 Positionen/Rotationen, je drei Aufbauten vor und
  nach Vorbereitung. 294 unbeschattete Quell-Lesevorgänge vorher, null nachher;
  alle erzeugten Vertex-/Indexbytes stimmen überein. Meshentladen gibt das Budget
  frei. Das ist ein Aufbauvergleich, keine komplette nachgestellte Flugroute.
- Insgesamt 34.216 native Vegetationsprüfungen einschließlich originaler
  Kanal-/Indexdaten, Windvarianten, Höhenabfrage und Ende des Renderers.
- Begrenzter XML-Cache und tatsächlicher ResourceManager getestet; ein zählendes
  Testarchiv bestätigt den entfallenen Vollscan bei weiter geprüften Inhalten.
  Die vorherige MyGUI-DLL scheitert gezielt an dieser neuen Gegenprobe.
- Echte UI-Prüfung umfasst fehlgeschlagene Layouts, entfernte Vorwärmwidgets,
  native Phasenzähler und wiederholte Enhanced-Timervorbereitung.

Maßgebliche Editions-/Paketprüfung und Dateihashes stehen im
[aktuellen Prüfstand](../verification/RELEASE-STATUS-0.2-alpha.9.md) und den dort genannten Belegen.
Originalressourcen und rohe Messdaten bleiben privat.

## Noch im Spiel zu prüfen

Calon: dieselbe Strecke beim ersten und wiederholten Durchflug, neue Gegner im
Sichtfeld, Kamerawechsel sowie Orbit/Rückkehr. Je ein Durchlauf mit und ohne
Diagnose; Venar und ein Planet mit einfacher Vegetation als Vergleich. Auf
unveränderte Pflanzen, HUD-Größe, Timer, Zielanzeigen und Speicherrückgang nach
Planetenwechsel achten. Falls große Seiten weiterhin dominieren, ist eine
schrittweise Verarbeitung innerhalb einer Seite der nächste gezielte Schritt.

Kein neuer Live-Flug oder Live-Leistungsvergleich zum 32-Bit-Client erfolgt.
Die zuvor geprüften 176 Originalkonfigurationen bleiben unverändert. D3D9-native
Bibliotheken bleiben bytegleich. Frühere GC-, Wasser-, Präsentations- und
Allokationskorrekturen bleiben erhalten; der ungeklärte große Updateausreißer
aus der letzten Aufnahme gilt weiterhin als offen.
