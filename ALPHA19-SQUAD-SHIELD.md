# Enhanced alpha.19: Schutzpunkte in der Staffel

Enhanced-Update auf Spielbasis **1002133**, ausgehend von alpha.18.
Der Nutzer hat den D3D11-Sandbox-Test am 21.11.2026 bestätigt und die
Veröffentlichung beauftragt. Enhanced-Kanal: Sequenz 100; Core bleibt alpha.17.

## Anzeige und Bedienung

Eine blaue, drei logische Pixel starke Umhüllung liegt außerhalb des grünen
Staffel-Lebensbalkens. Die gesamte Umhüllung wird von rechts nach links gekürzt;
bei halber Reserve bleiben ihre linke Kante und die linke Hälfte der oberen
und unteren Kante sichtbar. Lebenspunkte und Schutzreserve bleiben unabhängig.
Die vorhandene Fenstergröße, Zeilenhöhe und ursprünglichen Klickziele bleiben
erhalten. Die Umhüllung nimmt weder Maus- noch Tastaturfokus an.

Unter **Forge → Anzeige → Kampf & Effekte → Staffel: Schutzanzeige**:

- **Aus:** bisherige HP-/Effektdarstellung.
- **Umhüllung:** zusätzliche blaue Restkapazität; bisherige Zeit-/Aktivitätslabels.
- **Umhüllung + Prozent:** zusätzlich die Restkapazität des jeweiligen Schild- oder
  Schutzeffekts unter seinem Symbol. Standardwert für neue und bestehende Profile.

Die übergeordnete Option „Staffel: HP und Effekte“ bleibt maßgeblich.
„Übernehmen“ speichert `squad.shieldDisplay` im vorhandenen Einstellungsspeicher;
„Verwerfen“, bloßes Aufrufen und Schließen speichern keine Entwurfsänderungen.
Unverwandte Optionen und Positionen bleiben erhalten.

Der Tooltip des Effekts zeigt bekannte aktuelle und Referenzpunkte sowie eine
gegebenenfalls bekannte Restlaufzeit. Prozent und Zeit sind getrennte Größen.
Unter einem Prozent Restkapazität erscheint **<1%**, nicht 0%. Ist die Kapazität
unbekannt, bleibt das bisherige Zeit-/Aktivitätslabel erhalten und der Tooltip
nennt die fehlenden Punkte. Es gibt keine erfundene volle oder leere Reserve.

## Daten und Lebensdauer

- Ausschließlich bereits empfangene native `uu`-Effekte aus dem effektiven
  `tk`-Container: `vO()` liefert aktuelle Punkte, `vP()` den Referenzwert und
  `vQ()` die Schild-/Schutz-Unterscheidung. Ausrüstung, Effektnamen und vergangene
  Zeit liefern keine Kapazität. Andere Schadensreduktionen zählen nicht als Schild.
- Die originale Zielanzeige berechnet ihren Balken ebenfalls aus aktuellem Wert
  und Referenz. Der originale eigene HUD-Beobachter `anx` verarbeitet mehrere
  Reserven gemeinsam. Forge übernimmt diese Grundidee, behandelt Neuanwendungen
  aber ausdrücklich als Ersatz der verbrauchten Reserve desselben Produzenten.
- Die Umhüllung zeigt die gemeinsame Reserve; der Prozentwert am Symbol gehört
  ausschließlich zu diesem Effekt. Der native Container entscheidet über stärkere
  und untergeordnete Effekte; dieselbe Instanz wird nie doppelt gezählt.
- Eine nachweislich verbrauchte Reserve bleibt während überlappender Effekte im
  Referenzwert, damit das Entfernen des leeren Effekts den Balken nicht auffüllt.
  Ein erneuter Effekt desselben Produzenten ersetzt diese verbrauchte Referenz.
  Ein mit positiven Punkten entfernter Effekt wird nicht als verbraucht geraten.
  Ohne aktive Reserve, nach Containerreset oder bei neuer Schiffbindung wird
  die Historie verworfen. Historie und aktuelle Reserven sind begrenzt.
- Ein unbekannter Referenzwert macht die gemeinsame Kapazität unbekannt.
  Einzelne bekannte Effekte behalten ihre eigenen Prozentwerte.
- Die vorhandene lokale Staffelaktualisierung läuft alle 200 ms; die bestehende
  Szenenliste wird höchstens einmal pro Sekunde neu zugeordnet. **Zusätzliche
  Spielserveraufrufe: 0.** Keine Zielauswahl, Scans oder automatischen Spielaktionen.
- UI-Arbeit bleibt auf dem bestehenden HUD-Thread. Zustände sind an den
  effektiven Schiffbeobachter gebunden; keine dauerhaft gespeicherten nativen
  Widgetzeiger. Geschlossene/fehlende Fenster, Staffel-, Piloten-, Schiffs- und
  Szenenwechsel verwenden die bestehenden Aufräumwege.
  Ein Wechsel der Szene, Zone oder des eigenen Schiffes verwirft die Bindungen
  sofort, ohne auf die nächste Ein-Sekunden-Szenenabfrage zu warten.

## Grafik und Editionsgrenze

Die Umhüllung verwendet den bereits geladenen Originalatlas `PG_core.png`,
Texel 614/264 (RGB 112/187/249). Keine zusätzliche Bilddatei, Shader- oder
DLL-Änderung. Prozentbeschriftung und vollständige Effektliste verwenden dieselbe
Wertauswertung. Alle Quellen sind ausschließlich unter Enhanced deklariert.

Gegenüber dem 32-Bit-Client ist dies eine zusätzliche Staffelanzeige vorhandener
Effektdaten. Es ändert keine Schutzmechanik und behauptet keine serverseitig
garantierte Datenversorgung für entfernte oder nicht anvisierte Schiffe.

## Prüfung und verbleibende Sandbox-Abnahme

Automatisierte Prüfungen verwenden echte Original-Effektklassen und native
PG-Widgets mit isolierten Beispieldaten: current/reference, Wiederauffüllen,
effektive Ersetzung und Rückkehr, Aufbrauchen vor Entfernen, mehrere Reserven,
fehlende Daten, Reset/Abmelden, Apply/Discard, alle drei Modi, Prozenttextbreite,
Umhüllungsgeometrie, ursprüngliche Klickziele und Wiedererzeugung der Widgets.
D3D9 und D3D11 werden getrennt bei 100/150/200 % HUD geprüft.

Der Nutzer hat den Sandbox-Test mit „funktioniert“ bestätigt. Diese Rückmeldung
und die synthetischen Prüfungen sind keine vollständige Replikationsmatrix für
alle Schiffe und Entfernungen. Weiterführende Spielprüfungen:

1. Ein Staffelmitglied ohne Zielauswahl schützen und Schaden beobachten;
   anschließend mit der originalen Zielanzeige vergleichen.
2. Schutz bei vorhandener eigener Schildreserve, vollständiges Aufbrauchen,
   Auffrischen und stärkerer Ersatz. Zuordnung von Gesamtbalken und Einzeleffekt.
3. Staffelbeitritt/-austritt, Tod/Wiederbelebung, Landung/Orbit, Sichtbereichs-
   und Planetenwechsel: keine übernommenen Werte eines vorherigen Schiffes.
4. Live-Einstellung, HUD-Skalierung, ursprüngliches Anklicken des Staffelmitglieds
   und uneingeschränkte Komponententasten.

Konkrete Build-, Paket- und Testbelege: [Release-Prüfstand](RELEASE-STATUS-0.2-alpha.19.md).
