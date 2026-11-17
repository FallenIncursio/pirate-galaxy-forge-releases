# Core und Enhanced 0.2.0-alpha.7 — D3D11-Absturzfix

Stand: 17.11.2026. Veröffentlichung beider Editionen ausdrücklich beauftragt.
Zielsequenzen: Core 7 / Enhanced 88; Starterrevision 12. Kanalaktivierung erst
nach Prüfung der öffentlichen Paketdownloads.

Der gemeinsame D3D11-Code prüft die Lebensdauer eines Ziel-Passes, bevor dessen
Shader-Bindung entfernt wird. Die Korrektur vermeidet den nachgestellten Zugriff
auf freigegebenen, wiederverwendeten Speicher. [Ursache und Grenzen](ALPHA7-MATERIAL-CLEANUP.md).
D3D9 sowie die Remnant-/Aggrobeacon-Fixes bleiben erhalten.

## Bestandene Prüfungen

- 800 Materialbereinigungszyklen in acht Szenarien; fünf Fehlerfälle stürzen in
  alpha.5 und alpha.6 ab. Reguläre Bereinigung, Shader-Neuerzeugung und Beenden
  mit aktivem Material bestehen mit dem Fix.
- 45 Partikel-/Materialprüfungen, 48 Partikelaktivierungen, 21 Materialvererbungs-
  prüfungen, 160 bestehende Bereinigungszyklen und 49 Overlayprüfungen.
- Elf Calon-Himmels-/Wasserbilder und fünf Wasser-Testszenarien unverändert;
  72 Molikar-Kameraansichten plus Diagnosebild pixelgleich zur geprüften alpha.5-
  Referenz. Kein neuer Original32-Lauf und keine neue Ingame-Aufnahme behauptet.
- 40 Editions-/Oberflächensuiten und sechs Negativkontrollen. Native Oberflächen
  unter D3D9 und D3D11 geprüft; 113 gemeinsame Klassen identisch. D3D9-Dateien
  unverändert gegenüber alpha.6. Öffentliche native Exportschnittstellen und
  Klassenlayouts unverändert.

Native Ausgabe: `.build/alpha7-render`; exakte Testdateien:
`.build/alpha7-work/final-native`. Build: `.build/editions/alpha7-ready-build`;
finale Tests: `.build/editions/alpha7-versioned-tests`. Private Pakete:
`.build/alpha7-final-sandbox`, je Edition `Pirate-Galaxy-Forge-{Core,Enhanced}-0.2.0-alpha.7`.
Frühere Zwischenstände nicht für den Teststart verwenden.

Belege: `distribution/tests/material-cleanup-alpha7.json` und
`distribution/tests/editions-0.2-alpha.7-readiness.json`. Pakethashes sind im
letzteren Beleg erfasst. Es handelt sich um private Sandbox-Pakete mit lokalen
Spielressourcen, nicht um veröffentlichbare Installer.

## Noch offen

Der Nutzer bestätigt für Enhanced bisher keine weiteren Abstürze. Dauer und
Wechselzahl wurden nicht erfasst. Eine gesonderte Core-Spielsitzung und eine
quantitative Langzeitprüfung sind offen. Welche vorherige
Operation den Pass in der ursprünglichen Sitzung ungültig machte, ist ohne
Heapabbild nicht vollständig rekonstruiert. Andere Absturzursachen, weitere
GPUs und Wine sind nicht pauschal abgedeckt.

Kein Nutzerclient wurde für die Vorbereitung geschlossen oder ersetzt. Vor
einem angeforderten Sandbox-Start den dann aktuellen Profil-, Einstellungs-,
Anmelde- und Windows-Mixerstand übernehmen und den kurzen Sandbox-Pfad prüfen.
Neue signierte Installer-/Update-/Reparaturpakete und deren Prüfung sind ein
verbindliche Releasegates. Signierte Kandidaten: `.build/alpha7-release-candidates`;
Editionsprüfung: `.build/editions/alpha7-publication-tests`. Ergebnisse stehen in
`distribution/tests/editions-0.2-alpha.7-release-candidates.json`. Die autorisierte
Veröffentlichung wird anschließend gesondert im Publikationsbeleg dokumentiert.

## Angeforderter Enhanced-Teststart am 17.11.2026

Enhanced alpha.7 wurde mit D3D11 in `PGForgeAlpha7Crash` gestartet. 19 Profil-/
Einstellungsdateien einschließlich drei Spielprofilen und geschützter Anmeldung
vom zuletzt verwendeten normalen alpha.6-Client übernommen; Windows-Mixer 8 %,
nicht stumm. Dieser alte Client war bereits geschlossen. 16 Selector-Zyklen,
33 geladene native Dateihashes, Spielserververbindung und Sirius-Systemkarte
bestätigt. Privater Beleg im Chat-Arbeitsordner:
`work/alpha7-enhanced-launch/verified.json`. Anschließend meldete der Nutzer bisher keine weiteren Abstürze und autorisierte
die Veröffentlichung. Der Startbeleg allein ist keine vollständige Stabilitätsabnahme;
Core wurde nicht separat im Spiel gestartet.
