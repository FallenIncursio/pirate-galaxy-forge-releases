# Daten und freiwillige Berichte

[Zurück zur Übersicht](../README.md)

## Lokale Spieldaten

Forge verwendet eine getrennte Spielkopie. Die Originalinstallation bleibt unverändert; ihre gespeicherten Anmeldedaten werden nicht übernommen.

Bewusst in Forge gespeicherte Anmeldedaten werden lokal mit Windows DPAPI geschützt und an das Windows-Benutzerkonto gebunden. Forge-Einstellungen und der lokale Spielstand der zuletzt verwendeten Forge-Version werden bei Updates übernommen. Gelöschte Anmeldedaten werden nicht aus älteren Versionen wiederhergestellt.

Die Bauplanansicht lädt den eigenen Profilstand über die vorhandene Spielabfrage nach. Solange dieser Tab geöffnet ist, erfolgt die nächste Aktualisierung fünf Sekunden nach Abschluss der vorherigen Anfrage. Außerhalb dieses Tabs läuft die automatische Aktualisierung nicht.

Der Remnant-Kampfbericht erfasst erst nach **Remnant-Aufnahme starten** beobachtete Kampfdaten mit lokalen Pilotenkennungen. **Remnant-Bericht öffnen** speichert den letzten Bericht als `remnant-kampfbericht.html` im Forge-Datenordner. Die Auswertung bleibt lokal.

## Freiwillige Aktivitätszählung

Die Zählung ist standardmäßig **aus**. Bei Zustimmung sendet Forge während des Spiels alle zwei Minuten eine zufällige Installationskennung und die Version per HTTPS.

Der Zähler speichert eine HMAC-Kennung, die Version und die letzte Aktivität. Er erfasst keine Spielkonten, Spielernamen, Hardware- oder Standortdaten. IP-Adressen werden für die Verbindung benötigt, vom Zähler jedoch nicht protokolliert. Einträge verfallen nach sieben Tagen ohne Meldung.

Die Teilnahme lässt sich jederzeit über **Pirate Galaxy Forge - Einstellungen** ausschalten. Gezählt werden teilnehmende Installationen, nicht alle Spieler.

## Freiwillige Fehlerberichte

**Erst der Klick auf „Bericht senden“ überträgt einen Absturzbericht an das Forge-Team.** Der Bericht kann Fehlercode, Forge-Version, Build-Prüfsumme und die eigene Beschreibung enthalten. Aus einem passenden lokalen Speicherabbild können zusätzlich Bibliotheks- und Buildkennungen sowie relative Fehler- und Aufrufstellen übernommen werden.

Das Speicherabbild selbst ist separat und standardmäßig **abgewählt**. Es kann private Speicherinhalte enthalten.

Rohlogs, lokale Pfade und absolute Speicheradressen werden nicht als Metadaten mitgesendet. Die Serverberichte sind privat und werden nach 14 Tagen gelöscht. Diese Frist löscht keine lokalen Kopien auf dem eigenen Rechner.

Lokale Diagnoseaufnahmen werden nicht allein durch das Aufzeichnen an das Forge-Team übertragen. Die mitgelieferte `DIAGNOSE.txt` beschreibt Aufnahmen und den optionalen nativen Rekorder.

## Discord-Spielstatus

Standardmäßig zeigt Forge bei geöffnetem Discord „Pirate Galaxy“ mit Logo und Spielzeit an, sofern Discord deine Aktivitäten teilen darf. Unter **Komfort → Anzeige → Discord und Aufnahme** lässt sich dies ausschalten. Nur bei **Spiel und Ort** wird zusätzlich dein aktuelles Spielgebiet angezeigt. Pilotennamen, Chattexte und Koordinaten werden dafür nicht übertragen.

Die Anbindung verwendet die lokal geöffnete Discord-App; eine zusätzliche Kontoanmeldung in Forge ist nicht nötig. Die Sichtbarkeit steuerst du auch über Discord.
