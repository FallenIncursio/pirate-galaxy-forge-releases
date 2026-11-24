> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Enhanced alpha.25 – Bauplanliste als CSV

Veröffentlicht nach bestätigtem Enhanced-D3D11-Sandbox-Test, Spielversion 1002133.
Core bleibt alpha.17 / Sequenz 16. Der laufende Nutzerclient blieb geöffnet.

## Bedienung

Unter **Forge → Baupläne** Suche, Typ, System, Fortschritt und Merkliste einstellen,
dann unten **CSV exportieren** wählen. Alle Treffer werden in der aktuellen
Reihenfolge exportiert, auch auf anderen Seiten. Die Seitenauswahl begrenzt den
Export nicht. Nach Erfolg zeigt Forge die Anzahl; **Ordner öffnen** öffnet den
Exportordner nur auf ausdrücklichen Klick. Bei leerer Auswahl oder noch nicht
geladenem eigenen Profil ist der Export nicht verfügbar.

Dateien liegen im Ordner `exports` neben `comfort.properties`, also im persistenten
Forge-Datenverzeichnis. Dateiname `Forge-Bauplaene-YYYYMMDD-HHMMSS.csv`, bei
gleichen Zeitstempeln mit nummeriertem Zusatz. Kein Überschreiben älterer Exporte,
keine automatische Öffnung einer Tabellenkalkulation, kein automatischer Versand.
Exporte sind vom Nutzer erzeugte Dateien und werden nicht automatisch bereinigt.

## Inhalt und Format

Eine Zeile je Bauplan mit den Spalten Bauplan, Typ, System, Variante, Level,
Gesammelt, Benötigt, Fehlend, Status und Merkliste. Namen entsprechen der geladenen
Spiellokalisierung; Spaltentitel und Status entsprechen der deutschen Forge-Ansicht.
Keine Pilot-/Konto-IDs, Filterhistorie oder internen Zuordnungsschlüssel.

Unbekannte Mengen bleiben leer. Ein fehlender Profileintrag ist keine belegte
Null. Bekannte Referenz-Nenner bleiben erhalten; der Status unterscheidet
„Nicht im Profil“ und „Ungeklärt“. Remnant-Bestände über der nötigen Teilezahl
bleiben unverändert, z. B. 8/6 mit 0 fehlenden Teilen. Explizit vollständige
Profileinträge haben 0 fehlende Teile, auch wenn der Nenner nicht übermittelt wurde.

UTF-8 mit BOM, Semikolon, CRLF, korrekt maskierte Anführungszeichen und Zeilenumbrüche.
Formelartige Zelltexte erhalten ein sichtbares typografisches Apostroph als Präfix;
CSV-Anführungszeichen allein verhindern keine Formelauswertung. Gewöhnliche
Bauplannamen bleiben unverändert. Bei einem anders konfigurierten Tabellenprogramm
gegebenenfalls UTF-8 und Semikolon beim Textimport wählen.

## Implementierung

`ComfortUi.blueprintSelection` ist der gemeinsame Filterweg für Anzeige und Export.
Der Klick liest einen vorhandenen, an den eigenen Piloten gebundenen Snapshot,
ohne `poll` oder `request` aufzurufen. Alle Daten werden auf dem UI-Thread als
unveränderliche Text-/Zahlenwerte kopiert; Dateiarbeit läuft auf einem dedizierten
Daemon-Worker. Der Worker hält keine Spielobjekte oder nativen Widgetzeiger.

`BlueprintCsvExport` schreibt zuerst eine eigene temporäre Datei im Zielordner,
schließt sie und benennt sie ohne Ersetzen einer bestehenden CSV um. Schreibfehler
melden einen Fehlschlag, abbrechbare Pilotwechsel verwerfen alte Arbeit und
veraltete Erfolgsmeldungen. Der bewusste Export bleibt erhalten, wenn lediglich
das Forge-Fenster geschlossen wird. Maximal ein Export/Ordneröffnen gleichzeitig;
keine Warteschlange aus wiederholten Klicks. Begrenzung auf 20.000 Zeilen,
8.192 Zeichen pro Zelle und insgesamt 8 Millionen Zeichen.

Zusätzliche Serverabfragen: **0**. Die bereits bestehende Profilaktualisierung der
geöffneten Bauplanansicht bleibt unverändert. Das ist eine Enhanced-Zusatzfunktion
gegenüber dem 32-Bit-Client; keine neuen Grafik-, Leistungs- oder Sicherheitszusagen.

## Prüfung und Sandbox-Abnahme

Automatisierte Prüfungen decken Datensemantik, kombinierte Filter, Reihenfolge,
mehrseitige Auswahl, Sonderzeichen, Formelschutz, Dateikollisionen, Schreibfehler,
Doppelklick und Pilotwechsel ab. Native D3D9-/D3D11-Maustests prüfen die tatsächlichen
Exportknöpfe, Filter, Seitenauswahl und Layout bei drei Auflösungen/HUD-Größen.
Konkrete Ergebnisse stehen im [Prüfstand](../verification/RELEASE-STATUS-0.2-alpha.25.md).

Für weitergehende Tabellenprogramm-Prüfungen: eigene Merkliste filtern, von Seite 2
exportieren, CSV im verwendeten Tabellenprogramm öffnen und Teilezahlen sowie
Umlaute vergleichen. Ebenso einmal keine Treffer und einen Remnant-Bestand testen.
Die native Offlineprüfung ersetzt diese Ingame-/Tabellenprogramm-Abnahme nicht.

Der Nutzer bestätigt die Funktion in der D3D11-Sandbox. Ein konkreter Liveimport
in Excel/LibreOffice ist durch diese allgemeine Rückmeldung nicht belegt.
In Sandboxie wird auch der Exportordner in den Container umgeleitet; der normale
Explorer kann deshalb ohne den physischen Containerpfad einen anderen Ordner öffnen.
