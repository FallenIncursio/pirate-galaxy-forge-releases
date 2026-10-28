# Pirate Galaxy Forge

Inoffizieller 64-Bit-Communityclient für Pirate Galaxy. Die aktuelle öffentliche Testversion ist **0.1.0-alpha.3**.

**[Installer herunterladen](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases/download/v0.1.0-alpha.3/PirateGalaxyForge-0.1.0-alpha.3-Setup.exe)** · [Releasehinweise und Prüfsummen](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases/tag/v0.1.0-alpha.3)

## Installation

1. Die offizielle Pirate-Galaxy-Version installieren beziehungsweise aktualisieren. Forge unterstützt aktuell Spielstand **1002132** und benötigt dessen `Basic.jar`, `PirateGalaxy.jar` und `core`.
2. Den Forge-Installer ausführen und anschließend **Pirate Galaxy Forge** starten.
3. Den Ordner der Originalinstallation auswählen, normalerweise `%APPDATA%\Splitscreen Studios\Game Launcher\gamedata\Pirate Galaxy`.
4. Der Start lädt und prüft das Forge-Paket sowie Java direkt vom Hersteller. Danach im Spiel anmelden.

Windows 10/11 x64 und .NET Framework 4.8 werden benötigt. Forge arbeitet in einer getrennten Kopie; Originalspiel und Original-Anmeldedaten werden nicht verändert oder mitgeliefert. Fehlende Ressourcen werden vom Spiel nachgeladen. Das Setup ist derzeit nicht Authenticode-signiert; die SHA256-Prüfsummen stehen beim Release.

## Updates und Einstellungen

Bei jedem Start prüft Forge den signierten Alpha-Updatefeed. Neue Clientversionen werden heruntergeladen, geprüft und erst danach aktiviert. Bei einem fehlgeschlagenen Update bleibt die vorhandene Version erhalten. FPS/VSync werden dauerhaft gespeichert; vorhandene Forge-Spieleinstellungen werden in die neue Version übernommen. Ein späterer Spielabsturz löst keinen automatischen Versionswechsel aus.

Der Installer selbst startet das Spiel nicht automatisch. Die Deinstallation entfernt Startanwendung und Verknüpfungen; heruntergeladene Spielkopien und Einstellungen unter `%LOCALAPPDATA%\PirateGalaxyForge` bleiben erhalten.

## Freiwillige Aktivitätszählung

Die Zählung ist standardmäßig **aus**. Bei Zustimmung werden während des Spiels alle zwei Minuten eine zufällige Installationskennung und die Version per HTTPS gesendet. Der Dienst speichert eine HMAC-Kennung, Version und letzte Aktivität, keine Spielkonten, Namen, Hardware- oder Standortdaten. IP-Adressen werden beim Zähler nicht protokolliert. Einträge verfallen nach sieben Tagen. Die Teilnahme lässt sich jederzeit über **Pirate Galaxy Forge - Einstellungen** ausschalten. Gezählt werden teilnehmende Installationen, nicht alle Spieler.

## Alpha-Einschränkungen

Native Abstürze sowie einzelne Grafik- und Performancefehler sind noch möglich. Weiße Mantissen, sporadisches Schattenflackern, Ruckler unter Last und weitere UI-/Musikfälle werden weiter bearbeitet. 240 FPS in jeder Situation und die Erkennung durch Discord/Medal sind nicht zugesichert. Bekannte Probleme stehen in den Releasehinweisen.

## Quellen und Bibliotheken

Der Forge-Entwicklungscode liegt in einem privaten Repository. Die passenden Bibliotheksquellen und vollständigen Lizenzhinweise stehen als separate Archive beim jeweiligen Release bereit. Java wird direkt vom offiziellen Azul-CDN geladen und nicht hier weiterverteilt. Unveränderte Originalspiel-JARs, Ressourcen, Benutzerprofile oder Zugangsdaten sind keine Releaseassets.

Pirate Galaxy Forge ist kein offizielles Produkt von Splitscreen Studios.
