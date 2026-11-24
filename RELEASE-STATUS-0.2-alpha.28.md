# Enhanced 0.2.0-alpha.28 – Veröffentlichung autorisiert

Der Nutzer bestätigt die Reparaturfeld-Trennung im D3D11-Sandbox-Test. Der laufende Client bleibt während der Veröffentlichung geöffnet.
Spielversion 1002133, Starter 17, Enhanced-Sequenz 109; Core alpha.17 / 16 unverändert.

## Prüfung

64 Editionsprüfungen, 25 Negativkontrollen, 48 Python-Tests, 35 Enhanced-Funktionssuiten,
56 Reparaturprüfungen und je 457 GPU-/3507 native UI-Prüfungen unter D3D9/D3D11 bestanden.
Getrennte Modi, Migration, Übernehmen/Verwerfen, unbekannte Herkunft, überlappende
Felder, Animation, begrenzte Ressourcenhaltung und Szenenwechsel geprüft.

Reparaturfeld-Trennung vom Nutzer im D3D11-Sandbox-Test bestätigt. Die finalen
signierten Pakete bestanden Neuinstallation, Alpha-73-/alpha.27-Upgrade, Reparatur,
Rollback, Profilübernahme und Installer-UI-Prüfung (59/64/24 Checks).
Nur künstliche Testprofile verwendet. JAR-Einträge bytegleich zum bestätigten
Spielstand. Öffentliche Downloads werden vor der Kanalaktivierung geprüft.

## Grenzen

Weitere Feldquellen, PvP-/Turmkombinationen, GPUs, Wine/macOS und Langzeittests bleiben
gesondert. Bekannte Terrainhelligkeits- und native Absturzfragen sind nicht Teil
dieses Updates. Keine Änderung an Heilung, Reichweite oder Spielserverabfragen.
Unabhängige lokale Updater-Speicherpflege ist nicht enthalten.

## Belege

- `distribution/tests/repair-fields-alpha28-staging.json`
- `distribution/tests/repair-fields-alpha28-launch.json`
- `distribution/tests/alpha28-user-acceptance.json`
