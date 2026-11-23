# Enhanced 0.2.0-alpha.27 – veröffentlicht

Enhanced **0.2.0-alpha.27** ist veröffentlicht, Updatekanal Sequenz 108 aktiv.
Alle sieben öffentlichen Downloads, RSA-Manifest, normaler Updatekanal und
README-Installerlink geprüft. Core alpha.17 / Sequenz 16, dessen Repository,
Kanal und Downloadassets bleiben unverändert. Spielversion 1002133, Starter 17.
Binärquellencommit: `9c5c00ff76bcb5de9745feb8faefaf82ab55bec3`. Beleg: `distribution/tests/editions-0.2-alpha.27-publication.json`.

Der Nutzer bestätigt die nativen Forge-Meldungen im D3D11-Sandbox-Test. Der laufende Client bleibt während der Veröffentlichung geöffnet.

## Prüfung

Native Forge-Meldungen vom Nutzer im D3D11-Sandbox-Test bestätigt. Die vollständige
Einzelabnahme aller Spielfunktionen und weiterer Hardware bleibt offen.

59 Neuinstallations-/Alpha-73-Prüfungen, 64 Upgrade-/Reparatur-/Rollbackprüfungen
ab 0.2.0-alpha.26 und 24 Installer-UI-Prüfungen auf isoliertem Desktop bestanden.
Nur künstliche Profile in eigenen Test-Sandboxes verwendet. Die einzelnen JAR-
Einträge sind bytegleich zum bestätigten Sandbox-Test; ZIP-Normalisierung geprüft.

Alle sieben Releaseassets wurden ohne Anmeldung über öffentliche URLs geladen,
Größen und SHA-256 geprüft und das RSA-Manifest verifiziert. Erst danach wurde
der Enhanced-Kanal aktiviert und sein Manifest erneut heruntergeladen/geprüft.
Der normale Updateabruf und der README-Installerlink liefern 0.2.0-alpha.27.
Vorherige Releaseassets sowie der ältere Enhanced-Kanal bleiben unverändert.
Quellstand auf main und feature/core-enhanced-0.2 gepusht; Quellrepo bleibt privat.
Keine Profile, Rohlogs, Originalspielarchive oder privaten Schlüssel hochgeladen.


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

- `distribution/tests/editions-0.2-alpha.27-publication.json`
- `distribution/tests/editions-0.2-alpha.27-release-candidates.json`
