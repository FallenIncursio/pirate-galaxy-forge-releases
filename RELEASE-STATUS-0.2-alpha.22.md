# Release-Prüfstand: Enhanced 0.2.0-alpha.22

Enhanced alpha.22 / Sequenz 103, Spielversion 1002133, Starter 17.
Core bleibt alpha.17 / Sequenz 16. Keine neuen nativen Bibliotheken.

BP-Import für alle Gebiete korrigiert, seltene Gegner getrennt behandelt,
begrenzte Scannerdiagnose in den vorhandenen bereinigten Export integriert.
Keine zusätzlichen Tooltips oder Änderungen am Scanfenster.
[Details, Grenzen und Sandbox-Testplan](ALPHA22-SCAN-MAPPING.md).

Der Nutzer bestätigt den D3D11-Sandbox-Test und autorisiert Veröffentlichung,
Quellpush und Enhanced-Kanalwechsel. Signierte Installationspakete und öffentliche
Downloads wurden vor der Kanalaktivierung geprüft. Der laufende Client bleibt offen.

## Veröffentlichung geprüft

Enhanced **0.2.0-alpha.22 / Sequenz 103** ist veröffentlicht. Alle sieben
öffentlichen Downloads, RSA-Release-/Kanalmanifest und README-Installerlink sind
geprüft. Erst danach wurde der Enhanced-Updatekanal aktiviert. Core bleibt
alpha.17 / Sequenz 16: Repository, Kanal, Assets und lokale Core-Dateien unverändert.
Vorherige Enhanced-alpha.21-Dateien und der alte Migrationskanal bleiben erhalten.

Binärquellencommit: `e7fc01f8231123b7fbf60f53bb12ebe27eb152a8`; Beleg: `distribution/tests/editions-0.2-alpha.22-publication.json`.
Der Nutzerclient blieb geöffnet.

## Signierte Releasepakete geprüft

62 Editionsgates, 18 Negativkontrollen, 9.267 Scanner-Checks und je 2.854 native
Enhanced-UI-Prüfungen auf D3D9/D3D11 bestanden. Finale Prüfung: `C:\PGF22PT`.
59 Neuinstallations-/Alpha-73-Prüfungen,
64 Upgrade-, Reparatur-, Rollback- und Profilprüfungen
ab Enhanced alpha.21 sowie 24 Installer-UI-Prüfungen bestanden.
Separate Sandboxie-Boxen mit künstlichen Profilen; der Nutzerclient bleibt offen.
Core wurde ausschließlich mit vorhandenen alpha.17-Paketen als Vergleich geprüft.

Ein erster aktueller Upgrade-Testaufbau wurde vor dem Sandbox-Start abgewiesen:
Core alpha.17 war versehentlich auch als Vorgänger angegeben. Der vollständige
Lauf verwendet den vorhandenen Core-alpha.16-Vorgänger und Enhanced alpha.21.
Die signierten Releasepakete wurden dabei nicht verändert; der Fehlbeleg bleibt erhalten.

RSA-Signaturen, Paket-Inventar und 8.772 Bibliotheksquellendateien geprüft.
Normalisierte Update-JARs enthalten exakt die Klassen und Ressourcen des vom
Nutzer bestätigten Teststands. Keine privaten Profile, Rohlogs oder Spielcaches.
Die öffentliche Downloadprüfung vor der Kanalaktivierung ist im Publikationsbeleg dokumentiert.
Beleg: `distribution/tests/editions-0.2-alpha.22-release-candidates.json`.

## Weitere bekannte Grenzen

Kamerabhängige Helligkeit, die native Sirius-Absturzursache und bereits
dokumentierte Materialprobleme werden durch dieses BP-Update nicht behoben.
Andere GPUs/Treiber, Wine/macOS und Langzeittests bleiben separat.
Installer ohne Windows-Authenticode-Signatur; Updates mit vorhandener RSA-Identität.

## Automatische Prüfung abgeschlossen

- Frische Builds: `C:\PGF22\final-build`, Prüfung: `C:\PGF22\final-tests`.
- 62 Editionsgates und 18 Negativkontrollen bestanden.
- 9.267 Scanner-Checks, 18 Export-/Diagnose-Checks und 8 Importtestfälle bestanden.
- Je 2.854 native Enhanced-Oberflächenprüfungen auf D3D9 und D3D11 bestanden,
  dazu die bestehenden Fokus-, Rendering- und Core-Regressionsprüfungen.
- Alle 138 Core-Helferklassen, Core-Spiel-JAR und nativen Eingaben sind gegenüber
  dem veröffentlichten Vergleichsstand bytegleich; 135 Klassen bleiben zwischen
  Core und Enhanced identisch.
- Diagnose-ZIP enthält ausschließlich die fünf erlaubten Dateien; private
  Testmarker aus Anmeldung und Speicherabbild sind nicht enthalten.
- `git diff --check` ohne Fehler. Kein Live-Server und keine echten Drops getestet.

Der erste Prüflauf scheiterte an einer neuen Testannahme: Ein Imperial-Sniper
hatte neben seltenen Farb-BPs auch allgemeine Gold-BP-Regeln. Die Diagnose war
korrekt; der Variantentest nutzt nun eine eindeutige isolierte Regel. Der finale
vollständige Prüflauf ist erfolgreich. Beide Prüfverzeichnisse bleiben erhalten.

Private Paketablage:
`C:\PGF22\packages\Pirate-Galaxy-Forge-Enhanced-0.2.0-alpha.22`.
Der Paketbeleg unter `distribution/tests/scan-drops-alpha22-staging.json` bindet
Dateihashes, Build, Tests und Veröffentlichungssperre. Das ebenfalls lokal
verpackte Core dient ausschließlich als unveränderter Vergleich.

Der allgemeine BP-Sandbox-Test ist vom Nutzer bestätigt. Nicht bestätigt ist die
vollständige Abdeckung sämtlicher Gegner, Level und Sondervarianten.
Die derzeit nicht sicher unterscheidbaren DS-/Missionsbedingungen sind keine
behobenen oder verifizierten Dropzuordnungen; siehe Detaildokument.

## Auf Nutzerauftrag gestarteter Sandbox-Test

Enhanced alpha.22 läuft mit D3D11 in PGForgeAlpha22ScanDrops / C:\PGF22A,
PID 29744. Startkopie: C:\PGF22V\E\versions\0.2.0-alpha.22.
Der vorherige Client wurde auf ausdrücklichen neuen Auftrag regulär geschlossen.
Drei Profile und 19 Zustandsdateien einschließlich Anmeldung/gerätegebundener
Identität übernommen und hashgeprüft; Windows-Lautstärke 8 %, nicht stumm.
Anmeldeleser und 16 Selectorzyklen erfolgreich; 56 geladene Dateihashes,
Sandboxie/D3D11, Verbindung und sichtbare Planetenoberfläche geprüft.
Keine ERROR/FATAL-, Verify- oder Linkfehler im Spiel-Startlog. 20 bekannte
MyGUI-Widget-Lookups separat dokumentiert. Dieser Start wurde anschließend vom Nutzer für die Veröffentlichung bestätigt.
Beleg: `distribution/tests/scan-drops-alpha22-launch.json`. Veröffentlichung jetzt autorisiert.
