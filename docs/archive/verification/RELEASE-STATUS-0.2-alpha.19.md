> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Release-Prüfstand: Enhanced 0.2.0-alpha.19

21.11.2026. Staffel-Schutzanzeige für Enhanced; Spielversion 1002133 und Starter
17 bleiben erhalten. Core bleibt alpha.17 / Sequenz 16. Enhanced alpha.19 /
Sequenz 100, veröffentlicht am 21.11.2026 nach bestätigtem D3D11-Sandbox-Test.
Core-Repo, Core-Downloads und Core-Kanal bleiben unverändert.

Ausgangscommit: `acbeb4801d732bd253b17cfc5bb423e371cc7c32`.
Buildbelege binden die tatsächlichen Quellen über ihre Hashes. Der finale
Quellcommit ist `5f2485cda499d6d6752e3056b7c282e098565850`;
die späteren Publikationsbelege ändern keine veröffentlichten Paketbytes.

## Build und Prüfungen

- Finaler Build: `.build/editions/alpha19-squad-shield-final-build`.
- Bestätigter Spieltest: `.build/editions/alpha19-squad-shield-final-tests`.
- Abschließende Veröffentlichungsgates: `.build/editions/alpha19-release-tests`.
- Beide Editionsbuilds und alle 62 Editionsprüfungen bestanden; 10 negative
  Kontrollen haben die absichtlich ungültigen Eingaben zurückgewiesen.
- 143 Schutzmodellprüfungen und 103 bestehende Staffelprüfungen bestanden.
- Je 1.944 native Enhanced-UI-Prüfungen unter D3D9 und D3D11 bestanden,
  einschließlich 100/150/200 % HUD-Größe, Apply/Discard, Prozentbreite,
  passiver Umhüllung, unveränderter Klickziele und Widget-Neuerzeugung.
- 135 gemeinsame Klassen sind zwischen Core und Enhanced identisch.
  Core-Spiel-JAR und native Bibliotheken bleiben gegenüber dem vorherigen
  finalen Stand bytegleich; keine neue Core-Funktion.

SHA-256 der finalen Spiel-JARs:

- Enhanced: `30da05088d773c1f1186f5535c1dfc207a8404c1ef692f1d4ad18c3f505a92ff`
- Core: `918093c4e935e8f8af3eab689b956736843c73573332a574e82752eda0612310`

## Spieltest und Releasepakete

Enhanced wurde mit exakt dieser Spiel-JAR in der Sandbox mit D3D11 gestartet.
Drei Profile, 19 Zustandsdateien, eine geschützte Anmeldung und Windows-Mixer
wurden übernommen und geprüft. Verbundene Orbitszene beobachtet; der Nutzer
bestätigte die Staffel-Schutzanzeige anschließend mit „funktioniert“.
Beleg: `distribution/tests/squad-shield-alpha19-launch.json`.

## Veröffentlichung und Installationsprüfung

Die finalen signierten Pakete unter `.build/alpha19-final-candidates` bestanden
59 Neuinstallations-/Alpha-73-Prüfungen, 64 alpha.18-Upgrade-/Reparatur-/Rollback-
Prüfungen und 24 Installer-Bedienprüfungen mit künstlichen Profilen.
Core-alpha.17 diente unverändert als Editionsvergleich und wurde nicht neu
veröffentlicht. Der laufende Nutzerclient blieb während der Veröffentlichung offen.

Alle sieben Enhanced-Assets wurden über ihre öffentlichen URLs heruntergeladen
und anhand von SHA-256 und Größe geprüft. Release- und Kanalmanifest wurden mit
der bestehenden RSA-Identität verifiziert. Erst danach wurde der Enhanced-Kanal
unter erneuter Prüfung seines vorherigen Stands auf Sequenz 100 aktualisiert.
Das vorige Kanalmanifest bleibt als Backup erhalten. Normaler Update-Link und
README-Installerlink liefern alpha.19. Core-Kanal, Core-Repo und alte Releaseassets
sind unverändert; der ältere Enhanced-Kanal bleibt erhalten.
Quellstand auf main und feature/core-enhanced-0.2 gepusht; Quellrepo bleibt privat.
Keine Spielerprofile, Anmeldedaten, Rohlogs, Originalspielarchive oder privaten
Schlüssel wurden hochgeladen.

Belege: `distribution/tests/editions-0.2-alpha.19-release-candidates.json`,
`distribution/tests/editions-0.2-alpha.19-publication.json` und
`distribution/tests/alpha19-user-acceptance.json`.

## Grenzen

Funktionsumfang, Datenregeln und weiterführender Testplan:
[ALPHA19-SQUAD-SHIELD.md](../technical/ALPHA19-SQUAD-SHIELD.md).
Die Nutzerbestätigung ist keine vollständige Matrix aller Schutzkombinationen,
Entfernungen, Szenenwechsel oder nicht anvisierten Staffelmitglieder. Nur empfangene
Werte werden dargestellt; unbekannte Kapazität wird nicht geschätzt. Keine neue
Wine-/macOS-, Langzeit- oder Leistungsmessung. Frühere Helligkeits-/Material- und
weitere Absturzbefunde werden durch diese Zusatzanzeige nicht behoben.
