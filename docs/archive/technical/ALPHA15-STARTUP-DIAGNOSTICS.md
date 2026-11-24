> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Alpha.15: Live-Logs und Startdiagnose

Gemeinsam für Core und Enhanced, Spielversion 1002133, Starter 15.

## Bedienung

Der Start läuft wie bisher ohne zusätzliche Bestätigung. „Live-Logs“ und
„Diagnose“ sind von Beginn an erreichbar. Sobald die Anmeldung vorbereitet ist,
blendet sich der Starter aus. Sein Symbol im Windows-Infobereich, erneutes Öffnen
des Starters und der neue Startmenüeintrag „Diagnose“ öffnen die aktuelle Sitzung.
Nach dem Beenden zeigt der Diagnoseeintrag die letzte gespeicherte Sitzung.

Die Übersicht zeigt Schritt, Laufzeit, ältesten offenen Ressourcenauftrag,
Render-Lebenszeichen, Prozesszustand, Fenstergröße, Arbeitsspeicher und GPU/Treiber.
„Loginbereitschaft gemeldet“ bedeutet einen internen Bereitschaftszustand, keine
unabhängige Bestätigung des sichtbaren Bildschirms. Bei weiter sichtbarem Splash
bleibt „30 Sekunden aufnehmen“ verfügbar. Die Aufnahme hält den Client offen.

Die Live-Logs enthalten strukturierte technische Ereignisse. „Neueste Ereignisse
verfolgen“ lässt sich abschalten, um frühere Zeilen zu lesen. Es werden keine
unbegrenzten Rohlogs in ein Textfeld geladen. „Diagnose speichern“ erstellt eine
neue ZIP-Datei; „Bericht senden“ öffnet zuerst einen Dialog mit Beschreibung und
explizitem Sendeknopf. Netzwerkfehler erlauben Wiederholung desselben Berichts.

## Erkennung und technische Grenzen

Jeder Ressourcenauftrag hat eine eigene Fortschrittsuhr und eine nur innerhalb
der Sitzung gültige Nummer. Bytefortschritt wird zugehörigen Abhängigkeiten
zugeordnet; unverwandte Downloads setzen deren Uhr nicht zurück. Wiederholte
Phasenmeldungen reichen nicht als Startfortschritt. Die bestehenden Zeitgrenzen,
CRC-Prüfungen und Serveraufrufe bleiben erhalten. Es entstehen keine zusätzlichen
Spielserveranfragen durch die Diagnose.

Der Starter bleibt vom Spielprozess unabhängig. Die Java-Aufnahme wird über
einen sitzungsgebundenen lokalen Auftrag angefordert und liefert drei begrenzte
Thread-Snapshots in etwa zehn Sekunden Abstand. Auch nach Loginbereitschaft
bleibt dieser Diagnoseweg aktiv. Bei einem blockierten JVM-Scheduler, einem
nativen Stillstand oder einem Fehler vor JVM-Start können die Snapshots fehlen:
Die Oberfläche meldet dies, erhält aber Startverlauf und externe Prozessdaten.
Ein Lebenszeichen allein ist kein Nachweis eines fehlerfreien Grafik-Presents.

Ressourcennamen, URLs, Profile und Passwörter werden nicht in die strukturierten
Ereignisse übernommen. Ein Speicherabbild wird hier nicht automatisch erstellt.
Der bestehende Absturzreporter behält seine gesonderte, standardmäßig deaktivierte
Zustimmung zum Anhängen eines bereits vorhandenen Dumps.

## Speicher, Export und Berichtsdienst

Die Diagnose beginnt vor dem Lesen der Einstellungen. Ist der reguläre
Datenordner nicht beschreibbar, wird ein editionsgetrennter temporärer Ordner
versucht. Sind beide nicht beschreibbar, bleiben Daten im Arbeitsspeicher.
Die regelmäßigen Dateischreibarbeiten finden außerhalb der Ereignissperre und
des UI-Threads statt. Auch das Anlegen der Sitzung läuft im Hintergrund.

Obergrenzen: 20 regulär aufbewahrte Sitzungen, je 32 KiB lokale stdout-/stderr-Tails,
192 Ereignisse, 90 Prozessmesswerte, 32 älteste offene Aufträge im Export und
bis zu sechs gekürzte Thread-Snapshots. Unbekannte Dateien werden nicht gelöscht.
Die lokalen Roh-Tails werden weder in den Supportexport noch in Berichte übernommen.

Export und Versand nutzen denselben Schema-3-Umschlag: `report.json` und
`diagnostics.json`, letzteres maximal 256 KiB. Der Dienst prüft Felder, Typen,
Identitäten, Grenzen und Threadsyntax strikt. Alte Schema-1-/Schema-2-Berichte
bleiben gültig. Diagnoseberichte werden im privaten Dashboard nach Edition,
Version, Starter, Phase und Renderer filterbar; Gruppierung ist eine Triagehilfe,
kein Beweis einer gemeinsamen Fehlerursache. Die Aufbewahrung bleibt 14 Tage.

## Abnahme

Aktuelle, an Quell- und Pakethashes gebundene Belege stehen im
[Release-Prüfstand](../verification/RELEASE-STATUS-0.2-alpha.15.md). Reale Hänger auf betroffenen
Spielerrechnern, andere GPUs, Wine, kamerabhängige Helligkeit und die konkrete
native Sirius-Absturzursache bleiben gesondert offen.
