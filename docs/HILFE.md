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

Seit Alpha 53 versucht der Starter bei vorübergehenden Downloadfehlern zusätzlich einen alternativen GitHub-Zugriff. Die Signatur- und Prüfsummenprüfung bleibt dabei erhalten. Ein erfolgreicher Browserdownload allein schließt eine programmspezifische Blockade nicht aus.

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

## Anzeige einstellen

Öffne **Forge** über den **F-Knopf** in der oberen Menüleiste. Andere Fenster und Aktionen außerhalb bleiben bedienbar. Der F-Knopf oder das Kreuz schließt Forge.

Alle Forge-Anzeigeoptionen liegen unter **Forge → Anzeige**:

- **HUD & Grafik:** Oberflächengröße, FPS-Limit, VSync, Leistungsanzeige und Ping anzeigen.
- **Komponenten:** Slot-Timer, Quantensprung-Reichweite, Zielhaltung nach Quantensprung, Reichweiten-Markierungen und Kryonit-Drohnenwechsel.
- **Kampf & Effekte:** Staffel, Bossleisten, Reparaturfelder und Orbitalschläge. Bossleisten lassen sich auf Aus, Remnants, Königin oder Alle stellen. Die Königin benötigt keine Remnant-Jagd; eine bisher ausgeschaltete Bossanzeige bleibt ausgeschaltet.
- **Widgets:** Kryonit, Positionssperre, Energiekugel-Markierung und Drohnen-Levelzeit.
- **Meldungen & Discord:** Seltene Mantis, Discord-Spielstatus und Uhrzeit im Chat.

**Übernehmen** speichert alle Gruppen und bestätigt dies kurz neben den Aktionen. **Verwerfen** oder Schließen verwirft ungespeicherte Auswahlen; beim Seitenwechsel bleiben sie erhalten. VSync wird nach einem Neustart wirksam. Die ursprünglichen Spieleinstellungen enthalten weiterhin Sprache, Auflösung, Grafikqualität und Lautstärke.

Ping steht unten rechts; die optionale Leistungsanzeige erscheint links daneben. Beide lassen sich unabhängig schalten und halten Abstand zu Minimap und Komponentenleiste.

Mit **Uhrzeit im Chat** erscheinen Nachrichten mit `[HH:mm]` in deiner lokalen Zeitzone. Der Schalter gilt für Kommunikationsfenster und kleinen HUD-Chat; **Übernehmen** aktualisiert auch bereits angezeigte Zeilen.

Mit **Ziel nach Quantensprung behalten** bleibt die bisherige Auswahl nach einem erkannten Sprung erhalten, solange die Einheit weiterhin vorhanden und auswählbar ist. Die Option ist standardmäßig an; bewusste Zielwechsel und Abwahl haben Vorrang.

## Spielerstatus einfärben

Im eigenen **Pilotenprofil** rechts neben dem Status auf den unterstrichenen **A-Knopf** klicken. Markiere einen Textabschnitt und wähle eine Farbe. Ohne Markierung gilt die Farbe für den ganzen Status; in einem leeren Feld für die nächste Eingabe. **Standard** stellt die normale Schriftfarbe wieder her.

Die Vorschau aktualisiert sich direkt. **Speichern** oder Enter übernimmt den Entwurf, **Abbrechen** oder Esc verwirft ihn. Strg+Z macht Text- und Farbänderungen rückgängig; Strg+Y stellt sie wieder her. Bereits vorhandene Farben bleiben beim Öffnen erhalten. Beim Schließen oder Wechseln des Profils wird ein ungespeicherter Entwurf verworfen.

## Antriebsspuren ausprobieren

Unter **Forge → Antrieb** stehen Uni-, Zwillings- und Tristar-Spuren in je neun Farben sowie der Schiffsstandard. Mit Typ- und Farbfilter grenzt du die Liste ein.

Im Modus **Vorschau** erscheint die Auswahl sofort an deinem Schiff. Du kannst weiterfliegen und mit **Vor/Zurück** die gefilterten Spuren vergleichen. **Normal**, Schließen oder ein Tab-, Schiffs- oder Szenenwechsel beendet die Vorschau. Deine tatsächliche Ausrüstung bleibt erhalten; andere Spieler sehen weiterhin diese. Die Vorschau wird nicht über einen Neustart gespeichert.

## Orbitalschläge

Unter **Forge → Anzeige → Kampf & Effekte → Orbitalschläge** wählst du **Aus**, **Nur Kontur** oder **Zeit + Füllung**. Mit **Übernehmen** wirkt die Auswahl sofort und bleibt gespeichert. Aus entfernt sämtliche zusätzlichen Forge-Markierungen; die ursprünglichen Spieleffekte bleiben sichtbar.

Die Anzeige erkennt stationäre rote NPC-Warnkörper, auch bei den aufgezeichneten Gazica-Angriffen. Dadurch können Konturen auch außerhalb von Remnant-Kämpfen erscheinen. Nur bekannte Varianten mit auswertbaren Zeitdaten bekommen einen Countdown; unbekannte Varianten erhalten eine Kontur. Je nach bekannter Variante beträgt die geschätzte Vorwarnzeit etwa 5, 6,25 oder 12,25 Sekunden. Countdown und Füllung verwenden dieselbe Zeit. Zeiten und Grenzen bleiben Schätzungen; ein Einschlag kann früher erfolgen.

## Reparaturfelder

Unter **Forge → Anzeige → Kampf & Effekte → Reparaturfelder** kannst du die Darstellung einstellen. **Reduziert** dämpft standardmäßig das Leuchten überlappender Felder und erhält ihre Animation. **Original** zeigt die gewohnte Darstellung; **Nur Kontur** ersetzt die große Aura durch eine Außenlinie. **Übernehmen** wirkt sofort und speichert die Auswahl.

## Discord und Medal

Den Discord-Spielstatus stellst du unter **Forge → Anzeige → Meldungen & Discord** ein. Discord muss geöffnet sein und die Anzeige deiner Aktivitäten erlauben. Für das Overlay den laufenden Client unter **Discord → Registrierte Spiele** hinzufügen und das Overlay einschalten. Veraltete Forge-Einträge gegebenenfalls vorher entfernen.

Medal kann den 64-Bit-Client aufnehmen. Wird er nicht erkannt, das laufende Spiel über **Add New Game** hinzufügen. Die offizielle Kategorie „Pirate Galaxy“ wird noch nicht zuverlässig zugeordnet; „Requested“ kann trotz funktionierender Aufnahme stehen bleiben. Clips und Aufnahmeoptionen verwaltest du in Medal.

## Grenzen der Alpha

Einzelne Grafik-, Musik- und Performanceprobleme sowie native Abstürze werden weiter untersucht. Hohe FPS unter jeder Last und die Erkennung durch Discord oder Medal sind nicht zugesichert. Den Umfang einzelner Korrekturen beschreiben die [Releasehinweise](https://github.com/FallenIncursio/pirate-galaxy-forge-releases/releases).

## Kritische Lebenspunkte

Unter **Forge → Anzeige → Kampf & Effekte** stellt der Regler die Warnschwelle von **5 bis 50 %** ein. Standard sind **25 %**. Der vorhandene Warnsound und die roten Bildschirmränder richten sich nach dieser Grenze. **Rote Bildschirmränder** lassen sich unabhängig abschalten. Mit **Übernehmen** speichern; ein Neustart ist nicht nötig.

## Remnant-Trägertabelle

Klicke auf die bekannte Beutekategorie, um mögliche Baupläne mit Icons und deinem Bestand zu sehen. Komponenten sind nach Familie zusammengefasst; Normal, Schnell, Stark und Lang haben getrennte Bestände. Nur tatsächlich vorhandene Varianten werden angezeigt. Große Kategorien haben mehrere Seiten.

Bestände wie 8/6 bleiben erhalten und aktualisieren sich nach Verbrauch. „Nicht im Profil“ steht für einen unbekannten Bestand, nicht automatisch für null Teile. Die Anzeige verändert keine Baupläne und sagt keinen konkreten Drop voraus.

Neue Träger zeigen zunächst die geschätzte Wartezeit bis zur Systemmeldung. Planet und Beute erscheinen erst nach ihrer Bekanntgabe; bekannte Lebenspunkte stehen als Prozentzahl im Balken. Der ursprüngliche Abflugtimer bleibt erhalten.

## Kryonit-Drohnenwechsel

Unter **Forge → Anzeige → Komponenten** eine **Tauschdrohne** auswählen und **Beim eigenen Sammeln** einschalten. Die Kryonitdrohne muss ausgerüstet und geladen sein. Vor deinem manuellen Sammelauftrag wartet Forge auf den bestätigten Wechsel; nach der Sammelfolge kehrt die vom Helfer geänderte Belegung zurück. Ein freier aktiver Platz wird ohne unnötigen Tausch genutzt.

Für Beute von Mitspielern **Sammelmodus starten** und danach **beenden**. Der Modus bleibt bis dahin aktiv und startet nicht automatisch beim Login. Ein kleines **A** am Drohnensymbol kennzeichnet die Hilfe. Manuelle Drohnenwechsel haben Vorrang. Nach einem unterbrochenen Gebietswechsel oder einer unklaren Serverantwort die Belegung prüfen. Die Hilfe ist standardmäßig aus und kauft oder lädt keine Drohnen.
