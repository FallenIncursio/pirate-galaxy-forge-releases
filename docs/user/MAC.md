# Enhanced auf Apple-Silicon-Macs

[Übersicht](../../README.md) · [Diagnose](DIAGNOSE.md)

**[Mac-Starter herunterladen](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases/download/v0.2.0-alpha.42/PirateGalaxyForge-Enhanced-0.2.0-alpha.42-macOS.zip)** · [Kurzanleitung als HTML](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases/download/v0.2.0-alpha.42/Mac-Kurzanleitung.html)

Der Starter richtet den gemeinsamen Windows-x64-Client von Enhanced unter
CrossOver ein. Spielupdates kommen aus demselben signierten Enhanced-Kanal.
Ein eigener Mac-Spielbuild ist nicht erforderlich.

## Einrichten

1. [CrossOver](https://www.codeweavers.com/crossover) installieren und einmal
   öffnen. Es bietet eine Testphase und benötigt danach eine eigene Lizenz.
   Falls macOS Rosetta anbietet, dessen Einrichtung abschließen.
2. Das ZIP entpacken und **Forge Enhanced Mac.app** nach **Programme** ziehen.
3. Die App öffnen, CrossOver bei Bedarf auswählen und **Einrichten** drücken.
   Microsoft-Laufzeit und Shadercompiler werden geladen und geprüft.
   Etwa 15 GB freier Speicher werden benötigt.
4. **Spielen** wählen. Der Forge-Starter lädt die Spielbasis und Java-Laufzeit.
   D3D11 mit D3DMetal und der geprüfte Audiopuffer sind voreingestellt.

Die App ist noch nicht mit einer Apple Developer-ID signiert oder notarisiert.
Wenn macOS sie blockiert und du der Downloadquelle vertraust: nach dem ersten
Öffnungsversuch unter **Systemeinstellungen → Datenschutz & Sicherheit → Dennoch
öffnen** nur diese App freigeben. Globale Sicherheitseinstellungen eingeschaltet
lassen. [Apples Anleitung](https://support.apple.com/de-de/102445).

## Spielen und Updates

Forge über die Mac-App starten; sie aktiviert das Audio- und Ping-Profil.
Der Windows-Starter prüft Spielupdates automatisch. Profil und Einstellungen
bleiben erhalten. Die Mac-App selbst wird nur bei Änderungen am Startumfeld
ersetzt. **Spiel beenden** schließt gezielt ihren Client, auch wenn Wine nach dem
Schließen des Spielfensters einen Hintergrundprozess zurückbehält.

**Diagnose öffnen** zeigt die Einrichtungsprotokolle; für Spielprobleme die
Diagnose im Forge-Starter verwenden. **Reparieren** öffnet dessen Reparatur.
Eine unterbrochene Einrichtung lässt sich erneut starten.

Daten liegen unter `~/Library/Application Support/PirateGalaxyForge-Mac`.
Andere Installationen und Anmeldedaten werden nicht automatisch übernommen.
CrossOver und Spielprofile sind nicht im Mac-Download enthalten.

## Geprüfter Umfang

Apple M5, 16 GB, macOS 27.2.1, CrossOver 26.3.0: Neuinstallation, signiertes
Versionsupdate mit Testprofil-Erhalt, Anmeldung, Planetenwechsel, Ton und
Vollbild unter D3DMetal. Die passive Ping-Messung erzeugt keine zusätzlichen
Spielserver-Abfragen. Andere M-Chips, macOS-Versionen, DXMT und längere
Spielsitzungen sind noch nicht umfassend geprüft. Core bleibt hier die gemeinsame
technische Grundlage; der Mac-Starter installiert Enhanced.
