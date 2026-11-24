> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Core / Enhanced 0.2.0-alpha.15 – veröffentlicht

Core und Enhanced **0.2.0-alpha.15** veröffentlicht. Alle 14 öffentlichen Downloads,
zugehörigen RSA-Updatekanäle und README-Installerlinks wurden heruntergeladen und geprüft.
Aktualisierte Sequenzen: Core 14, Enhanced 96. Binärquellencommit: `4682bc65afd1b6a95d5a778fe4257446568f14a2`.
Beleg: `distribution/tests/editions-0.2-alpha.15-publication.json`. Frühere Releasepakete bleiben unverändert.
Spielversion 1002133; Starter 15. Der kompatible Schema-3-Berichtsdienst ist bereitgestellt.

Stand: 20.11.2026. Die getesteten Installer und Spielpakete wurden unverändert
veröffentlicht. Alle sieben Assets je Edition wurden ohne Anmeldung über ihre
öffentlichen URLs heruntergeladen und anhand von Größe und SHA-256 geprüft.
Die RSA-Signaturen beider Release-Manifeste sind gültig.

Erst nach diesen Prüfungen wurden beide Updatekanäle unter erneuter Prüfung des
vorherigen Assetstands umgestellt. Die aktiven Kanalmanifeste wurden auch über
ihre normalen URLs geladen und signaturgeprüft. Die vorherigen alpha.14-Manifeste
sind als Kanal-Assets gesichert; alpha.14-Releases und der alte Enhanced-Kanal
`channel-alpha` bleiben unverändert. Beide öffentlichen README-Installerlinks
liefern die geprüften alpha.15-Dateien. Der Quellstand ist auf `main` und
`feature/core-enhanced-0.2` gepusht; die Quellrepo bleibt privat.

Die Sandbox-Prüfung umfasst den tatsächlichen Diagnoseablauf beider Editionen
mit D3D11, einschließlich sichtbarer Oberfläche vor der Anmeldung, Aufnahme,
Export und archivierter Sitzung. Die eigenen Testclients wurden regulär beendet.
Kein echtes Spielerprofil und keine Anmeldung am Spielkonto wurden verwendet.
Die in den geprüften Paketen eingebetteten Vorbereitungsnotizen bleiben unverändert;
die aktuellen Release-Seiten dokumentieren die Veröffentlichung.

## Änderungen

Live-Logs und Diagnose sind direkt im Starter, über dessen Infobereichsymbol,
beim erneuten Öffnen und per Startmenüeintrag erreichbar. Eine freiwillige
30-Sekunden-Aufnahme sammelt Prozessdaten und drei begrenzte JVM-Snapshots.
Export und freiwilliger Versand enthalten denselben strukturierten Umfang.
Die letzte Sitzung bleibt nach Spielende verfügbar. Ein Fehler vor dem JVM-Start
wird mit fehlender JVM-Aufnahme ausdrücklich gekennzeichnet.

Ressourcenaufträge werden getrennt verfolgt; unverwandte Downloads und wiederholte
Phasenmeldungen verdecken einen blockierten Auftrag nicht mehr. Die Diagnose
beginnt vor dem Lesen der Einstellungen und verwendet bei Schreibproblemen einen
temporären Rückfall. Der Berichtsdienst verarbeitet die neuen strukturierten
Daten und bleibt mit Schema 1 und 2 kompatibel. Keine zusätzlichen Spielserver-RPCs,
kein automatischer Berichtversand, keine Rohlogs in Exporten oder Berichten.

## Prüfung

- 60 Editionssuiten, sechs Build-Negativkontrollen und native UI-/Fokusprüfungen
  mit D3D9 und D3D11 bestanden.
- Je Edition 59 Starterprüfungen, 30 Zuverlässigkeits- und 32 Updaterprüfungen;
  signierter Starterwechsel 14 auf 15 und 113 Absturzreporterprüfungen bestanden.
- Je Edition neun echte Prozessprüfungen einschließlich einer 45-Sekunden-
  Blockade trotz gleichzeitigem Datenfortschritt anderer Ressourcen. Elf negative
  Berichtskontrollen sowie lokale HTTP-Rundreise und Wiederholungsversand bestanden.
- 58 Installer-/Upgradeprüfungen von alpha.14, 55 Neuinstallations-/Alpha73-
  Prüfungen sowie 24 Installer-Bedienprüfungen bestanden. Künstliche Profile,
  geschützte Anmeldung, Einstellungen und eigene Audiodateien bleiben erhalten.
- Beide unveränderten signierten Kandidaten tatsächlich installiert und mit
  D3D11 bis zur Anmeldeoberfläche gestartet. Beschädigte Einstellungen,
  Diagnosezugang, Wiederöffnen, drei JVM-Aufnahmen, Prozessmesswerte, nativer
  Speicherdialog, gültiger ZIP-Export und freiwilliger Berichtsdialog geprüft.
  Eigene Testclients anschließend regulär beendet; archivierte Diagnose geöffnet.
- Serverbereitstellung mit Quellabgleich, Rückfallmöglichkeit und HTTPS-Prüfungen
  für Schema 1/2/3 bestanden. Nur synthetische Berichte verwendet und entfernt.

Maßgebliche Belege: `distribution/tests/editions-0.2-alpha.15-release-candidates.json`,
`distribution/tests/startup-observability-alpha15.json` und
`distribution/tests/editions-0.2-alpha.15-readiness.json`. Sie binden Quellen,
Spiel-JARs, signierte Pakete, Installer und Testergebnisse an SHA-256-Werte.

Die Sandbox-Bedienprüfung wurde nach Korrektur dreier Automationsdetails
fortgesetzt: sichtbarer Start des Testfensters, Prozessabfrage ohne in der Box
gesperrtes WMI und eindeutiges Dateiname-Editfeld im Windows-Speicherdialog.
Die finalen Kandidaten wurden dabei nicht verändert. Eine im ersten Kandidaten
erkannte Zeichenkodierung wurde vor dessen Ersatz und erneuter Prüfung behoben.
Frühere alpha.15-Testkandidaten sind verworfen.

## Grenzen

Kein echtes Spielerprofil und kein laufendes Gameplay wurden für diese Tests
verwendet. Die sichtbare Anmeldeoberfläche und der Diagnoseablauf sind geprüft;
eine Behebung sämtlicher Hänger auf betroffenen Spielerrechnern ist damit nicht
bewiesen. Loginbereitschaft ist ein internes Signal und kein eigener Nachweis
eines sichtbaren Bildes. Ein nativer Stillstand kann JVM-Snapshots verhindern;
Prozessmesswerte und Startverlauf bleiben dann verfügbar.

Kamerabhängige Helligkeit, konkrete native Sirius-Absturzursache, andere GPUs,
Wine/macOS und Langzeit-Gameplay bleiben offen. Bisherige Spiel- und native
Rendererklassen bleiben unverändert; geändert sind die gemeinsamen Diagnose-
und Ressourcenhelfer. Installer und Starter besitzen weiterhin keine
Windows-Authenticode-Signatur; Updatepakete sind RSA-signiert.

[Bedienung, Technik und Datenschutz](../technical/ALPHA15-STARTUP-DIAGNOSTICS.md)
