# Release-Prüfstand: Enhanced 0.2.0-alpha.21

21.11.2026. Der Nutzer bestätigt den Lesbarkeitsstand mit „okey, funktioniert“
und beauftragt Veröffentlichung, Quell-Push, Updatekanal und Downloadprüfung.
Die folgenden Vorbereitungs- und Startbelege bleiben an ihre geprüften Bytes gebunden.
Der Lesbarkeitsstand wurde vor der Freigabe auf Nutzerauftrag mit D3D11 gestartet;
Startbeleg und Grenzen stehen unten.
Enhanced alpha.21 / reservierte Sequenz **102**; Spielversion **1002133**, Starter **17**.
Core bleibt **alpha.17 / Sequenz 16**. Keine neuen nativen Dateien.

## Signierte Releasepakete geprüft

Der finale vollständige Prüflauf unter `C:\PGF21PT` bindet auch den aktualisierten
Dokumentationsgenerator: 62 Editionsgates, 18 Negativkontrollen, 100 Gravitonen-
Prüfungen und je 2854 native Enhanced-UI-Prüfungen auf D3D9/D3D11 bestanden.
**59** Neuinstallations-/Alpha-73-Prüfungen,
**64** Prüfungen für das Upgrade von alpha.20, Reparatur,
Rollback und Profilübernahme sowie **24** Installer-UI-Prüfungen bestanden.
Die Tests verwenden künstliche Profile in separaten Sandboxie-Boxen. Core wurde
mit bereits veröffentlichten alpha.17-Dateien als unveränderter Vergleich geprüft.
Es wird kein neues Core-Paket veröffentlicht.

Der erste Installerlauf wurde bei der Core-alpha.17-Reparatur durch einen
verweigerten Verzeichniswechsel der entpackten Laufzeit beendet (IOException,
0x80070005). Dieser fehlgeschlagene Lauf bleibt erhalten. Die oben genannten
Ergebnisse stammen aus einer vollständigen frischen Sandbox mit unveränderten
Paketen. Der sperrende Prozess ist nicht ermittelt; alpha.21 enthält keine
allgemeine Korrektur dieser Windows-Dateisperren.

Signaturen, vollständiges Paketinventar und Bibliotheksquellen sind geprüft.
Klassen und Ressourcen in den normalisierten Update-JARs stimmen bytegenau mit
dem vom Nutzer bestätigten Sandbox-Build überein; nur die ZIP-Verpackung wird
für reproduzierbare Patches normalisiert. Private Profile, Rohlogs und Spielcaches
sind ausgeschlossen. Die öffentliche Downloadprüfung folgt nach dem Upload.
Beleg: `distribution/tests/editions-0.2-alpha.21-release-candidates.json`.

## Inhalt

Gravitonen-Dropstatus im ursprünglichen sechsten Slot, Originalsymbol und voller
Name im Tooltip, einzeiliger geschätzter Countdown und unbekannter Zustand.
Weiße, fette Schrift auf deckendem dunklem Hintergrund; zentriert und nach
echter Schriftbreite eingepasst. Aufgerundete Stunden (`~6h`) bzw. unter einer
Stunde Minuten (`~45m`); vollständige Stunden/Minuten im Tooltip. Timeranker,
Beobachtung und Serverabfragen bleiben unverändert.
Anzeige-Schalter mit Übernehmen/Verwerfen, isolierte vierteilige Vorschau und
begrenzte Gravitonen-Diagnose im bereinigten lokalen Bericht. Keine neuen RPCs.
Kurzzeitige Dateisperren werden nur im Enhanced-Einstellungsspeicher begrenzt
wiederholt; atomare Speicherung und sichtbare Fehler bei dauerhaftem Scheitern
bleiben erhalten. [Bedienung und Datenquellen](ALPHA21-GRAVITON-DROP.md).

## Abgeschlossene automatische Prüfungen

- **62 Editionsgates**, **18 Negativkontrollen** bestanden.
- **100 Gravitonen-/Speicher-/Diagnoseprüfungen**: Zeitgrenzen, Neustart, Uhrsprung,
  ungültige Werte, getrennte Pilot-/Serveridentität, späte und doppelte
  Einsammelereignisse, fremde Kollektoren, fehlende Felder und begrenzter Export.
- Je **2854 native Enhanced-UI-Checks auf D3D9 und D3D11**. Neue Anzeige bei
  100/115/150/200 %, fünf Originalsymbole, echtes Mouse-Hover, passiver Fokus,
  leeres Inventar, Ein-/Ausklappen, HUD-Neuaufbau und Originalslot-Vorrang geprüft.
  Countdown-Grenzen, vollständige Textausdehnung, Zentrierung sowie dunkle und
  helle Pixel im GPU-Bild geprüft; reale 26×26-Slots statt nur großer Vorschau.
- Vorschau verändert weder Einstellungen noch echte Messung/Diagnose.
  Ein-/Ausschalten, Übernehmen, Verwerfen und Wiederöffnen über echte Mausklicks.
- Vorhandene Errungenschaften-, Scanner-, Staffel-, OTB- und weitere Regressionen
  bestanden. Neue Hooks bleiben auf drei Methoden einer Enhanced-Klasse begrenzt.
- Core-Spiel-JAR und **135 gemeinsame Klassen** bytegleich; native Quellen und
  Bibliotheken unverändert. Core braucht keine neue Klasse oder Ressource.

Die anfänglichen UI-Läufe zeigten kurzzeitige Windows-Zugriffssperren auf den
atomaren Austausch der Einstellungsdatei. Der Enhanced-Adapter wiederholt nur
AccessDenied-Fehler mit 10/20/40 ms Pause; zusätzliche Tests prüfen permanenten
Fehler, andere IO-Fehler und Unterbrechung. Die finalen nativen Läufe sind bestanden.
Schnelle synthetische Klicks enthalten einen kurzen Idle-Schritt; kein Testfehler
wird ignoriert oder nachträglich als bestanden umgedeutet.

Drei vorherige Lesbarkeits-Prüfläufe (`D:\PGF21\readability-tests`, `-r2`
und `C:\PGF21T`) scheiterten am atomaren Austausch isolierter Einstellungen
(AccessDeniedException in CoreStore/HudScale bzw. CoreSettingsUi/SocialPresence).
Diese Läufe bleiben als fehlgeschlagen dokumentiert. Die UI-Prüfprogramme
geben vor einer getrennten synthetischen Übernehmen-Aktion jetzt 100 ms
Leerlaufzeit; keine Wiederholung fehlgeschlagener Aktionen und keine entfernte
Speicherprüfung. Die oben genannten Ergebnisse stammen aus dem vollständigen
frischen Lauf unter `C:\PGF21T2` mit unveränderten Spielbytes. Der sperrende
Prozess ist nicht ermittelt; dies belegt keine allgemeine Behebung von Windows-
Dateisperren. CoreStore und der produktive Einstellungsablauf bleiben unverändert.

## Dateien und Bindung

Build: `D:\PGF21\readability-build`; Testbelege: `C:\PGF21T2`.
Privates Paket: `D:\PGF21\readability-packages\Pirate-Galaxy-Forge-Enhanced-0.2.0-alpha.21`.
Quell-Ausgangspunkt: `6b3fe5102ee3470f93fa2f956ec5d0e068091286`; Änderungen noch
nicht committet. Quelleninventar, einzelne Eingabehashes und der Paketbeleg binden
stattdessen den tatsächlichen Arbeitsstand. Keine alten Belege auf neue Bytes übertragen.

Enhanced-Spiel-JAR: `594fe74e0b35fe705b16277932b78fe316e10c3728b5f62fbddb6e419feef14b`.
Core-Spiel-JAR: `918093c4e935e8f8af3eab689b956736843c73573332a574e82752eda0612310`.
Beleg nach Paketprüfung: `distribution/tests/graviton-drop-alpha21-readability-readiness.json`.
Private Manifeste verbieten Veröffentlichung und Updates. Keine Profile oder
Anmeldedaten wurden in die Pakete übernommen. Öffentliche Kanäle bleiben unberührt.

## Historischer Sandbox-Start vor dem Lesbarkeitsfix

Auf ausdrücklichen Startauftrag läuft Enhanced alpha.21 mit D3D11 in
`PGForgeAlpha21Graviton` / `C:\PGF21A`, PID 16528. Startkopie:
`C:\PGF21V\E\versions\0.2.0-alpha.21`. Vorherige alpha.20-Sitzung regulär
beendet; deren zusammengeführten Zustand vor und nach Schließen gesichert.
Drei Profile, 19 Zustandsdateien, versteckte Identität und eine geschützte
Anmeldung übernommen. Echter Anmeldeleser und 16 Selectorzyklen bestanden.
Windows-Mixer 8 %, nicht stumm; 51 geladene Dateihashes, D3D11 und Sandboxie
geprüft. Angemeldeter Orbit und Serververbindungen beobachtet. Spiel-Startlog
ohne ERROR/FATAL, Verify- oder Linkfehler; generische MyGUI-Widget-Lookups
im Beleg dokumentiert. Normale Installation und ursprüngliche Profile erhalten.
Beleg: `distribution/tests/graviton-drop-alpha21-launch.json`.
Dieser Beleg gilt ausschließlich für die vorherigen Spielbytes. Der neue
Lesbarkeitsstand wurde noch nicht als Nutzerclient gestartet; seine nativen
UI-Prüfungen liefen in isolierten Prozessen mit Beispieldaten.

## Sandbox-Start des Lesbarkeitsstands

PID 34040, Box `PGForgeAlpha21GravitonReadable`, Container `C:\PGF21B`,
Startkopie `C:\PGF21W\E\versions\0.2.0-alpha.21`. Vorherigen PID 16528
regulär beendet (Exit 0), aktuellen zusammengeführten Zustand vor und nach
Schließen gesichert. Drei Profile, 19 Zustandsdateien samt Geräteidentität und
eine geschützte Anmeldung frisch übernommen. Echten Anmeldeleser, 16 Selector-
Zyklen, 55 geladene Dateihashes, D3D11 und Sandboxie geprüft. Windows-Mixer
8 %, nicht stumm. Serververbindung und angemeldete Planetenoberfläche sichtbar.
Spiel-Startlog ohne ERROR/FATAL-, Verify- oder Linkfehler; 20 generische MyGUI-
Widget-Lookups dokumentiert. Originalinstallation und gesicherte Quellen erhalten.
Beleg: `distribution/tests/graviton-drop-alpha21-readability-launch.json`.
Client bleibt für die Gravitonen-Abnahme offen. Keine Veröffentlichung.

## Noch offen

Live-Sichtung und eigenes Einsammeln eines echten Gravitons, serverseitige
Zeitbasis und Sechs-Stunden-Auslöser sind **nicht bestätigt**. Der Timer ist eine
mit `~` markierte lokale Schätzung ab Einsammeln. Ein sichtbarer Drop bestätigt
keinen persönlichen Besitz. Andere Sitzungen können die Schätzung überholen.
Die native UI-Abnahme verwendet echte Widgets mit synthetischen Daten; sie ist
kein Server-/Spieltest. Wine, macOS und weitere GPU-/Treiberkombinationen ungetestet.
Die gestartete Testsitzung bleibt geöffnet. Die Veröffentlichung ist für Enhanced
freigegeben; Core bleibt unverändert. Installations- und öffentliche Downloadprüfungen
werden gesondert dokumentiert.
