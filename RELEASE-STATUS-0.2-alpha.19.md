# Release-Prüfstand: Enhanced 0.2.0-alpha.19

21.11.2026. Staffel-Schutzanzeige für Enhanced; Spielversion 1002133 und Starter
17 bleiben erhalten. Core bleibt alpha.17 / Sequenz 16. Enhanced alpha.19 /
Sequenz 100. Veröffentlichung und Quell-Push am 21.11.2026 nach bestätigtem
D3D11-Sandbox-Test beauftragt; Core bleibt unverändert.

Ausgangscommit: `acbeb4801d732bd253b17cfc5bb423e371cc7c32`.
Buildbelege binden die tatsächlichen Quellen über ihre Hashes. Der finale
Quellcommit wird im Releasekandidaten- und Publikationsbeleg festgehalten.

## Build und Prüfungen

- Finaler Build: `.build/editions/alpha19-squad-shield-final-build`.
- Finaler Testlauf: `.build/editions/alpha19-squad-shield-final-tests`.
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

Signierte Enhanced-Kandidaten: `.build/alpha19-final-candidates`.
Neuinstallation, Alpha-73-/alpha.18-Upgrade, Reparatur, Wiederanlauf, Rollback und
Profilübernahme werden an diesen finalen Bytes vor der Kanalaktivierung geprüft.
Core-alpha.17 dient unverändert als Editionsvergleich und wird nicht neu
veröffentlicht. Belege: `distribution/tests/editions-0.2-alpha.19-release-candidates.json`
und nach Upload `distribution/tests/editions-0.2-alpha.19-publication.json`.
Private Spielcaches, Profile und Anmeldungen gehören nicht in Releasepakete.

## Grenzen

Funktionsumfang, Datenregeln und weiterführender Testplan:
[ALPHA19-SQUAD-SHIELD.md](ALPHA19-SQUAD-SHIELD.md).
Die Nutzerbestätigung ist keine vollständige Matrix aller Schutzkombinationen,
Entfernungen, Szenenwechsel oder nicht anvisierten Staffelmitglieder. Nur empfangene
Werte werden dargestellt; unbekannte Kapazität wird nicht geschätzt. Keine neue
Wine-/macOS-, Langzeit- oder Leistungsmessung. Frühere Helligkeits-/Material- und
weitere Absturzbefunde werden durch diese Zusatzanzeige nicht behoben.
