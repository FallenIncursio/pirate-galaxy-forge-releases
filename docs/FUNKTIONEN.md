# Funktionen im Vergleich

[Übersicht und Download](../README.md) · [Bildergalerie](BILDER.md) · [Bedienung und Hilfe](HILFE.md)

Stand: **0.1.0-alpha.53 · 8. November 2026**. Diese Übersicht beschreibt veröffentlichte Funktionen, keine geplanten Experimente.

Die Grundlage bleibt das offizielle Pirate Galaxy: Spielwelt, Missionen, Ausrüstung, Baupläne, Originalsounds/-grafiken und Serverregeln stammen aus dem Spiel. Die Ergänzungen unten sind Änderungen des **Forge-64-Bit-Clients**. Sie gelten nicht für den unveränderten offiziellen **32-Bit-Client**, den der Starter ebenfalls öffnen kann. „64 Bit“ bezeichnet die technische Architektur; die Komfortfunktionen wurden zusätzlich entwickelt.

**Neu** = zusätzliche Forge-Funktion. **Erweitert** = vorhandene Spielfunktion ergänzt. **Korrigiert** = konkreter Fehlerpfad verbessert. Die Einordnung bezieht sich auf die genannte Ergänzung, nicht auf den gesamten Spielbereich.

## Baupläne, Ausrüstung und Remnants

| Funktion | Herkunft | Ergänzung durch Forge |
| --- | --- | --- |
| Bauplansuche | Erweitert | Eigene Übersicht mit Suche nach Name/Typ sowie Filtern nach System, Kategorie und Fortschritt. |
| Ergänzter Bauplankatalog | Erweitert | Referenzeinträge ergänzen Baupläne, die noch nicht im persönlichen Profil auftauchen. |
| Persönliche Merkliste | Neu | Baupläne pro Pilot vormerken; passende Einträge in Sirius-Planetendetails wiederfinden. |
| Remnant-Bestände | Erweitert | Eigener Remnant-Systemfilter; Normal, Schnell, Stark und Lang bleiben getrennt. Bestände wie 8/6 werden nach Verbrauch aktualisiert. |
| Ausrüstungsvergleich | Neu | Komponenten desselben Typs anhand eingebetteter Referenzwerte vergleichen. |
| Einkaufsplan | Neu | Einträge lokal vormerken und den Einkauf planen. |
| Remnant-Beuteansicht | Erweitert | Die vorhandene Beutekategorie öffnet Karten möglicher Baupläne mit Spielicons und eigenen Variantenbeständen. |
| Remnant-Wartephase und HP | Erweitert | Geschätzte Wartezeit bis zur Systemmeldung, klare Texte für noch unbekannte Angaben und Prozentzahl im vorhandenen HP-Balken. |
| Remnant-Zielfilter | Erweitert | Während der aktiven Mission „Jagd auf die Remnanten“ bekannte Remnant-Gegner getrennt von normalen Gegnern filtern. |

Die Trägertabelle, ihre Bekanntgaben, der Lebensbalken und der Abflugtimer stammen aus dem Original. Forge ergänzt ihre Darstellung und die Verknüpfung mit dem Profil. Eine Beutekategorie zeigt **mögliche Beute**, keinen garantierten Drop.

„Nicht im Profil“ bedeutet **unbekannter Bestand**, nicht automatisch null Teile. Der ergänzte Katalog enthält auch historische Referenzen und ist keine Zusage aktueller Verfügbarkeit aller Einträge. CQ-Baupläne gehören zum Clanfortschritt und werden nicht als persönliche Baupläne ergänzt. Vergleich und Einkaufsplan nutzen Referenzwerte ohne persönliche Boni und ohne Garantie aktueller Shoppreise; Quellen und Stand stehen in der jeweiligen Ansicht.

[Bauplanübersicht ansehen](BILDER.md#bauplaene) · [Remnant-Beute ansehen](BILDER.md#remnant-beute)

## Kampf, Komponenten und Ziele

| Funktion | Herkunft | Ergänzung durch Forge |
| --- | --- | --- |
| Bossleisten | Neu | Für Remnant-Träger und das Mutterschiff der Königin: Name, großer HP-Balken mit Prozentwert und bis zu zehn Effektsymbole. Weitere über +N; Details per Klick. |
| Staffel-HP und Effekte | Erweitert | Prozentwerte in den Lebensbalken, aktive Effekte als Icons, Wirkung/Quelle und verfügbare Laufzeiten. Weitere Effekte als Symbolraster. |
| Komponenten verschieben | Erweitert | Ausgerüstete Komponenten durch Halten und Ziehen lokal umordnen; die sichtbare Reihenfolge wird gespeichert. |
| Tastenbelegung | Erweitert | Tasten für die sichtbaren Komponentenpositionen wählen; Chat und Texteingaben behalten Vorrang. |
| Slot-Timer | Erweitert | Aktive Restzeit in Grün und verbleibende Abklingzeit direkt auf der Komponente. Die Zahlen lassen sich getrennt ein-/ausschalten. |
| Zielreichweiten-Markierung | Neu | Slot-Umrandung für passende Komponenten mit Eigen-/Orts- und Zielanwendung, wenn das ausgewählte Ziel in Reichweite ist. |
| Blitzketten-Markierung | Neu | Die Blitzkette leuchtet bei einem geeigneten bekannten Gegner in direkter Reichweite auf, auch ohne ausgewähltes Ziel. |
| Quantensprung-Ring | Neu | Optionaler kontrastreicher Reichweitenring auf Planeten mit entsprechend ausgerüstetem Schiff. |
| Zielhaltung nach Quantensprung | Erweitert | Die Option **Zielhaltung außerhalb von PvP** kann die Auswahl bei NPCs und anderen Zielen ohne feindliche PvP-Beziehung erhalten. Bei feindlichen Spielern greift ab Alpha 63 die Original-Abwahl. Die Einheit muss weiterhin vorhanden und auswählbar sein. |
| Orbitalschlaganzeige | Erweitert | Zusätzliche Konturen und bei bekannten Varianten geschätzter Countdown mit Füllung/Farbverlauf. Aus, Nur Kontur oder Zeit + Füllung. |
| Reparaturfelder | Erweitert | Original, Reduziert oder Nur Kontur. Reduziert erhält die Animation und dämpft überlappende Leuchteffekte. |
| HP-Warnschwelle | Erweitert | Der originale Warnsound bei 25 % richtet sich nach einer einstellbaren Schwelle von 5 bis 50 %. |
| Rote Bildschirmränder | Neu | Weiche visuelle Warnung bei kritischen HP; standardmäßig an und separat abschaltbar. Bildmitte und HUD bleiben frei. |

Anzeigen verwenden verfügbare Clientdaten. Sie machen keine noch nicht übermittelten Gegner sichtbar. Unbekannte Effektlaufzeiten bleiben „aktiv“; Quellen werden nur bei vorhandener Zuordnung genannt. Reichweitenmarkierungen ändern weder Reichweite noch Trefferregeln.

Orbitalzeiten und Grenzen sind **Schätzungen**. Unbekannte Varianten erhalten keinen erfundenen Countdown. Konturen können auch bei passenden roten NPC-Warnungen außerhalb von Remnant-Kämpfen erscheinen. **Aus** entfernt die zusätzlichen Forge-Markierungen, nicht die Originaleffekte.

[Bossleiste ansehen](BILDER.md#bossleiste) · [Slot-Timer ansehen](BILDER.md#slot-timer)

## Sammeln, Drohnen und Reise

| Funktion | Herkunft | Ergänzung durch Forge |
| --- | --- | --- |
| Kryonitstatistik | Neu | Kompaktes Widget mit Sammlung, Rate und Bilanz; Tages-/Farmansicht sowie Start, Pause und Zurücksetzen. Verschobene Position bleibt erhalten. |
| Energiekugel-Markierung | Neu | Dezente Ecken markieren die größte übermittelte Energiemenge im nahen Kugelfeld. |
| Drohnen-Levelzeiten | Erweitert | Geschätzte aktive Zeit bis zum nächsten und maximalen Level. Bei Maximallevel entfällt der zusätzliche Bereich. |
| Drohnenslots im Hangar | Korrigiert | Seit Alpha 64 aktualisiert sich die Liste nach einem Schiff- oder Konfigurationswechsel aus der aktuellen Drohnenbelegung. |
| Eigene Positionsmerker | Neu | Aktuelle Positionen benennen, speichern und in einer schematischen Übersicht wiederfinden. |
| Sirius-Reichweitenfenster | Neu | Vom aktuellen Clanschiff-Planeten berechnete Zeitfenster mit Datum/Uhrzeit und relativem Stundenbereich. |
| Sirius-Reiseerinnerungen | Neu | Eine ausgewählte Route vormerken; Hinweis vor und bei Beginn des Reichweitenfensters. |

Die Kryonitstatistik erfasst beobachtete Werte während der Nutzung; sie ist keine vollständige Verkauf-/Ausgabenbuchhaltung. Die Energiekugel-Markierung sammelt nichts automatisch. Ab Alpha 63 werden Drohnen beim Kryonit-Sammeln manuell gesteuert.

Positionsmerker sind keine Wegfindung. Bei erneutem Gebietsbesuch werden sie bestätigt. Sirius-Prognosen ersetzen keine Quarc-, Lade- oder Zugangsbedingungen und lösen keine Reise aus.

## Oberfläche, Audio und Personalisierung

| Funktion | Herkunft | Ergänzung durch Forge |
| --- | --- | --- |
| Forge-Fenster | Neu | Acht Tabs: Baupläne, Ausrüstung, Reise, Tasten, Anzeige, Diagnose, Audio und Antrieb. F in der oberen Menüleiste öffnet/schließt das Fenster. |
| Bedienung neben Forge | Erweitert | Andere Spielfenster und Aktionen außerhalb des Forge-Fensters bleiben bedienbar. |
| Globale HUD-Größe | Erweitert | 100/115/130/150/175/200 %, abhängig von der Fenstergröße; gilt auch für native Spielfenster. |
| Gebündelte Anzeigeoptionen | Neu | Fünf Gruppen für HUD & Grafik, Komponenten, Kampf & Effekte, Widgets sowie Meldungen & Discord. Seit Alpha 63 erklärt ein Tooltip jede Option. |
| Chat-Uhrzeit | Erweitert | Optional [HH:mm] vor Nachrichten im Kommunikationsfenster und kleinen HUD-Chat; lokale Zeitzone. |
| Status-Farbeditor | Erweitert | Textabschnitte oder ganzen eigenen Status einfärben, Vorschau, Standardfarbe und Rückgängig. Farbige Statustexte selbst unterstützt bereits das Original. |
| Meldungsfilter | Erweitert | Seltene-Mantis-Sichtungen und Angriffs-/Siegesmeldungen getrennt schalten. |
| Eigene Musik und Sounds | Neu | Einzelne Musikstücke, Komponenten- und allgemeine Effekte durch eigene Ogg-Vorbis-/WAV-Dateien ersetzen; Suche, Filter und Original-/Eigenvorschau. |
| Ausschnitte und Lautstärke | Neu | Start/Länge wählen, optional automatisch kürzen und Lautstärke pro Eintrag von 0–300 % einstellen – auch ohne Ersatzdatei. |
| Audio live übernehmen | Neu | Änderungen ohne Client-Neustart aktivieren; laufende kurze Effekte enden regulär, folgende Wiedergaben nutzen die neue Zuordnung. |
| Antriebsvorschau | Neu | Uni-, Zwillings- und Tristar-Spuren in je neun Farben plus Schiffsstandard. Typ-/Farbfilter und direktes Durchschalten im Vorschaumodus. |
| Discord-Spielstatus | Neu | „Pirate Galaxy“ mit Original-Logo und Sitzungsdauer; aktueller Ort optional. |
| Lokaler Planetenname | Erweitert | Lyris heißt in den lokalen Spieltexten „Lörres“, auch in Missions- und Reiseanzeigen. Die Planetenidentität bleibt gleich. |

Eigene Sounds und die Antriebsvorschau gelten lokal. Die Vorschau erwirbt keine Antriebsspur und verändert die tatsächliche Ausrüstung nicht; andere Spieler sehen weiterhin die ausgerüstete Spur. Normal, Schließen oder Gebietswechsel beendet die Vorschau.

Discord benötigt den geöffneten Desktopclient und erlaubte Aktivitätsanzeige. **Medal-Aufnahme und Discord-Overlay wurden im Spiel getestet; sie sind Funktionen der jeweiligen Anwendungen.** Medal kann weiterhin „Requested“ statt der offiziellen Spielkategorie anzeigen. [Einrichtung und Grenzen](HILFE.md#discord-und-medal).

[Audio ansehen](BILDER.md#audio) · [Antrieb vergleichen](BILDER.md#antrieb) · [HUD-Größe ansehen](BILDER.md#hud)

## Technik, Diagnose und Korrekturen

| Bereich | Herkunft | Änderung in Forge |
| --- | --- | --- |
| 64-Bit-Client | Neu | 64-Bit-Laufzeit und native Bibliotheken statt des 32-Bit-Adressraums. Die Grundlage bleibt die vorhandene Spiel-Engine. |
| FPS-Limit und VSync | Erweitert | Direkt erreichbare Einstellungen in Forge; FPS-Limit nach Übernehmen, VSync nach Neustart. |
| Ping und Leistungsanzeige | Erweitert | Der Ping steht unten rechts. Daneben zeigt Forge auf Wunsch FPS oder FPS mit Bildzeit und P99. |
| Detaildiagnose | Neu | FPS, 1%-Lows, Bildzeiten, Aussetzer, Java-Speicher und GC-Aktivität; manuell gestartete lokale Diagnoseaufnahmen. |
| Speicherarbeit im Renderpfad | Erweitert | Wiederverwendung kurzlebiger Objekte für Antriebsspuren, Kamera, Matrizen, Szenenwerte, Render-Passes und Zielstrahlen. |
| UI-Aktualisierung | Erweitert | Weniger wiederholte Abfragen und unnötige Aktualisierungen. |
| Textdarstellung | Korrigiert | Gezielte Korrekturen gegen verschluckte Zeichen und fehlerhafte Zeilenumbrüche. |
| Planeten- und Zielvorschauen | Korrigiert | Material-/Texturzuordnung, Vorschau-Clipping und Nachladen verbessert, einschließlich Armene. |
| Profil-/Clan-Vorschau | Korrigiert | Absicherung verzögerter Ladevorgänge gegen inzwischen geschlossene oder ersetzte Vorschaufenster. |
| Commerce-Central-Gebäude | Korrigiert | Bekannte defekte Detailstufen verursachen keine gestreckten Texturstreifen mehr; auffällige Materialwechsel wurden gezielt angepasst. |
| Landen bei mittlerer Grafikqualität | Korrigiert | Gefundenen Fehler im Wolken-/Shaderpfad behandelt. |
| Audioverarbeitung | Korrigiert | Streamversorgung, Decoderfehler und Pufferbehandlung verbessert. |
| Komponentenstatus | Korrigiert | Falsche Aktivierungsanzeige nach ausdrücklich abgelehnten Aktionen zurücknehmen und mit dem tatsächlichen Cooldown abgleichen. |
| Zielelisten-Fokus | Korrigiert | Komponententasten nach Auswahl eines Gegenstands in der Zieleliste wieder nutzbar. |
| Installer und Updates | Neu | Getrennte Forge-Spielkopie, automatische Versionswechsel, signierte Metadaten und Downloadprüfung; alternative Downloadversuche bei vorübergehenden GitHub-Fehlern. |

Korrekturen betreffen sowohl übernommene Fehler als auch Probleme der Portierung. Beispielsweise ließen sich die fehlerhaften Commerce-Central-Geometrie-LODs mit den gleichen Ressourcen auch im isolierten 32-Bit-Renderer reproduzieren. Andere Korrekturen stammen aus konkreten Forge-Absturz- oder Darstellungsberichten; daraus folgt keine pauschale Aussage über jeden Originalclient.

Alpha 60 korrigiert einen Fehler in der Schattenprojektion, der auf Hoch und Ultra zu flackernden Bodenschatten führen konnte. Beim Skalieren des HUD behebt die Version einen Absturz, der auftreten konnte, wenn das Renderfenster bereits geschlossen war.

Seit Alpha 61 richtet sich die Projektion der Bodenschatten für gerichtetes Licht nach dem sichtbaren Schattenbereich. Das behebt den erneut beobachteten Projektionssprung bei ungewöhnlich großen Objektbegrenzungen.

Seit Alpha 62 läuft die Ladeansicht bei Übergängen zwischen Oberfläche, Orbit und Sternkarte früher an. Für Erebos bereitet Forge die Aufteilung der Szene im Orbit lokal vor. Entfernte Dekoration erscheint nach der ersten spielbaren Ansicht. Wenn die Quelldatei fehlt, sich geändert hat oder die Vorbereitung noch läuft, lädt Forge die Originalszene.

**Noch offen:** spät übermittelte Gegner und weitere mögliche Ruckler/Absturzursachen. Ein größerer Adressraum allein garantiert keine höheren FPS. Diagnoseaufnahmen sind Messdaten, keine Bildschirmvideos. Für Linux gibt es eine [Wine-Vorschau](../README.md#linux-vorschau-wine). Ein Grafikmodus über Ultra und neue 4K-Texturen sind nicht enthalten.

[Releasehinweise mit den einzelnen Änderungen](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases) · [Fehler melden](HILFE.md#startfehler-und-abstürze)
