## Ergänzung R3, 23.11.2026

Sieben planetengebundene Legendenzuordnungen ergänzen 51 Laufzeitbereiche für
21 weitere Baupläne. Referenzkatalog jetzt 684 BPs mit Gebieten, freigegebene
Laufzeitauswahl 664 BPs / 1.387 Gebiete. Die Tabelle `coverage.md` und alle
Prüfhashes wurden neu erzeugt. Der ursprüngliche Datenphasenbericht unten
beschreibt den R2-Ausgangspunkt. Zuordnung und Grenzen:
[Bauplan-Fundorte R3](ALPHA26-BLUEPRINT-LOCATIONS.md#r3-fehlende-angaben-und-passende-icons).
Unbekannte Drop-Level bleiben unbekannt; vorhandene Kartenlevel dürfen separat
als solche angezeigt werden. Noch keine räumliche Live-Bestätigung des R3-Stands.

# Enhanced alpha.26 – Fundort-Datenprüfung

Nachfolgend wurde die Laufzeitintegration R2 beauftragt. Sie übernimmt nur die
auch nativ eindeutig zuordenbaren Referenzdaten: 1.336 Bereiche für 643 Baupläne,
zusammen mit 1.333 Fundort-Bauplänen. Die unten dokumentierte Dateninventur bleibt
als ursprünglicher Quellenstand erhalten. Die kleinere Laufzeitauswahl schließt
offene Identitäten und Varianten aus.
Details: [Bauplan-Fundorte R2](ALPHA26-BLUEPRINT-LOCATIONS.md).

Stand 23.11.2026. Der Nutzer priorisiert den Datenbestand vor weiteren Icons und
UI-Änderungen. Dieser Stand erweitert ausschließlich den Offline-Referenzkatalog.
Der laufende alpha.26-Client und seine 30 bisherigen Kartenbereiche wurden nicht
ersetzt. Keine Spielserverabfragen, kein Neustart, kein Push und keine Veröffentlichung.
Core und die unabhängigen Starter-/Updateränderungen bleiben erhalten.

## Ergebnis

- Alle 44 statischen Karteneinträge der Prelude-Planetenübersicht inventarisiert,
  mit Quellname und tatsächlichem Sternsystem; zusätzlich fünf Sirius-Ringe.
  Einige Einträge stehen für Eroberung, Orbit oder mehrere Karten, nicht für
  einen regulären Farmplaneten. 20 reguläre Karten besitzen geprüfte native IDs.
- Alle 209 veröffentlichten individuellen Gegner-Ebenen verarbeitet. 1.573
  Referenzbereiche einschließlich Patrouillen erhalten; 18 abgetrennte
  Zahlen-/Fähigkeitssymbole ausdrücklich nicht als Fundort interpretiert.
- 1.625 BP-Quellzeilen ergeben 2.057 einzelne Quellenbehauptungen. Das Inventar
  umfasst 1.968 Baupläne; 1.572 besitzen mindestens eine solche Quellenangabe,
  einschließlich bedingter Angaben und ausgeschlossener Sirius-Bosse. Das ist
  nicht die Zahl der freigegebenen Scannerregeln oder sicher verfügbaren Drops.
- 663 Baupläne sind anhand von Planet, Fraktion, Gegnertyp und bekannter
  Levelbedingung mit mindestens einem Referenzbereich verknüpft.
- 241 Quellenangaben ohne Drop-Level bleiben ohne Drop-Level. Ein Mars-Mender-
  Patrouillenbereich besitzt keine lesbare Levelangabe; auch dieser bleibt unbekannt.

Die vollständige Tabelle pro Planet steht in
[Datenabdeckung](ALPHA26-REFERENCE-COVERAGE.md).
`coverage.json` enthält die einzelnen offenen Kombinationen; `drop-facts.json`
erhält nicht ausgewertete Quellenzeilen samt Grund. Null Datensätze bedeutet
keinen Nachweis über das Fehlen von Drops.

## Konkrete Korrekturen und Regeln

- Der neue Import berücksichtigt ausgelassene HTML-Zellenabschlüsse. Dadurch
  bleiben die neun Formationsfeld-Einträge der Quelle nicht mehr verschachtelt
  in einer Preiszelle verborgen. Eine eng begrenzte Erkennung des unbeschrifteten
  Drop-Felds ergänzt außerdem „Mizar Mountain“: Baumar, Harvester, Level 39.
  Andere unbeschriftete Zahlen-/Preisfelder werden nicht als Dropquelle verwendet.
- Erebos gehört zu Oort. Das Technologie-System eines dort gefundenen
  Tau-Ceti-Bauplans bleibt unabhängig davon Tau Ceti.
- Tau Ceti Tsunami Angriffsladung (Quellname „Tau Ceti Torrent“) erhält die
  vorhandenen Berserker-Referenzbereiche auf Erebos. Weil die BP-Tabelle kein
  Drop-Level nennt, werden die Kartenlevel nicht als nachträgliche Dropbedingung
  ausgegeben. Native Identität: `attackbuff.rare.tauceti.name`.
- Mehrere Planeten und Gegnerzeilen werden nur bei belegter Zeilenpaarung
  verbunden. Eine Fundstelle auf einem Planeten gilt nicht für die anderen
  Planeten desselben BP-Quelleintrags.
- Level 97/98 und 99/100 bleiben getrennt. Seltene Gegner, seltene Baupläne,
  DS-/Commander-Varianten, Landeflächen- und Aussehensbedingungen sind verschiedene
  Merkmale. Eine gewöhnliche Gegnerkarte beweist keine dieser Sonderbedingungen.
- Formulardaten sind maßgeblich für die Ebenenidentität. Veraltete numerische
  JavaScript-Kommentare vertauschen Runner/Skirmisher und werden nicht verwendet.
- „Custodian C.“ ist eine Commander-Ebene, „Drone“ keine automatisch bestätigte
  Attack-Drone-Identität. DeathSquad-Gebiete erhalten keine erfundenen Mitglieder.

## Noch offene Datenlücken

Die Referenzbasis ist ausdrücklich **nicht vollständig für jeden Drop und jede
Spawnstelle**. Insbesondere fehlen in der veröffentlichten Einzelkartenliste die
Gegnerpositionen für Commerce Central und Technatoria; Baumar und Molikar besitzen
nur wenige Ebenen. Stichproben der entsprechenden Dateien in beiden Wiki-Pfaden
liefern 404. Die Fandom-Planetenseiten enthalten keine ergänzenden Koordinaten.

Auf Erebos widersprechen sich teilweise die Fraktionen in BP-Tabellen und
Kartenebenen, etwa Mantis-Baiter/Defender gegenüber Ancient-Baiter/Defender.
Diese Angaben werden nicht allein wegen ähnlicher Namen verbunden. Custodian,
generische Turrets und Interceptors besitzen weitere nicht belegte Zuordnungen.
Für Erebos haben 97 von 113 BP/Gegner/Bedingungs-Gruppen mindestens einen passenden
Bereich, für Calon 62 von 78. Das bestätigt nicht jede Spawnstelle einer Gruppe.

Die zusätzlichen alten Sammelkarten und seltenen „R“-Markierungen sind als Quellen
inventarisiert. Ohne eindeutigen Gegnertyp werden daraus keine seltenen Gegnerdrops
abgeleitet. Historische Events, Missions- und Shopangaben bleiben außerhalb der
gewöhnlichen Farmpositionszuordnung. Sirius bleibt dynamisch; Giza, Soris und
Amarna werden weiterhin nicht als bestätigte Dropquellen freigegeben.

## Quellen und Überprüfung

Primärquelle: [Prelude-Planetenübersicht](https://prelude-myzen.co.uk/PirateGalaxy/Planets.html)
und deren BPList-Tabellen, einzeln mit URL und SHA256 in `source-manifest.json`.
Die heruntergeladenen BP-Tabellen reproduzieren exakt die vorhandenen 4.748
Scanner-Aliasregeln. Diese bestehenden Laufzeitregeln wurden nicht verändert.

Wegen des nicht funktionierenden HTTPS-Zugriffs wurde die öffentliche HTTP-Adresse
der Quelle verwendet, ohne die Zertifikatsprüfung abzuschalten. Die heruntergeladenen
Dateien sind auf ihre Hashes festgelegt; spätere Änderungen brechen die Prüfung ab.
Quellbilder und Originalspielressourcen bleiben im privaten Arbeitsverzeichnis.
Nur Fakten, Annotationen und Nachweise liegen im Repository, keine Wiki-Bildkopien.

Die Marker wurden aus den transparenten Einzelbildern gewonnen und auf 14
nummerierten Übersichtsseiten visuell geprüft. OCR-Vorschläge wurden anhand der
Bildteile korrigiert. Räumlich verbundene Symbole bleiben gemeinsame Bereiche,
größere Routen bleiben Patrouillenflächen. Die Koordinaten beziehen sich auf
367 × 367 Pixel der Quellkarte, nicht auf live gemeldete Gegnerpositionen.

Alle 20 regulären Karten wurden gegen die Original-Minimaps von Spielversion
1002133 abgeglichen: jeweils mehr als 600 übereinstimmende Bildmerkmale; maximale
Abweichung der identischen Kartenprojektion an den Ecken rund 3,03 native Pixel.
Die Bildkalibrierung bestätigt Ausschnitt, Orientierung und Maßstab. Sie beweist
keinen aktuellen Gegner-Spawn und ersetzt nicht die spätere Ingame-Stichprobe.

Ergänzend geprüft, ohne Übernahme ungeklärter Koordinaten:
[Commerce Central](https://pirategalaxy.fandom.com/wiki/Commerce_Central),
[Technatoria](https://pirategalaxy.fandom.com/wiki/Technatoria) und das
[ältere Wiki](https://www.c3709203.myzen.co.uk/PG/).

## Wiederholbare Prüfung

Vom Repository aus:

```powershell
python project/client-bp-locations/prepare_reference_catalog.py --evidence C:/PGFWork/bp-locations-analysis/catalog-sources --check
python -m unittest tools.forge.tests.test_reference_catalog tools.forge.tests.test_blueprint_locations tools.forge.tests.test_scan_drops tools.forge.tests.test_editions
```

Ohne `--check` erzeugt der erste Befehl ausschließlich die Referenzdateien unter
`project/client-bp-locations/catalog`; keine Laufzeitressourcen und keine Pakete.
Die visuellen Annotationen und Kalibrierungsnachweise sind eigenständige Eingaben,
keine ungeprüft bei jedem Lauf neu übernommenen OCR-Ergebnisse.

43 Tests bestanden: Identitäten, HTML-Reparaturen, falsche Planeten-/Level- und
Variantenverknüpfungen, Bildkalibrierung, unbekannte Werte, vollständiges
Quelleninventar, Prüfsummen, Sirius-Ausschlüsse und vorhandene Editionsverträge.
Der neue Datentest ist in den künftigen Editionsprüflauf aufgenommen. Ein erneuter
nativer GUI-/Spielbuild wurde in dieser reinen Datenphase nicht ausgeführt.
Prüfbeleg: `distribution/tests/blueprint-reference-catalog-alpha26.json`.

Als nächster Datenschritt sind die oben gelisteten Quellenkonflikte und fehlenden
Positionen gezielt zu ergänzen. Nur belegte Verknüpfungen dürfen anschließend in
Laufzeitdaten und die spätere Icon-Darstellung übernommen werden.
