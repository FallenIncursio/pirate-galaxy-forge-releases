# Alpha.17 – lokale OTB-Aktivität in Enhanced

Spielversion 1002133. Core enthält den gemeinsamen Namens-/Zielanzeigenfix,
aber keine OTB-Funktionen. Der Nutzer hat den neuen Enhanced-Sandbox-Stand
bestätigt und alpha.17 am 21.11.2026 zur Veröffentlichung freigegeben.

## Anlass und Anzeige

Die Live-Diagnose vom 20.11.2026 fand den eigenen Teilnehmer und laufende
Erzänderungen, aber keine verwertbaren Aktivitätszähler. Fehlende Daten sind
kein Nachweis von Inaktivität. Deshalb wertet das Widget jetzt lokale Signale aus.
Die kleine Fußzeile lautet in jedem Zustand **Serverwertung unbekannt**. Die alte
Prozentanzeige und Schlussfolgerungen aus dem historischen Client-Prädikat
werden nicht mehr im Widget verwendet.

Vier passive Zeilen unter dem originalen OTB-HUD zeigen eigene angenommene
Systemnutzungen seit Messbeginn, die Zeit seit Systemnutzung und Bewegung,
den Countdown und die unbekannte Serverwertung. Die letzten 15 Sekunden vor
der lokalen Schwelle werden gelb hervorgehoben; ab Ablauf zeigt ein orange
hervorgehobenes Band ein Warnzeichen und die Dauer ohne lokales Signal.
Unter Forge → Anzeige → Widgets sind 60 (Standard), 90, 120 Sekunden oder Aus
wählbar. Aus, pausierte Messung und fehlende Daten stehen explizit anstelle des
Countdowns. Unbekanntes Signalalter wird als Gedankenstrich dargestellt.
Keine Prozentpunkte, Flugstrecken oder technischen Bewegungssample-Zähler.
Das ist eine lokale Erinnerung, keine bestätigte Serverfrist, Punkteprognose
oder Schutz vor einer OTB-Sperre. Kein Ton, Blinken, Popup oder Eingabefokus;
das Widget verschwindet außerhalb des eigenen OTB.

Der Systemzähler bleibt über Messpausen/Tod erhalten und beginnt bei einer neuen
lokalen Matchbindung (auch nach Wiederverbindung oder Aus-/Einschalten) neu.
Er bezeichnet keinen garantierten vollständigen Matchstand; Messlücken werden
nicht nachträglich aufgefüllt. Beide Signalalter bleiben getrennt sichtbar.

**OTB-Warnung testen** unter Anzeige → Widgets öffnet eine beschriftete Vorschau
mit Beispieldaten im bestehenden Forge-Fenster. Ein verkürzter Fünf-Sekunden-
Countdown wechselt in dieselbe Warnanzeige wie das HUD. „Erneut testen“ und
„Zurück zu Widgets“ ermöglichen Wiederholung und Rückkehr. Die Vorschau nutzt
die noch nicht gespeicherte Schwellenwahl (bei Aus ein ausdrücklich bezeichnetes
60-Sekunden-Beispiel). Sie schreibt weder Einstellungen noch OTB-Messwerte oder
Diagnoseeinträge, erzeugt keine Spielaktion und benötigt kein laufendes OTB.

## Code und Grenzen

- `OtbActivity` verwendet unverändert die bereits empfangenen lokalen Register,
  den eigenen Teilnehmer und die aktive OTB-Phase. Keine zusätzliche API-Abfrage.
- `OtbLocalProbe` nutzt den bestehenden Enhanced-Hook
  `ComponentObservations.acknowledged`. Nur die positive Antwort auf einen
  tatsächlich gestarteten eigenen Systemaufruf zählt. Tastendruck, Warmup,
  Cooldown, Ablehnung, Timeout und fremde Systeme sind keine Aktivitätssignale.
  Der Hook bleibt unabhängig vom Schalter der Staffel-/Effektbeobachtung.
- Worker berühren keine GUI und schreiben keine Dateien. Eine Sitzung enthält
  höchstens 64 Ereignisse und 64 Duplikatmarken. Der UI-Thread verarbeitet sie;
  Scope, Schiff, Verbindung, Planet, Pilot, Match und Lebenszustand werden geprüft.
  Antworten auf vor der Sitzung gestartete Aktionen werden verworfen; Antworten
  dürfen in anderer Reihenfolge eintreffen, aber nur einmal zählen.
- Bewegung wird ausschließlich aus der bereits aktualisierten eigenen
  Voyager-Position (`azv.djD`, unter Lesesperre) gelesen, ohne dessen
  `TK/TL`-Interpolation erneut auszulösen. Das Schiffmodell besitzt keinen
  verlässlichen separaten `worldposition`-Wert. Acht Einheiten aufsummierter
  Ortsänderung gegenüber dem letzten Anker unterdrücken kleines Positionszittern.
  Sprünge über 4000 Einheiten pro Sekunde (mindestens 2000 pro Abtastung) werden
  als Diskontinuität behandelt. Diese Filter sind lokale Heuristiken, keine
  Serverstrecke oder bestätigte Maximalgeschwindigkeit.
- Messlücken über drei Sekunden, Zeitrücksprünge, Teleports, Tod/Wiederbelebung,
  fehlende Positionen und Sitzungswechsel setzen den Warnzeitraum zurück.
  Fehlende Teilnehmer-/Schiffsdaten pausieren die Beobachtung. Es werden keine
  ausgefallenen Sekunden nachträglich als Aktivität oder Inaktivität gezählt.
- Beobachtete Bewegung kann auch eine Positionskorrektur sein; eine angenommene
  Systemnutzung beweist weder Wirkung noch relevanten Schaden oder Unterstützung.
  Stationäre legitime Rollen können eine Erinnerung auslösen. Die Endwertung
  ist weiterhin unbekannt und wird nicht aus diesen Signalen berechnet.

## Diagnose

Das bestehende abschaltbare lokale Journal unter `diagnostics/otb` verwendet
Format 2. Es enthält zusätzlich die lokale Signalquelle, Zustand, Frist,
Signalalter, Zähler, Resets und verworfene Ereignisse. `server_verdict` bleibt
`unknown`; `state` und `client_thresholds` beschreiben nur den historischen
Client-Prädikatbefund. Die bisherigen Rohfeldwerte bleiben zur Fehlersuche
getrennt erhalten. Keine Koordinaten, Spielernamen, Eingaben oder Zugangsdaten.
Asynchroner Schreiber, Queue 64, zwei Dateien mit je maximal 256 KiB.
Keine automatische Übertragung und keine zusätzlichen Serveraufrufe.

## Prüfung und nächste Sandbox-Abnahme

Automatisiert: Originalmodell-/Observerfälle, tatsächlicher gepatchter
System-Worker mit synthetischen Antworten, fehlende Serverzähler, abgelehnte/
doppelte/vertauschte Antworten, begrenzte Queues, lokale Warnschwelle, Tod,
Wiederbelebung, Scopewechsel, Messlücken und passive native UI. Beide Editionen
werden mit D3D9 und D3D11 sowie dem gemeinsamen Namensfix geprüft.

Der Widget-Folgestand prüft zusätzlich unabhängige Signalalter, 15-Sekunden-
Vorwarnung, Schwellengrenzen, native Textbreiten, passive Eingabe und die
Vorschau samt Rückkehr/Verwerfen/Schließen auf den neuen Paketbytes.

Für die spätere echte Sandbox-Abnahme: Allianz-Namen vor/nach Auswahl,
Widget nur im eigenen OTB, Systemnutzung im Stillstand, normale Bewegung,
60 Sekunden ohne Signal, deaktivierte Warnung, Tod/Wiederbelebung und Matchende.
Die Einstellung muss nach Übernehmen und Neustart erhalten bleiben. Echte
Serverwertung weiterhin unbekannt lassen. Ein Fixture-Test ersetzt kein live OTB.

Neuer Widgetstand: 62 Testsuiten, sechs Negativkontrollen, 698 OTB-Checks und
je 1.239 native Enhanced-Bedienprüfungen unter D3D9/D3D11 bestanden. Die frühere
64-Check-Installerprüfung betrifft ausschließlich die damaligen Paketbytes.
Die neue Anzeige wurde noch nicht im echten OTB abgenommen.

Aktuelle Artefakte und hashgebundene Belege stehen im
[privaten Prüfstand](RELEASE-STATUS-0.2-alpha.17.md).
