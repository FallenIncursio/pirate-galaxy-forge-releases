# Installation, Updates und Profile

Core und Enhanced 0.2.0-alpha.1 benötigen Windows 10/11 x64 und .NET Framework 4.8.
Die passende Java-27-Laufzeit lädt der Starter bei Bedarf selbst.

## Installieren

1. Den Windows-Installer der gewünschten Edition von ihrer GitHub-Release-Seite laden.
2. Setup ausführen und den Installationsordner wählen. Für Core und Enhanced
   unterschiedliche Ordner verwenden; das Setup verhindert eine Vermischung.
3. Die installierte Startanwendung öffnen. Sie lädt die geprüfte Spielbasis direkt
   von Splitscreen, die Laufzeit von Azul und das signierte Forge-Updatepaket.
4. Im Spiel anmelden. D3D11 ist der Standardrenderer; D3D9 bleibt wählbar.

Core behält die ursprüngliche Hilfe. Zusätzliche Core-Optionen stehen in der
nativen Erweiterung der Spieleinstellungen. Enhanced besitzt den Forge-Dialog.

## Bestehender Forge und Profilübernahme

Der bisherige Forge wird als **Enhanced** fortgeführt. Das Setup übernimmt den
registrierten Installationsort. Qualität, Komfort, Rendererwahl, eigene Sounds und
bewusst gespeicherte geschützte Anmeldedaten bleiben erhalten. Maßgeblich ist das
zuletzt verwendete Rendererprofil; gelöschte Einstellungen werden nicht aus älteren
Versionen zurückgeholt.

**Core** ist unabhängig und besitzt einen eigenen Updatekanal. Es übernimmt
keine Profile oder Anmeldedaten aus Enhanced automatisch. Beide Editionen können
nebeneinander installiert bleiben.

| Daten | Core | Enhanced |
|---|---|---|
| Spielkopien und Profile | `%LOCALAPPDATA%\PirateGalaxyForgeCore` | `%LOCALAPPDATA%\PirateGalaxyForge` |
| Starter | `PirateGalaxyForgeCore.exe` | `PirateGalaxyForge.exe` |

## Updates und Wiederherstellung

Der Starter prüft RSA-Signatur, Edition, Produkt, Versionssequenz, Dateigrößen und
Hashes. Ein Paket der anderen Edition wird abgewiesen. Downloads und Vorbereitung
erfolgen neben der aktiven Version; erst das vollständig geprüfte Paket wird
aktiviert. Der Wiederanlauf berücksichtigt die aktuellen Profile erneut.

Ein Rollback erhält den jüngsten Profilstand und die höchste bereits gesehene
Updatesequenz. Der feste native Prozesspfad erhält die Windows-Lautstärkezuordnung.
Deinstallation entfernt Starter und Verknüpfungen; Spielkopien und Profile bleiben
erhalten. Die ursprüngliche Spielinstallation wird nicht überschrieben.

## Prüfstand und Grenzen

Beide Editionen wurden über ihre Installer mit D3D11 in Sandboxie gestartet;
Kontobildschirm und Serververbindung wurden geprüft und der Nutzer bestätigte die
Funktion. Installer-, Profil-, Wiederanlauf-, Rollback- und Editionstests sind
bestanden. Native UI-Probes decken zusätzlich D3D9 ab. Vollständige D3D9-
Spielsitzungen, Wine und quantitative Langzeitmessungen sind nicht abgenommen.

Bei Sandboxie kurze Boxwurzeln verwenden. Zu lange umgeleitete Socket-Pfade können
beim Java-Verbindungsaufbau einen irreführenden Firewall-Dialog auslösen.

Der Installer hat keine Windows-Authenticode-Signatur; Update-Manifeste sind mit
der bestehenden Forge-RSA-Identität signiert. Bibliotheksquellen, Lizenzhinweise und
SHA256-Prüfsummen stehen bei beiden Releases. 240 FPS ist ein wählbares Limit,
keine Leistungszusage. Forge bleibt eine inoffizielle experimentelle Alpha.
