# Funktionen und Vergleich zur 32-Bit-Basis

Stand: Core und Enhanced **0.2.0-alpha.3**, Windows-Alpha-Ausgaben auf
Basis von Alpha 73 und dem veröffentlichten alpha.2. Frühere Releasepakete bleiben unverändert.
Die gemeinsamen Calon-Fixdateien wurden in Enhanced praktisch bestätigt.
Enhanced enthält sämtliche Core-Funktionen. „Original“ bezeichnet
die gepinnte offizielle 32-Bit-Spielbasis dieses Projekts, keine Aussage über künftige
Updates des Herstellers. Eine Splitscreen-Freigabe wird nicht behauptet.

| Bereich | Core | Enhanced | Gegenüber der 32-Bit-Basis |
|---|---|---|---|
| Architektur | Windows x64, Java 27 | identisch | Größerer adressierbarer Speicher; keine RAM-Verbrauchsgarantie |
| Bibliotheken | Modernisierte Laufzeit, Logging, Netzwerk, Archiv-/Bilddecoder | identisch | Gepinnte modernisierte Komponenten aus Alpha 73 |
| Renderer | D3D11, D3D9 separat startbar | identisch | Port mit Alpha-73-Sonnen-, Filter-, Transparenz- und UI-Korrekturen |
| Grafikstart | Automatische Geräteprüfung, begrenzter D3D9-Fallback, bestätigte Grafikauswahl | identisch | Neue Forge-Startlogik; keine allgemeine Treiber-Kompatibilitätszusage |
| Installation/Reparatur | Einfaches Setup, geprüfte Neuaufbereitung derselben Version mit Profilübernahme | identisch | Neue Forge-Verteilung; keine Änderung der offiziellen Installation |
| Fehlerberichte | Begrenzte lokale Startprotokolle, freiwilliger Versand technischer Metadaten | identisch | Forge-Diagnose; keine automatische Übermittlung von Rohlogs |
| Speicher/Leistung | Weniger temporäre Objekte, begrenzte Caches, Ressourcenlebensdauer | identisch | Optimierte Pfade; keine pauschale FPS-/Prozentzusage |
| Laden | Lokale Szenen-/Terrainvorbereitung, insbesondere Erebos, mit Fallback | identisch | Weniger Arbeit im betreffenden Szenenaufbau; kein globales Vorladen aller Planeten |
| FPS/VSync | Limit 30–240; VSync nach Neustart | identisch | Zusätzliche lokale Optionen; Limit ist keine garantierte Bildrate |
| Oberfläche | Native HUD-Skalierung | identisch | Skalierung statt ausschließlich höherer Auflösung |
| Chat | Optionale lokale Uhrzeit | identisch | Ergänzung vorhandener Nachrichten |
| Komponenten | Lokales Verschieben, passende Tastenbelegung | identisch | Visuelle Reihenfolge; Server-Slotreihenfolge bleibt erhalten |
| Statuszeile | Passiver TCP-Ping; einfache FPS optional | Erweiterte Status-/Diagnoseanzeige | Keine eigenen Ping-Pakete |
| Discord | Optional, neues Core-Profil: aus | Vorhandene Option; neuer Standard: Spiel | Separater externer Datenfluss bei Aktivierung |
| Zieleliste | Missionsabhängiger Remnant-Filter | identisch | Filter bestehender Einträge, keine Erkennung unbekannter Einheiten |
| Sirius-Baupläne | Farben nach eigenem bekannten Fortschritt | identisch, zusätzlich Katalog/Planung | Keine erfundenen Besitzstände |
| Kryonit | Menge am vorhandenen Zieleintrag | zusätzlich Statistik/Export | Keine Sammelautomatik |
| Hilfe/Einstellungen | Originale Hilfe; native Einstellungserweiterung | F-/Forge-Einstieg, acht Bereiche | Unterschiedliche Bedienoberfläche |
| Orbitalschläge | Originaldarstellung | Konturen, Füllung, bekannte Countdown-Varianten | Lokale Zusatzinformation; Schätzwerte sind keine Servergarantie |
| Bosse | Originaldarstellung | Remnant, Queen, Sirius: HP, Effekte, Quellen, bekannte Zeiten | Zusätzliche Darstellung empfangener Daten |
| Bossauftritt | Original | Name, Bildschirmränder, optionale Musik | Lokale Präsentation |
| Staffel | Original | Erweiterte HP-/Effektanzeigen | Zusätzliche Übersicht |
| Komponententimer | Original | Zahlen, transparente/radiale Anzeigen, letzte Sekunden | Lokale Darstellung vorhandener Zustände |
| Reichweiten | Original | Ziel-, Blitzketten- und Quantensprung-Anzeigen | Zusätzliche Visualisierung |
| Quantensprung-Zielhaltung | Original | Eingeschränkte Regel außerhalb feindlichem/unklarem PvP | Feindliche und unbekannte Spielerbeziehungen behalten Originalreset |
| Reparatur-/HP-Darstellung | Original | Reduzierte Felder/Konturen, HP-Warnung | Zusätzliche lokale Darstellungsoptionen |
| Baupläne/Ausrüstung | Eigener Sirius-Fortschritt | Katalog, Suche, Merkliste, Referenzen, Vergleich, Einkaufsplan | Erweiterte Planungsoberfläche |
| Remnant-Informationen | Filter | Beutekarten, Kategorien, Wartezeiten | Zusätzliche lokale Aufbereitung |
| Statistik | Einfache FPS | Kryonit, KW, Exporte, große Energiekugel | Erweiterte lokale Auswertung |
| Drohnen | Allgemeine Hangarkorrekturen | Zusätzlich Levelzeitschätzungen und Meldungen | Schätzungen bleiben gekennzeichnet |
| Navigation | Original | Positionsmerker, Sirius-Prognosen, Reiseerinnerungen | Lokale Planung |
| Eigene Sounds/Musik | Originale Inhalte mit allgemeinen Audiofixes | Import, Zuschnitt, Einzelpegel, Live-Übernahme | Zusätzliche lokale Medien |
| Antriebsspuren | Original | Lokale Vorschau und dauerhafte Spuren für Schiff/Drohnen | Keine Änderung fremder Clients |
| Farben/Meldungen/Namen | Original | Statuspaletten, Meldungsfilter, lokale Namen wie „Lörres“ | Enhanced-spezifische Darstellung |
| Kampfberichte | Keine zusätzliche Aufzeichnung | Lokale Remnant-Berichte | Keine automatische Veröffentlichung |
| Wine | Geerbte Kompatibilitätsarbeit | identisch | Vorschau; diese 0.2-Pakete nicht unter Wine geprüft |

## Gemeinsame Fehlerkorrekturen

- Neu in alpha.2: D3D11-Himmelsgradienten auch für Calons Reflexionskamera;
  neutrales Verhalten bei ungebundenen optionalen Wassertexturen. Die gelbe
  Darstellung war eine Portierungsregression, kein belegter Fehler des 32-Bit-Clients.
- Neu in alpha.2: Ressourcenabmeldung vor Freigabe und fortschreitende
  Shaderbereinigung verhindern den reproduzierten D3D11-Hänger mit veralteten
  Schiffsmaterialien. Keine Zusage, dass sämtliche Hänger dieselbe Ursache haben.

- Komponentenaktivierung: Nach ausdrücklicher Ablehnung wird der lokale Aktivzustand
  korrigiert und der tatsächliche Cooldown begrenzt abgeglichen. Kein erneutes
  `useItem`, keine Interpretation unbekannter Antworten als Cooldown null.
- Missionsannahme/Bestätigungsdialoge: konkurrierende Dialoge, zurückbleibende
  Klickzustände und blockierte Missionstafelelemente.
- Scan-Details bei schneller Auswahl; verspätete Antworten und Lebensdauer von
  Ziel-, Profil- und Clanvorschauen.
- Drohnenslots nach Schiff-/Konfigurationswechsel, verspätete Containerdaten und
  Listener-Lebensdauer im Hangar.
- Weiße oder texturlose Zielvorschauen; Materialidentitäten; Planetenpreview,
  Armene-Clipping und Commerce-Central-LOD-/Texturpfade.
- Wolken-/Landepfade, Schattenprojektion, Fenster-/HUD-Geometrie und Fokus der Zieleliste.
- Audio-Streaming, Puffer-/Objektlebensdauer, Gerätewiederanlauf und allgemeine
  Übergangspfade; eigene Medien bleiben Enhanced.
- Gespeicherte Pilotenauswahl; Java-27-Serialisierung, Legacy-Login-Kompatibilität,
  UI-/Ressourcenlebensdauer, begrenzte Dekompression und geschützter lokaler Login-Speicher.
- D3D11-Portkorrekturen aus Alpha 71–73 einschließlich Sonne, Filtervererbung,
  Sternkarte, Ressourcen und optionalen Glyphen.
- D3D11-HUD-Texturen bleiben während ihrer Verwendung gebunden. Das verhindert
  fortlaufendes Nachladen nach Ressourcenbereinigung; der Erebos-/Orbit-Test wurde
  als verbessert bestätigt. Es liegt keine quantitative Langzeitmessung vor.

Ein Teil dieser Fehler war eine Portierungsregression. Die Liste behauptet nicht,
dass jeder Punkt ein Fehler des offiziellen 32-Bit-Clients war. Korrekturen an
Orbital-, Boss-, KW- oder anderen Zusatzfunktionen bleiben Enhanced.
Die neue Core-Statusanzeige platziert FPS und Ping auch mit Spielleiste und Minimap
unten rechts. Enhanced erhält die korrekte Mouse-Up-Weiterleitung zum Forge-Dialog;
das ist eine Korrektur seiner zusätzlichen Oberfläche.
Neu in alpha.2 sind außerdem vollständige D3D11-Shader für Enhanced-Energiekugel-
Markierung und Quantensprungkreis. Das korrigiert den Port dieser Zusatzanzeigen;
der 32-Bit-Originalclient enthält diese Forge-Funktionen nicht.

## Daten und Anfragen

Die Darstellung lokaler Daten und die spielerische Wirkung sind getrennte Fragen.
Zusätzliche Anzeigen können die Wahrnehmung verändern. Es gibt keine pauschale
Zusicherung „keine zusätzliche Serverlast“:

- Sirius-/Planetendetails können `getAllAvatarBlueprints` zum eigenen Fortschritt nachladen.
- Die offene Enhanced-Bauplanansicht aktualisiert ihren Profilstand nach dem
  bisherigen, begrenzten Aktualisierungspfad (fünf Sekunden nach Abschluss).
- Aktivierungsablehnung: höchstens ein laufender `getShipCooldown`-Abgleich,
  maximal drei Versuche pro Ablehnung; kein erneutes Aktivieren der Komponente.
- Ping liest den TCP-RTT der bestehenden Spielverbindung passiv.
- Discord ist optional. Der lokale Sandbox-Launcher enthält weder Aktivitätszähler,
  automatische Fehlerberichte noch einen Update-Client.

Automatischer Kryonit-Drohnenwechsel bleibt in beiden Editionen entfernt.
Live-Leistungswerte und Wine-Abnahme müssen mit den konkreten Kandidaten erhoben werden.
