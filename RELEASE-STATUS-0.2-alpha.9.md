# Releasestand: Core und Enhanced 0.2.0-alpha.9

Veröffentlichung am 18.11.2026 nach dem Enhanced-Calon-Test vom Nutzer freigegeben.
Core-Sequenz 8, Enhanced-Sequenz 90, Starterrevision 12. Die Releasepakete werden
mit den getesteten Spielbytes erstellt; Kanalaktivierung erst nach Downloadprüfung.

## Änderungen

GUI-Schriftatlanten bleiben innerhalb fester Grenzen über normale
Ressourcenbereinigungen erhalten. Manuelle Vegetations-LODs werden vorbereitet;
zu große LOD-Indizes werden korrekt begrenzt. Optionale Baum-/Windseiten bauen
ihre Geometrie schrittweise auf. Unfertige Seiten bleiben unsichtbar; Entladen
und Loader-Wechsel verwerfen ihre Arbeit. Ein uninitialisierter vierter
Tangentenwert wird aus dem Quellmodell übernommen.

Beide Editionen nutzen die gemeinsamen D3D11-Korrekturen. D3D9-Paketbibliotheken,
Pflanzendichte, Sichtweite und Planetenparameter bleiben unverändert.
Die bisherigen alpha.9-Fixes und die 62-spaltige Diagnose bleiben enthalten.
[Code, Messwerte und Grenzen](ALPHA9-ATLAS-LOD-STAGING.md).

## Abgeschlossene Prüfungen

- 48 Editionssuiten und sechs bestehende Negativkontrollen bestanden;
  119 gemeinsame Klassen bytegleich. Native D3D9-/D3D11-GUI beider Editionen geprüft.
- 35.548 native Vegetationsprüfungen im abschließenden Lauf; die Anzahl enthält
  Prüfungen je Fortsetzungsschritt und kann mit der Laufzeit variieren.
  Normal-/Windbatches, LOD-Auswahl, Abbruch, Seitenwiederverwendung,
  explizites Vorladen, Loader-Wechsel und Shutdown geprüft.
- 49 echte Quellmodelle: 43 Calon, sechs Venar. Vor Vorbereitung 294
  unbeschattete Quellenlesevorgänge, danach null. Gestufter und korrigierter
  vollständiger Aufbau liefern identische Geometriebytes.
- 148 Schriftprüfungen einschließlich 32 Bereinigungszyklen bei wirksamen
  HUD-Größen 100/115/200 %. Echte Zielanzeige nach Bereinigung 0,17–0,30 ms;
  Gegenprobe mit vorheriger DLL 31,20–32,38 ms und erneute Rasterisierung.
- 212 XML-Cache- und 148 ResourceManager-Prüfungen einschließlich alter DLL
  als Negativkontrolle. 86 GUI-Bilder und neun Baum-/Windbilder pixelgleich.
- Lose und eingebettete native Bibliotheken sowie Quellen sind durch Hashbelege
  an die geprüften Builds gebunden. Keine Profile in den Kandidaten.

Build: `.build/editions/alpha9-atlas-lod-verified-build`.
Tests: `.build/editions/alpha9-atlas-lod-final-tests`.
Native Ausgabe: `.build/alpha9-atlas-lod-native`.
Private Pakete: `C:\PGF9AB`, je `Pirate-Galaxy-Forge-<Core|Enhanced>-0.2.0-alpha.9`.
Codebeleg: `distribution/tests/calon-alpha9-atlas-lod-fixes.json`.
Abschließender Paketbeleg: `distribution/tests/editions-0.2-alpha.9-atlas-lod-readiness.json`.

## Offene Spielprüfung

Enhanced mit diesen Bytes am 18.11.2026 in der Sandbox gestartet; neue Calon-
Diagnose ausgewertet. Zielanzeigen, Vegetationsspitzen und unvorbereitete
LOD-Lesezugriffe deutlich verbessert. Gesamtaufnahme weiterhin mit acht
Frameabständen über 16,67 ms und einem Maximum von 49,362 ms; Timer-/JNI- und
Renderausreißer bleiben offen. Keine vollständige Calon-Leistungsabnahme.
[Livebefund und Vergleich](ALPHA9-ATLAS-LOD-LIVE-ANALYSIS.md).
Dieselbe Strecke wiederholt fliegen, neue Gegner und Zielanzeigen, Kamerawechsel
sowie Orbit/Rückkehr prüfen. Mit und ohne Diagnose vergleichen; Venar und einen
schwächer bewachsenen Planeten ergänzen. HUD-Größe und sichtbare Pflanzen prüfen.

Das 2-ms-Budget ist weich: sofort benötigte Seiten, einzelne Treiberuploads,
Material-/Shaderarbeit und sehr große Seiten können länger dauern. Gras bleibt
synchron. Wasser-Einzelausreißer, andere Grafikkarten, Wine und längere Sitzungen
bleiben offen. Keine Zusage vollständiger Rucklerfreiheit, kein neuer kontrollierter
32-Bit-Flugvergleich. Historische alpha.9-Belege gelten nur für ihre damaligen Bytes.

Laufenden Client erhalten. Bei einem später beauftragten Start Profil,
Einstellungen, Anmeldedaten einschließlich versteckter Gerätekennung und
Windows-Lautstärke frisch aus der aktuellen Sitzung übernehmen. Kurze
Sandboxpfade und versions/data-Layout verwenden; keine alten Snapshots über
aktuelle Daten kopieren. Die gemessene Verbesserung wurde für dieses Update akzeptiert; bekannte Einzelspitzen
bleiben dokumentiert. Installer-/Updateprüfung wird an die finalen Pakete gebunden.
