# Pirate Galaxy Forge

Inoffizieller 64-Bit-Communityclient für Pirate Galaxy. Aktuelle öffentliche Alpha-Vorschau: **0.1.0-alpha.15**.

**[Installer herunterladen](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases/download/v0.1.0-alpha.15/PirateGalaxyForge-0.1.0-alpha.15-Setup.exe)** · [Releasehinweise und Prüfsummen](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases/tag/v0.1.0-alpha.15)

**Neu in Alpha 15:** Weniger kurzlebige Speicherobjekte bei Antriebsspuren, Kamera- und Matrixabfragen, Szenenknoten und Zielauswahl sowie weniger unnötige UI-Arbeit. Die Diagnose zeigt maximale Bildzeit und GC-Aktivität im aktuellen Zeitfenster. Textumbruch, Bauplankatalog, Staffel-Effekte und alle Einstellungsoptionen bleiben erhalten. „Forge Komfort öffnen“, „Einzeln einstellen …“ und Quantensprung-Reichweite sind im endgültigen Performance-Stand gemeinsam geprüft.

**Bestehende Nutzer ab Starterrevision 2 erhalten das Update beim nächsten Forge-Start automatisch.** Starterrevision 5 bleibt gegenüber Alpha 14 unverändert. Nur bei einem älteren Starter ist einmal das aktuelle Setup nötig. Der alte Kanal bleibt auf Alpha 5; der aktuelle Starter nutzt `channel-alpha-v2`. Der Starter bietet weiterhin Forge (64 Bit) und den installierten offiziellen Client (32 Bit) an.

Anmeldedaten werden lokal mit Windows DPAPI geschützt; Forge-Einstellungen und der feste Prozesspfad für die Windows-Lautstärke bleiben über Updates erhalten. Bei geöffneter Bauplanansicht lädt Forge den eigenen Profilstand über die vorhandene Spielabfrage alle fünf Sekunden nach Abschluss der letzten Anfrage neu. Unveränderte Daten behalten die aktuelle Listenansicht. Außerhalb des Bauplan-Tabs läuft diese automatische Aktualisierung nicht.

Neuinstallation, Update von Alpha 14 mit synthetischen Profilen, Rollback und 17 Installerprüfungen sind bestanden. Der neue Stand wurde auf einer frisch installierten öffentlichen Alpha 14 aufgebaut und gegen alle 8.177 vorhandenen Klassen abgeglichen. 3.240 Funktionstests, 1.068 UI-Prüfungen und zusätzlich 236 Prüfungen je Version für Komfort, Staffel/Kryonit, Bedienung, Zieleliste und Quantensprungring bestehen. Die UI- und Performance-Prüfungen wurden mit den installierten Release-Dateien wiederholt; öffentliche Downloads und der signierte Updateweg sind geprüft. Zwei native Helfer kommen hinzu, die bisherigen Bibliotheken, Java-Laufzeit, Heap-Grenzen und der Garbage Collector bleiben unverändert. Zusätzliche Allokationszähler und ausführliche GC-Protokolle sind abgeschaltet. Orbit-Tests und die korrigierte Text-/Quantensprung-Anzeige wurden im Testclient bestätigt; ein Leistungsnachweis für große Gefechte steht aus. **Die Veröffentlichung bleibt eine experimentelle Alpha.**

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
