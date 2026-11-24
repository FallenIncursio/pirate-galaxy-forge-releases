# Installation und Updates

[Übersicht und Download](../../README.md) · [Diagnose](DIAGNOSE.md) · [Bedienung](HILFE.md)

**Pirate Galaxy Forge Enhanced 0.2.0-alpha.35 · Spielversion 1002133**

## Installieren

Voraussetzungen: Windows 10/11 x64, .NET Framework 4.8 und Internetzugang.
Die passende Java-Laufzeit lädt der Starter selbst.

1. Den [Windows-Installer](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases/download/v0.2.0-alpha.35/PirateGalaxyForge-0.2.0-alpha.35-Setup.exe) herunterladen und ausführen.
2. Forge über die angelegte Verknüpfung starten. Der vorgeschlagene Installationsort genügt.
3. Der Starter lädt die geprüfte Spielbasis, Laufzeit und Forge-Dateien. Anschließend im Spiel anmelden.

D3D11 ist Standard; D3D9 bleibt in den Startereinstellungen auswählbar. Die automatische
Auswahl kann bei einem erkannten D3D11-Startfehler einmal D3D9 versuchen. Vorhandene
manuelle Einstellungen werden erhalten. Die Originalinstallation wird nicht überschrieben.

## Vorhandene Installation aktualisieren

Forge prüft beim Start den Updatekanal seiner Edition. Download, RSA-Signatur,
Edition, Produkt, Sequenz, Dateigröße und Prüfsummen werden vor der Aktivierung geprüft.
Passende vorhandene Laufzeit- und Ressourcendateien können geprüft übernommen werden.
Der Starter zeigt den aktuellen Schritt, Datenmenge und Geschwindigkeit.

Bei einer vorhandenen, vollständig geprüften und kompatiblen Installation ist
**Update später – vorhandene Version starten** möglich. Eine alte oder beschädigte
Spielbasis wird dadurch nicht freigegeben. Falls ein alter Starter nicht aktualisiert,
das aktuelle Setup über dieselbe Edition installieren.

## Profile und Editionen

Der bisherige Forge wird als Enhanced fortgeführt. Innerhalb der Edition bleiben
Profile, Qualität, Komfort, Rendererwahl, eigene Sounds und bewusst gespeicherte
geschützte Anmeldungen erhalten. Maßgeblich ist das zuletzt verwendete Rendererprofil.
Gelöschte Einstellungen und Anmeldungen werden nicht aus älteren Kopien zurückgeholt.

| Edition | Lokaler Datenordner | Starter |
| --- | --- | --- |
| Core | `%LOCALAPPDATA%\PirateGalaxyForgeCore` | `PirateGalaxyForgeCore.exe` |
| Enhanced | `%LOCALAPPDATA%\PirateGalaxyForge` | `PirateGalaxyForge.exe` |

Core und Enhanced können nebeneinander installiert bleiben. Core übernimmt keine
Enhanced-Profile oder Anmeldungen automatisch. Der feste Spielprozesspfad erhält
die Windows-Mixerzuordnung über Updates hinweg.

## Reparieren oder deinstallieren

**Installation reparieren** ist über Startereinstellungen, Startmenü oder Fehlerdialog
erreichbar. Die signierte aktuelle Version wird neu vorbereitet; Profile und geschützte
Anmeldungen bleiben erhalten. Für die Vorbereitung wird zusätzlicher freier Speicher benötigt.

Bei einem unterbrochenen Update zunächst **Update erneut versuchen** oder
**Diagnose öffnen** verwenden. Cachedateien und Profile müssen nicht auf Verdacht gelöscht werden.
Ein unerwartetes Spielende ist kein automatischer Versionswechsel.

Die Deinstallation entfernt Starter und Verknüpfungen; lokale Spielkopien und Profile
bleiben erhalten. Ein geprüfter Rollback bewahrt den jüngsten Profilstand und die
höchste bereits gesehene Updatesequenz.

## Prüfsummen und Plattformen

[Release und Prüfsummen](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases/tag/v0.2.0-alpha.35) · [Bibliotheksquellen](../sources/QUELLEN.md)

Update-Manifeste sind RSA-signiert. Der Windows-Installer besitzt keine
Authenticode-Signatur. Eine Sicherheitssoftwaremeldung anhand des konkreten Fundes
prüfen; die Schutzsoftware muss nicht pauschal deaktiviert werden.

Aktuelle geprüfte Ausgaben sind Windows-Alphas. Historische Wine-Vorschauen gehören
zum [Archiv](../archive/README.md) und sind kein aktueller, geprüfter Installer für Linux oder macOS.
