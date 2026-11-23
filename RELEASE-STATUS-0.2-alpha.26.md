# Enhanced alpha.26 – Release-Prüfstand

Enhanced-Sequenz 107 zur Veröffentlichung freigegeben. Core alpha.17 / Sequenz 16,
Spielversion 1002133 und Starter 17 bleiben erhalten. Der Nutzer bestätigt den
D3D11-Fundorttest R4; sein laufender Client bleibt geöffnet.

62 Editionsgates, 22 Negativkontrollen, 48 Python-Tests und 5.082 Fundortprüfungen
bestanden. Je 3.348 native Enhanced-UI-Prüfungen mit D3D9 und D3D11 testen reale
Mausbedienung, HUD-Skalierung, Kartenaktionen und nicht verfügbare Bilder.
R3 scheitert ohne fremdes Systemarchiv; R4 besteht die gleiche Gegenprobe.
Core-Spielbytes und native Inputs sind unverändert. Keine zusätzlichen Serverabfragen.

## Prüfung

Fundortansicht R4 vom Nutzer im D3D11-Sandbox-Test bestätigt. Die finalen
signierten Pakete bestanden Neuinstallation, Alpha-73-/alpha.25-Upgrade, Reparatur,
Rollback, Profilübernahme und Installer-UI-Prüfung. Nur künstliche Testprofile
verwendet. JAR-Einträge bytegleich zum bestätigten R4-Spielstand.
Die öffentlichen Downloads werden vor der Kanalaktivierung erneut geprüft.
59 Neuinstallations-/Alpha-73-Prüfungen, 64 Upgrade-/Reparatur-/Rollbackprüfungen
und 24 Installer-UI-Prüfungen auf isoliertem Desktop bestanden.
Die unabhängige Starter-Bereinigung ist nicht enthalten.

## Grenzen

Die Referenzdaten enthalten 1.333 Baupläne und 1.387 Bereiche auf 18 Karten für
664 Baupläne. Bekannte Fundstellen sind keine Live-Spawnanzeige und keine
Dropgarantie. Widersprüchliche Identitäten, fehlende Karten, besondere Varianten
und dynamische Sirius-Positionen werden nicht geraten. Vollständige räumliche
Live-Abnahme, weitere GPUs, Wine/macOS und Langzeittests bleiben separat.
Bekannte Terrainhelligkeits-, Material- und native Absturzfragen bleiben offen.

[Bedienung und Prüfungen](ALPHA26-BLUEPRINT-LOCATIONS.md) ·
[Referenzdaten](ALPHA26-REFERENCE-DATA.md).
