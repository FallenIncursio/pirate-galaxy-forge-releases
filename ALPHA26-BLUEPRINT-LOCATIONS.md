# Enhanced alpha.26 – Bauplan-Fundorte

Bestätigter Enhanced-D3D11-Sandbox-Test (R4), Spielversion 1002133.
Veröffentlichung freigegeben; Core bleibt alpha.17 / Sequenz 16.
Der laufende Nutzerclient bleibt geöffnet.

Bauplan-Fundorte mit Planet, Sternsystem, Gegner, Level und Sammelstand. Ein
vorgemerktes Suchziel erscheint auf der nativen Planetenkarte; Gegnericons und
Filter erleichtern die Suche. Alle Bilder lokal, keine zusätzlichen Serverabfragen.

## Test- und Umsetzungshistorie

## R4 gestartet, 23.11.2026

D3D11-Start auf Nutzerauftrag mit Profil-/Anmelde-/Mixerübernahme geprüft.
Sirius-Orbit und gefüllte Tangens-Fundortkarte sichtbar; vollständige räumliche
Abnahme bleibt offen. R4/PID 4004 jetzt offen lassen. Nichts veröffentlicht.
Beleg: distribution/tests/blueprint-locations-alpha26-r4-launch.json.
Die folgenden R3-Erhaltungsangaben beschreiben die abgeschlossene Vorbereitung.

## R4: Leere Fundortkarten nach dem R3-Start

Der R3-Start war technisch erfolgreich (D3D11, Profil-/Anmeldeübernahme und
Serververbindung), die Fundortansicht fiel aber in der Nutzersitzung aus.
Der exportierte Bericht bestätigt 1.333 BPs, 1.387 Bereiche und einen registrierten
Atlas. Deshalb ist R3 keine erfolgreiche Ingame-Abnahme des Features.

Die native Gegenprobe mit unverändertem R3-JAR zeigt: Ohne das registrierte Archiv
`r-573915839` wirft das direkte Setzen von `mantissystem.jpg` im Fundortkartenaufbau
eine RuntimeException. Mit dem Archiv besteht dieselbe Probe. Die vorherigen
GUI-Prüfungen hatten alle Archive verfügbar und deckten diese Situation nicht ab.

R4 verwendet für alle neun Systembilder lokale Atlaszellen (Indices 89–97),
generiert aus den SHA-256-geprüften Originalbildern der Spielbasis 1002133.
Die Originalnamen und Archive bleiben im Herkunftsmanifest; zur Laufzeit werden
keine fremden Systemarchive geladen und keine zusätzlichen Serverabfragen gemacht.
Die neun `system-*.jpg`-Quelldateien liegen zusammen mit Gegner-/Planetenbildern im
zentralen `PGFORGE_REFERENCE_ASSETS`-Cache. Zum Wiederaufbau die in `enemy-icons.json`
angegebenen Einträge aus der gepinnten, XOR-0x55-kodierten Spielarchivbasis lesen,
SHA-256 prüfen und unter dem jeweiligen `file`-Namen ablegen. `--fetch` lädt nur
Wiki-Grafiken; Originalgrafiken werden nicht aus dem Netz nachgeladen.

Ein nicht lesbares Icon wird ausgeblendet; Fundorttext, Level, Kartenknopf und
Detailwechsel bleiben erhalten. Derselbe fehlgeschlagene Atlas wird nicht in jeder
Karte erneut geladen. Diagnoseformat 3 enthält Fehlerphase und Exception-Klasse,
keine Fehlermeldung mit lokalen Pfaden oder Kontodaten.

Native Regression: alle neun Original-Systemarchive vor den Fundortprüfungen
abmelden; zusätzlich den lokalen Atlas im isolierten Testverzeichnis vorübergehend
unzugänglich machen. Quelle, Map-Aktion, Detailwechsel und stabile Folgebilder prüfen.
Core-Spielbytes/138 Helfer/native Inputs/Startvorlagen und sechs unabhängige
Updaterdateien gegen R3 geprüft: unverändert. R3-Client bleibt geöffnet; R4 ist ein
separater privater Kandidat. Kein Commit, Push, Upload oder Kanalwechsel.

# Enhanced alpha.26 – Bauplan-Fundorte

Privater Sandbox-Kandidat, Spielversion 1002133. Nicht veröffentlicht.
Core bleibt alpha.17 / Sequenz 16; Enhanced alpha.25 / Sequenz 106 bleibt öffentlich.
Der laufende Nutzerclient wird bei der Vorbereitung nicht geschlossen.

Der Datenumfang stammt aus R3; R4 behebt den oben dokumentierten Anzeigefehler.
Der laufende R3-Client wird nicht ersetzt. Der neue private Kandidat benötigt
einen eigenen Sandbox-Startauftrag.

## Bedienung

Unter **Forge → Baupläne** einen Bauplan auswählen. **Fundorte** zeigt den
Planeten mit dem passenden Planetensymbol und einer separaten Systemzeile mit
dem originalen PG-Sterntorbild. Danach folgen
Gegnertyp, bekannte Gegnerlevel und der eigene Sammelstand. **Details** erhält
die bisherigen Informationen. Lange Namen werden anhand der nativen Schrift
umgebrochen, die Fundortliste scrollt unabhängig von der Bauplanliste.

**Hier erhältlich** begrenzt die vorhandenen Such-, Typ-, Fortschritts-, System-
und Merklistenfilter auf die aktuelle reguläre Planetenoberfläche. Der CSV-Export
nutzt dieselbe Auswahl über alle Seiten. Außerhalb einer bestätigten Oberfläche
steht der Filter nicht neu zur Verfügung; ein aktiver Filter kann ausgeschaltet
werden. Das System des Bauplans bezeichnet weiterhin die Technologie, das System
eines Fundorts dagegen dessen tatsächliche Position: Erebos gehört zu Oort.

Bei belegten Kartenpositionen gibt es **Auf Karte zeigen** auf der passenden
Oberfläche, sonst **Vormerken**. Ein vorgemerkter Bauplan pro Pilot wird lokal
gespeichert. Seine bekannten Fundstellen erscheinen mit passendem Gegnerbild und
lesbarer Levelzahl auf dunklem Hintergrund in der nativen Planetenkarte.
Patrouillen behalten einen dezenten Gebietsrahmen. **Ausblenden** entfernt das Suchziel.
Ein neues Ziel ersetzt das vorherige. Orbit, instanzierte Missionen und andere
Planeten erhalten keine übertragenen Markierungen. Die vorhandenen Live-Symbole
und die eigene Position bleiben der nativen Karte überlassen.

Unter **Forge → Anzeige → HUD & Grafik → Bauplan-Fundstellen auf der Karte**
kann die Kartenebene deaktiviert werden. Änderungen werden erst mit Übernehmen
gespeichert; Verwerfen erhält den bisherigen Wert. Die Fundortliste bleibt lesbar.

## Daten und Grenzen

- Fundortindex mit 1.333 Bauplänen, 20 statischen Planeten plus fünf Sirius-Ringen:
  alle 1.323 bisherigen Scanner-Baupläne sowie zehn im Quellenimport wiedergewonnene
  Fundorteinträge. Native Schlüssel und bekannte Aliaszuordnungen dienen als
  Identität; keine unscharfe Zuordnung übersetzter Namen. Der bestehende Scanner-
  Regelbestand bleibt erhalten; diese Ergänzung betrifft die Fundortansicht.
- Unbekannter Sammelstand bleibt unbekannt. Ein nicht übermittelter Profileintrag
  wird nicht als null Teile ausgegeben. Unbekannte Gegnerlevel bleiben ausdrücklich
  unbekannt; der interne Platzhalter 1–150 wird nicht als Levelbereich angezeigt.
  Sind nur die Level der zugeordneten Karte bekannt, steht ausdrücklich
  **Kartenlevel** davor. Dies ist keine neue Drop-Levelbeschränkung.
- 1.387 ungefähre Referenzbereiche auf 18 Planeten, verknüpft mit 664 Bauplänen.
  Jeder Bereich ist ausdrücklich dem Bauplan, Planeten und Gegner zugeordnet;
  gleiche Level oder ähnliche Namen allein erzeugen keine Kartenmarkierung.
  Unter anderem besitzt Tau Ceti Tsunami Angriffsladung nun Berserker-Fundstellen
  auf Erebos. Fehlende und widersprüchliche Positionen bleiben weiterhin offen.
- Die Quelleninventur umfasst mehr Daten als die freigegebene Laufzeitauswahl:
  ungeklärte native Identitäten, Sondervarianten, Bossgruppen und unlesbare
  Levelangaben erzeugen keine neuen Marker. Alle verwendeten Gegner besitzen
  ein zugeordnetes Bild; 37 zusätzliche native Namensschlüssel sind hinterlegt.
- Sirius zeigt Ring und Gegnerklasse, keine erfundenen festen Positionen oder
  aktuelle Dropbestätigungen für einen bestimmten dynamischen Planeten.
  Giza, Soris und Amarna bleiben ausgenommen.
- Suchbereiche sind statische Referenzstellen, keine Live-Gegner, Spawnmeldung,
  Dropgarantie oder Prozentchance. Seltene Varianten werden nicht auf gewöhnliche
  Gegnerstellen übertragen.

Quelle: [Prelude-Planetenübersicht](https://prelude-myzen.co.uk/PirateGalaxy/Planets.html)
und der bereits versionierte Scannerkatalog. Wegen des abgelaufenen TLS-Zertifikats
der Quellseite erfolgte die manuelle Kartenprüfung über deren öffentliche
HTTP-Adresse; die Zertifikatsprüfung wurde nicht deaktiviert. Quellenbilder und
originale Minimap-Dateien sind in `catalog/map-observations.json`,
`catalog/source-manifest.json` und `catalog/map-calibration.json` durch SHA256 referenziert.
Wiki-Kartenbilder werden nicht in das Paket kopiert. Die 69 kleinen Gegnerbilder
und 20 Planetensymbole aus Prelude werden als ein lokal mitgelieferter Atlas
aufbereitet. Neun originale Systembilder stammen aus den vorhandenen Spielressourcen;
Sirius-Ringe erhalten kein erfundenes festes Planetensymbol.
Bildrechte: Pirate Galaxy / Splitscreen Studios; Referenzzusammenstellung von
Redthorne / Prelude PG Wiki. URLs, Einzelhashes und Atlas-Hash stehen in
`enemy-icons.json`; Rohbilder verbleiben außerhalb von Git. Die Originalkarten und
Wiki-Karten wurden auf Ausschnitt und Orientierung verglichen. Die räumliche Abnahme im Spiel
bleibt erforderlich, bevor die Kartenbereiche als live bestätigt gelten.

## R3: fehlende Angaben und passende Icons

Die Kartenlegende verwendet teils Bild-/Modellpräfixe, die nicht mit der
Fraktionsangabe der BP-Tabelle übereinstimmen. Sieben geprüfte, ausdrücklich
planetengebundene Zuordnungen stehen in `catalog/layer-identities.json`:

- Erebos: `AncBaiter` → Mantis-Köderer, `AncDefender` → Mantis-Verteidiger.
- Calon: `MagnetTrap` → Antike Magnetfalle.
- Erde, Mars und Mond: `ImpHarvester` → Mantis-Sammler.
- Erde im Unruhezustand: `Pyro` → Antiker Pyro.

Das sind geprüfte Verbindungen zwischen den veröffentlichten Referenzquellen,
keine neu vom Server bestätigten Spawn- oder Fraktionsdaten. Originale Legenden-
identität, Kartenhash und genaue BP-Quellzeilen bleiben im Katalog erhalten.
Die Erzeugung bricht ab, sobald diese Quelle einen konkurrierenden normalen
Fraktionseintrag für denselben Planeten/Gegnertyp enthält. Mehrdeutige Varianten
auf Vénar werden nicht zusammengelegt. Keine globale Zuordnung allein nach Name.

Damit erhalten 21 weitere Baupläne Fundbereiche (+51 Bereiche). Tau Ceti Tempo
Beschleuniger (Quellname „Tau Ceti Turbo“) bekommt acht Köderer-Bereiche auf
Erebos und **Kartenlevel 97–100**. Die BP-Tabelle nennt weiterhin keine explizite
Drop-Levelbedingung. Blaue 97/98- und 99/100-Baupläne behalten ihre genaue Auswahl.

Jeder der 20 statischen Planeten besitzt ein eigenes, vollständig skaliertes
Planetensymbol. Das separate Systembild stimmt mit dem Aufenthaltsort überein:
Baumar/Mizar und Erebos/Oort; es wird nicht aus der BP-Technologiestufe abgeleitet.
Die Bildzeilen richten sich nach der gemessenen Textgröße. Atlas und Quellen
bleiben gepinnt und lokal; es gibt keine Internetabrufe durch den Client.

## Technik und Diagnose

`BlueprintSources` lädt kompakte, offline erzeugte Quellenzeilen und explizite
BP/Gebiets-Verknüpfungen. Native und Faction-Aliase derselben Gegneridentität
werden zusammengeführt; Level-Lücken, Fraktionen und Seltenheitsbedingungen bleiben
erhalten. Versionierte TSV-Dateien und der deterministische Offline-Generator sind
im Enhanced-Quellmanifest registriert. Neue Klassen und Ressourcen fehlen in Core.

Für lokale Builds `PGFORGE_REFERENCE_ASSETS` auf den Ordner mit den 89 gepinnten
Quellbildern setzen. Der Atlas wird offline erzeugt und gegen den geprüften SHA256
verglichen. Ein fehlender Cache kann ausdrücklich mit
`python -m tools.forge.blueprint_assets --cache <Ordner> --fetch` aufgebaut werden;
auch dabei muss jeder Download dem versionierten Einzelhash entsprechen.
Die Bilddaten werden einmal pro Prozess aus dem Paket bereitgestellt und in einer
festen Cachedatei ersetzt; Kartenwechsel erzeugen keine weiteren Bilddateien.

Die Kartenebene läuft auf dem bestehenden UI-Takt, verwendet keine dauerhaften
nativen Zeiger und baut bei unverändertem Ziel/Map-Layout keine Widgets neu.
Zonen-, Piloten-, Karten- und Einstellungswechsel räumen ihre eigenen Widgets auf.
Das Öffnen wählt ausschließlich die bereits registrierte native Planetenkarte.
Keine zusätzlichen Spielserverabfragen und keine Webzugriffe im Client.

Bei der nativen Abnahme aufgedeckt und im Enhanced-Dialog korrigiert: HUD-Größe und
Discord-Status verwenden beim Übernehmen jetzt ebenfalls begrenzte Wiederholungen
bei `AccessDeniedException`. Die jeweiligen Besitzer speichern vor der Übernahme
oder stellen ihren alten Zustand wieder her; andere Fehler werden nicht wiederholt.
Ein dauerhaft gesperrtes Ziel führt weiterhin zu einem Fehler, nicht zu einer
unbelegten Erfolgsmeldung. Gemeinsamer Einstellungsspeicher und Core bleiben erhalten.

Der bereinigte Forge-Diagnoseexport enthält `blueprint-locations.json`: begrenzte
Grundzähler, Kataloggröße und Zahl der gezeichneten Marker. Keine Pilot-/Konto-IDs,
Positionen, Chattexte oder rohen Serverantworten. Der Export bleibt lokal.

## Sandbox-Abnahme

1. Verschiedene lange Bauplannamen auswählen, Fundorte/Details wechseln und eine
   lange Fundortliste scrollen. Sammelstand mit der bestehenden Liste vergleichen.
2. Auf Erebos Level-97/98- und Level-99/100-Aggrobomben vergleichen; nur die jeweils
   passenden Sprengschiff-Fundstellen dürfen markiert sein.
3. Einen passenden Calon-Bauplan vormerken, Oberfläche betreten und Karte öffnen.
   Orientierung und Suchbereiche mit der tatsächlichen Umgebung vergleichen.
4. Karte schließen/öffnen, Orbit und Planeten wechseln, Suchziel ersetzen und
   ausblenden. Keine alte Ebene oder Legende darf übrig bleiben.
5. „Hier erhältlich“ mit Suche und Merkliste kombinieren und CSV exportieren.
6. Einstellung verwerfen/übernehmen; Clientneustart und getrennte Piloten prüfen.

Automatisierte Prüfung und konkrete Artefakte:
[Prüfstand alpha.26](RELEASE-STATUS-0.2-alpha.26.md).
Gegenüber dem 32-Bit-Client eine lokale Enhanced-Zusatzansicht; keine neuen
Leistungs-, Sicherheits- oder Dropchancen-Zusagen.
