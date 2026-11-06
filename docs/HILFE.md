# Installation, Updates und Hilfe

[Zurück zur Übersicht](../README.md)

## Originalinstallation finden

Forge sucht beim ersten Start nach vorhandenen Pirate-Galaxy-Installationen. Auch ein übergeordneter Launcher-Ordner oder dessen Ordner `gamedata` kann ausgewählt werden.

Typische Speicherorte sind:

- `%APPDATA%\Splitscreen Studios\Game Launcher\gamedata\Pirate Galaxy`
- `%APPDATA%\Splitscreen Studios\Pirate Galaxy\gamedata\Pirate Galaxy`

Der Spielordner muss `Basic.jar`, `PirateGalaxy.jar` und `core` enthalten. Die unterstützte Version wird beim Einrichten geprüft. Die Auswahl lässt sich später über **Pirate Galaxy Forge - Einstellungen** ändern.

Forge lädt Java direkt vom offiziellen Azul-CDN und richtet es lokal ein. Eine separate Java-Installation ist nicht nötig. Der Starter bietet außerdem die installierte offizielle 32-Bit-Version über deren eigenen Launcher an.

## Aktualisieren

Beim Start prüft Forge den signierten Updatekanal. Neue Versionen werden vollständig heruntergeladen und geprüft, bevor sie aktiviert werden. Bei einem fehlgeschlagenen Update bleibt die vorhandene Version erhalten. Ein späterer Spielabsturz löst keinen automatischen Versionswechsel aus.

Wenn ein alter Starter bereits bei der Updateprüfung scheitert, das [aktuelle Setup von der Projektübersicht](../README.md) im Browser laden, Forge regulär beenden und das Setup über die vorhandene Installation ausführen. Spieleinstellungen und Daten bleiben erhalten. Das gilt auch für sehr alte Starter, die sich noch nicht selbst aktualisieren können.

Seit Alpha 18 verwendet der Starter bei bestimmten .NET-Verbindungsfehlern einen zusätzlichen Windows-Downloadweg. Ein erfolgreicher Browserdownload allein schließt eine programmspezifische Blockade nicht aus.

## Startfehler und Abstürze

Für eine Fehlermeldung sind diese Angaben hilfreich:

- Forge-Version und genauer Wortlaut beziehungsweise Fehlercode.
- Zeitpunkt: Updateprüfung, Download, Login oder Laden eines Planeten.
- Bei Grafikproblemen: Planet, Grafikkarte und Grafikqualität.
- Falls vorhanden: die konkrete Meldung der Sicherheitssoftware.

Nach einem unerwarteten Spielende kann der Forge-Absturzdialog einen freiwilligen Bericht senden. Beschreibe möglichst kurz, was unmittelbar davor passiert ist. Ein Speicherabbild wird nur nach gesonderter Zustimmung angehängt; [Details zu den übertragenen Daten](DATENSCHUTZ.md).

Das Setup ist derzeit nicht Authenticode-signiert. SHA256-Prüfsummen stehen beim jeweiligen Release. Eine Antivirus-Meldung sollte anhand ihres konkreten Fundes geprüft werden; die Schutzsoftware muss für Forge nicht pauschal deaktiviert werden.

## Einstellungen und Deinstallation

Forge-Spieldaten und Einstellungen liegen standardmäßig unter `%LOCALAPPDATA%\PirateGalaxyForge`. Gespeicherte Anmeldedaten sind an das Windows-Benutzerkonto gebunden. Der feste Spielprozesspfad hält den Windows-Mixerpegel über Updates hinweg stabil.

Die Deinstallation entfernt die Startanwendung und Verknüpfungen. Heruntergeladene Spielkopien und Einstellungen bleiben erhalten.

## Discord und Medal

Den Discord-Spielstatus stellst du unter **Komfort → Anzeige → Discord und Aufnahme** ein. Discord muss geöffnet sein und die Anzeige deiner Aktivitäten erlauben. Für das Overlay den laufenden Client unter **Discord → Registrierte Spiele** hinzufügen und das Overlay einschalten. Veraltete Forge-Einträge gegebenenfalls vorher entfernen.

Medal kann den 64-Bit-Client aufnehmen. Wird er nicht erkannt, das laufende Spiel über **Add New Game** hinzufügen. Die offizielle Kategorie „Pirate Galaxy“ wird noch nicht zuverlässig zugeordnet; „Requested“ kann trotz funktionierender Aufnahme stehen bleiben. Clips und Aufnahmeoptionen verwaltest du in Medal.

## Grenzen der Alpha

Einzelne Grafik-, Musik- und Performanceprobleme sowie native Abstürze werden weiter untersucht. Hohe FPS unter jeder Last und die Erkennung durch Discord oder Medal sind nicht zugesichert. Den Umfang einzelner Korrekturen beschreiben die [Releasehinweise](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases).
