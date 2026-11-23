# Enhanced alpha.27 – Veröffentlichung freigegeben

Stand: 23.11.2026. Spielversion 1002133. Enhanced-Sequenz 108 autorisiert; Core unverändert.

## Prüfung

Native Forge-Meldungen vom Nutzer im D3D11-Sandbox-Test bestätigt. Die finalen
signierten Pakete bestanden Neuinstallation, Alpha-73-/alpha.26-Upgrade, Reparatur,
Rollback, Profilübernahme und Installer-UI-Prüfung (59/64/24 Checks).
Nur künstliche Testprofile verwendet. JAR-Einträge bytegleich zum bestätigten
Spielstand. Öffentliche Downloads werden vor der Kanalaktivierung geprüft.

- Build: `C:/PGFWork/forge-notices-alpha27/candidate-build`.
- Vollständige Gates: `C:/PGFWork/forge-notices-alpha27/candidate-tests`.
- Sandbox-Paket: `C:/PGFWork/forge-notices-alpha27/packages/Pirate-Galaxy-Forge-Enhanced-0.2.0-alpha.27`.
- 62 Edition-Gates, 22 Negativkontrollen und 48 Python-Tests bestanden.
- 29 gezielte Meldungsprüfungen; 23 Diagnoseprüfungen einschließlich Export-Allowlist.
- Native D3D9- und D3D11-Oberfläche: je 3.471 Checks bei 100/150/200 % HUD-Größe,
  inklusive ursprünglicher Detailbedienung, Mausdurchleitung, Fokus und Einstellungen.
- Original-PG-Meldungen bleiben erhalten. Keine zusätzlichen Serverabfragen.
- Core-Spiel-JAR unverändert:
  `918093c4e935e8f8af3eab689b956736843c73573332a574e82752eda0612310`.
- Enhanced-Spiel-JAR:
  `544429dcca7422d1372ddfb54d380dc4f68ad300e59ac4dcf1747a56fa447108`.

Auf separaten Nutzerauftrag alpha.26 R4/PID 4004 regulär beendet. Alpha.27 läuft
mit D3D11 als PID 19716 in `PGForge27NativeNotices`, Installation `C:/PGFWork/27NH/E`.
Drei Profile, 21 Dateien, geschützte Anmeldung und Mixer 8 %/nicht stumm frisch
übernommen und geprüft. Original-Anmeldeleser und 16 Selectorzyklen bestanden.
55 geladene Paketdateien, Sandboxie und D3D11 hash-/modulgeprüft. Verbundene
Sirius-Systemkarte und native Forge-Fundortbestätigung über der Leiste sichtbar.
Nutzer bestätigt den Test. Vollständige Einzelabnahme weiterer Bedienungsfälle
bleibt separat; Client jetzt offen lassen.
Startbeleg: `distribution/tests/forge-notices-alpha27-launch.json`.
Startlogs: kein ERROR/FATAL im Spiel-Errorlog, 20 bekannte MyGUI-Widget-Lookups.
Standardfehler enthält 22 ursprüngliche Zustandswarnungen und zwei Abbrüche alter
Ressourcenanfragen beim Dienstwechsel (`CancellationException`, vorhandener Guard).
Client danach verbunden und bedienbar; keine Meldungs-/Verify-/Linkfehler.
Die automatisierten UI-Prüfungen verwenden weiterhin native Offline-Fixtures;
der Startbeleg dokumentiert separat die verbundene Spielsitzung.

Sechs unabhängige Starter-/Updater-Dateien unverändert erhalten. Starter 17 bleibt
die Basis. Nur Enhanced wird nach Paket- und Downloadprüfung veröffentlicht.

Verbindlicher Paket-/Quellen-/Testbeleg:
`distribution/tests/forge-notices-alpha27-staging.json`.
Bedienung und Testplan: [Native Forge-Meldungen](ALPHA27-NATIVE-NOTICES.md).
