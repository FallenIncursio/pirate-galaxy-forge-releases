# Pirate Galaxy Forge

Inoffizieller 64-Bit-Communityclient für Pirate Galaxy. Aktuelle öffentliche Alpha-Vorschau: **0.1.0-alpha.7-preview.8**.

**[Installer herunterladen](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases/download/v0.1.0-alpha.7-preview.8/PirateGalaxyForge-0.1.0-alpha.7-preview.8-Setup.exe)** · [Releasehinweise und Prüfsummen](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases/tag/v0.1.0-alpha.7-preview.8)

**Neu:** Erweiterte Absturzberichte mit vorhandenen Fehlerstellen, Aufrufstellen und passenden Buildkennungen. Der Dienst kann wiederkehrende Fehler genauer gruppieren und nimmt weiterhin ältere Berichtsformate an. Der Starter wird auf Revision 4 aktualisiert. Spielbibliotheken, Java-Dateien und JVM-Einstellungen entsprechen Preview 7; deren Stabilitätskorrekturen und Komfortfunktionen bleiben enthalten.

**Bestehende Nutzer ab Starterrevision 2 erhalten das Update beim nächsten Forge-Start automatisch**, einschließlich des Starters (Revision 4). Nur bei einem älteren Starter ist einmal das aktuelle Setup nötig. Der alte Kanal bleibt auf Alpha 5; der aktuelle Starter nutzt `channel-alpha-v2`. Der Starter bietet weiterhin Forge (64 Bit) und den installierten offiziellen Client (32 Bit) an.

Anmeldedaten werden lokal mit Windows DPAPI geschützt; Forge-Einstellungen und der feste Prozesspfad für die Windows-Lautstärke bleiben über Updates erhalten. Die neuen Anzeigen verwenden vorhandene Clientdaten und schicken keine zusätzlichen Spielanfragen.

Neuinstallation, Update von Preview 7 mit synthetischen Profilen, Rollback und Installerprüfung in einer separaten Sandbox sind bestanden. Geprüft sind außerdem der Starterwechsel von Revision 3 auf 4, die gepackten Reporter und beide Berichtsformate über HTTPS. Das installierte Paket bestand drei Grafik-/JNI-Teststarts. Ein realer Spielerabsturz wurde für diese Veröffentlichung nicht getestet; vollständige Live- und Langzeittests stehen weiterhin aus. **Die Veröffentlichung bleibt eine experimentelle Alpha.**

## Installation

1. Die offizielle Pirate-Galaxy-Version installieren beziehungsweise aktualisieren. Forge unterstützt aktuell Spielstand **1002132** und benötigt dessen `Basic.jar`, `PirateGalaxy.jar` und `core`.
2. Den Forge-Installer ausführen und anschließend **Pirate Galaxy Forge** starten.
3. Den Ordner der Originalinstallation auswählen, normalerweise `%APPDATA%\Splitscreen Studios\Game Launcher\gamedata\Pirate Galaxy`.
4. Der Start lädt und prüft das Forge-Paket sowie Java direkt vom Hersteller. Danach im Spiel anmelden.

Windows 10/11 x64 und .NET Framework 4.8 werden benötigt. Forge arbeitet in einer getrennten Kopie; Originalspiel und Original-Anmeldedaten werden nicht verändert oder mitgeliefert. Fehlende Ressourcen werden vom Spiel nachgeladen. Das Setup ist derzeit nicht Authenticode-signiert; die SHA256-Prüfsummen stehen beim Release.

## Updates und Einstellungen

Bei jedem Start prüft der neue Starter den signierten Alpha-Updatefeed `channel-alpha-v2`. Neue Clientversionen werden heruntergeladen, geprüft und erst danach aktiviert. Bei einem fehlgeschlagenen Update bleibt die vorhandene Version erhalten. Die unveränderlichen Programmdateien werden vor dem Start geprüft. Gespeicherte Anmeldedaten werden bei der ersten Verwendung migriert; die Verschlüsselung bindet sie an das Windows-Benutzerkonto. FPS/VSync werden dauerhaft gespeichert; vorhandene Forge-Spieleinstellungen werden in die neue Version übernommen. Ein späterer Spielabsturz löst keinen automatischen Versionswechsel aus.

Der Installer selbst startet das Spiel nicht automatisch. Die Deinstallation entfernt Startanwendung und Verknüpfungen; heruntergeladene Spielkopien und Einstellungen unter `%LOCALAPPDATA%\PirateGalaxyForge` bleiben erhalten.

## Freiwillige Aktivitätszählung

Die Zählung ist standardmäßig **aus**. Bei Zustimmung werden während des Spiels alle zwei Minuten eine zufällige Installationskennung und die Version per HTTPS gesendet. Der Dienst speichert eine HMAC-Kennung, Version und letzte Aktivität, keine Spielkonten, Namen, Hardware- oder Standortdaten. IP-Adressen werden beim Zähler nicht protokolliert. Einträge verfallen nach sieben Tagen. Die Teilnahme lässt sich jederzeit über **Pirate Galaxy Forge - Einstellungen** ausschalten. Gezählt werden teilnehmende Installationen, nicht alle Spieler.

## Freiwillige Fehlerberichte

Nach einem unerwarteten Spielende kann ein Bericht mit Fehlercode, Version, Build-Prüfsumme und eigener Beschreibung gesendet werden. Aus einem passenden lokalen Speicherabbild können zusätzlich Bibliotheks- und Buildkennungen sowie relative Fehler-/Aufrufstellen übernommen werden. **Erst der Klick auf „Bericht senden“ überträgt Daten an das Forge-Team.** Das Speicherabbild selbst ist separat und standardmäßig abgewählt; es kann private Speicherinhalte enthalten. Rohlogs, lokale Pfade und absolute Speicheradressen werden nicht als Metadaten mitgesendet. Serverberichte sind privat und werden nach 14 Tagen gelöscht. Lokale Diagnoseaufnahmen und der optionale native Rekorder sind in `DIAGNOSE.txt` erklärt.

## Alpha-Einschränkungen

Native Abstürze sowie einzelne Grafik- und Performancefehler sind noch möglich. Weiße Mantissen, sporadisches Schattenflackern, Ruckler unter Last und weitere UI-/Musikfälle werden weiter bearbeitet. 240 FPS in jeder Situation und die Erkennung durch Discord/Medal sind nicht zugesichert. Bekannte Probleme stehen in den Releasehinweisen.

## Quellen und Bibliotheken

Der Forge-Entwicklungscode liegt in einem privaten Repository. Die passenden Bibliotheksquellen und vollständigen Lizenzhinweise stehen als separate Archive beim jeweiligen Release bereit. Java wird direkt vom offiziellen Azul-CDN geladen und nicht hier weiterverteilt. Unveränderte Originalspiel-JARs, Ressourcen, Benutzerprofile oder Zugangsdaten sind keine Releaseassets.

Pirate Galaxy Forge ist kein offizielles Produkt von Splitscreen Studios.
