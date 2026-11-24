> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Core und Enhanced 0.2.0-alpha.12 — veröffentlicht

## Veröffentlichung geprüft

Core und Enhanced **0.2.0-alpha.12** veröffentlicht. Alle 14 öffentlichen Downloads,
zugehörigen RSA-Updatekanäle und README-Installerlinks wurden heruntergeladen und geprüft.
Aktualisierte Sequenzen: Core 11, Enhanced 93. Binärquellencommit: `db93fe32b3fd8a9c013b030e343ad8a1b8859503`.
Beleg: `distribution/tests/editions-0.2-alpha.12-publication.json`. Frühere Releasepakete bleiben unverändert.
Spielversion 1002133; kamerabhängige Helligkeitswechsel bleiben offen und werden später untersucht.

Abschließende Releaseprüfungen: 53 Neuinstallations-/Alpha-73-Prüfungen, 56 Upgrade-/Reparaturprüfungen und 24 Installer-Oberflächenprüfungen bestanden. Die Belege binden die geprüften Kandidaten über ihre SHA-256-Werte.

## Historischer Vorbereitungs- und Diagnosestand

Stand: 19.11.2026. Spielversion **1002133**. Der Nutzer bestätigt den
Fokusfix in Enhanced/D3D11 und autorisiert nach Fehlerprüfung die Veröffentlichung
beider Editionen, den Quell-Push und die Updatekanäle.

## Inhalt

- Gemeinsame native Fokuskorrektur entsprechend dem ursprünglichen 32-Bit-Client:
  gewöhnliche Spielfenster und Buttons blockieren Komponententasten nicht mehr.
- Texteingabe, expliziter Tastaturfokus und modale Dialoge bleiben geschützt.
- Neuer Regressionstest für beide Editionen und Renderer, mit sauberem GUI-/Engine-Abbau.
- D3D11-Testabbruch als fehlendes `shutdown()` im Analyse-Test aufgeklärt; korrigierte
  Probe beendet sich bereits mit der bisherigen DLL regulär.
- Spielbasis, bisherige Forge-Fixes und Core-/Enhanced-Grenzen bleiben erhalten.

## Prüfung und Pakete

Finaler Build `.build/editions/alpha12-final-build`, Tests `.build/editions/alpha12-tests`.
Der abschließende Neubau nach Erhalt der ursprünglichen Manifest-Zeilenenden liefert
dieselben geprüften Spiel-JARs, Helfer, DLLs und Startvorlagen.

- 56 Editionssuiten und sechs Build-Negativkontrollen bestanden.
- Zwei zusätzliche Negativkontrollen: bisherige D3D9-/D3D11-DLLs scheitern gezielt
  am falschen Fensterstandard; die neuen DLLs bestehen.
- Vier Fokusproben mit jeweils 2.253 Prüfungen bestanden, anschließend mit den
  fertigen Paketen nochmals in einer separaten Sandbox mit gesperrtem Netzwerk.
  Je neun Fensterzyklen, drei HUD-Größen und sauberer GUI-/Engine-Abbau.
- D3D9: 10.067 native Basisprüfungen, 21 RenderBox-Prüfungen und 96
  Panelgeometrie-Prüfungen bestanden. D3D11: acht Schriften/1.792 Glyphen geprüft.
- Spielklassen und Ressourcen des PirateGalaxy-JARs unverändert gegenüber alpha.11;
  pro Renderer ausschließlich MyGui.dll ausgetauscht. Core-/Enhanced-Grenzen geprüft.
- Beide privaten Pakete vollständig erneut auf Hashes, Spiel-/Editionsidentität
  und identische lose/eingebettete MyGui.dll geprüft: 3.410 / 3.425 Dateien.

Pakete unter `C:\PGF12A`, jeweils
`Pirate-Galaxy-Forge-<Core|Enhanced>-0.2.0-alpha.12`.
Belege: `distribution/tests/editions-0.2-alpha.12-readiness.json` und
`distribution/tests/window-focus-alpha12.json`.

Für diese Veröffentlichung: Core-Sequenz **11**, Enhanced-Sequenz **93**;
Starterrevision **12** unverändert. Aktivierung erst nach Prüfung der öffentlichen Downloads.

## Nutzerabnahme und Testgrenzen

Enhanced am 19.11.2026 auf Nutzerauftrag mit D3D11 in `PGForgeAlpha12Focus`
gestartet. Serververbindung, Anmeldung und sichtbarer Orbit bestätigt. Drei
Profile, Einstellungen und eine geschützte Anmeldung aus der neuesten normalen
alpha.11-Installation übernommen; Quelldateien unverändert. Windows-Mixer 8 %,
nicht stumm. Gerätebindung, 16 Selector-Zyklen und 56 geladene Dateihashes geprüft.
Beleg: `distribution/tests/editions-0.2-alpha.12-launch.json`.
Der Nutzer bestätigt anschließend die erfolgreiche Fokusprüfung. Die Sitzungslogs
enthalten keine neue Exception, keinen Fatalfehler und keine Absturzspur. Bekannte
Tracking-, UI-/Shop- und Szenenwarnungen sind bereits im alpha.11-Vergleich vorhanden;
ein verworfenes doppeltes W-Tastenereignis entspricht dem bestehenden Wiederholungsschutz.
Beleg: `distribution/tests/alpha12-user-acceptance.json`.

Die Nutzerbestätigung betrifft den Fokus-Test in Enhanced/D3D11. Die vollständige
Einzelabnahme aller Fenster, Suchfelder, modalen Dialoge und freien Belegungen
ist damit nicht separat protokolliert. Die nativen Proben decken diese Eingabewege ab.
Die unveränderlichen Pakete enthalten keine importierten Profile oder Anmeldedaten;
die laufende Sandbox verwendet eine separate Startkopie mit frisch übernommenen Daten.
Die neue Testsitzung bleibt für den Nutzer geöffnet.

Kamerabhängige Helligkeitswechsel bleiben offen. Wine, andere GPUs, OTB-Endwertung
und reale Wiederbelebung sind nicht neu bestätigt. Installer, Upgrade ab Alpha 73/alpha.11, Reparatur, Profilübernahme, Wiederanlauf
und Rollback werden mit den finalen signierten Paketen geprüft. Paketbeleg:
`distribution/tests/editions-0.2-alpha.12-release-candidates.json`. Frühere
Releasepakete und der ältere Enhanced-Kanal bleiben erhalten.

[Implementierung und Testfehler](../technical/ALPHA12-WINDOW-FOCUS.md) ·
[Kumulative Funktionen und Originalvergleich](../overview/FEATURES.md).
