# Core / Enhanced 0.2.0-alpha.16 – veröffentlicht

Core und Enhanced **0.2.0-alpha.16** veröffentlicht. Alle 14 öffentlichen Downloads,
RSA-Updatekanäle und README-Installerlinks wurden heruntergeladen und geprüft.
Sequenzen: Core 15, Enhanced 97. Binärquellencommit: `bfcb46fe154038a77432bf0f3fe4c805c9545366`.
Beleg: `distribution/tests/editions-0.2-alpha.16-publication.json`. Frühere Releasepakete bleiben unverändert.
Spielversion 1002133; Starter 16. Der rückwärtskompatible Schema-4-Berichtsdienst ist bereitgestellt.

Die getesteten Paketbytes wurden unverändert veröffentlicht. Alle sieben Assets je
Edition wurden anonym heruntergeladen und auf Größe, SHA-256 sowie die Manifest-
Signaturen geprüft. Erst danach wurden die Updatekanäle unter erneuter Prüfung
des vorherigen Stands umgestellt. Der alte Enhanced-Kanal `channel-alpha` und
vorherige Releases bleiben unverändert; vorherige Kanalmanifeste sind gesichert.
Der Quellstand ist auf `main` und `feature/core-enhanced-0.2` gepusht.

## Änderungen

Veränderte optionale Servercaches verhindern die Aktivierung nicht mehr.
Programmdateien bleiben streng geprüft. Fehlgeschlagene Updates werden mit
vorhandener und gewünschter Version angezeigt. Nur eine verifizierte Installation
mit passender Spielbasis darf ausdrücklich als Rückfall gestartet werden.
Diagnosen erhalten Fehlerphase, feste Kategorie, bereinigte Methodenframes und
getrennte installierte, angestrebte sowie gestartete Versionen. Bei alten Clients
bleiben Loginbereitschaft und nicht unterstützte JVM-Aufnahmen ehrlich unbekannt.

## Bestandene Prüfungen

- 60 Editionssuiten und sechs Negativkontrollen einschließlich nativer UI-/Fokus-
  Prüfungen für D3D9 und D3D11. Spiel-JARs und native Renderer sind bytegleich
  zum veröffentlichten alpha.15-Stand; keine Gameplay-Klasse wurde geändert.
- Je Edition 69 Starter-, 38 Updater- und 30 Zuverlässigkeitsprüfungen; signierter
  Starterwechsel 15 auf 16. Manipulierter Kern und JARs bleiben abgewiesen.
- Je Edition neun echte Prozessprüfungen einschließlich 45-Sekunden-Hänger,
  drei JVM-Aufnahmen und Schema-4-Export. 14 negative Berichtskontrollen,
  lokaler HTTP-Versand und Wiederholung bestanden; alte Schema-3-Berichte akzeptiert.
- 113 Reporterprüfungen sowie fünf Berichtsdienst-Tests bestanden. Alte lokale
  Schema-3-Diagnosen können mit unbekannten neuen Feldern als Schema 4 exportiert werden.
- 65 Installer-/Upgrade-/Reparatur-/Rollback-Prüfungen ab alpha.10 einschließlich
  der gegen das alte signierte Inventar geprüften Datei `r1034324255` bestanden.
  Weitere 64 Prüfungen ab alpha.15 mit nachträglich verändertem Cache bestanden.
  Profile, Rendererwahl, geschützte Testanmeldung, Einstellungen und Audio erhalten.
- 24 native Installer-Bedienprüfungen bestanden.
- Beide finalen signierten Pakete in eigener Sandbox installiert: sichtbare
  Kontooberfläche unter D3D11, externe Serververbindung, Live-Logs, Wiederöffnen,
  30-Sekunden-Aufnahme, drei JVM-Snapshots, ZIP-Speichern, freiwilliger Berichtsdialog
  und archivierte Sitzung. Insgesamt 70 automatische UI-Prüfungen bestanden.
  Kontooberflächen und Diagnoseansichten zusätzlich visuell geprüft.
- Die eigenen Testclients anschließend regulär beendet. Keine echten Profile,
  keine Kontoanmeldung und keine Rohberichte echter Nutzer veröffentlicht.

Die erste Paketprüfung fand eine zu enge Cache-Whitelist: versionierte Sprach-
cache-Dateien sind ebenfalls optionale Importe. Diese erlaubten Dateinamen wurden
vor dem erneuten Bau ergänzt und als Regression geprüft. Die früheren Kandidaten
wurden verworfen; sämtliche Installations- und UI-Belege beziehen sich auf
`.build/alpha16-final-candidates`, nicht auf den ersten Versuch.

## Belege und Grenzen

Maßgeblich: `distribution/tests/editions-0.2-alpha.16-release-candidates.json`,
`distribution/tests/editions-0.2-alpha.16-readiness.json` und
`distribution/tests/cache-upgrade-alpha16.json`. Quellen, Pakete, Installer,
Testdateien und Prüfergebnisse sind durch SHA-256 gebunden.

Die Daten belegen den reproduzierten Cache-Aktivierungsfehler und den Sandbox-
Startablauf. Eine Behebung sämtlicher Ladehänger auf betroffenen Spielerrechnern
oder ein authentifizierter Gameplay-Langzeittest ist damit nicht nachgewiesen.
Helligkeit, native Sirius-Ursache, weitere GPUs, Wine/macOS bleiben offen.
Installer und Starter sind weiterhin nicht per Windows-Authenticode signiert;
die Updatepakete und Kanalmanifeste besitzen die bestehende RSA-Signatur.

[Technik und Vergleich](ALPHA16-CACHE-UPGRADE.md)
