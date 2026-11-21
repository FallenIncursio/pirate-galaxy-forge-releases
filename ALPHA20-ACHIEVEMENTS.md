# Enhanced alpha.20: Errungenschaften im Pilotenprofil

Enhanced-Update, Spielversion **1002133**, Starter **17**, Sequenz **101**.
Neue Funktion ausschließlich für Enhanced. Core bleibt alpha.17 / Sequenz 16.
Nach bestätigtem D3D11-Sandbox-Test veröffentlicht; alle sieben öffentlichen
Downloads, RSA-Manifest, Updatekanal und README-Installerlink sind geprüft. Profil, Einstellungen und gespeicherte Anmeldung
wurden beim Test übernommen. Die Zeilenvorlagen verwenden die ursprüngliche
Ermittlung der Archivgruppe; native Prüfungen geben diese nicht künstlich vor.

## Bedienung

Unter **Pilotenprofil → Errungenschaften** bleiben Kategorien, Gesamtpunkte,
Gesamtfortschritt und die bekannten orangefarbenen Fortschrittsbalken erhalten.
Abgeschlossene Erfolge verwenden wieder die originale goldene Medaille und
Abschlusszeile, offene Einträge die silberne Medaille mit Fortschrittsbalken.

- **Alle Kategorien** ermöglicht eine Suche über die ganze sichtbare Sammlung.
- **Suchen** filtert Namen ohne Beachtung von Großschreibung oder Akzenten.
  Mehrere Wörter müssen alle vorkommen. Das × leert die Suche.
- **Status:** Alle, Offen, Begonnen, Abgeschlossen.
- **System:** Alle Systeme, Vega bis Tau Ceti oder Nicht zugeordnet.
- **Bereich:** Zur gewählten Hauptkategorie passende Untergruppen, beispielsweise
  Baupläne, seltene Baupläne, Schiffe, Missionsarten oder Gegnergruppen. Angezeigt
  werden nur Bereiche, die in den vorhandenen sichtbaren Daten vorkommen.
- **Sortieren nach:** Fortschritt, Name A–Z, Punkte, Abschlussdatum.
  Abschlussdatum wählt zugleich abgeschlossene Erfolge; bei offenen Einträgen
  steht wieder Fortschritt zur Verfügung. „Letzte Aktivität“ zeigt alle vorhandenen
  Abschlüsse nach Datum, statt nur die bisherigen fünf.
- Trefferzahl und eindeutiger Leerzustand. Lange Namen werden gemessen umgebrochen;
  Zeilen beginnen oben und lassen sich mit dem Mausrad scrollen.
- Beschreibungen erscheinen beim Verweilen über einer Zeile. Die bestehenden
  Fragezeichen für offene Sammlungen öffnen weiterhin den originalen Detaildialog.

Unter **Forge → Anzeige → HUD & Grafik → Errungenschaften: erweiterte Ansicht**
lässt sich die Erweiterung ein- und ausschalten. Nach „Übernehmen“ wechselt auch
ein bereits geöffnetes Profil ohne Neustart zur ursprünglichen Ansicht oder zurück.
„Verwerfen“ behält die bisherige Auswahl. Filterpräferenzen bleiben beim Ausschalten
erhalten; die Einstellung ist standardmäßig eingeschaltet und lokal gespeichert.

Standard: Alle Kategorien, Offen, Fortschritt, alle Systeme/Bereiche.
Kategorie, Status, Sortierung, System und Bereich
werden lokal je eigenem Pilot gespeichert; eigenes und fremdes Profil sind getrennt.
Suchtext wird nicht dauerhaft gespeichert. Ein neuer Filter startet oben; reine
Fortschrittsänderungen lassen Position und Reihenfolge stabil.

## Daten und Leistung

Verwendet ausschließlich bereits empfangene Errungenschaften und Fortschritte.
Keine zusätzliche Spielserverabfrage, automatische Aktion oder Änderung an
Punkten, Belohnungen und Abschlussbedingungen. Versteckte offene, deaktivierte
und noch gesperrte Einträge bleiben verborgen. Bei fremden Profilen gelten weiter
die ursprünglichen Sichtbarkeitsregeln. Ein gerundeter Fortschritt bedeutet keinen
Abschluss; fehlende/ungültige Zielwerte erscheinen als unbekannt.

Systeme werden lokal aus vorhandenen Unterkategorien sowie ausdrücklichen System-
oder bekannten Planetennamen in Titel/Beschreibung zugeordnet. Bereiche bevorzugen
die ursprünglichen Unterkategorien; ergänzend dienen geprüfte Sprachschlüssel-
Familien und der originale Sammlungstyp. Das ist keine neue Serverklassifikation.
Unklare Systeme bleiben „Nicht zugeordnet“, unbekannte Bereiche unter „Weitere“
beziehungsweise „Sammlungen“. Insbesondere wird Erebos nicht allein aus einer
internen Planetenkennung einem System zugeschlagen. „Alle Systeme/Bereiche“ behält
sämtliche sonst sichtbaren Einträge. Die Abdeckung des echten Katalogs ist im
Spieltest zu prüfen; unbekannte interne Bezeichnungen werden nicht roh angezeigt.

Die native Liste verwendet höchstens 24 wiederverwendete Zeilen. Lokale
Werteprüfung nur bei sichtbarer Ansicht und höchstens einmal pro Sekunde;
unveränderte Daten werden nicht erneut sortiert. Suche reagiert nach 150 ms Pause.
Geschlossene oder inzwischen gewechselte Profile verwerfen verspätete Ergebnisse.
Bei einem UI-Fehler wird die ursprüngliche Ansicht wiederhergestellt.

Dies ist eine Enhanced-Erweiterung gegenüber dem 32-Bit-Client, keine neue
Spielmechanik oder bestätigte allgemeine Leistungssteigerung. Bestehende Grafik-,
Sicherheits-, Material- und Helligkeitsbefunde werden dadurch nicht behoben.

## Sandbox-Abnahme

1. Eigenes Pilotenprofil öffnen; All/Einzelkategorie, alle vier Statusfilter und
   alle Sortierungen kombinieren. Gesamtpunkte/-fortschritt müssen unverändert sein.
2. Nach „Sirius“, einem langen Namen und einem nicht vorhandenen Begriff suchen;
   Eingabe und Löschen dürfen keine Komponenten auslösen. Danach sind Komponenten-
   tasten außerhalb der Eingabe weiter verfügbar.
3. Lange Listen scrollen, Suchfilter zurücksetzen, HUD-Größen wechseln. Namen,
   Zahlen, Fragezeichen und Tooltip dürfen nicht abgeschnitten werden.
4. Fragezeichen einer BP-/Schiffssammlung öffnen und ursprüngliche Einzeldetails
   prüfen. Das ist zusätzlich zum isolierten nativen Test erforderlich.
5. Ein fremdes Profil öffnen; keine fremden offenen/versteckten Erfolge sichtbar.
   Rasch zwischen zwei Piloten und eigenem Profil wechseln, schließen und neu öffnen.
6. Kategorie/Status/Sortierung/System/Bereich merken lassen, Client später regulär neu starten;
   Suchtext soll leer sein. Zwischen Profilen dürfen keine Einstellungen überlaufen.
7. Einen Fortschritt/Abschluss erhalten: Werte aktualisieren sich, die Ansicht
   springt nicht. Bei Abschluss verschwindet der Eintrag aus „Offen“.
8. Abschlüsse auf goldene Medaille und Datumszeile prüfen; zwischen offenen und
   abgeschlossenen Listen wechseln und scrollen, damit auch wiederverwendete Zeilen
   jeweils die richtige Vorlage zeigen.
9. System und Bereich mit Kategorie, Status und Suche kombinieren, einschließlich
   „Nicht zugeordnet“. HUD-Größe ändern; die Filter müssen erhalten bleiben.
10. Den Anzeige-Schalter mit Übernehmen/Verwerfen testen, bei offenem Profil und
    nach erneutem Öffnen. Originalansicht muss gefüllt und bedienbar bleiben.

Automatisierte native Proben verwenden die tatsächlichen Spieldateien und
Beispieldaten, jedoch keine angemeldete Spielsitzung. Erfolgreiche Offlineprüfungen
ersetzen diese Abnahme, Wine/macOS-Tests oder einen Langzeittest nicht.

Technik: `project/client-achievements/README.md`. Aktuelle Belege:
[Release-Prüfstand](RELEASE-STATUS-0.2-alpha.20.md).
