> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Enhanced 0.2.0-alpha.28 – veröffentlicht

Enhanced **0.2.0-alpha.28** ist veröffentlicht, Updatekanal Sequenz 109 aktiv.
Alle sieben öffentlichen Downloads, RSA-Manifest, normaler Updatekanal und
README-Installerlink geprüft. Core alpha.17 / Sequenz 16, dessen Repository,
Kanal und Downloadassets bleiben unverändert. Spielversion 1002133, Starter 17.
Binärquellencommit: `f324dbb12c19ee085fa9344879055f3581c43c03`. Beleg: `distribution/tests/editions-0.2-alpha.28-publication.json`.

Der Nutzer bestätigt die Reparaturfeld-Trennung im D3D11-Sandbox-Test. Der laufende Client bleibt während der Veröffentlichung geöffnet.

## Prüfung

64 Editionsprüfungen, 25 Negativkontrollen, 48 Python-Tests, 35 Enhanced-Funktionssuiten,
56 Reparaturprüfungen und je 457 GPU-/3507 native UI-Prüfungen unter D3D9/D3D11 bestanden.
Getrennte Modi, Migration, Übernehmen/Verwerfen, unbekannte Herkunft, überlappende
Felder, Animation, begrenzte Ressourcenhaltung und Szenenwechsel geprüft.

Reparaturfeld-Trennung vom Nutzer im D3D11-Sandbox-Test bestätigt. Die vollständige
Einzelabnahme aller Feldquellen, PvP-Situationen und weiterer Hardware bleibt offen.

59 Neuinstallations-/Alpha-73-Prüfungen, 64 Upgrade-/Reparatur-/Rollbackprüfungen
ab 0.2.0-alpha.27 und 24 Installer-UI-Prüfungen auf isoliertem Desktop bestanden.
Nur künstliche Profile in eigenen Test-Sandboxes verwendet. Die einzelnen JAR-
Einträge sind bytegleich zum bestätigten Sandbox-Test; ZIP-Normalisierung geprüft.

Alle sieben Releaseassets wurden ohne Anmeldung über öffentliche URLs geladen,
Größen und SHA-256 geprüft und das RSA-Manifest verifiziert. Erst danach wurde
der Enhanced-Kanal aktiviert und sein Manifest erneut heruntergeladen/geprüft.
Der normale Updateabruf und der README-Installerlink liefern 0.2.0-alpha.28.
Vorherige Releaseassets sowie der ältere Enhanced-Kanal bleiben unverändert.
Quellstand auf main und feature/core-enhanced-0.2 gepusht; Quellrepo bleibt privat.
Keine Profile, Rohlogs, Originalspielarchive oder privaten Schlüssel hochgeladen.


## Grenzen

Weitere Feldquellen, PvP-/Turmkombinationen, GPUs, Wine/macOS und Langzeittests bleiben
gesondert. Bekannte Terrainhelligkeits- und native Absturzfragen sind nicht Teil
dieses Updates. Keine Änderung an Heilung, Reichweite oder Spielserverabfragen.
Unabhängige lokale Updater-Speicherpflege ist nicht enthalten.

## Belege

- `distribution/tests/repair-fields-alpha28-staging.json`
- `distribution/tests/repair-fields-alpha28-launch.json`
- `distribution/tests/alpha28-user-acceptance.json`

- `distribution/tests/editions-0.2-alpha.28-publication.json`
- `distribution/tests/editions-0.2-alpha.28-release-candidates.json`
