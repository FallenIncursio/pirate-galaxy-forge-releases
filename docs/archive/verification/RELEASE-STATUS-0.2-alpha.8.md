> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Release-Prüfstand: Enhanced 0.2.0-alpha.8

## Veröffentlichung geprüft

Enhanced **0.2.0-alpha.8** veröffentlicht. Alle 7 öffentlichen Downloads,
zugehörigen RSA-Updatekanäle und README-Installerlinks wurden heruntergeladen und geprüft.
Aktualisierte Sequenzen: Enhanced 89. Binärquellencommit: `f833a34ce6494b8dfa56475d5ad5371ba57a2bef`.
Beleg: `distribution/tests/editions-0.2-alpha.8-publication.json`. Frühere Releasepakete bleiben unverändert.
Core bleibt unverändert auf 0.2.0-alpha.7, Sequenz 7.
Live-OTB-Datenfluss und serverseitige Endauswertung bleiben unbestätigt; keine Belohnungs- oder Sperrfreiheitsgarantie.

Abschließende Releaseprüfungen: 53 Neuinstallations-/Alpha-73-Prüfungen, 56 Upgrade-/Reparaturprüfungen und 24 Installer-Oberflächenprüfungen bestanden. Die Belege binden die geprüften Kandidaten über ihre SHA-256-Werte.

## Historischer Vorbereitungs- und Diagnosestand

Stand: 17.11.2026. Veröffentlichung nach dem Enhanced-D3D11-Sandboxstart
beauftragt. Nur Enhanced erhält alpha.8, Sequenz 89, Starterrevision 12.
Core bleibt auf alpha.7, Sequenz 7. Frühere Releases bleiben erhalten.

Änderung: [passives OTB-Widget und seine Grenzen](../technical/ALPHA8-OTB-ACTIVITY.md).
Der Nutzer konnte noch kein echtes OTB testen. Die Freigabe ist keine
Bestätigung des Live-Datenflusses oder der serverseitigen Endauswertung.

## Nachgewiesen

- 461 gezielte OTB-Prüfungen gegen die Clientlogik, Datenlücken, Aktualität,
  Rückschritte sowie Teilnehmer-/Verbindungswechsel.
- 40 Editionssuiten, sechs Negativkontrollen und je 624 native Enhanced-
  Oberflächenprüfungen unter D3D9/D3D11 mit mehreren Auflösungen/HUD-Größen.
- Core-Spiel-JAR und native Bibliotheken gegenüber alpha.7 unverändert.
  OTB-Code ausschließlich in Enhanced; keine zusätzlichen Serverabfragen.
- Verbundene Enhanced-D3D11-Spielsitzung, sichtbare OTB-Einstellung, Profil-
  und Anmeldungserhalt sowie Windows-Mixer im Sandbox-Teststand beobachtet.

Die signierten Releasepakete haben zusätzlich 53 Neuinstallations-/Alpha-73-,
56 Upgrade-/Reparatur- und 24 Installer-Oberflächenprüfungen bestanden.
Das Enhanced-Upgrade wurde von alpha.7 auf alpha.8 geprüft; als unveränderte
Core-Gegenprobe dient alpha.7 mit alpha.6 als Vorgänger. Die Prüfung deckt
Wiederanlauf, Rollback, Editionsverwechslung, Profile, geschützte Anmeldungen
und Renderer-Erhalt ab. Je Edition bestehen außerdem 32 Updater- und 29
Grafikstartprüfungen sowie der signierte Starterwechsel 11 → 12. Drei native
Fehlerstartfälle wurden mit dem tatsächlichen Enhanced-Starter geprüft.
Der abschließende Paketbeleg bindet die Ergebnisse an Hashes und Quellcommit:
`distribution/tests/editions-0.2-alpha.8-release-candidates.json`.

## Offene Grenzen

Keine bestätigte Live-OTB-Übermittlungsrate/Vollständigkeit, kein Mitschnitt einer
Partie und kein Vergleich mit einer echten Endauswertung. Clientkriterien sind
keine Garantie für Belohnung oder Sperrfreiheit. Keine absichtliche Inaktivität
oder provozierte Sperre zum späteren Testen erforderlich.
Weitere GPUs/Treiber, Wine und Langzeittests bleiben gesondert. Der Installer
besitzt keine Windows-Authenticode-Signatur; Updatepakete sind RSA-signiert.
