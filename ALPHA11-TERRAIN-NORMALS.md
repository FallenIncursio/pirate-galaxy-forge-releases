# alpha.11: Terrain-Normalen und gemeinsame Grafikdiagnose

**Bekanntes Problem:** Starke kamerabhängige Helligkeitswechsel sind weiterhin gemeldet. Dieses Release behebt sie nicht abschließend; die weitere Analyse folgt separat.


Implementierung für Core und Enhanced, 19.11.2026. Veröffentlichung für Spielversion 1002133 beauftragt; Helligkeitsproblem weiterhin offen.

## Nachgewiesene Ursache

Der frühere Molikar-Fix für vererbte Material-/Texturzuweisungen ist weiterhin
vorhanden. Vor dieser Änderung reproduzierte der aktuelle Renderer dessen
gespeicherte Vergleichsbilder unverändert. Ein Rückbau dieses Fixes oder eine
abweichende DLL-Mischung wurde in der untersuchten Installation nicht gefunden.

Die rekonstruierte `SplitScreenHeightField`-Klasse erbte jedoch die generische
HeightField-Normalenberechnung. Der originale 32-Bit-Client hat eine eigene
Implementierung: acht geklemmte Nachbarhöhen, zwei Sobel-Tangenten, Kreuzprodukt,
komponentenweise Skalierung und Normalisierung. Abweichende Normalen ändern die
Beleuchtung sichtbarer Hänge und deren winkelabhängige Glanz-/Reflexionsanteile.

Isolierte Sirius-Vergleiche zeigten die Abweichung auch ohne Schatten und ohne
Glanzanteil. Mit identischen flachen Normalen stimmten die Lichtwerte beider
Renderer in allen sechs Kontrollansichten überein. Die Korrektur setzt deshalb
am Höhenfeld an; Gamma, Helligkeitsregler und Originalmaterialien bleiben erhalten.

## Implementierung

- `native-terrain/src/include/SplitScreenNormals.h`: rekonstruierter Algorithmus,
  geklemmte Randnachbarn, endliche Werte und sichere Ersatznormale für ungültige
  Eingaben. Die ungewöhnliche komponentenweise Skalierung entspricht bewusst
  dem Original und wird nicht durch eine andere Normalentransformation ersetzt.
- `OgrePagingLandScapeData2D_SplitScreenHeightField::getNormal`: verwendet diesen
  Algorithmus in beiden Editionen und beiden nativen Renderer-Builds.
- Zwei rein lesende Terrain-Optionen geben aktuellen Karten-/Materialnamen für
  die Diagnose frei. Keine Änderung an Terrain-LOD, Pflanzenmenge oder Sichtweite.
- `GraphicsSnapshot` in `modules/shared` und der JNI-Leser in
  `project/client-scene-values/native/GraphicsSnapshot.h` ersetzen die bisher
  nicht auflösbaren ogre4j-Diagnoseaufrufe. Der gemeinsame Leser prüft Szene und
  Kamera im aktuellen Engine-Register, behält keine Zeiger und fängt Fehler pro
  Abschnitt ab. Core benötigt dafür kein Enhanced-Modul.
- Die freiwillige 30-Sekunden-Diagnose enthält zusätzlich `graphics.json`:
  maximal 60 Zustände im Abstand von 500 ms. Enhanced verwendet denselben Leser
  auch in seiner vorhandenen Grafikdiagnose. Ohne Aufnahme erfolgt keine Abfrage.

Die Zustände enthalten Kamera, Umgebungslicht, Nebel, Schatteneinstellungen,
Terrain-Material und begrenzte geladene Shader-/Texturzustände. Automatische
Shaderparameter und die Lichtliste können zum letzten Renderdurchlauf gehören;
sie sind kein Nachweis der Werte einer einzelnen gezeichneten Kachel. Ressourcen-
Buchhaltung ist keine VRAM-Messung. Begrenzungen: 64 Szenen/128 Kameras bei der
Gültigkeitsprüfung, acht Lichter, höchstens zwei Terrain-Materialien mit je sechs
Techniken und acht Texturstufen, höchstens 32 KiB je Snapshot. Fehlende Abschnitte
werden ausdrücklich markiert. Keine zusätzlichen Renderdurchläufe oder
Serveraufrufe, keine automatische Übertragung, keine Profil-/Anmeldedaten.

## Nachweis gegen das Original

`native-terrain/normals-audit/run.py` prüft vor Ausführung den vollständigen Hash
der privaten x86-Referenz-DLL. Das separate x86-Prüfprogramm ruft deren tatsächliche
Normalenfunktion an RVA `0x16540` mit synthetischen Höhenfeldern auf. Es vergleicht
3×3-, 17×17- und 33×33-Felder einschließlich Rändern und Ecken bei vier Skalierungen,
darunter anisotrope Werte. Ergebnis: 16.644 Komponentenvergleiche, kein Fehler,
maximale absolute Abweichung `1.84774e-6` bei Toleranz `2e-5`.

Kontrollierte Rendervergleiche verwenden unveränderte private Original-Assets
von Sirius01, Sirius09 und Molikar (`mizar2`) mit jeweils 24 Kamerawinkeln bei
drei Neigungen. Die finalen Dateien verbessern in allen 216 Ansichten den
mittleren absoluten Helligkeitsunterschied auf gemeinsam sichtbarer Fläche.
Die reproduzierbare Maske umfasst Pixel mit mindestens einem nichtnull RGB-Kanal
in Referenz, Vorher- und Nachher-Bild; sie ist keine Objekt-ID-Maske der Engine.
Mittlerer absoluter Unterschied der kodierten Bildhelligkeit zur x86-Referenz:

| Oberfläche | Vorher | Korrigiert |
|---|---:|---:|
| Sirius01 | 12,34 | 10,15 |
| Sirius09 | 8,90 | 6,45 |
| Molikar | 17,01 | 16,18 |

Das sind Bildvergleichswerte auf einer 0–255-Skala (RGB-Gewichte
0,2126/0,7152/0,0722), keine lineare Lichtmessung und keine Prozentverbesserung.
Über das gesamte Bild einschließlich unterschiedlicher Terrain-Silhouetten
verbessern sich 57/72, 57/72 beziehungsweise 72/72 Ansichten; diese Vollbildwerte
werden im Vergleichsbeleg ebenfalls gespeichert. Filterung, Geometrie und
Rasterisierung erzeugen weiterhin Pixelunterschiede. Der abschließende Prüfstand bindet die finalen
Dateihashes und ist unter [Release-Status](RELEASE-STATUS-0.2-alpha.11.md) dokumentiert.

## Grenzen und Sandbox-Abnahme

Die konkrete Nutzeraufnahme und der genaue betroffene Sirius-Planet lagen für
diesen Vergleich nicht vor. Kontrollierte Offline-Szenen ersetzen keinen Flugtest
mit Himmel, Wetter, Wasser und sämtlichen Spieleffekten. Verbliebene Unterschiede
sind anhand der neuen Diagnose messbar; vollständige Original32-Gleichheit wird
nicht behauptet. Keine neue Sicherheits- oder FPS-Zusage.

Für die Abnahme zunächst Enhanced/D3D11 auf demselben Sirius-Planeten: am gleichen
Ort Kamera langsam vollständig drehen, flache und steile Blickwinkel vergleichen,
dann Orbit und erneut landen. Molikar und Calon als Regression prüfen. Falls noch
starke Sprünge auftreten, eine 30-Sekunden-Diagnose während der Kamerabewegung
aufnehmen. D3D9 und Core werden separat bewertet. Der laufende Client wird durch
die Vorbereitung weder geschlossen noch verändert.
