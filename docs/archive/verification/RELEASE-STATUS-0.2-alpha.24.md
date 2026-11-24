> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Enhanced 0.2.0-alpha.24 – veröffentlicht

Enhanced **0.2.0-alpha.24** ist veröffentlicht, Updatekanal Sequenz 105 aktiv.
Alle sieben öffentlichen Downloads, RSA-Manifest, normaler Updatekanal und
README-Installerlink geprüft. Core alpha.17 / Sequenz 16, dessen Repository,
Kanal und Downloadassets bleiben unverändert. Spielversion 1002133, Starter 17.
Binärquellencommit: `fcb2e2c0c9a12ff260dea926f2cd07bbf35e85b1`. Beleg: `distribution/tests/editions-0.2-alpha.24-publication.json`.

## Änderungen

- Zentrierter Bossname und bekannte Remnant-Itemklasse darunter.
- Blaue, von rechts nach links abnehmende Schutzumhüllung unabhängig von HP;
  optionale Prozentwerte, keine scheinbar volle Leiste bei unbekannter Kapazität.
- Getrennte XC-/SC-Farben und abschaltbare dezente oder klassenbezogene Animation.
- Bestätigter Landeschutz mit dem ausgewählten originalen goldenen PG-Schildsymbol.
  Die empfangene XC-Anteer-Signatur ohne zweites Visual ist gezielt abgedeckt.
- Name oder Lebensleiste per Linksklick anwählen; Effektdetails und Anzeigeauswahl
  bleiben getrennt. Keine Komponentenaktivierung oder automatische Zielauswahl.
- Einstellungen unter Forge → Anzeige → Bossleisten, begrenzte lokale Diagnose.

## Prüfung

62 Editionsgates und 22 Negativkontrollen bestanden. Darin enthalten: 61
Bossstil-/Datenprüfungen, 32 Zielauswahlprüfungen und je 3163 native UI-Prüfungen
mit D3D9/D3D11. Die nativen Maustests umfassen Namen/HP, Rechtsklick, Loslassen
außerhalb, getrennte Effektdetails und Boss-Umschaltung. Originalsymbol, Textur-
wechsel und Auflösungen 1024×768/100 %, 1920×1080/150 % und 3440×1440/200 % geprüft.
Core-Spiel-JAR, 138 Core-Helferklassen und native Bibliotheken bleiben unverändert.
Enhanced enthält 367 Helferklassen. Der öffentliche Spielinhalt muss bytegleich
zum bestätigten Sandbox-Stand bleiben; die ZIP-Normalisierung wird separat geprüft.

Der Nutzer bestätigt den allgemeinen Sandbox-Test; nicht jeder Effektzustand
und jede XC-/SC-Klasse wurde ausdrücklich einzeln als live geprüft bestätigt.
59 Neuinstallations-/Alpha-73-Prüfungen, 64 Upgrade-/Reparatur-/Rollbackprüfungen
ab alpha.23 und 24 Installer-UI-Prüfungen auf einem isolierten Desktop bestanden.
Nur künstliche Profile in eigenen Test-Sandboxes verwendet. Die einzelnen JAR-
Einträge sind bytegleich zum bestätigten R3-Test; ZIP-Normalisierung ist geprüft.

Alle sieben Releaseassets wurden ohne Anmeldung über öffentliche URLs geladen,
Größen und SHA-256 geprüft und das RSA-Manifest verifiziert. Erst danach wurde
der Enhanced-Kanal aktiviert und sein Manifest erneut heruntergeladen/geprüft.
Der normale Updateabruf und der README-Installerlink liefern alpha.24.
Vorherige Releaseassets sowie der ältere Enhanced-Kanal bleiben unverändert.
Quellstand auf main und feature/core-enhanced-0.2 gepusht; Quellrepo bleibt privat.
Keine Profile, Rohlogs, Originalspielarchive oder privaten Schlüssel hochgeladen.

## Grenzen und Erhaltung

Keine zusätzlichen Hintergrund-Datenabfragen. Explizite Zielauswahl nutzt die
Originalfunktion einschließlich ihrer normalen Meilensteinmeldungen. Fehlende
Klassen, Schutzkapazitäten und Restzeiten werden nicht erfunden. Die exakte
XC-Signatur wird erkannt; abweichende unbekannte Effekte bleiben ungeklärt.
Es gibt keine neue Leistungs- oder Sicherheitszusage. Offene Terrainhelligkeits-,
Material- und native Absturzfragen sind nicht Bestandteil dieses Updates.
Andere GPUs/Treiber, Wine/macOS und Langzeitverhalten benötigen eigene Tests.
Der Installer hat keine Windows-Authenticode-Signatur; Updates verwenden die
bestehende RSA-Identität. Unabhängige Starter-Speicherpflege bleibt außerhalb.
Der laufende Nutzerclient, seine Profile und Anmeldedaten bleiben erhalten.

## Belege

- `distribution/tests/alpha24-user-acceptance.json`
- `distribution/tests/boss-hud-alpha24-r3-staging.json`
- `distribution/tests/boss-hud-alpha24-r3-launch.json`
- [Bedienung und Datenvertrag](../technical/ALPHA24-BOSS-HUD.md)

- `distribution/tests/editions-0.2-alpha.24-publication.json`
- `distribution/tests/editions-0.2-alpha.24-release-candidates.json`
