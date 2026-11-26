# Funktionen und Editionen

[Übersicht](../../README.md) · [Bedienung](HILFE.md) · [Änderungen](../../CHANGELOG.md)

Stand: **Core 0.2.0-alpha.37 · Enhanced 0.2.0-alpha.37 · Spielversion 1002133**.

Core enthält die gemeinsame 64-Bit-Technik, allgemeine Fehlerkorrekturen und
begrenzten Komfort. Enhanced ergänzt dieselbe Grundlage um die Forge-Oberflächen.
Die Tabelle beschreibt den veröffentlichten Umfang, keine verworfenen Versuche.

## Technik und gemeinsamer Komfort

| Bereich | Core und Enhanced | Gegenüber dem offiziellen 32-Bit-Client |
| --- | --- | --- |
| Architektur | 64-Bit-Java und native Bibliotheken, modernisierte Abhängigkeiten | Größerer nutzbarer Adressraum; keine pauschale FPS-Zusage |
| Grafik | D3D11 als Standard, D3D9 als auswählbarer Fallback | Portierung mit gezielten Grafik- und Ressourcenfixes |
| Darstellung | FPS-Limit bis 240, VSync, HUD-Größe, FPS/Ping unten rechts | Zusätzliche lokale Einstellmöglichkeiten |
| Bedienung | Verschiebbare Komponenten, Chat-Uhrzeit, Discord-Spielstatus | Komfort ohne Änderung von Serverregeln |
| Clankasse | Stabile Mitgliedsauswahl, Bestätigung mit Empfänger/Menge und Schutz vor doppelten Zuweisungen | Korrektur einer Sortierungsregression und Absicherung verzögerter Anfragen |
| Ziele | Remnant-Filter, Sirius-Bauplanfarben, Kryonitmenge | Ergänzung vorhandener Zielinformationen |
| Einrichtung | Eigener Starter, geprüfte Updates, Reparatur, Profilübernahme innerhalb der Edition | Getrennte Spielkopie mit eigenen Updatekanälen |
| Diagnose | Live-Logs, Start-/Laufzeithängerdiagnose, gezielter Neustart und freiwilliger Bericht | Zusätzliche lokale Fehlersuche |

Gezielte gemeinsame Korrekturen betreffen unter anderem Komponentenstatus,
Missionsdialoge, schnelle Scans, Drohnenslots, Zielvorschauen, Namen und Statusbalken,
Ranglisten/Divisionswechsel, Shop-Vorschauen, HUD-Skalierung, Eingabefokus,
Calon-Reflexionen sowie Ressourcen- und Materiallebensdauer. Die Arbeiten an
Schriftatlas, LOD und Vegetation reduzieren wiederholte Arbeit auf Calon.
Ein Teil betrifft Portierungsregressionen; die Liste behauptet keine entsprechenden
Fehler in jeder Version des 32-Bit-Originals.

## Zusätzliche Enhanced-Funktionen

| Bereich | Ergänzung | Einstellung / Einstieg |
| --- | --- | --- |
| Bauplanliste | Suche, Typ-/Bereichs-/Fortschrittsfilter mit originalen Spielbezeichnungen, eigene Bereiche für Events und RDX/Parsec, optionales automatisches Abhaken vollständiger BPs; stabile Seiten beim Markieren, Vergleich und Einkaufsplan | Forge → Baupläne / Ausrüstung; Anzeige → HUD & Grafik |
| Bauplanexport | CSV aller gefilterten Treffer, einschließlich Teilezahlen, System und Bereich | Forge → Baupläne → CSV exportieren |
| Bauplan-Fundorte | Planet/System, Gegner, bekannte Level und Kartenbereiche mit Gegnerbildern | Forge → Baupläne → Fundorte |
| Scanfenster | Mögliche blaue/goldene Baupläne mit eigenem Bestand, einschließlich Sirius-Zuordnung; gemeinsame geprüfte Dropdaten mit der Fundortsuche | Forge → Anzeige; Giza/Soris/Amarna ausgeschlossen |
| Sirius | Bekannte Quarc-Freigabe und Teilezahlen gelber Baupläne; Sortierung und Merkliste | Forge → Anzeige → HUD & Grafik |
| Errungenschaften | Suche, Status-/System-/Bereichsfilter und Sortierung; goldene Abschlussanzeige | Pilotenprofil → Errungenschaften; unter Anzeige abschaltbar |
| Bossleisten | HP, Effekte, bekannte Itemklasse, Schild-/Schutzreserve, Zielwahl per Klick | Forge → Anzeige → Bossleisten |
| Bossauftritte | Namen und optionale Musik; Remnants nur XC/SC, außerdem Königin und Sirius-Bosse | Forge → Anzeige → Kampf & Effekte |
| Staffel | Erweiterte HP-/Effektanzeige und Schild-/Schutzreserve mit optionalen Prozentwerten | Forge → Anzeige → Kampf & Effekte |
| Clan-Sperrfrist | Restzeit für das ausgewählte Mitglied aus bereits bekannten Beitrittsdaten; unbekannte Werte bleiben gekennzeichnet | Clankasse → Schädel-/Gravitonen-/Kryonit-Zuweisung |
| Reparaturfelder | Spieler, PvE und feindliche Spieler getrennt: Original, leicht/stark reduziert, Kontur; PvP-Felder optional rot | Forge → Anzeige → Kampf & Effekte |
| Komponenten | Eigene Tasten, Reichweitenmarkierungen, Zahlen-/Kreis-Zeitanzeige | Forge → Anzeige → Komponenten / Forge → Tasten |
| Kampfansicht | Orbitalschlaghinweise, HP-Warnschwelle, rote Bildschirmränder | Forge → Anzeige → Kampf & Effekte |
| Remnants | Beutekarten und Variantenbestände, ergänzte Warte-/HP-Anzeigen, lokale Kampfberichte | Remnant-Anzeige / Forge |
| OTB | Lokale Aktivitätswerte und Warn-Countdown mit Testvorschau | Forge → Anzeige → Widgets |
| Gravitonen | Beobachteter Drop oder geschätzter Countdown im sechsten Slot | Forge → Anzeige → Widgets |
| Reisekosten | Nächster niedrigerer Hypersprungpreis mit Countdown und gültigem Mitgliedschaftsrabatt | Reisefenster; Forge → Anzeige → HUD & Grafik |
| Sammeln | Große Energiekugel markieren, Kryonitstatistik, Drohnen-Levelzeitschätzung | Forge → Anzeige → Widgets |
| Kriegswertung | KW-Tracker, letzte Gutschriften, Kategorien, Verlauf und CSV | Forge → Anzeige → Widgets |
| Updates | Lokale Releasehistorie mit Datum, Versionsreihen und Seitenwechsel; leuchtendes F und einmalige PG-Meldung bei ungelesenen Neuigkeiten | Forge → Updates; Anzeige → Meldungen & Discord |
| Meldungen | Native PG-Leiste, Alle / Nur wichtige, Testmeldung | Forge → Anzeige → Meldungen & Discord |
| Anpassung | Statusfarben, eigene Sounds/Musik und lokale Antriebsspuren | Forge → Anzeige / Audio / Antrieb |

Die Originalhilfe bleibt in Core erhalten. Enhanced verwendet den Forge-Einstieg.
Core enthält keine versteckt aktivierbaren Enhanced-Module.

## Was die Anzeigen aussagen

- Bauplan-Fundorte und Drops sind Referenzzuordnungen, keine garantierten Drops oder Live-Spawnmeldungen.
- Unbekannter Bestand bedeutet nicht null. Unbekannte Zeit, Reserve oder Quarc-Freigabe wird nicht erfunden.
- OTB-Warnungen beschreiben lokale Beobachtungen; die Serverwertung bleibt unbekannt.
- Der Gravitonen-Countdown ist eine lokale Schätzung und kann frühere unbeobachtete Drops nicht rekonstruieren.
- Kartenmarkierungen verändern keine Gegner, Reichweiten oder Serverentscheidungen.
- Die verworfene Schiffskonfigurations-/Erstcache-Ansicht und ein automatischer Kryonit-Drohnenwechsel gehören nicht zum veröffentlichten Umfang.

Kamerabhängige Terrainhelligkeit, einzelne Ruckler sowie weitere native Grafik-/Absturzfälle
bleiben offene Untersuchungen. Wine/macOS, zusätzliche GPUs und Langzeitläufe sind
keine vollständig bestätigten Plattformabnahmen. Forge ist ein inoffizieller Alpha-Client.
