> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Enhanced 0.2.0-alpha.26 – veröffentlicht

Enhanced **0.2.0-alpha.26** ist veröffentlicht, Updatekanal Sequenz 107 aktiv.
Alle sieben öffentlichen Downloads, RSA-Manifest, normaler Updatekanal und
README-Installerlink geprüft. Core alpha.17 / Sequenz 16, dessen Repository,
Kanal und Downloadassets bleiben unverändert. Spielversion 1002133, Starter 17.
Binärquellencommit: `ed61cadda90ac62befd9b0fe0fef3084b4452bed`. Beleg: `distribution/tests/editions-0.2-alpha.26-publication.json`.

Der Nutzer bestätigt den D3D11-Fundorttest R4. Sein Client blieb während der Veröffentlichung geöffnet.

## Prüfung

Fundortansicht R4 vom Nutzer im D3D11-Sandbox-Test bestätigt. Vollständige
räumliche Live-Abnahme aller Referenzbereiche und weiterer Hardware bleibt offen.

59 Neuinstallations-/Alpha-73-Prüfungen, 64 Upgrade-/Reparatur-/Rollbackprüfungen
ab 0.2.0-alpha.25 und 24 Installer-UI-Prüfungen auf isoliertem Desktop bestanden.
Nur künstliche Profile in eigenen Test-Sandboxes verwendet. Die einzelnen JAR-
Einträge sind bytegleich zum bestätigten Sandbox-Test; ZIP-Normalisierung geprüft.

Alle sieben Releaseassets wurden ohne Anmeldung über öffentliche URLs geladen,
Größen und SHA-256 geprüft und das RSA-Manifest verifiziert. Erst danach wurde
der Enhanced-Kanal aktiviert und sein Manifest erneut heruntergeladen/geprüft.
Der normale Updateabruf und der README-Installerlink liefern 0.2.0-alpha.26.
Vorherige Releaseassets sowie der ältere Enhanced-Kanal bleiben unverändert.
Quellstand auf main und feature/core-enhanced-0.2 gepusht; Quellrepo bleibt privat.
Keine Profile, Rohlogs, Originalspielarchive oder privaten Schlüssel hochgeladen.

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

[Bedienung und Prüfungen](../technical/ALPHA26-BLUEPRINT-LOCATIONS.md) ·
[Referenzdaten](../technical/ALPHA26-REFERENCE-DATA.md).

- `distribution/tests/editions-0.2-alpha.26-publication.json`
- `distribution/tests/editions-0.2-alpha.26-release-candidates.json`
