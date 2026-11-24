> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Core / Enhanced 0.2.0-alpha.17 – veröffentlicht

Core und Enhanced **0.2.0-alpha.17** sind veröffentlicht. Alle 14 öffentlichen Downloads,
RSA-Release-/Kanalmanifeste und README-Installerlinks sind heruntergeladen und geprüft.
Sequenzen: Core 16, Enhanced 98. Spielversion 1002133, Starter 17.
Binärquellencommit: `2bc3a56f0c46b363fd99848e32f8e3f6c64dab27`; Beleg: `distribution/tests/editions-0.2-alpha.17-publication.json`.
Die vorherigen Releases und der ältere Enhanced-Kanal bleiben unverändert.

## Änderungen

- Beide Editionen: anfängliche Namens-/Beziehungs-/Symbolmeldungen bleiben bis
  zum Layout erhalten; unabhängige Lebens-/Schildbalken und geschlossene Anzeigen
  werden sicher behandelt. Begrenzte UI-/Audio-Diagnose, kein automatischer Versand.
- Enhanced: lokale angenommene Systemnutzungen und Bewegungssignale, Signalalter,
  Warn-Countdown und gekennzeichnete Testvorschau. Keine zusätzlichen Spielserver-
  abfragen. Serverwertung bleibt unbekannt; keine garantierte Aktivitätsfrist.
- Spielbasis, native Rendererdateien, Profilformate und Editionsgrenzen bleiben erhalten.

## Prüfung und Veröffentlichung

62 Testsuiten und 6 Negativkontrollen, native D3D9-/D3D11-Bedienprüfungen,
698 OTB-Checks und 1.239 Enhanced-Bedienchecks je Renderer bestanden.
59 Neuinstallations-/Alpha-73-Prüfungen, 64 Upgrade-/Reparatur-/Rollbackprüfungen
von alpha.16 und 24 Installer-Bedienprüfungen mit künstlichen Profilen bestanden.

Der Nutzer bestätigt den Enhanced-Sandbox-Stand mit neuem Widget. Gespeicherte
Anmeldung, drei Profile, Einstellungen und Windows-Lautstärke wurden bei diesem
Spieltest übernommen. Der veröffentlichte Game-JAR entspricht exakt diesem
Teststand. Die Starter-/Installerpakete wurden danach neu gebündelt und geprüft.
Der laufende Nutzerclient wurde für die Veröffentlichung nicht geschlossen.

Alle sieben Assets je Edition wurden ohne Anmeldung über ihre öffentlichen
URLs heruntergeladen, anhand von SHA-256 und Größe geprüft und beide RSA-
Manifeste verifiziert. Erst danach wurden die Kanäle unter erneuter Prüfung
des vorherigen Assetstands aktiviert. Frühere Manifeste sind als Kanalassets
gesichert. Normale Update-URLs und README-Installerlinks liefern die neue Version.
Quellstand auf main und feature/core-enhanced-0.2 gepusht; Quellrepo bleibt privat.
Keine Spielerprofile, Rohlogs, Originalspielarchive oder privaten Schlüssel hochgeladen.

## Verbleibende Grenzen

Vollständige OTB-Matchabläufe, Warnübergänge im echten Match, Tod/Wiederbelebung
und alle Namens-/Beziehungszustände sind nicht umfassend abgenommen. Core hat
keine eigene neue Gameplay-Bestätigung. Andere GPUs/Treiber, Wine/macOS und
quantitative Langzeittests bleiben separat. Kamerabhängige Helligkeit, native
Sirius-Absturzursache und der reproduzierte D3D11-Materialfehler bleiben offen.
Installer ohne Windows-Authenticode-Signatur; Updates mit bestehender RSA-Identität.

## Zugehörige Belege

- `distribution/tests/editions-0.2-alpha.17-publication.json`
- `distribution/tests/editions-0.2-alpha.17-release-candidates.json`
- `distribution/tests/alpha17-user-acceptance.json`
- `distribution/tests/otb-widget-alpha17.json`
- `distribution/tests/editions-0.2-alpha.17-otb-widget-launch.json`
