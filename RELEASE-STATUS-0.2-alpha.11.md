# Core und Enhanced 0.2.0-alpha.11 — Veröffentlichung beauftragt

Stand: 19.11.2026. Beide Editionen verwenden die offizielle Spielversion **1002133**.
Der Nutzer hat Quell-Push, beide Releases und Updatekanäle ausdrücklich freigegeben.
Das gemeldete Helligkeitsproblem bleibt offen und wird später weiter untersucht.
Die enthaltene Normalenkorrektur ist keine Zusage einer vollständigen Behebung.

## Änderungen und Prüfstand

- Herstelleränderungen an Schiffsinformationen und Ressourcen vollständig übernommen;
  keine Umgehung der Versionsprüfung. Drei geänderte und eine zusätzliche Methode.
- Alpha.11-Normalenberechnung und gemeinsame begrenzte Grafikdiagnose bleiben erhalten,
  ebenso die bisherigen Forge-Fixes und die Trennung zwischen Core und Enhanced.
- 52 Editionssuiten, sechs Negativkontrollen, Dreiwege-Konfliktprüfungen, sechs
  JAR-Delta-Rundläufe und vier native Schiffsinformationsproben bestanden.
- 121 gemeinsame Helfer sind bytegleich zwischen Core und Enhanced. Sämtliche
  Forge-Helfer und DLLs sind unverändert gegenüber dem vorigen alpha.11-Teststand.
- Enhanced/D3D11 mit 1002133 in der Sandbox angemeldet und bis in den Orbit gestartet;
  54 geladene Dateien sowie Profil-, Einstellungs- und geschützte Anmeldeübernahme geprüft.

Build: `.build/editions/alpha11-game1002133-final-build`.
Die Veröffentlichungstests binden dieselben Spiel-JARs und DLLs.
Belege: `distribution/tests/editions-0.2-alpha.11-game1002133-readiness.json`,
`distribution/tests/editions-0.2-alpha.11-game1002133-launch.json` sowie der
nach den Pakettests erzeugte `editions-0.2-alpha.11-release-candidates.json`.

Installer, signierte Pakete, Upgrade ab Alpha 73/alpha.10, Reparatur, Profilübernahme,
Abbruch/Wiederanlauf und Rollback werden mit den finalen Releasepaketen geprüft.
Core-Sequenz **10**, Enhanced-Sequenz **92**, Starterrevision **12**.
Erst nach öffentlicher Downloadprüfung werden die beiden Updatekanäle aktiviert.
Frühere unveränderliche Releasepakete und der ältere Enhanced-Kanal bleiben erhalten.

## Bekannte Grenzen

Kamerabhängige Helligkeitswechsel bleiben ausdrücklich offen. Die kontrollierten
Original32-Vergleiche belegen den Normalenalgorithmus, keine vollständige
Bildgleichheit oder erfolgreiche Live-Sirius-Abnahme. Eine separate Core-Spielsitzung,
andere GPUs/Treiber, Wine und Langzeittests sind nicht neu bestätigt.
Auch OTB-Endwertung und reale Wiederbelebung sind weiterhin separat zu prüfen.
Installer sind nicht Authenticode-signiert; Updates verwenden die bestehende RSA-Identität.
Laufenden Nutzerclient und normale Installation erhalten.

[Spielbasis und Übernahme](GAME-BASIS-1002133.md) ·
[Normalenvergleich und Diagnose](ALPHA11-TERRAIN-NORMALS.md) ·
[Kumulative Funktionen und 32-Bit-Vergleich](FEATURES.md).
