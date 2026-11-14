# Installation, Updates und Profile

Core und Enhanced 0.2.0-alpha.3 benötigen Windows 10/11 x64 und .NET Framework 4.8.
Die passende Java-27-Laufzeit lädt der Starter bei Bedarf selbst.

## Installieren

1. Den Windows-Installer der gewünschten Edition von ihrer GitHub-Release-Seite laden.
2. Setup ausführen und den vorgeschlagenen Ordner verwenden. Eine abweichende
   Ordnerwahl ist optional. Core und Enhanced erhalten getrennte Installationen.
3. Auf der Abschlussseite „jetzt einrichten und starten“ wählen. Der Starter lädt
   die geprüfte Spielbasis direkt
   von Splitscreen, die Laufzeit von Azul und das signierte Forge-Updatepaket.
4. Im Spiel anmelden. „Automatisch“ prüft D3D11 und verwendet bei fehlender
   Unterstützung D3D9. Vorhandene manuelle Grafikeinstellungen bleiben erhalten.

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

## Startprobleme und Reparatur

Die Startereinstellungen enthalten „Automatisch“, D3D11 und D3D9. Bei einem
erkannten D3D11-Startfehler versucht die automatische Auswahl einmal D3D9.
Ein allgemeiner Exitcode 1 allein löst keinen Grafikwechsel aus.

„Installation reparieren“ ist in den Startereinstellungen, im Startmenü und im
Fehlerdialog erreichbar. Die aktuelle signierte Version wird neu vorbereitet;
Profile, eigene Sounds und geschützte Anmeldedaten bleiben erhalten. Ein Abbruch
während des Austauschs wird beim nächsten Start berücksichtigt. Zusätzlicher
freier Speicher für die Reparaturkopie wird benötigt.

Fehlerberichte können nach bewusster Bestätigung gesendet werden. Sie enthalten
auch Startphase, Grafikdaten und erkennbare Java-Fehlerklassen. Rohe lokale
Konsolenausgaben und private Fehlermeldungstexte werden nicht automatisch versandt.

## Prüfstand und Grenzen

Beide Installer wurden mit Upgrade, Profilübernahme, Reparatur, Abbruch und Rollback
in Sandboxie geprüft. Enhanced alpha.3 wurde mit D3D11 bis zur verbundenen
Spielsitzung gestartet und vom Nutzer bestätigt. Core alpha.3-Ingame-Abnahme,
längere D3D9-/D3D11-Sitzungen, weitere Rechnerkonfigurationen und Wine bleiben offen.

Bei Sandboxie kurze Boxwurzeln verwenden. Zu lange umgeleitete Socket-Pfade können
beim Java-Verbindungsaufbau einen irreführenden Firewall-Dialog auslösen.

Der Installer hat keine Windows-Authenticode-Signatur; Update-Manifeste sind mit
der bestehenden Forge-RSA-Identität signiert. Bibliotheksquellen, Lizenzhinweise und
SHA256-Prüfsummen stehen bei beiden Releases. 240 FPS ist ein wählbares Limit,
keine Leistungszusage. Forge bleibt eine inoffizielle experimentelle Alpha.
