# Pirate Galaxy Forge

Inoffizieller **64-Bit-Communityclient für Pirate Galaxy** – mit zusätzlichen Spielanzeigen, anpassbarem HUD, eigenen Sounds und gezielten Performance- und Fehlerkorrekturen.

**[Windows-Installer herunterladen](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases/download/v0.1.0-alpha.59/PirateGalaxyForge-0.1.0-alpha.59-Setup.exe)** · **[Linux-Vorschau herunterladen (Wine)](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases/download/v0.1.0-alpha.59/PirateGalaxyForge-Linux-Wine-Preview-Alpha59.zip)** · **0.1.0-alpha.59** · [Releasehinweise und Prüfsummen](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases/tag/v0.1.0-alpha.59)

[Alle Funktionen im Vergleich](docs/FUNKTIONEN.md) · [Bildergalerie](docs/BILDER.md) · [Installation und Hilfe](docs/HILFE.md)

Mit Alpha 54 startet Forge direkt in 64 Bit. Forge lädt die benötigten Spielbasisdateien beim ersten Start direkt von Splitscreen.

Alpha 55 ergänzt die Bossleiste für Ancient-Giza, Ancient-Soris und Ancient-Amarna in Sirius.
Alpha 58 ergänzt die Effekt-Tooltips um Empfänger, beobachtete Wirkzeit und bestätigte eigene Anwendungen.

Alpha 59 bringt die lokale Vorschau des Remnant-Kampfberichts mit Pilot- und Staffelansicht. [Aufnahme und Auswertung](docs/HILFE.md#remnant-kampfbericht-vorschau)

## Ein Blick ins Spiel

**Bossleisten mit HP-Prozent und aktiven Effekten**

[![Remnant SC-Tyme mit Bossleiste, 40,3 Prozent HP und vier Effektsymbolen](docs/bilder/bossleiste.png)](docs/BILDER.md#bossleiste)

**Mögliche Remnant-Beute direkt mit dem eigenen Bauplanbestand vergleichen**

[![Remnant-Trägertabelle mit Beutekarten und getrennten Beständen für normale, schnelle, starke und lange Varianten](docs/bilder/remnant-beute.png)](docs/BILDER.md#remnant-beute)

**Baupläne durchsuchen, Fortschritt filtern und eine Merkliste führen**

[![Forge-Bauplanübersicht mit Tau-Ceti-Filter, Suchfeld und gesammelten Teilen](docs/bilder/bauplaene.png)](docs/BILDER.md#bauplaene)

[Weitere Bilder: Audio, Antriebsvorschau, HUD-Größe und Komponenten-Timer →](docs/BILDER.md)

## Was ergänzt Forge gegenüber dem Original?

Die Spielwelt, Missionen, Gegenstände, Originalgrafiken und Grundfunktionen stammen aus **Pirate Galaxy**. Forge baut darauf auf.

| Bereich | Im Original bereits vorhanden | Zusätzlich in Forge |
| --- | --- | --- |
| Baupläne und Ausrüstung | Bauplanprofil, Shop und Komponentenwerte | Suche, Fortschritts-/Systemfilter, Referenzkatalog, Merkliste, Vergleich und Einkaufsplan |
| Remnant-Träger | Trägertabelle, Bekanntgaben, Statusbalken und Abflugtimer | HP-Prozent, verständliche Wartephase und Beutekarten mit eigenen Variantenbeständen |
| Staffel und Bosse | Staffel- und Zielanzeigen | Staffel-HP in Prozent, Effektsymbole und zusätzliche Bossleisten für Remnants und Königin |
| Komponenten und Ziele | Aktivierung, Abklingzeiten und Zielauswahl | Slots umordnen, Tasten belegen, Aktivzeit-Timer, Reichweitenmarkierungen und Zielhaltung nach Quantensprung |
| Sammeln und Drohnen | Energiekugeln, Kryonit und manuelle Drohnensteuerung | Größte Energiekugel markieren, Kryonitstatistik, optionaler Drohnenwechsel und geschätzte Levelzeiten |
| Kampfansicht | Reparaturfelder, Orbitalwarnungen und HP-Warnsound | Gedämpfte Reparaturfelder, zusätzliche Orbitalanzeigen, einstellbare HP-Warnschwelle und rote Bildschirmränder |
| HUD und Chat | Spielfenster, Chat und Statusformatierung | Globale HUD-Skalierung, Chat-Uhrzeit, Status-Farbeditor und schaltbare Meldungen |
| Musik und Sounds | Originalmusik, Effekte und Lautstärkeregler | Eigene Ogg-Vorbis-/WAV-Dateien, Ausschnitte, Vorschau und Lautstärke pro Sound; ohne Client-Neustart übernehmen |
| Antriebsspuren | Tatsächlich ausgerüstete Spur | 27 Spuren und Schiffsstandard als lokale Live-Vorschau am eigenen Schiff |
| Reise und Sirius | Sternkarte und Planeteninformationen | Positionsmerker, berechnete Reichweitenfenster und Reiseerinnerungen |
| Leistung und Diagnose | Vorhandene Spiel-Engine und Pinganzeige | Einstellbares FPS-Limit/VSync, schaltbarer Ping, Bildzeiten, 1%-Lows und lokale Diagnoseaufnahmen |
| Discord | Externe Spiel-/Overlay-Erkennung | Integrierter Spielstatus als „Pirate Galaxy“ mit Logo, Sitzungsdauer und optionalem Ort |

**Neu, erweitert oder korrigiert?** Die [ausführliche Funktionsübersicht](docs/FUNKTIONEN.md) kennzeichnet die Herkunft jeder Ergänzung und erklärt ihre Grenzen. Beispielsweise sind farbige Statustexte und der HP-Warnsound Originalfunktionen; Farbeditor und einstellbare Warnschwelle kommen von Forge.

## Technik und Korrekturen

- **64-Bit-Laufzeit:** größerer nutzbarer Adressraum als im 32-Bit-Client.
- **Weniger Speicherarbeit:** Wiederverwendung kurzlebiger Render-/Kameraobjekte und weniger unnötige UI-Aktualisierungen.
- **Gezielte Fehlerkorrekturen:** unter anderem Textumbruch, Planeten-/Schiffsvorschauen, Commerce-Central-Gebäudetexturen, Audioverarbeitung und Komponentenstatus.
- **Eigener Updateweg:** getrennte Spielkopie, signierte Update-Metadaten und geprüfte Downloads.

64 Bit allein garantiert weder höhere FPS noch Absturzfreiheit. Forge bleibt eine **experimentelle Alpha**; unter anderem Schattenflackern und spät erscheinende Gegner sind nicht allgemein behoben. Es werden keine neuen 4K-Texturen mitgeliefert.

## Installation

Voraussetzungen sind **Windows 10/11 (64 Bit), .NET Framework 4.8 oder neuer und Internetzugang**. Forge unterstützt den Spielstand **1002132**.

1. Den Forge-Installer ausführen und **Pirate Galaxy Forge** starten.
2. Forge lädt und prüft die Spielbasis von Splitscreen und Java von Azul. Sobald das Spielfenster erscheint, im Spiel anmelden.

Bei vorhandenen Installationen übernimmt Forge die Einstellungen. Falls der alte Starter vor der Updateprüfung einen Originalordner verlangt oder das Update scheitert, Forge schließen und das aktuelle Setup über die vorhandene Installation ausführen.

Im Spiel öffnet **F in der oberen Menüleiste** das Forge-Fenster. Andere Fenster und Spielaktionen außerhalb bleiben bedienbar. Anzeigeoptionen sind dort in fünf Gruppen zusammengefasst.

### Linux-Vorschau (Wine)

Du brauchst **Linux x86_64, Python 3.9 oder neuer**, eine grafische Sitzung und Internetzugang. Wine muss 32- und 64-Bit-Windows-Programme unterstützen und `winepath` bereitstellen. Installiere auch die Wine-Schriften (unter Ubuntu `fonts-wine`).

Entpacke das [ZIP der Linux-Vorschau](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases/download/v0.1.0-alpha.59/PirateGalaxyForge-Linux-Wine-Preview-Alpha59.zip) und öffne im entpackten Ordner ein Terminal. Der erste Befehl richtet ein eigenes Wine-Profil für Forge ein, der zweite startet den Client.

```sh
python3 forge_wine.py install
python3 forge_wine.py launch
```

Danach kannst du Forge auch über den Menüeintrag **Pirate Galaxy Forge (Wine Preview)** starten.

Forge bezieht Spielupdates beim Start aus dem signierten Kanal. Für die aktualisierten Linux-Startdateien das neue ZIP entpacken und `python3 forge_wine.py install` erneut mit demselben Profilpfad ausführen. Wenn Wine den gespeicherten Kampfbericht nicht öffnet, `python3 forge_wine.py report` verwenden. Bei einem eigenen Profil für alle Befehle denselben `--root`-Pfad angeben.

## Hilfe und Projekt

- [Installation, Updates und Fehler melden](docs/HILFE.md)
- [Lokale Daten, freiwillige Aktivitätszählung und Fehlerberichte](docs/DATENSCHUTZ.md)
- [Alle Veröffentlichungen](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases)

Bibliotheksquellen und Lizenzhinweise stehen beim jeweiligen Release als separate Archive bereit. Der Forge-Entwicklungscode ist privat. Die Screenshots zeigen Forge; sie sind keine Vergleichsaufnahmen des Originalclients.

Pirate Galaxy Forge ist kein offizielles Produkt von Splitscreen Studios.
