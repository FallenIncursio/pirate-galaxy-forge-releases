# Enhanced 0.2.0-alpha.24 – bestätigter Releasestand

Der Nutzer hat den R3-Test mit D3D11 am 23.11.2026 bestätigt und Veröffentlichung,
Quell-Push, Enhanced-Updatekanal und Downloadprüfung autorisiert. Enhanced-Sequenz
105 ist vorbereitet. Core alpha.17 / Sequenz 16 bleibt unverändert und wird
nicht erneut veröffentlicht. Spielversion 1002133, Starterrevision 17.

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
Die finalen Pakete bestanden 59 Neuinstallations-/Alpha-73-Prüfungen, 64 Upgrade-,
Reparatur- und Rollbackprüfungen ab alpha.23 sowie 24 Installer-UI-Prüfungen auf
isoliertem Desktop. Die öffentliche Downloadprüfung folgt nach Upload und vor
Kanalaktivierung; ihr Ergebnis wird anschließend hier dokumentiert.

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
- [Bedienung und Datenvertrag](ALPHA24-BOSS-HUD.md)
