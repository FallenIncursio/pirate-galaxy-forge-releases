# Alpha.9: Vegetationsaufbau und Allokationen nach dem zweiten Calon-Test

Privater Folgestand vom 17.11.2026 für Core und Enhanced. Nicht veröffentlicht.
Der vorherige Wasser-/AWT-Fix genügte laut Nutzer noch nicht gegen die Mini-Ruckler.

## Neue Messung

Der Nutzer bestätigte den Calon-Flug während der gestarteten Diagnose. Die interne
Aufnahme enthält 6.894 Frames in 30 Sekunden: P99 laut Diagnose 9,238 ms,
Maximum 39,776 ms, 30 Frames über 16,67 ms und sechs über 33,33 ms.
Zwei GC-Pausen dauern 26,572 und 25,719 ms. Mehrere weitere lange Frames liegen
im Vegetations-Update, dort bis zu 33,779 ms. Es bleiben auch lange Update-Frames,
die weder durch die gemessene Vegetation noch durch eine überlappende GC-Pause
erklärt sind. Die Unterphasen sind verschachtelt und dürfen nicht addiert werden.

Die 1.785 tatsächlichen Wasserreflexionen entsprechen rund 59,5 Aufrufen/s.
Die zeitliche Wasserbegrenzung ist damit im Spiel nachgewiesen; sie beseitigt
die übrigen Spitzen nicht. Es wurde keine Wasserbrechung gezeichnet.

Die zeitlich überlappende externe 60-s-Aufnahme zählt 13.763 Presents,
rund 229,5 FPS im Mittel, P99 9,081 ms und Maximum 43,144 ms. Sie enthält auch
Diagnosefenster-Bedienung und ist keine uninstrumentierte Vergleichsmessung.
Der beobachtete Present-Modus ist weiterhin Copy/GDI. Ein einfacher Wechsel
zur zuvor sichtbar fehlerhaften Flip-Ausgabe ist deshalb kein neuer Fix.

## Vegetationspuffer

`BatchedGeometry::SubBatch::build()` und der eigene Wind-Pfad
`WindBatchedGeometry::WindSubBatch::build()` sperrten dieselben Quellpuffer
für jede einzelne Instanz erneut mit `HBL_READ_ONLY`.
Der verwendete OGRE-14-D3D11-Backendpfad legt dafür bei GPU-Puffern einen
temporären Stagingpuffer an, kopiert die Daten und mappt sie zum CPU-Lesen.
Viele gleiche Pflanzen konnten entsprechend viele synchrone Readbacks auslösen.

`ReadOnlyBufferLocks` hält jeden eindeutigen Quellpuffer jetzt nur innerhalb
eines synchronen SubBatch-Aufbaus einmal zum Lesen offen. Vertex- und
Index-Offsets werden weiter angewendet. Vor dem Zeichnen werden alle Quellen
entsperrt, bei Fehlern ebenfalls. Es gibt keinen dauerhaften Meshcache,
keine Zeiger über Szenenwechsel hinweg und keinen zusätzlichen Serveraufruf.
Die Änderung ist auf OGRE 14/D3D11 begrenzt; die D3D9-Bibliothek bleibt bytegleich.

Im Test mit 200 Instanzen, zwei Vertexpuffern und einem Indexpuffer sinken
die Quell-Lesezugriffe von 600 auf drei pro SubBatch. Das ist ein geprüfter
Aufrufvergleich, keine gemessene 200-fache Spielbeschleunigung. Ein erster
Readback und der eigentliche Geometrieaufbau bleiben weiterhin synchron.

## Speicherallokationen

Beide internen Aufnahmen zeigen `com.splitscreen.cf.super(boolean)` als größten
einzelnen obersten Allokationspfad. In der bestätigten Flugaufnahme entfallen
geschätzte 43,923 MiB von 191,655 MiB auf diesen Pfad. Das sind gewichtete
JFR-Stichproben, keine vollständige Bytezählung aller Objektketten.

Die ursprüngliche Suche erstellt bis zu 100 Namen `Ogre/ShadowTexture<n>Cam`
je Frame neu. OGRE 14 verwendet kameraseitige Namen mit zusätzlichem Layerindex,
etwa `Ogre/ShadowTexture0Cam0`. Damit kann die alte Suche dauerhaft erfolglos
bleiben. `ShadowCameraNames` berechnet die 100 ursprünglichen Namen einmalig
und verwendet dieselben unveränderlichen Strings erneut.

Die Suche und ihre ursprünglichen Kameraeinstellungen bleiben erhalten.
Die modernen Namen werden absichtlich nicht einfach in den alten Einstellpfad
eingesetzt: Dieser setzt unter anderem FOV auf null und LOD-Bias auf 5.000.000.
Eine Übertragung auf die aktuelle Schattenkamera benötigt eine eigene visuelle
Prüfung. Dieser Fix beansprucht deshalb keine Änderung der Schattenkonfiguration
und entfernt noch nicht die erfolglosen nativen Kameraabfragen selbst.

`QualityUi.dim()` verwendet für die vier laufend abgefragten HUD-Dimensionen
ebenfalls feste Methodennamen statt neuer Zeichenketten. Sonstige Getter behalten
ihren bisherigen Namensaufbau. HUD-Geometrie und Nutzereinstellungen ändern sich
dadurch nicht. Beide Java-Korrekturen sind gemeinsame Core-Implementierungen.

## Nachweise und Grenzen

- 33.909 native Prüfungen: normale und windanimierte Batches, 200 Instanzen,
  wiederholter Aufbau, 16-/32-Bit-Indizes mit Startoffset, exakte Vertexdaten
  aller sechs ursprünglichen Kanäle, Fehlerbereinigung und tatsächliches Rendern.
- Neun deterministische Baum-/Wind-Bilder sind pixelgleich zur vorherigen
  Testausgabe. Die 36 zufallsabhängigen Grasbilder werden funktional geprüft,
  aber nicht als pixelgleicher Vorher-/Nachher-Nachweis gewertet.
- Gegenproben mit den ursprünglichen normalen bzw. Wind-Batchmethoden scheitern
  jeweils an der erwarteten Readback-Anzahl. Alle 585 JNI-Exportnamen samt
  Ordinalen bleiben erhalten.
- Je Edition 206 Schattennamensprüfungen mit dem tatsächlich gepatchten
  Spielverfahren. 2.000 aufgewärmte Suchdurchläufe belegen nur 32.032 Bytes
  einschließlich des reflektierenden Testaufrufs. Der vorherige Spielcode
  scheitert an der Wiederverwendungs-Gegenprobe. Keine native Szene nötig.
- 46 Editionssuiten und sechs bestehende Negativkontrollen bestanden;
  117 gemeinsame Klassen bytegleich. Native Oberflächen in D3D9 und D3D11 geprüft.

Build `.build/editions/alpha9-readback-build`, Prüfungen
`.build/editions/alpha9-readback-tests-final`, native Ausgabe
`.build/alpha9-readback-native`. Beleg: `distribution/tests/calon-alpha9-readback-fix.json`.
Die privaten Rohmessungen, Spielbilder und Profile sind nicht Bestandteil des Belegs.

Eine erneute Calon-Messung mit diesen neuen Bytes steht aus. Der laufende
Testclient wurde nicht ersetzt. Andere Update-Spitzen und weitere Allokationspfade
bleiben offen; keine vollständige Ruckelfreiheit, Original32-Leistungsparität oder
Freigabe für andere GPUs/Wine behaupten. Kein Commit, Push oder Updatekanalwechsel.
