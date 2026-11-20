# Installation, Updates und Profile

Core und Enhanced 0.2.0-alpha.14 benötigen Windows 10/11 x64 und .NET Framework 4.8.
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

Ab alpha.13 sind neue Updatepakete komprimiert. Passende Java-Dateien und bereits
geladene Spielressourcen werden geprüft übernommen. Der Starter zeigt den aktuellen
Schritt, die übertragene Datenmenge und die Geschwindigkeit. Unterstützt die
Downloadquelle eine sichere Fortsetzung, können bereits geladene Teile weitergenutzt
werden. Für die erste Einrichtung können zusätzliche Downloads erforderlich sein.

Bei vorhandener Installation lässt sich ein Update vor der Aktivierung über
„Update später – vorhandene Version starten“ verschieben. Der bisherige Client
wird vor dem Start weiterhin geprüft. Bei Erstinstallation und Reparatur steht
diese Möglichkeit nicht zur Verfügung.

Ein Rollback erhält den jüngsten Profilstand und die höchste bereits gesehene
Updatesequenz. Der feste native Prozesspfad erhält die Windows-Lautstärkezuordnung.
Deinstallation entfernt Starter und Verknüpfungen; Spielkopien und Profile bleiben
erhalten. Die ursprüngliche Spielinstallation wird nicht überschrieben.

## Ladebildschirm vor der Anmeldung

Ab alpha.14 bietet der Starter nach 45 Sekunden ohne Ladefortschritt ein eigenes
Hilfefenster. Bei einem langsamen Start „Weiter warten“ wählen. Für die Fehlersuche
lässt sich eine begrenzte lokale Diagnose als ZIP speichern; ein Fehlerbericht
wird nur nach bewusster Bestätigung versandt. „Neustart“ beziehungsweise
„Reparieren und neu starten“ beendet nur den zugehörigen Spielprozess. Die
Reparatur legt heruntergeladene Ressourcen beiseite und lädt sie bei Bedarf neu;
Profile, Einstellungen und geschützte Anmeldedaten bleiben erhalten.

Das Spiel über den Forge-Starter öffnen, damit diese Hilfe verfügbar ist.

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
auch Startphase, Grafikdaten und getrennte Java-Fehlerereignisse. Passende vorhandene
native Fehlerdateien liefern begrenzte Metadaten wie Fehlercode und Modul. Rohe
Konsolenausgaben, JVM-Fehlerdateien und Speicherabbilder werden nicht automatisch
versandt. Ein Java-Ereignis allein belegt keine native Absturzursache.

## Prüfstand und Grenzen

Die Abnahme jeder Ausgabe ist an deren signierte Paketbytes gebunden. Für alpha.14
bestanden Neuinstallation, Upgrade von Alpha 73 sowie Core/Enhanced alpha.13,
Profilübernahme, Reparatur, Abbruch und Rollback in Sandboxie. Maßgeblich
ist der [Release-Prüfstand](RELEASE-STATUS-0.2-alpha.14.md).
Enhanced wurde mit D3D11 im Spiel geprüft; der Nutzer meldet bisher keine Probleme.
Der konkrete native Sirius-Landeabsturz ist nicht nachweislich behoben und
kamerabhängige Helligkeitswechsel bleiben offen. OTB-Endauswertung und reale
Wiederbelebung sind weiterhin separat zu prüfen; das OTB-Widget garantiert weder
Belohnung noch Sperrfreiheit.
Weitere Rechnerkonfigurationen, längere Sitzungen und Wine bleiben gesonderte Prüfungen.
Die zuvor akzeptierten Calon-Verbesserungen aus alpha.9 bleiben enthalten;
einzelne Ruckler sind weiterhin bekannt.

Bei Sandboxie kurze Boxwurzeln verwenden. Zu lange umgeleitete Socket-Pfade können
beim Java-Verbindungsaufbau einen irreführenden Firewall-Dialog auslösen.

Der Installer hat keine Windows-Authenticode-Signatur; Update-Manifeste sind mit
der bestehenden Forge-RSA-Identität signiert. Bibliotheksquellen, Lizenzhinweise und
SHA256-Prüfsummen stehen bei beiden Releases. 240 FPS ist ein wählbares Limit,
keine Leistungszusage. Forge bleibt eine inoffizielle experimentelle Alpha.
