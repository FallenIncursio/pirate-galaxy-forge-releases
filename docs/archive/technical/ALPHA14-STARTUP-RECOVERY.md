> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Alpha.14: Ladebildschirm, Diagnose und Wiederherstellung

Core und Enhanced, Spielbasis 1002133. Am 20.11.2026 nach ausdrücklicher Freigabe
veröffentlicht und die öffentlichen Downloads geprüft. Enhanced wurde über Starter 14 mit D3D11 in der Sandbox gestartet;
der Nutzer meldet bisher störungsfreien Betrieb. Die getesteten Paketbytes bleiben
unverändert. Die laufende Sitzung bleibt während der Veröffentlichung geöffnet.

## Ursache und 32-Bit-Vergleich

Originalklasse ds hatte nur einen Verbindungs-, keinen Lesetimeout und endlose
Inhaltswiederholungen. Original-dw wartete in mehreren Varianten ausschließlich
auf SUCCESS ohne Frist. Alpha.13 begrenzte Metadaten-Retries, ließ diese abhängigen
Wartezustände aber unverändert. Die Diagnose bestätigte schon nach drei Render-
durchläufen den Spielstart. Vor der Anmeldung war kein Hängerbericht erreichbar.
Isolierte Proben bestätigten blockierte Antworten und wiederholte HTTP-503;
der konkrete Auslöser bei betroffenen Spielern ist dadurch nicht nachgewiesen.

## Gemeinsame Java-Korrektur

`ResourceTransfers` ersetzt ausschließlich den Inhalts-Transport über die
fingerprintgebundene ds-Methode. Connect 5 s, Read 15 s, maximal drei Versuche,
180 s Budget und 256 MiB je Antwort. Geschlossene Streams/Verbindungen auch auf
Fehlerpfaden, Größen-/CRC-Prüfung vor atomarem Austausch, vorhandener gültiger
Cache wird wiederverwendet. Die originale Archivregistrierung bleibt erhalten.

`ResourceLoads` kapselt den bestehenden Validator, begrenzt dessen Schleifen und
Future-Wartezeiten und beendet offene Download-Futures beim Verlassen. Die
ursprüngliche worker-false-Antwort wird zum terminalen Transaktionsfehler, statt
die äußere Schleife erneut anzustoßen. Der bestehende RPC-Transport behält seinen
eigenen Timeout; es gibt keinen zusätzlichen RPC-Executor oder aktive Serverprobe.

`ResourceWaits` führt abhängig wartende Aufträge über Erfolg, Fehler oder Abbruch
zusammen. Tickets sind an die konkrete Dienstbindung gebunden, auf 1.024 aktive
Einträge und 180 s beschränkt. Auch verzögerte UI-Fortsetzungen prüfen die Bindung.
UI-Aufträge bleiben auf dem bestehenden UI-Scheduler. Lokale Fehler aus dp
beenden betroffene Gruppen. Nur die optionalen Login-Dateien `logindata` und
`framework_logindata*` erhalten den bestehenden Login-Callback auch bei Fehlschlag;
die bereits vorhandene Lesefehlerbehandlung öffnet dann das normale Formular.
Keine Zugangsdaten werden protokolliert oder entfernt.

`StartupFixes.java`, `EditionFixes.java` und `edition-fixes.tsv` binden Originalhash,
komponierten Eingang und erwartete Änderungen. Beide Renderer und Editionen
verwenden dieselben Helfer. Native DLLs und der Fokus-/Terrainstand bleiben erhalten.

## Startnachweis und Hängerdiagnose

Die native Login-Initialisierung meldet Erfolg nur nach ihrem erfolgreichen
UI-Abschnitt und zwei weiteren Renderdurchläufen. Der initialisierte Spielkontext
liefert denselben Bereitschaftspfad für einen übersprungenen Login. Drei Render-
durchläufe dürfen das Starterfenster aus dem Weg nehmen, bestätigen aber weder
Login noch Grafikerfolg. Alte installierte Clients behalten den Legacy-Handshake.

Nonce-gebundene lokale Meldungen erfassen Schritte, tatsächlichen Ressourcen-
fortschritt, Renderlebenszeichen, Fehlerklasse und HTTP-Status ohne URL/Argumente.
Nach 45 s ohne Fortschritt erzeugt ein JVM-Wächter bis zu drei lokale Snapshots:
maximal 128 Plattformthreads, je 16 Stackrahmen, Zustände und Lock-Owner-IDs.
Keine Threadnamen, Quelldateipfade, Accountdaten oder Speicherinhalte. Snapshots
können einen vollständig blockierten JVM-Prozess nicht garantiert auslesen;
der unabhängige Starter bietet trotzdem Hilfe an. Java Attach bleibt deaktiviert.

`StartupDiagnostics` unterscheidet laufenden Hänger von Prozess-Exit. Gespeicherte
Sessions bleiben auf 20 begrenzt. Der freiwillige Bericht bleibt mit dem bestehenden
Schema-2-Dienst kompatibel. Es findet kein Dienst-Deployment oder automatischer
Upload statt. Der lokale ZIP-Export enthält Zusammenfassung, Kontext und begrenzte
Threaddateien, keine stdout-/stderr-Tails oder Zugangsdaten. Ein existierendes
Exportziel wird nicht überschrieben.

## Wiederherstellung

`StartupHangDialog` bietet Weiterwarten, Diagnose, Bericht, Neustart, Reparatur
und Beenden. Warten schließt den Client nicht; die Hilfe schließt sich selbst,
wenn die Anmeldemaske bereit ist oder der Prozess endet. Neustart/Reparatur
beenden nur den behaltenen eigenen Kindprozess nach ausdrücklichem Klick.
Zunächst normal schließen, nach fünf Sekunden gegebenenfalls diesen Prozess
beenden. Kein zweiter Client vor bestätigtem Prozessende.

Reparatur verschiebt nur kanonische `r<int32>`-REMOTE-Dateien der beiden Renderer
in einen privaten Quarantäneordner. LOCAL-Dateien, geschützte Anmeldungen und
Profile werden nicht entfernt. Pfade, Edition und aktuelle Version werden geprüft.
Danach greift die bestehende signierte Installationsreparatur mit Rückfalljournal.

## Prüfung

Pflichtprüfungen: HTTP-Erfolg/503/Integritätsfehler/stockender Datenstrom,
Dienstwechsel während Download, endende äußere Transaktion, Dateizugriffsfehler
vor Login und realer dp/dw-Auftragsfehler. Starter: falscher Nonce, Render- versus
Loginbereitschaft, Fortschritt bei langsamem Download, Hänger/Exit-Unterscheidung,
Export, Profilschutz und Beenden ausschließlich eines eigenen Testprozesses.
Dazu vollständige Editions-/JNI-/D3D9-/D3D11-Prüfungen und Installer-Upgrades.
Aktueller Belegstand steht in RELEASE-STATUS-0.2-alpha.14.md.

`StartupHangIntegrationTests.cs` startet zusätzlich ausschließlich eine künstliche
Java-Startsequenz mit dem tatsächlich gebauten Spiel-JAR: Renderbereitschaft,
45 s ohne Fortschritt, automatischer Threadsnapshot, Export und anschließende
Loginmeldung. Sie prüft den Prozess-/Nonce-Übergang mit dem echten Starterparser,
ohne Spielverbindung oder Nutzerprofil.

Für die unabhängige Hängeroberfläche den installierten **Starter 14** verwenden.
Ein direkter Start des nativen Spielprozesses umgeht die Starteraufsicht.
Nach 45 Sekunden ohne Fortschritt kann der Nutzer weiter warten, eine lokale
Diagnose speichern oder den eigenen Spielprozess neu starten beziehungsweise
reparieren. Es gibt keinen automatischen Berichtversand oder Neustart.

Der Enhanced-Start über den installierten Starter wurde bis in die verbundene
Spielsitzung geprüft. Profil, Einstellungen, geschützte Anmeldung und Windows-
Lautstärke wurden übernommen. Die Hängeroberfläche wurde mit künstlichen
Prozessprüfungen getestet, nicht durch einen erzwungenen Hänger im Nutzerclient.
Die konkrete Ursache auf betroffenen Spielerrechnern bleibt ohne deren Diagnose
offen; ebenso andere GPUs, Wine, längere Sitzungen und gesondertes Core-Gameplay.
