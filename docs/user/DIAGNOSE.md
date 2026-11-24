# Diagnose und Hilfe bei Start- und Spielproblemen

[Übersicht](../../README.md) · [Installation und Reparatur](INSTALLATION.md) · [Datenschutz](DATENSCHUTZ.md)

## Ladebildschirm vor der Anmeldung

1. Im Starter **Diagnose** öffnen. Ist er ausgeblendet, Forge erneut öffnen, das Forge-Symbol im Windows-Infobereich doppelklicken oder **Forge – Diagnose** im Startmenü wählen.
2. Bei sichtbarem Hänger **30 Sekunden aufnehmen** wählen und die Aufnahme abwarten.
3. **Diagnose speichern** erstellt einen Bericht. Über **Bericht senden** lässt er sich nach eigener Bestätigung mit einer Problembeschreibung übermitteln.

Erneutes Öffnen des Starters erzeugt keinen zweiten Spielclient. **Live-Logs** zeigen
den technischen Startverlauf. Eine intern gemeldete Loginbereitschaft beweist nicht,
dass der Ladebildschirm sichtbar verschwunden ist. Die Diagnose bleibt deshalb verfügbar.

Bei länger ausbleibendem Fortschritt bietet der Starter Hilfe an. **Weiter warten**
erhält den laufenden Start. **Neustart** und **Reparieren und neu starten** beenden
den zugehörigen Client; vorher offene Arbeit beziehungsweise eine laufende Spielsitzung beachten.

## Spiel hängt oder Fenster ist verschwunden

Die Starterdiagnose bleibt nach der Anmeldung verfügbar. Ihre Übersicht unterscheidet
einen laufenden, beendeten und nicht ermittelbaren Prozess. **Spiel neu starten**
beendet nach Bestätigung ausschließlich den zu diesem Starter gehörenden Client.
Profile, Einstellungen und gespeicherte Anmeldedaten bleiben erhalten.

Wenn länger als 45 Sekunden keine neuen Render-Lebenszeichen eintreffen, bietet
der Starter Hilfe an. Ein minimiertes Spiel löst diese Hilfe nicht automatisch aus.
Ein beendeter Grafikthread wird auch dann protokolliert, wenn Java noch weiterläuft.
Vor dem Neustart lässt sich die vorhandene Diagnose speichern; eine neue Aufnahme
ist dafür nicht erforderlich. Der Starter beendet einen Hänger nicht eigenmächtig.

## Grafikfehler, Ruckler oder Abstürze

Für eine verwertbare Beschreibung genügen:

- Forge-Version und gewählter Renderer, D3D11 oder D3D9.
- Zeitpunkt und Ort: vor Anmeldung, Serverwahl, Planet oder bestimmte Aktion.
- Was sichtbar passiert und ob es sich wiederholen lässt.
- Der freiwillig exportierte Diagnosebericht; bei Rucklern möglichst eine Aufnahme in der betroffenen Szene.

Enhanced bietet zusätzlich **Forge → Diagnose** im Spiel. Ein einzelner hoher
Heapwert oder ein Java-Fehlereintrag belegt noch keine Ursache für einen FPS-Abfall
oder einen nativen Absturz. Screenshots und Aufnahmen ergänzen den Bericht.

Für die Enhanced-Reisekosten-Vorschau enthält der Export zusätzlich eine begrenzte
Historie von Preis, Reisezeit, Mitgliedschaftsfaktor und ausgeblendeten Zuständen.
Es werden dafür keine zusätzlichen Serveranfragen ausgelöst und keine Kontodaten erfasst.

Bei Enhanced-Reparaturfeldern erfasst der Export die drei Darstellungsstufen,
die Rotmarkierung sowie Zähler für Spieler, PvE, PvP und unbekannte Absender.
Damit lässt sich zwischen fehlender Spielerzuordnung und Darstellungsfehlern
unterscheiden. Spielernamen und Spielerkennungen werden dabei nicht gespeichert.

Bei aktivierter OTB-Anzeige und OTB-Diagnose zeichnet Enhanced außerdem Phasenwechsel,
die letzten Countdown-Sekunden und das Ende der lokalen Zuordnung auf. Verwendet
werden bereits empfangene Modelle, keine zusätzlichen Serverabfragen. Die
Serverwertung und der Grund eines serverseitigen Abbruchs bleiben unbekannt.

## Grenzen und Daten

Berichte werden nicht allein durch das Aufzeichnen versandt. Der Startbericht
enthält begrenzte technische Zustände; gemeldete interne Fehler werden getrennt
nach Java- und verfügbaren nativen Daten betrachtet. Vor dem freiwilligen Senden
den angebotenen Umfang prüfen. [Weitere Angaben](DATENSCHUTZ.md).

Kamerabhängige Terrainhelligkeit, einzelne Ruckler und weitere native Grafikfehler
bleiben offen. Eine erfolgreiche Prüfung auf einem Rechner ist keine vollständige
GPU-, Wine-/macOS- oder Langzeitabnahme. Die [Versionsberichte](../../CHANGELOG.md)
führen die jeweils bestätigten Prüfungen auf.

Bei Sandboxie sind kurze Boxpfade wichtig: zu lange umgeleitete Socket-Pfade können
einen irreführenden Verbindungs-/Firewallfehler verursachen.

Ressourcen-Downloads melden Weiterleitungen und Fehler als begrenzte Zähler mit
HTTP-Status, Protokoll und festen Hostkategorien. Vollständige URLs und
Abfrageparameter werden dafür nicht in den Diagnosebericht übernommen.
