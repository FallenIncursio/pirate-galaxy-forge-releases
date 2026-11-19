# Spielbasis 1002133 für Core und Enhanced alpha.11

Releasebasis vom 19.11.2026; Veröffentlichung von Core und Enhanced beauftragt.
Die offizielle Spielbasis ist 1002133, Revision `181120261720`. Alpha 73 bleibt
die unveränderliche Vorlage der historischen Forge-Patches und nativen Basis.

## Übernahme

Die offiziellen Basic-/PirateGalaxy-/core-Archive wurden über den Hersteller-CDN
geladen, gegen Größe und CRC des offiziellen `gameCurrent.xml` geprüft und mit
SHA-256 gepinnt. `editions/game-basis.json` bindet die entpackten Dateien und den
vollständigen Unterschied zur historischen Basis 1002132. Der öffentliche
Downloadkatalog für spätere Pakete liegt unter `distribution/game-sources/1002133.json`.
Es wurden keine Spielarchive in die Quellrepo aufgenommen.

53 Spielklassen unterscheiden sich binär. Der normalisierte Methodenvergleich
findet drei geänderte und eine neue Methode: Schiffsliste, Schiffsinformationen
und deren zweite Textspalte. Die übrigen Klassendifferenzen betreffen Debug- und
Konstantenpooldaten. `patches/game-basis-1002133.tsv` hält alle vier ausführbaren
Änderungen fest. Es gibt keine Überschneidung mit bestehenden Forge-Patches.

`GameBasisRebase` führt Original 1002132, Original 1002133 und die historische
Forge-Vorlage zusammen. Änderungen an derselben Methode auf beiden Seiten werden
bei abweichenden Ergebnissen abgewiesen. Neue Herstellermethoden bleiben erhalten,
ebenso die bisherigen Forge-Methoden. Anschließend laufen die unveränderten 326
Kompositionsverträge und die späteren Editionskorrekturen über diese neue Basis.
Die Versionsprüfung selbst wird nicht verändert.

Basic enthält dieselben Java-Klassen und Hersteller-DLLs wie zuvor. Geändert sind
Manifest, Signaturen und Zeilenenden der Pluginliste. Forge übernimmt die neuen
Manifestangaben und behält seine geprüften x64-/D3D9-/D3D11-Implementierungen.
Originalsignaturen gelten nicht für gepatchte Archive und werden nicht übernommen.

Das neue `core`-Archiv und beide deutschen Sprachdateien werden im privaten
Testpaket mitgeführt. Eine zusätzliche Prüfung fand das alte Schiffslayout im
historischen Cache. Eine einmalige normale, lesende Ressourcenabfrage für
`player_info_arti.layout` lieferte elf Abhängigkeiten; genau eine davon musste
neu geladen werden. Ihre Server-CRC und ihr SHA-256 sind geprüft. Die neue
Cachedatei ist als optionaler Import gepinnt; alte Pakete und Nutzerdaten blieben
unverändert. Keine Kontoanmeldung und keine Spielaktion für diese Abfrage.

## Prüfungen

- Dreiwegeübernahme inklusive negativer Konflikt- und Fehlende-Klasse-Kontrollen.
- Vergleich beider neuen Spiel-JARs mit dem vorigen alpha.11: nur die vier
  freigegebenen ausführbaren Änderungen, sämtliche Forge-Methoden erhalten.
- Alle 124 Core- und 306 Enhanced-Helfer sowie sämtliche nativen DLLs bytegleich
  zum vorigen alpha.11. Terrain-Normalenfix, Grafikdiagnose und bisherige Fixes
  bleiben damit enthalten. 121 gemeinsame Helfer sind zwischen den Editionen identisch.
- Native Schiffsinformation mit fünf benötigten Widgets und Auflösung der neuen
  Herstellermethode in beiden Editionen unter D3D9 und D3D11 geprüft. Der alte
  Cache war die fehlgeschlagene Negativkontrolle; mit aktueller Ressource bestanden.
- Bestehende Editions-/JVM-/Wire-/Feature-/UI-Regressionen werden an die finalen
  Paketbytes gebunden. Maßgeblich sind der neue Readiness- und Startbeleg.

Die frühere 32-Bit-Terrainprüfung bleibt ein Nachweis für die unveränderten
alpha.11-Terrain-DLLs. Sie ist keine neue Live-Abnahme auf Sirius. Der Nutzer meldet weiterhin Helligkeitsprobleme; deren weitere Bearbeitung ist aufgeschoben.

## Bauen

`editions-build` benötigt zusätzlich `--game-originals <1002133-Ordner>` mit
`Basic.jar`, `PirateGalaxy.jar` und `core`. `--original-jars` bleibt auf die
historische 1002132-Basis gerichtet, um Alpha 73 unverändert zu rekonstruieren.
Aktuelle Spielbasis, historische Patchvorlage und Nutzerdaten bleiben getrennt.
Für spätere Releasepakete bezeichnet `editions-release-candidates --originals`
die neue 1002133-Basis; der Paketierer erzeugt die dazu passenden Deltas und den
Downloadkatalog. Die Veröffentlichung dieser Basis einschließlich beider Updatekanäle ist ausdrücklich autorisiert.
