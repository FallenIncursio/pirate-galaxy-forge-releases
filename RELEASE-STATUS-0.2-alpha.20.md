# Release-Prüfstand: Enhanced 0.2.0-alpha.20

21.11.2026. Der Nutzer bestätigt den nachgebesserten D3D11-Sandbox-Test mit
„okey, funktioniert“ und hat Veröffentlichung, Quellstand-Push, Updatekanal und
Downloadprüfung ausdrücklich freigegeben. Spielversion **1002133**, Starter **17**,
Enhanced-Sequenz **101**. **Core bleibt alpha.17 / Sequenz 16 unverändert.**

## Inhalt und Abnahme

- Suche, Status, Sortierung, System und zur Hauptkategorie passende Bereiche im
  Pilotenprofil. Originale goldene Abschlussmedaille und Datumszeile; offene
  Einträge behalten ihre silberne Medaille und ihren Fortschrittsbalken.
- Forge → Anzeige → HUD & Grafik: „Errungenschaften: erweiterte Ansicht“ mit
  Übernehmen/Verwerfen und Rückkehr zum ursprünglichen Renderer, auch bei einem
  bereits geöffneten Profil. Gespeicherte Filter bleiben erhalten.
- Lokale Zuordnungen und Anzeige aus bereits empfangenen Daten. Keine zusätzliche
  Spielserverabfrage, keine Änderung an Punkten, Belohnungen oder Sichtbarkeitsregeln.
- Lange Namen werden vollständig umgebrochen; Zeilen werden sparsam wiederverwendet.
  Der frühere Fehler beim Laden der Zeilenvorlage ist mit der ursprünglichen
  Archivgruppen-Ermittlung korrigiert und als Negativkontrolle abgesichert.

Der bestätigte r4-Spielbuild bleibt unverändert. Im Starttest wurden Profile,
Einstellungen und gespeicherte Anmeldung übernommen; Windows-Mixer ebenfalls.
Anmeldeleser, 16 Selectorzyklen, 51 geladene Dateihashes, D3D11 und Serververbindung
wurden geprüft. Angemeldeter Hangar sichtbar; keine ERROR/FATAL-, Verify-/Link-
oder Layoutladefehler im geprüften Startlog. Bekannte generische MyGUI-Lookups
bleiben im lokalen Startbeleg dokumentiert. Der Nutzerclient bleibt geöffnet.

## Automatische Prüfung

- 62 Editionsgates und 14 zurückgewiesene Negativkontrollen.
- 143 Errungenschaftenchecks und je 2262 native Enhanced-UI-Checks auf D3D9/D3D11,
  einschließlich 100/150/200 % HUD-Skalierung, Gold-/Offen-Zeilenwechsel,
  kombinierter Filter und Ein-/Ausschalten der Erweiterung.
- Präferenzen v2 übernehmen v1; System und Bereich bleiben bei HUD-Wechseln erhalten.
- Core-Spiel-JAR, 135 gemeinsame Klassen und native Bibliotheken bytegleich.
- Finale signierte Pakete: **59** Prüfungen für Neuinstallation/Alpha-73-Upgrade,
  **64** für Upgrade von alpha.19, Reparatur, Rollback und Profilübernahme sowie
  **24** Installer-UI-Prüfungen bestanden. Installierte Spiel-JARs entsprechen
  exakt dem bestätigten Sandbox-Spielbuild; Testprofile waren künstliche Fixtures.
- Signatur, vollständiges Paket-Inventar und Bibliotheksquellen geprüft.
  Der endgültige Veröffentlichungsbeleg folgt nach der öffentlichen Downloadprüfung.

Belege im Quellrepository:
`distribution/tests/achievements-alpha20-refinement-readiness.json`,
`distribution/tests/achievements-alpha20-r4-launch.json`,
`distribution/tests/alpha20-user-acceptance.json`,
`distribution/tests/editions-0.2-alpha.20-release-candidates.json`.

Spiel-JAR Enhanced:
`821802c4ddc0dbb80f1e31a27dcd1654889baffe16ac110ca33b058a54e4d00f`.
Ausgangscommit: `11089f0efe2ddb2b51bfe3e9649a1c07be4b4c46`.
Buildbelege binden die tatsächlichen Dateien über SHA-256; der finale Quellcommit
wird im Veröffentlichungsbeleg festgehalten.

## Grenzen

Systeme und Bereiche sind lokale Zuordnungen, keine verbindliche Serverklassifikation.
Unklare Systeme bleiben „Nicht zugeordnet“, unbekannte Bereiche „Weitere“ oder
„Sammlungen“. Die vollständige Katalogabdeckung ist nicht bestätigt. Die native
Prüfung verwendet echte Spieldateien mit synthetischen Daten; sie ersetzt keine
vollständige Live-Abnahme fremder Profile, Sammlungsdetails und Fortschrittswechsel.
Weitere GPUs/Treiber, Wine/macOS und quantitative Langzeittests bleiben offen.

Bekannte kamerabhängige Helligkeit, native Sirius-Absturzursache und weitere
Materialbefunde bleiben offen. Keine neue gemeinsame Grafik-/Sicherheitsänderung
und keine Leistungszusage. Der Installer besitzt keine Windows-Authenticode-
Signatur; Update-Manifeste verwenden die bestehende RSA-Signaturidentität.

[Funktionsumfang, Bedienung und 32-Bit-Vergleich](ALPHA20-ACHIEVEMENTS.md).
