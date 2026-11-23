# Enhanced 0.2.0-alpha.25 – Veröffentlichung autorisiert

Der Nutzer bestätigt den D3D11-CSV-Test und hat die Veröffentlichung freigegeben.
Enhanced-Kanal Sequenz 106 wird nach Prüfung der öffentlichen Downloads aktiviert.
Core alpha.17 / Sequenz 16 bleibt unverändert; Nutzerclient bleibt geöffnet.
Spielversion 1002133, Starter 17. Sechs unabhängige Starteränderungen ausgeschlossen.
Anmeldung, drei Profile, 21 Zustandsdateien und Windows-Lautstärke wurden beim
Sandbox-Start übernommen. Die öffentliche Ausgabe enthält keine Nutzerdaten.

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
separate, nicht belegte Prüfungen. Die finalen signierten Pakete bestanden
59 Neuinstallations-/Alpha-73-Prüfungen, 64 Upgrade-/Reparatur-/Rollbackprüfungen
ab alpha.24 und 24 Installer-UI-Prüfungen auf isoliertem Desktop. Keine echten
Nutzerprofile verwendet. Spiel-JAR-Einträge bytegleich zum bestätigten Sandbox-Test.
Die öffentlichen Downloads werden vor der Kanalaktivierung erneut geprüft.
