# Calon: verbleibende Ruckler nach dem GC-/Update-Test

Stand: 17.11.2026. Analyse des neuen Enhanced-alpha.9/D3D11-Laufs.
Der Nutzer bestätigt weiterhin sichtbare Ruckler, derzeit besonders auf Calon.
Keine Produktionsänderung, kein Neustart und keine Veröffentlichung in diesem Schritt.

## Was die neue Aufnahme belegt

7.076 Frames in knapp 30 Sekunden. Der gemessene Frameabstand hat P99 **6,240 ms**,
Maximum **70,461 ms**, neun Abstände über 16,67 ms, davon drei über 33,33 ms.
Die vorherige Aufnahme hatte P99 16,750 ms und 56 Abstände über 16,67 ms.
Flugroute, Gegner, Kameraführung und Aufwärmzustand sind nicht kontrolliert gleich;
dies ist deshalb kein kausaler Leistungsnachweis für einzelne Änderungen.

Keine GC-/Pause-/Allokationsstau-Ereignisse wurden in diesem Zeitfenster exportiert.
Damit erklären die vorherigen langen GC-Pausen diese Aufnahme nicht. Das ist keine
Garantie, dass künftig unter höherem Speicherdruck keine Sammlung stattfinden wird.

`frame_total_ns` erfasst den aktuellen Schleifendurchlauf einschließlich Limiter;
`frame_delta_ns` erfasst den vom FrameClock gelieferten Abstand. Diese Größen
nicht gleichsetzen: zwölf Schleifendurchläufe dauern über 16,67 ms, während die
Zusammenfassung neun entsprechend lange Frameabstände zählt.

| Befund | Zeit in der betroffenen Phase | Zuordnung |
|---|---:|---|
| Acht der zwölf langen Durchläufe | Vegetation 11,45–20,18 ms | Gemeinsam genutztes Vegetationsupdate |
| Zwei lange Durchläufe | Layout 20,99 und 21,16 ms | Ursprüngliche Zielanzeigen |
| Größter Durchlauf: 72,85 ms | Spielupdate 69,08 ms | Einzelne Stichprobe im nativen Symbol-Lookup des Enhanced-Timers |
| Weiterer Durchlauf: 53,48 ms | Spielupdate 48,91 ms | Kein passender Methodenstichproben-Treffer; Ursache offen |

Die Wasserreflexion erreicht maximal **3,33 ms**, der gemessene Present-Abschnitt
**0,97 ms**, der instrumentierte Terrain-Ladeabschnitt **0,0183 ms**.
Sie erklären die großen Ausreißer hier nicht. Present ist keine GPU-Zeit und der
Terrain-Messabschnitt deckt nicht sämtliche Terrain-, Höhenabfrage- oder Pflanzenarbeit ab.
Ein Shader-Bereinigungs-Sample liegt in einem normalen 4,87-ms-Durchlauf.
Die Diagnose selbst hat Anlaufkosten; Kontrollflug ohne Aufnahme bleibt erforderlich.

## Vergleich der lokalen Planetendaten

176 lokale CFG-/Konfigurationsressourcen des installierten Originalclients wurden
mit der effektiven Ressourcensicht des laufenden Kandidaten verglichen: **176 bytegleich**.
Darunter befinden sich zwölf Vegetationsvorlagen. Das ist ein Datenvergleich,
kein Flugbenchmark aller Planeten und kein Laufzeitvergleich zur originalen x86-DLL.

| Vorlage | Definierte aktive Geometrieschichten | Verschiedene Meshreferenzen | Konfigurierte Zielanzahl | Gras-Sichtweite |
|---|---:|---:|---:|---:|
| Calon (`tauceti2`) | 6 | **43** | 34.000 | **9.000** |
| Venar (`tauceti1`) | 7 | 6 | 66.000 | 5.000 |
| Erebos (`mantis1`) | 6 | 23 | 36.000 | deaktiviert |
| Sirius-Vorlagen: waste/bones/gasstones/methanoid/mushroom/city | 2–3 | 4–13 | 2.900–6.000 | deaktiviert |
| `sol3invaded` | 2 | 9 | 8.000 | deaktiviert |
| `draconis1`, `draconis4` | Geometrie deaktiviert | 0 | 0 | 5.000 |

Alle zwölf Vorlagen verwenden eine Seitengröße von 16.384. Calons Geometrie hat
drei konfigurierte Detailstufen bis 6.000 / 8.000 / 20.000 Entfernung, Venar bis
5.000 / 10.000 / 16.000. Zielanzahlen gelten vor Dichte-, Gelände- und Filterregeln;
sie sind **keine gezählten gleichzeitig sichtbaren Pflanzen**.

Calons `geometry_layers=50` bedeutet nicht 50 aktive Schichten: nur die Indizes
0, 1, 2, 30, 31 und 32 enthalten Meshdefinitionen. Der originale Java-Loader
überspringt die übrigen. Eine Kürzung auf sechs würde die Schichten 30–32 entfernen.
Die außerhalb definierter Schichten stehenden Mengen anderer Vorlagen wurden
ebenfalls nicht als aktive Geometrie mitgezählt.

Calon hat weniger konfigurierte Instanzen als Venar, aber wesentlich mehr
verschiedene Meshquellen und eine größere Gras-/Fernsicht. Daraus folgt eine
plausibel höhere Vielfalt beim Seitenaufbau, **kein bewiesener höherer Gesamtaufwand**.
Die vier geprüften Java-Methoden für Grundeinstellungen, Gras, Geometrie und
Geometrieschichten entsprechen nach Normalisierung der Konstantenindizes und
Sprungadressen dem Original. Die nativen Bibliotheken sind dagegen rekonstruierte
Implementierungen; vollständige Verhaltens- oder Leistungsparität ist nicht belegt.

## Konkrete Codepfade

### 1. Vegetation: gesicherte Phase, Unterursache noch zu trennen

`com.splitscreen.df.int(nf)` ruft `PagedGeometry.update()` für Gras und Geometrie auf.
In `native-forests/src/source/PagedGeometry.cpp` lädt `GeometryPageManager::update`
alle bereits benötigten, fehlenden Seiten sofort. Nur das zusätzliche Vorladen
beschränkt sich auf eine Seite pro Update über `enableCache`.
`_loadPage()` führt anschließend `loader->loadPage(info)` und `page->build()`
synchron aus. Ein einzelner großer Seitenaufbau kann deshalb den Frame blockieren.

`TreeLoader2D::loadPage` berechnet Höhe, Farbe und Transformation je Instanz;
`GrassLoader::loadPage` erzeugt Grasgeometrie. `BatchPage::build` baut Puffer und
Shader-/Materialbindungen auf. Die aktuelle Diagnose fasst diese Arbeiten zusammen.
Sie trennt weder Gras von Geometrie noch Höhenabfrage, CPU-Transformation, Upload
und GPU-Rücklesen. Diese Unterursachen sind noch nicht einzeln nachgewiesen.

Der letzte Fix in `BatchedGeometry::SubBatch::build` liest einen Quellpuffer nur
einmal **innerhalb dieses Aufbaus**. Beim nächsten Subbatch/Seitenaufbau beginnt
der lokale `ReadOnlyBufferLocks`-Cache neu. D3D11 kann beim Lesen eines nicht
CPU-lesbaren Puffers weiterhin temporären Staging-Speicher anlegen, kopieren und
über `Map` synchronisieren. Die 43 unterschiedlichen Calon-Meshreferenzen machen
diesen verbleibenden Pfad untersuchenswert; eine Anzahl tatsächlicher Readbacks
der Aufnahme liegt noch nicht vor.

### 2. Zielanzeige: Widgetaufbau bleibt trotz XML-Cache

Beide langen Layout-Stacks lauten sinngemäß:
`awa$2.go → aqe.<init> → ft/fw → LayoutManager.loadLayout`.
`aqe.bQ()` liefert `targetinfo.layout`. Diese drei Zielanzeigenklassen sind
bytegleich zur Originalbasis, es handelt sich nicht um den Forge-Dialog.
`MyGUI_LayoutManager.cpp::parseWidget` erzeugt weiterhin jeden Widgetbaum und
setzt seine Eigenschaften. Der neue XML-Cache beseitigt diese Arbeit nicht.
Welche Widget-/Skin-/Textur-Unteroperation die rund 21 ms verbraucht, bleibt offen.

### 3. Enhanced-Komponententimer: separater Startausreißer

Im 69,08-ms-Update fällt eine Stichprobe auf:
`NativeLibrary.findEntry0 → HudCooldown.styleNative → style → update → button`.
`project/client-controls/src/pg64/client/HudCooldown.java` bindet die nativen
Timerfunktionen bei Bedarf; `ForgeComfort.cpp` kann dabei auch Schriftressourcen
anlegen. Die Stichprobe belegt den dort laufenden Pfad, nicht 69 ms exklusive
Laufzeit dieser Funktion. Dieser Befund ist Enhanced-spezifisch und erklärt allein
keine wiederkehrenden Calon-Vegetationsspitzen. Der zweite große Updateausreißer
ohne Methodenstichprobe bleibt ausdrücklich ungeklärt.

## Empfohlener nächster Fixstand

1. **Vegetationsaufbau gezielt zerlegen und entschärfen (Core und Enhanced).**
   Native Messwerte für Gras/Geometrie, sofortiges Laden/Vorladen, Aufbau, Abbau,
   Höhenabfragen und Quellpufferlesevorgänge ergänzen. Mit den echten Calon- und
   Venar-Ressourcen eine reproduzierbare Kameraroute offline prüfen. Statische
   Meshdaten beim Laden für CPU-Nutzung vorbereiten und begrenzt je Ressource
   wiederverwenden; an Ressourcenlebensdauer/Änderungen binden. Vorladen nach
   Bewegungsrichtung priorisieren. Für harte Zeitbudgets muss auch ein einzelner
   großer Seitenaufbau in Arbeitsschritte zerlegt werden. Ein Limit nur für die
   Anzahl kompletter Seiten reicht bei einer 20-ms-Seite nicht.
2. **Zielanzeigen vorwärmen und Aufbaukosten begrenzen (beide Editionen).**
   Zuerst Widget-, Skin-/Schrift- und Texturladezeiten separat messen. Statische
   Ressourcen während des Ladebilds vorbereiten; danach gegebenenfalls wenige
   vollständig zurückgesetzte Zielanzeigen pro Szene wiederverwenden. Identität,
   Listener, Sichtbarkeit und Lebensdauer müssen korrekt bleiben; keine allgemeine
   Wiederverwendung beliebiger GUI-Zeiger und kein Verzögern bereits sichtbarer Gegnerdaten.
3. **Timer vorbereiten (nur Enhanced).** Native Bindungen und die tatsächlich
   benötigten Schrift-/Atlasressourcen vor dem ersten Komponentenlauf initialisieren.
   Nicht alle optionalen Atlasvarianten ohne Speicherbudget laden.

Die Calon-Vegetation zuerst priorisieren. Weder die Pflanzendichte reduzieren noch
global die FPS begrenzen oder Wasser/Bewegungsinterpolation auf Verdacht verändern.
Die Implementierung muss Erscheinungsbild und Sichtbarkeit erhalten. Keine neuen
Serverabfragen sind für diese lokalen Maßnahmen erforderlich.

Abnahme: dieselbe Strecke auf Calon, Venar als Vergleich mit Gras/Geometrie und
ein Planet mit einfacher Vegetation; jeweils erster und wiederholter Durchflug,
Kamerawechsel und Orbit-Rückkehr. Zeitliche Zuordnung der sichtbaren Schiffsruckler
zu Frame- und Bewegungstakt prüfen. Derzeit liegen keine neuen Flugaufnahmen
anderer Planeten oder des 32-Bit-Clients vor.

Messbeleg: `distribution/tests/calon-alpha9-planet-analysis.json`.
Private Rohdaten, extrahierte Originalressourcen und Bytecodeansichten bleiben
im Chatordner `work/alpha9-planet-analysis` und gehören nicht in Releases.
