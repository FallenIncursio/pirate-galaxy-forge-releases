# Core und Enhanced 0.2.0-alpha.3 — Release- und Prüfstand

**Zur Veröffentlichung freigegeben.** Core und Enhanced verwenden Starterrevision 12.
Sequenzen: Core 3, Enhanced 84. Die veröffentlichten Dateien entsprechen den geprüften
lokalen Kandidaten. Beide Updatekanäle werden erst nach erneutem öffentlichem Download
und Hash-/Signaturprüfung aktiviert. Frühere Pakete bleiben unverändert.

## Abnahme und Belege

- Alpha.2-Upgrades und Reparaturen: 56 Prüfungen; Alpha-73-Übernahme: 53 Prüfungen.
- Installeroberfläche: 24 Prüfungen; Start/Grafik/Diagnose: 29 je Edition;
  editionsgebundener Updater: 32 je Edition; Starterupgrade von Revision 11 auf 12.
- Sicherheitsprüfungen: 160; Laufzeit: 46; Transport: 58; Fehlerberichte: 108.
- 31 Java-/native Testsuiten einschließlich D3D9- und D3D11-Oberflächen.
- Enhanced alpha.3 mit D3D11 in der Sandbox gestartet; verbundene Spielsitzung im
  Orbit beobachtet. Der Nutzer bestätigt „klappt“. Das ist keine vollständige
  Abnahme sämtlicher Funktionen oder Rechnerkonfigurationen.
- Binärquellenstand: `2336323423d0454eb42187af53050d9558945dea`.
  Nachfolgende Dokumentationsänderungen verändern die getesteten Binärdateien nicht.

## Gemeinsame Änderungen

- Der Starter erfasst stdout und stderr parallel und begrenzt jedes lokale Ende
  auf 32.768 Zeichen. Die letzten 20 eigenen Startsitzungen bleiben lokal erhalten.
  Berichte enthalten Edition, Version, Windows-Version, Starterrevision, Startphase,
  Renderer, GPU/Treiberversion, Transportstatus und Java-Fehlerklasse/Methodennamen.
  Fehlermeldungstexte, Kontodaten, Dateipfade und rohe Konsolenausgaben werden nicht
  automatisch in den Versandbericht übernommen. Versand bleibt ausdrücklich freiwillig.
  Das bestehende Schema 2 des privaten Berichtsdienstes bleibt kompatibel.
- Neue Grafikauswahl **Automatisch (empfohlen)**. D3D11 wird in einem eigenen,
  zeitlich begrenzten Prozess auf Geräteerzeugung geprüft. Fehlender Support führt
  zu D3D9; ein erkannter D3D11-Startfehler erlaubt genau einen D3D9-Versuch.
  Ein allgemeiner Exitcode 1 löst keinen blinden Grafikwechsel aus. Explizite alte
  D3D9-/D3D11-Einstellungen bleiben erhalten.
- Erst nach drei abgeschlossenen Render-Schleifendurchläufen bestätigt das Spiel
  seinen Grafikstart mit einem zufälligen Token. Eine funktionierende Grafikauswahl
  wird für Version und Adapter/Treiber gemerkt. Das bestätigt weder Login noch
  Serververbindung und ist keine Zusage für eine fehlerfreie Spielsitzung.
- **Installation reparieren** in den Startereinstellungen, im Startmenü und nach
  Startfehlern. Eine frische geprüfte Kopie ersetzt dieselbe Version, übernimmt das
  zuletzt aktive Rendererprofil und lässt externe Einstellungen, Audio und geschützte
  Anmeldedaten erhalten. Die Versionssequenz wird nicht abgesenkt. Unterbrechungen
  zwischen den Verzeichnisumbenennungen werden beim nächsten Start wiederhergestellt.
  Alte Reparaturkopien bleiben lokal; keine rekursive Löschung von Nutzerdaten.
- Verifizierte Updatepakete werden für Reparaturen zwischengespeichert. Beschädigte
  Java-Archive werden beiseitegelegt und neu geladen. Hash-, Signatur-, Pfad- und
  Editionsprüfungen gelten weiterhin. Reparaturen benötigen ausreichend freien Platz
  für eine zusätzliche Kopie.
- Setup mit normalem Standardpfad und optionaler erweiterter Ordnerwahl, Start der
  Einrichtung auf der Abschlussseite und verständlicher .NET-Voraussetzungsprüfung.
  Schreibrechte und freier Platz werden vor der Vorbereitung geprüft. Fehlerdialoge
  bieten Wiederholen, Reparieren, Grafik-Einstellungen und Bericht an.

## Grenzen und Sandbox-Abnahme

Die native Grafikbasis bleibt bytegleich zu alpha.2. D3D11, Treiberwechsel, D3D9,
Neuinstallation und Reparatur sind getrennt zu beurteilen. Die bisherigen Meldungen
ohne Java-Ausgabe beweisen keine gemeinsame Absturzursache; alpha.3 verbessert auch
die Diagnose bislang ungeklärter Fälle. Keine allgemeine Absturzfreiheit behaupten.

Die automatisierten Prüfbelege sind an die exakten Kandidatenhashes gebunden.
Weitere Ingame-Abnahme für Core alpha.3, längere Spielsitzungen, Calon und wiederholte
Planetenwechsel sowie Rückmeldungen der bislang betroffenen Rechner bleiben offen.
Wine und weitere GPU-/Treiberkombinationen sind separat zu prüfen. Die Installer
haben keine Windows-Authenticode-Signatur; Updatepakete verwenden die vorhandene
RSA-Releaseidentität. Es wurde kein neuer Signierschlüssel erzeugt.

Bei fehlendem .NET 4.8 öffnet das Setup auf Wunsch die offizielle Microsoft-Seite.
Java und die geprüfte Spielbasis lädt der Starter selbst. Die Hinweise „lokaler
Kandidat“ in den unveränderten Paketbeilagen beschreiben den damaligen Teststand;
maßgeblich für den Veröffentlichungsstatus sind diese Release-Seiten und Kanäle.

## Technische Referenzen

- [Microsoft: D3D11CreateDevice](https://learn.microsoft.com/en-us/windows/win32/api/d3d11/nf-d3d11-d3d11createdevice)
- [Microsoft: .NET-Releasewert prüfen](https://learn.microsoft.com/en-us/dotnet/framework/install/how-to-determine-which-versions-are-installed)
- [Microsoft: .NET Framework 4.8](https://dotnet.microsoft.com/en-us/download/dotnet-framework/net48)

Kumulative Funktionen und 32-Bit-Vergleich: [FEATURES.md](FEATURES.md).
Vorherige native Korrekturen: [Enhanced alpha.2](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases/tag/v0.2.0-alpha.2).
