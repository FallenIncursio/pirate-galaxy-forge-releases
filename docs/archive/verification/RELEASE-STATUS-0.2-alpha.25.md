> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Enhanced 0.2.0-alpha.25 – veröffentlicht

Enhanced **0.2.0-alpha.25** ist veröffentlicht, Updatekanal Sequenz 106 aktiv.
Alle sieben öffentlichen Downloads, RSA-Manifest, normaler Updatekanal und
README-Installerlink geprüft. Core alpha.17 / Sequenz 16, dessen Repository,
Kanal und Downloadassets bleiben unverändert. Spielversion 1002133, Starter 17.
Binärquellencommit: `8d73f76fa87f685bf930644112750186a9911017`. Beleg: `distribution/tests/editions-0.2-alpha.25-publication.json`.

Der Nutzer bestätigt den D3D11-CSV-Test. Sein Client blieb während der Veröffentlichung geöffnet.

## Prüfung

62 Editionsgates und 22 Negativkontrollen bestanden. Darin enthalten: 41 gezielte
CSV-Prüfungen und je 3.202 native Enhanced-UI-Prüfungen unter D3D9 und D3D11.
Native Tests mit 1024×768/100 %, 1920×1080/150 % und 3440×1440/200 %: Filter,
Merkliste, zweite Seite, Export aller 44 Treffer, Änderung der Suche während des
Exports, leere Auswahl und Layout ohne Überschneidungen. Screenshots geprüft.

Separater strenger CSV-Parserimport: 7 Zeilen, 10 Spalten; Umlaute, Anführungszeichen,
eingebetteter Zeilenumbruch, Formeltextschutz und Mengen unverändert zurückgelesen.
Schreibfehler, doppelte Klicks, Namenskollisionen und Pilotwechsel gezielt geprüft.
Core-Spiel-JAR und 138 Helferklassen sowie sämtliche nativen Bibliotheken bytegleich
zum vorherigen Stand. Enhanced enthält 372 Helferklassen. Keine neuen RPCs.

Ein erster D3D11-Prüflauf scheiterte vor dem CSV-Test beim bestehenden Anzeige-Apply
an `AccessDeniedException` beim Ersetzen seiner lokalen Test-Einstellungsdatei.
Der Fehlerbeleg bleibt erhalten; im vollständigen frischen Prüflauf trat er nicht
erneut auf. Keine Änderung am gemeinsamen Preference-Store und keine Behauptung,
die Ursache dieser Dateizugriffssperre sei durch das CSV-Feature behoben.

Maßgeblich: `final-build`, `final-tests` und
`packages/Pirate-Galaxy-Forge-Enhanced-0.2.0-alpha.25` unter dem obigen Arbeitsordner.
Sanitisierter Beleg: `distribution/tests/blueprint-csv-alpha25-staging.json`.
Der erste Zwischenbuild ist kein Startkandidat. Build-/Test-Hashes und Editionen
werden bei der privaten Paketierung erneut abgeglichen.

Ingame-Test vom Nutzer bestätigt. Excel-/LibreOffice-Liveimport und Wine bleiben
separate, nicht belegte Prüfungen.

59 Neuinstallations-/Alpha-73-Prüfungen, 64 Upgrade-/Reparatur-/Rollbackprüfungen
ab 0.2.0-alpha.24 und 24 Installer-UI-Prüfungen auf isoliertem Desktop bestanden.
Nur künstliche Profile in eigenen Test-Sandboxes verwendet. Die einzelnen JAR-
Einträge sind bytegleich zum bestätigten Sandbox-Test; ZIP-Normalisierung geprüft.

Alle sieben Releaseassets wurden ohne Anmeldung über öffentliche URLs geladen,
Größen und SHA-256 geprüft und das RSA-Manifest verifiziert. Erst danach wurde
der Enhanced-Kanal aktiviert und sein Manifest erneut heruntergeladen/geprüft.
Der normale Updateabruf und der README-Installerlink liefern 0.2.0-alpha.25.
Vorherige Releaseassets sowie der ältere Enhanced-Kanal bleiben unverändert.
Quellstand auf main und feature/core-enhanced-0.2 gepusht; Quellrepo bleibt privat.
Keine Profile, Rohlogs, Originalspielarchive oder privaten Schlüssel hochgeladen.


- `distribution/tests/editions-0.2-alpha.25-publication.json`
- `distribution/tests/editions-0.2-alpha.25-release-candidates.json`
