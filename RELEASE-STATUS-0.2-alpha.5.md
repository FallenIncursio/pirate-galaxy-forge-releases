# Core und Enhanced 0.2.0-alpha.5 — Molikar-Fixrelease

Stand: 16.11.2026. **Veröffentlicht und öffentlich geprüft.**
Core-Sequenz 5, Enhanced-Sequenz 86; Starterrevision 12.
Die Abnahme umfasst den gemeldeten Molikar-Kamerawechsel, keine Vollabnahme aller Planeten.

Alle 14 öffentlichen Dateien, beide RSA-Release-/Kanalmanifeste, die normalen
Update-URLs und README-Installerlinks wurden erneut heruntergeladen und geprüft.
Binärquellencommit: `e1219c97ff4211374fe37daf8c35ed32a1a42229`. Die Veröffentlichungserfassung ändert keine
Programmbytes. Beleg: `distribution/tests/editions-0.2-alpha.5-publication.json`.
Frühere Releases und der ältere Enhanced-Kanal bleiben unverändert.

## Ursache und Änderung

Der erste alpha.5-Test zeigte auf Molikar weiterhin starke kamerabhängige
Helligkeitswechsel. Die Aufnahme und ein Replay mit den echten Terrainressourcen
weisen eine falsche Texturbelegung nach: D3D11 übernahm die erste geerbte
`set_texture_alias`-Zuweisung statt der späteren planetenspezifischen Zuweisung.
Der gemeinsame Materialparser verwendet wieder die ursprüngliche Regel des
32-Bit-Clients. Molikars Reflexionsslot erhält `refmap_12.png` statt
`planetsurface_falloff.png`. Core und Enhanced verwenden dieselbe Korrektur.
[Code, Vergleich und Grenzen](ALPHA5-TERRAIN-LIGHTING.md).

## Prüfung der neuen Dateien

- 72 kontrollierte Molikar-Kameraansichten mit originalem x86-Java, Original-JAR
  und originalen 32-Bit-DLLs verglichen: 24 Drehwinkel, drei Neigungen.
  Alle 34 Material-Texturbelegungen stimmen nach dem Fix überein. Alle Ansichten
  liegen näher an Original32; mittlere absolute RGB-Abweichung 43,90 → 16,81.
- 21 Vererbungsprüfungen: vorher 13 Fehler, danach null. Keine falsche Material-
  LOD bei 807.456 beobachteten Terrain-Zeichnungen; neun Qualitätsauswahlen bestanden.
- 5.208 kontrollierte Shader-Fälle gegen die beibehaltene x64-D3D9-Referenz
  (maximale Kanalabweichung 1), sieben COLOR-/Profilfälle, 160 Bereinigungszyklen,
  elf Calon-Bilder und fünf Wasser-Fallback-Bilder unverändert, 49 Overlayprüfungen.
- Beide Editionen neu gebaut; 40 Editions-/Java-/native Oberflächenprüfungen
  sowie sechs Negativkontrollen bestanden. D3D9 und D3D11, Core-Hilfe/-Einstellungen,
  Enhanced-Einstieg, HUD-Größe, Shop, MSAA und Ranglisten-Protokollfälle enthalten.
- Alle acht neu gebauten DLLs behalten ihre Exporte. Lose DLLs und eingebettete
  Basic-JAR-Dateien sind gegen den aktuellen Lock geprüft. Core bleibt ohne
  Enhanced-Module. D3D9-DLLs und Spiel-JARs sind unverändert.
- Beide neuen Sandbox-Kopien gegen ihre Paketmanifeste geprüft. Mit den jeweiligen
  Java-27-Laufzeiten je 16 Selector-Zyklen und lokale TCP-Übertragung in Sandboxie
  bestanden. Anschließend Enhanced mit D3D11 in der Sandbox gestartet: Serververbindung,
  Ingame-Terrainszene und 34 geladene native Module geprüft. Der Nutzer bestätigt den Molikar-Test.

Build: `.build/editions/alpha5-molikar-build`.
Tests: `.build/editions/alpha5-molikar-tests`.
Native Ausgabe: `.build/alpha5-molikar-render`.
Private Pakete: `.build/alpha5-molikar-sandbox`.
Belege: `distribution/tests/molikar-alpha5.json` und
`distribution/tests/editions-0.2-alpha.5-molikar-readiness.json`.
Die früheren alpha.5-Belege beschreiben weiterhin den ersten Teststand.

## Sandbox-Abnahme und Releaseweg

Enhanced wurde mit den Molikar-Fixdateien in einer getrennten Sandbox gestartet.
19 aktuelle Profil-/Einstellungsdateien einschließlich drei Spielprofilen und einer
verschlüsselten Anmeldung wurden aus der neuesten zusammengeführten Sandbox-Sicht
übernommen. Anmeldung, Serververbindung und geladene Spielszene wurden geprüft;
Windows-Mixer 8 %, nicht stumm, nach dem Start bestätigt. Der Nutzer meldet:
„okey, funktioniert. kannst als update pushen“. Beleg: `alpha5-user-acceptance.json`
im Quellverzeichnis `distribution/tests`. Es wurde kein Core-Spielkonto neu gestartet.

Öffentliche Pakete werden aus der geprüften Alpha-73-Inventarliste, JAR-Deltas,
den gepinnten nativen Dateien und dem bisherigen Signierschlüssel erzeugt.
Die privaten Sandbox-Kopien mit Spielcaches und Profilen werden nicht hochgeladen.
Die signierten Releasepakete bestanden 53 Neuinstallations-/Alpha-73-Prüfungen,
56 direkte alpha.4-Upgrade-/Reparatur-/Rollbackprüfungen und 24 Installer-UI-Prüfungen
in separaten Sandboxie-Boxen. Die erneute Editionsprüfung bestand 40 Suiten und
sechs Negativkontrollen. Dazu kommen je Edition 32 Updater-, 29 Startdiagnose-
und drei echte native Startfehlerfälle sowie der signierte Starterwechsel.
Die konkreten Paket-/Installerhashes und Prüfergebnisse stehen im Releasebeleg
`distribution/tests/editions-0.2-alpha.5-release-candidates.json` der Quellrepo;
der spätere Publikationsbeleg hält Downloads, Signaturen und Kanalaktivierung fest.

## Grenzen

Offen bleiben eine eigene Core-Spielsitzung mit diesem Stand, weitere Planeten,
Qualitäts-/Zoom-/Orbitwechsel, weitere GPUs, Wine und quantitative Langzeitmessungen.
Der Vergleich ist ein kontrollierter Terrain-Replay; Filter-, Raster- und
Geometriedetails unterscheiden sich weiterhin vom Original32-Client. Natürliche
Reflexionen bleiben erhalten. Keine vollständige Bildgleichheit behauptet.
Installer besitzen keine Windows-Authenticode-Signatur; Updates verwenden die
bestehende RSA-Releaseidentität. Frühere Releasepakete werden nicht ersetzt.
