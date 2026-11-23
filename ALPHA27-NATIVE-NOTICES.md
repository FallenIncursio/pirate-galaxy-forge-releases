# Enhanced alpha.27 – Forge-Meldungen in der PG-Leiste

Privater Sandbox-Teststand für Spielversion 1002133, nicht veröffentlicht.
Core bleibt bei alpha.17 / Sequenz 16. Enhanced-Sequenz 108 ist nur reserviert.

## Bedienung

Forge-Bestätigungen und Fehler erscheinen mit dem originalen PG-Symbol über
der Komponentenleiste, auch wenn das Forge-Fenster offen ist. Die separate
Meldungsbox und die kurze Speicherbestätigung neben „Übernehmen“ entfallen.
PG übernimmt Positionierung, Textumbruch, Einblendung und Ausblendung.

Unter **Forge → Anzeige → Meldungen & Discord → Forge-Meldungen**:

- **Alle** (Standard): Bestätigungen, Hinweise und Fehler.
- **Nur wichtige**: Warnungen und Fehler; normale Spielmeldungen bleiben unabhängig.
- **Testmeldung** zeigt ein Beispiel auch im eingeschränkten Modus. Sie speichert
  keine Einstellung. Übernehmen, Verwerfen und Seitenwechsel folgen dem bestehenden Entwurf.

Bestätigungen stehen fünf, Warnungen acht und Fehler zwölf Sekunden in der
nativen Karte. Lange Texte werden gekürzt; ein Klick öffnet die vollständige
native Detailansicht. Kurze Meldungen lassen Mausklicks durch und nehmen keinen
Tastaturfokus. Das Schließen von Forge beendet keine ausstehende Rückmeldung.

## Technischer Umfang

`ForgeFeedback` übergibt eigene `apo`-Karten an `atp.bHF` / `aoh.do`.
Nur die eigene Karte wird über die Forge-Ansicht gelegt. Andere PG-Karten werden
weder ersetzt noch umgestaltet. Es gibt keine neue Spielserverabfrage und keine
Änderung an Originalklassen oder Core.

`ForgeNoticeQueue` nimmt höchstens sechs wartende Einträge auf und übergibt
höchstens eine eigene Karte gleichzeitig an PG. Wiederholungen werden acht
Sekunden zusammengefasst; geänderte Ergebnisse derselben Aktion bleiben möglich.
Warnungen und Fehler haben Vorrang. Nach 30 Sekunden verfallen nicht angezeigte
Einträge. Die Diagnose zählt verworfene Meldungen, Überlauf und Dopplungen.

Hintergrundarbeiten benutzen eine Sitzungsgeneration. Piloten-/HUD-Wechsel und
Teardown verwerfen alte Rückmeldungen, ohne Original-PG-Meldungen anzutasten.
Ein noch wartender eigener PG-Eintrag wird unter der ursprünglichen Manager-Sperre
entfernt; aktive Karten werden dem nativen Aufräumablauf übergeben.
Widgetzugriffe erfolgen ausschließlich im bestehenden UI-Thread.

CSV-, Diagnose-, KW- und Remnant-Berichte sowie Einstellungs-/Positionsfehler
verwenden explizite Meldungstypen. Es werden keine Texte anhand deutscher
Fehlerstichwörter klassifiziert.

Der freiwillige lokale Diagnoseexport enthält `forge-notices.json`: Anzahl
angenommener, zusammengefasster, gefilterter, veralteter und verworfener Einträge,
HUD-Verfügbarkeit und technischen Fehlertyp. Keine Meldungstexte, Pfade,
Kontodaten oder zusätzlichen Uploads.

## Prüfung und verbleibender Sandbox-Test

Automatisierte Gates: deterministische Warteschlange einschließlich Parallelzugriff,
Sitzungswechsel, Prioritäten, Unicode-Grenzen und Diagnose; originaler PG-Manager
mit fremder Meldung; native D3D9-/D3D11-Karten, Einstellungen, Fokus, Klickdurchleitung
und Auflösungen 1024×768, 1920×1080 und 3440×1440 bei 100/150/200 % HUD-Größe.
Native Layoutfixtures ersetzen keine verbundene Spielsitzung.

Nach separatem Startauftrag im Sandbox-Client prüfen:

1. Testmeldung bei offenem und geschlossenem Forge, im Orbit und auf einem Planeten.
2. Fundorte vormerken und Merkliste ändern; mehrfach klicken, ohne Meldungsflut.
3. CSV und Diagnosebericht exportieren, Forge sofort schließen: Ergebnis bleibt sichtbar.
4. „Nur wichtige“ übernehmen: Bestätigungen aus, Testmeldung und echte Fehler sichtbar.
5. Neben einer nativen Remnant-/Spielmeldung weiterfliegen, Komponenten bedienen
   und in Chat/Suche tippen. Keine verlorenen Eingaben oder verdeckten Komponenten.
6. Bei langer Fehlermeldung Detailansicht öffnen/schließen; nach Szenen-/Pilotenwechsel
   keine alten Exportmeldungen und keine verwaisten Widgets.

Der bestehende Benutzerclient wird bei der Vorbereitung nicht beendet oder verändert.
Prüfergebnisse und Paketpfad stehen im privaten Staging-Beleg, sobald alle Gates bestehen.
