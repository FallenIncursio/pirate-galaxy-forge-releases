> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Alpha.9: Korrekturen nach dem Calon-Test

Privater Teststand für Core und Enhanced vom 17.11.2026. Nicht veröffentlicht.

**Folgestand:** Der Nutzer bestätigte weiter bestehende Ruckler. Die neue Aufnahme
und Vegetations-/Allokationskorrekturen stehen in [ALPHA9-CALON-READBACK.md](ALPHA9-CALON-READBACK.md).
Die folgenden Prüfstände bleiben historische Nachweise ihrer jeweiligen Bytes.

## Befund und Änderung

Die bestätigte Calon-Flugaufnahme enthält echte Framezeitspitzen. Im separaten
externen 30-s-Lauf: 6.622 Frames, rund 221 FPS im Mittel, P99 16,18 ms und
Maximum 56,34 ms. In der internen Aufnahme überschneiden sich drei lange
Frames mit GC-Pausen von 29,65–32,61 ms. Weitere Spitzen liegen im Update,
darunter ein einzelner Ausreißer von rund 297 ms. Die gemessenen Terrainqueues
und das Forge-HUD erklären diese Spitzen nicht. Die beiden Aufnahmen sind
getrennte Läufe; ihre Frames dürfen nicht direkt gleichgesetzt werden.

`com.splitscreen.dg.gQ()` aktualisiert die Wasser-Rendertexturen anhand eines
Framezählers. `qG` ist die Anzahl übersprungener Frames, also ergibt sich ein
Update alle `qG + 1` Frames. Bei 240 statt 60 FPS vervierfacht sich diese Arbeit.
Die Methoden `aD(String)` und `aC(String)` zeichnen Reflexion beziehungsweise
Brechung synchron über `RenderTexture.update()` im Spiel-Update. Dieser Pfad
fällt auch in den Methodenstichproben der Aufnahme auf. Das beweist noch nicht,
dass er jeden einzelnen langen Frame verursacht.

Der neue gemeinsame Helfer `WaterCadence` begrenzt die Berechnungen zeitlich auf
die 60-Hz-Referenz des Clients: `(qG + 1) / 60` Sekunden. Der ursprüngliche
Framezähler und die Ein-/Ausschaltbedingungen bleiben erhalten, sodass niedrige
FPS keine zusätzliche Wasserarbeit erzeugen. Jeder Wassercontroller hat seine
eigene Uhr; nach einer Pause wird einmal aktualisiert, ohne Nachholschleife.
Der Test bei 240 FPS und Intervall 0 zählt 720 statt 2.880 Updates in zwölf
Sekunden. Das ist ein Aufrufzähler im Test, keine gemessene FPS-Verbesserung.

Die Transformation prüft die Original-/Eingangshashes, Konstruktorform,
Aktivierungsverzweigung, beide Renderaufrufe und die genaue Anzahl der Änderungen.
Wassertexturen, Farbberechnungen, Reflexionskameras, Spielbewegung und Serverdaten
werden dabei nicht ersetzt. Die gemeinsame Java-Korrektur gilt für D3D11 und D3D9.

## Sichtbarer D3D11-Start

Der erste alpha.9-Test ließ auf dem realen Bildschirm das große Ladebild stehen,
obwohl eine Aufnahme des Fenster-DC bereits die Anmeldung zeigte. Mit Blt waren
Anmeldung und Spiel sichtbar. Die neue automatische Auswahl erkennt jetzt den
AWT-Canvas beziehungsweise einen AWT-Vorfahren des Fensters, auch mit dem
Sandboxie-Klassenpräfix. Dieser Fenstertyp benutzt Blt automatisch, ebenfalls
nach Wiederherstellung des Grafikgeräts. Der manuelle Prozessparameter ist dafür
nicht mehr erforderlich. Andere geeignete Hosts behalten den geprüften Flip-Pfad.

Das entspricht der [DXGI-Dokumentation zur Mischung von GDI und Flip im selben Fenster](https://learn.microsoft.com/en-us/windows/win32/direct3ddxgi/dxgi-flip-model).
Der neue Offline-Test erzeugt einen echten Java-Canvas und prüft zwölf wechselnde
Bildschirmfarben mit `Robot.getPixelColor`, einschließlich MSAA/Gamma, Resize und
Gerätewiederherstellung. Er liest keine fremden Fenster oder Spielinhalte aus.
Die vorherige Renderer-Version scheitert an der Modus-Gegenprobe. Diese Gegenprobe
weist den falschen Modus nach; sie behauptet keine eigenständige Reproduktion des
Ladebild-Hängers. Beleg: `distribution/tests/calon-alpha9-presentation-fix.json`.

Private Startkopien im `versions/<version>`-Layout verwenden nun automatisch
den benachbarten `data`-Ordner. Dadurch stimmt der vom vollständigen
Credential-Reader benötigte Verzeichnisvertrag. Flache Wegwerfprüfungen behalten
ihren getrennten Zustand. Profilübernahme wird bei einem neuen Spielstart erneut
gegen die dann aktuelle Sitzung geprüft.

## Genauere Folgeaufnahme

Die freiwillige Rucklerdiagnose erfasst zusätzlich:

- Dauer und Anzahl tatsächlicher Wasser-Renderaufrufe, getrennt nach Reflexion
  und Brechung; deaktivierte Durchläufe werden nicht als Zeichnen gezählt.
- Vegetations-Updates und zeitlich zuordenbare Methodenstichproben.
- Gedrosselte JFR-Allokationsstichproben mit geschätztem Gewicht, Klasse,
  oberster Methode und Spielthread-Markierung. Keine Objektinhalte oder Threadnamen.

Die beiden neuen Stichprobenlisten enthalten höchstens je 10.000 Zeilen; ausgelassene
Einträge werden gezählt. Roh-JFR bleibt temporär und wird entfernt. Attach-Schutz,
30-s-Grenze und lokaler Export bleiben erhalten. Messphasen können verschachtelt
sein und dürfen nicht addiert werden. Allokationsgewichte sind Stichprobenschätzungen,
keine exakte Zählung jedes Objekts. Die Diagnose selbst verursacht zusätzliche Arbeit.

Die drei GC-Pausen sind belegt, ihre verursachenden Allokationspfade wurden in der
vorherigen Aufnahme nicht erfasst. Der neue Bericht ermöglicht diese Zuordnung.
Eine Beseitigung der GC-Pausen oder sämtlicher Mini-Ruckler ist noch nicht bestätigt.

## Prüfung und nächste Abnahme

Die Wasserprüfung führt auch die tatsächlich gepatchten Aktivierungszweige aus;
sie umfasst 20/30/60/120/144/165/240 FPS, wechselnde Intervalle, unregelmäßige
Frames, Pause, Uhrüberlauf und neue Controller. Beide Editionen werden vollständig
gebaut und mit den konkreten JAR-/DLL-Hashes geprüft. Der aktuelle Gesamtbeleg steht
in `distribution/tests/editions-0.2-alpha.9-calon-fix-readiness.json`.

Als Nächstes dieselbe Calon-Strecke mit den bisherigen Einstellungen zuerst ohne
Aufzeichnung fliegen. Anschließend eine 30-s-Diagnose erstellen, falls Ruckler
bleiben, und Wasserzeiten/Allokationen den betroffenen Frames zuordnen. Ein neuer
Original32-Spielvergleich, andere GPUs, Wine, exklusives Vollbild und Alt-Tab sind
nicht abgenommen. Öffentliche Releases und Updatekanäle bleiben unverändert.
