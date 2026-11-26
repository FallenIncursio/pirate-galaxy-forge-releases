# Enhanced bedienen

[Übersicht](../../README.md) · [Alle Funktionen und Vergleich](FUNKTIONEN.md) · [Installation](INSTALLATION.md) · [Diagnose](DIAGNOSE.md)

## Forge öffnen und Einstellungen übernehmen

Der **F-/Forge-Knopf** in der oberen Menüleiste öffnet den Dialog.
Unter **Anzeige** sind die Optionen nach HUD & Grafik, Komponenten, Kampf & Effekte,
Widgets sowie Meldungen & Discord geordnet. **Übernehmen** speichert den Entwurf;
**Verwerfen** oder Schließen verwirft ungespeicherte Änderungen. Hinweise an den
Bedienelementen erklären den jeweiligen Umfang.

## HUD und Komponentenzeiten

Unter **Anzeige → HUD & Grafik** stehen HUD-Größe und Leistungsanzeige.
FPS und Ping erscheinen unten rechts. Die ursprünglichen Spieleinstellungen
behalten Sprache, Auflösung, Grafikqualität und Lautstärke.

Unter **Anzeige → Komponenten** lassen sich Aktiv- und Abklingzeiten als Zahlen,
Kreis oder Kreis mit Zahlen darstellen. Eigene Belegungen stehen unter **Forge → Tasten**.
Chat und Texteingaben behalten Vorrang vor Komponententasten.

## Clankasse und Sperrfrist

Zuweisungen von Schädeln, Gravitonen und Kryonit bestätigen Empfänger und Menge.
Unter der Mitgliederauswahl erscheint die verbleibende 14-Tage-Sperrfrist, sofern
der Beitrittszeitpunkt vorliegt. „Keine Zeitangabe“ bedeutet, dass dem Client diese
Information fehlt. „Sperrfrist abgelaufen“ ersetzt keine Serverfreigabe; Wochenlimit,
Bestand und Berechtigung gelten weiterhin. Bei unbekanntem Zuweisungsergebnis zuerst
den Bestand prüfen und nicht sofort erneut zuweisen.

## Reisekosten-Vorschau

Während eines interplanetaren Flugs zeigt die zusätzliche Zeile neben dem
Energiepreis den nächsten niedrigeren Hypersprungpreis und die verbleibende
Wartezeit. Gültige Mitgliedschaftsrabatte werden berücksichtigt. Bei kostenlosen
Sprüngen oder fehlender Zeitbasis wird die Zeile ausgeblendet.
**Forge → Anzeige → HUD & Grafik → Reisekosten-Vorschau** schaltet sie ein oder aus.
Der Hypersprung wird weiterhin ausschließlich über den ursprünglichen Knopf ausgelöst.

## Baupläne, Fundorte und CSV

**Forge → Baupläne** bietet Suche, Typ-, Bereichs- und Fortschrittsfilter sowie eine
Merkliste. Typen verwenden die Originalbezeichnungen des Spiels; bisherige Begriffe
wie Nanitenwolke sowie Angriffsbuff bleiben als Suchbegriffe verfügbar.
**Alle Bereiche** enthält die Systeme, **Events**, **RDX / Parsec** und
**Remnant**. Beim Markieren oder Aktualisieren bleiben Seite und Auswahl erhalten;
eine neue Suche oder Filterauswahl beginnt auf der ersten passenden Seite.
**Fundorte** zeigt zugeordnete Planeten, Systeme, Gegner und bekannte Level.
Auf dem passenden Planeten lässt sich ein Suchziel auf der Karte vormerken.
**Hier erhältlich** kombiniert den aktuellen Ort mit den übrigen Filtern.

Bestätigte vollständige Baupläne werden bei der vorhandenen Profilaktualisierung
automatisch von der Merkliste entfernt. **Anzeige → HUD & Grafik → Vollständige BPs
automatisch abhaken** schaltet dies aus oder ein. Ungeklärte Sammelstände bleiben
markiert, der Einkaufsplan bleibt erhalten. Bei wiederholt sammelbaren Bauplänen
zählt der aktuelle vollständige Teilesatz, nicht eine frühere Herstellung.

**CSV exportieren** exportiert alle passenden Treffer über sämtliche Seiten in
derselben Reihenfolge. Gesammelte, benötigte und fehlende Teile sowie System und
Bereich stehen getrennt;
unbekannte Werte bleiben leer. Die Ergebnisanzeige bietet den Exportordner an.
In einer Sandbox bezieht sich dieser Pfad auf deren Dateisicht.

Im Scanfenster erscheinen mögliche blaue/goldene Baupläne mit eigenem Bestand.
Die Anzeige berücksichtigt Sirius-Klassen, lässt Giza, Soris und Amarna aus und
erfindet bei fehlender Zuordnung keine Drops. Die Erweiterung ist unter **Anzeige** abschaltbar.

## Sirius und Errungenschaften

Die Sirius-Karte zeigt bekannte Quarc-Freigaben. Fehlen Daten, bleibt der Status
unbekannt. Gelbe Bauplaneinträge ergänzen bekannte Teilezahlen, etwa **2/6**.
Die Sirius-Erweiterung lässt sich unter **Anzeige → HUD & Grafik** abschalten.

Im **Pilotenprofil → Errungenschaften** stehen Suche, Status-, System- und
Bereichsfilter sowie Sortierung bereit. Abgeschlossene Einträge behalten die goldene
Medaille. Unter **Forge → Anzeige** lässt sich die Originalansicht wiederherstellen.

## Bossleisten und Staffel

Bossleisten zeigen HP, bekannte Itemklasse und beobachtete Effekte. Ein Klick auf
Name oder Lebensbalken wählt den Boss als Ziel. Effektsymbole öffnen weiterhin
deren Details. XC und SC können unterschiedliche Farben und eine abschaltbare
Randanimation verwenden; MN/DL erhalten keinen Remnant-Bossauftritt.

Bekannte Schild-/Schutzreserven umhüllen den Lebensbalken blau und nehmen von
rechts nach links ab. Entsprechende Reserven sind auch in der Staffelleiste mit
optionalem Prozentwert sichtbar. Unbekannte Reserven werden nicht als voll ausgegeben.
Die Einstellungen stehen unter **Anzeige → Kampf & Effekte / Bossleisten**.

## Reparaturfelder

Unter **Anzeige → Kampf & Effekte** gibt es getrennte Auswahlen für **Spieler**,
**PvE-Gegner** und **PvP-Gegner**. Alle bieten **Original**, **Leicht reduziert**, **Stark reduziert**
und **Nur Kontur**. Stark reduziert entspricht dem früheren Reduziert.

**PvP-Felder rot markieren** färbt Felder feindlicher Spieler optional rot,
auch bei voller Effektstärke mit **Original**. Spieler umfasst die eigenen,
freundlichen und neutralen Felder. Die Einteilung folgt der PG-Spielerbeziehung.

Die neue PvP-Auswahl übernimmt zunächst deine bisherige Spielerstufe; die
Rotmarkierung ist anfangs aus. Neue Profile verwenden Spieler/PvP Original und
PvE Stark reduziert. Bekannte Spielertürme werden ihrem Besitzer zugeordnet.
Bei unbekannter Spielerbeziehung wird kein Rot erzwungen; bei völlig unbekannter
Herkunft bleibt die Darstellung original. Heilung und Reichweite bleiben gleich.

## OTB und Gravitonen

Das OTB-Widget zeigt lokale Aktivitätswerte und einen Warn-Countdown. Die
**Serverwertung bleibt unbekannt**; ein lokaler Aktivitätswert garantiert keine
Belohnung und verhindert keine Sperre. Abschalten und Testvorschau stehen unter
**Anzeige → Widgets**.

Im sechsten Gravitonen-Slot erscheint ein beobachteter Drop, ein unbekannter
Zustand oder eine geschätzte einzeilige Restzeit. Details stehen im Tooltip.
Ein vor der Beobachtung gesammelter Drop wird nicht rückwirkend erraten.
Einstellung und Vorschau stehen ebenfalls unter **Widgets**.

## Meldungen, Statistik und Updates

Forge-Meldungen erscheinen über der Komponentenleiste im PG-Stil. Unter
**Anzeige → Meldungen & Discord** stehen **Alle / Nur wichtige** und eine Testmeldung.
Fehler haben Vorrang; wiederholte Rückmeldungen werden zusammengefasst.

Der KW-Tracker zeigt beobachtete Gutschriften, Kategorien, Verlauf und CSV-Export.
Weitere Widgets bieten Kryonitstatistik, Energiekugelmarkierung und geschätzte
Drohnen-Levelzeiten.

**Updates** steht ganz rechts neben **Antrieb**. Jede Karte zeigt Version, Datum
und eine kurze Beschreibung. **Neuer**, **Älter** und die Auswahl der Versionsreihe
erschließen die gesamte Historie. **Installiert** markiert den aktuellen Client;
**Neu** am Tab verschwindet, sobald der aktuelle Eintrag angezeigt wurde. Historische Daten sind
Veröffentlichungsdaten, **Stand** bezeichnet einen noch vorbereiteten Eintrag.
Die Anzeige benötigt keine Internetabfrage.

Bei ungelesenen Neuigkeiten leuchtet und glitzert das **F**. Ein Klick öffnet
direkt den aktuellen Updateeintrag. Zusätzlich erscheint einmal je Version die
native Meldung „Sepp, was steht in den Pirate Galaxy News?“. Unter
**Anzeige → Meldungen & Discord → Updatehinweise** stehen **Leuchten und Meldung**,
**Nur Leuchten** und **Aus** bereit. **Updatehinweis testen** zeigt eine kurze
Vorschau, ohne den Gelesen-Status oder deine Einstellungen zu verändern.
**Nur wichtige** bei Forge-Meldungen unterdrückt die automatische Update-Meldung.

Der frühere Reise-Tab entfällt; gespeicherte Positionsmerker werden nicht gelöscht.
Sirius-Karte, Quarc-Status und Bauplan-Fundorte bleiben separat verfügbar.
Schätzungen und Referenzen sind keine zusätzlichen Serverbestätigungen.

## Eigene Sounds und Antriebsspuren

Unter **Audio** lassen sich unterstützte eigene Ogg-Vorbis-/WAV-Dateien importieren,
zuschneiden und mit Einzelpegeln verwenden. **Antrieb** bietet lokale Spuren für
das eigene Schiff und zugehörige Drohnen. Diese Vorschauen verändern nicht die
Darstellung bei anderen Spielern. Die originalen Inhalte bleiben Spielbestandteile.
