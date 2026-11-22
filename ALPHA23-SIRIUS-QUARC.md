# Enhanced alpha.23 – Sirius-Quarc und Bauplanfortschritt

Enhanced 0.2.0-alpha.23 / Sequenz 104 für Spielversion 1002133.
Core bleibt alpha.17 / Sequenz 16.
Die zuvor verworfene Schiffskonfigurationsansicht und deren Erstcache sind nicht
Bestandteil dieses Standes. Starterrevision 17 bleibt erhalten.

## Bedienung

- Auf der Sirius-Sternkarte zeigt ein kleines Häkchen eine bestätigte
  Quarc-Freigabe an. Es verändert keine Planetenfarbe und fängt keine Klicks ab.
- Im ausgewählten Planeten stehen zuerst `Quarc: freigeschaltet`,
  `Quarc: nicht freigeschaltet` oder `Quarc: Status unbekannt`.
  Planetendetails, Baupläne und Sprungfenster bleiben erhalten.
- Unter **Forge → Anzeige → HUD & Grafik → Sirius: Quarc-Freigaben anzeigen**
  lässt sich diese Ergänzung ausschalten. Übernehmen/Verwerfen gelten wie bisher.
- Gelbe Sirius-Bauplaneinträge enthalten bekannte Teilezahlen, etwa
  `Sirius-Blaster (2/6)`, in Sternkarte und Orbit. Grüne und weiße Einträge bleiben
  unverändert. Ein unbekannter Nenner wird nicht durch eine Schätzung ersetzt.
- Die bisherige Gruppierung nach Teilezahl (18/14/12/5), Namenssortierung und
  der Merkliste-Hinweis bleiben erhalten. Nur bekannte gelbe Teilezahlen werden ergänzt.

Die Freigabe bestätigt keinen momentan auf der Oberfläche liegenden Quarc.
Der bekannte Quarc-Typ eines antiken Planeten ist ebenfalls keine Freigabe.

## Daten und Grenzen

`SiriusQuarc` liest ausschließlich das bereits von der Originalkarte geladene
`ClanExplorationMemory_<clan>` aus `gq.GK`. Die Zuordnung erfolgt über die
numerische `singularityzoneid`, nicht über einen Planetennamen. Nur ein explizites
`quarcvisible_<id>` wird als positiv oder negativ bewertet. Ein fehlendes Feld
bleibt unbekannt, auch wenn der Originalgetter dafür `false` liefert: Die
Bedeutung fehlender Schlüssel im realen Anfangssnapshot ist noch nicht bestätigt.
Exploration, Quarc-Typ und antiker Planet sind keine Ersatzbeweise. Fehlen die
Spielerdaten/der Clan oder dessen empfangener Cache, bleibt beim ausgewählten
Sirius-Planeten die Zeile `Quarc: Status unbekannt` sichtbar. Ohne angemeldeten
Piloten, bei geschlossener Karte, Wurmlöchern und kollabierten Planeten entfällt sie.

Die lokale Kartenübersicht wird maximal viermal pro Sekunde gelesen; die
Projektion folgt der Kamera. Ein Wechsel von Auswahl oder Freigabestatus
aktualisiert die Detailzeile unmittelbar, unabhängig vom Sprungfenster-Takt.
Maximal 128 Markierungen; nahe beieinanderliegende und außerhalb des Bildes
liegende Markierungen werden unterdrückt. Aufräumen bei Karten-/Piloten-/Clanwechsel,
Szenenende, Kollaps und Abschalten. Keine zusätzliche Zustandsdatei.

`SiriusBlueprints` verwendet genau den vorhandenen, an den aktuellen Piloten
gebundenen `HudBlueprints`-Snapshot. Zwei fingerprintgeschützte Formatierungs-
Aufrufstellen werden nur in Enhanced umgebunden. Der Core-Helfer inklusive
seines bisherigen Ladeverhaltens bleibt unverändert. **Zusätzliche Serveraufrufe
dieses Features: null.** Die bereits existierenden Abfragen der Originalkarte und
der bisherigen BP-Farbanzeige bleiben bestehen.

## Diagnose und Abnahme

Der lokale Forge-Diagnoseexport enthält `sirius-quarc.json`: Datenverfügbarkeit,
Anzahl bekannter/freigegebener/gesperrter/unbekannter Planeten, Auswahlstatus,
Bindungswechsel und Fehlerzähler. Maximal 64 geänderte Zustände im Speicher;
kein automatischer Dateiexport. Keine Namen, Konto-/Clan-/Planeten-IDs oder Positionen.
Schema 2 trennt zusätzlich Karte und Orbit: Anzahl der Formatteraufrufe, gelistete
und zugeordnete BPs, gelbe Einträge, ausgegebene Teilezahlen, fehlende Gesamtzahlen
und Merkliste-Ausgabe. Fehlt der Snapshot, lädt er noch oder gehört er zu einem
anderen Piloten, wird der Grund explizit protokolliert; die Zähler bei `fallback`
sind keine Aussage über den Besitzstand. Technische Fehler enthalten Bereich und
Exceptionklasse, keine Meldungen oder Stackargumente. Markerfehler löschen keinen
gültigen Quarc-Text. Der Export ist auch ohne vorangehende 120-Sekunden-Aufnahme möglich.

Automatisierte Prüfungen verwenden echte Spielmodelle mit künstlichen Daten und
die native MyGUI auf D3D9/D3D11. Sie ersetzen keine Live-Freigabe nach einer
Clanmission. Im späteren Sandbox-Test prüfen:

1. Sirius-Karte mit/ohne empfangene Freigabedaten, schnelle Planetenauswahl.
2. Bekannte Freigabe und Zustandswechsel nach einer Clanmission, auch durch
   ein anderes Mitglied. Fehlendes Feld bleibt ausdrücklich unbekannt.
3. Ring 5 mit bekanntem Quarc-Typ ohne Freigabe: kein falsches Häkchen.
4. Kamera, Zoom, Planetenklicks, Kollaps, Clan-/Pilotenwechsel, Karte schließen.
5. Gelbe BP-Einträge mit Teilbesitz und langen Namen in Karte und Orbit;
   vollständige/unbekannte BPs und fehlende Gesamtzahl.
6. BP-Gruppierung 18/14/12/5 und Namenssortierung vergleichen. Ein BP auf der
   Merkliste erzeugt den bisherigen Hinweis genau einmal, auch beim Planetenwechsel.
7. Mit sichtbarer Planetenliste und Detailfenster Kamera/Zoom ändern: freigegebene
   Planeten bleiben markiert, Markierungen verdecken keine der beiden Listen.
8. Einstellung übernehmen/verwerfen und lokale Diagnose exportieren. Nach Besuch
   beider Ansichten müssen Karte und Orbit getrennt als beobachtet erscheinen;
   fehlende Snapshots/Gesamtzahlen und Quarc-Daten haben nachvollziehbare Gründe.

Der Nutzer hat den Enhanced-D3D11-Sandbox-Test bestätigt. Die aufgeführten
Einzelfälle sind eine Prüfliste und keine Zusage vollständiger Serverabdeckung.
Ein nativer Float-/Integer-Castfehler bei sichtbaren Kartenpanels wurde
reproduziert und behoben. Modell- und Markierungsfehler sind getrennt behandelt.
