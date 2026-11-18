# Alpha.9: Rucklerdiagnose und D3D11-Ausgabe

Aktuelle Veröffentlichung und Testgrenzen: [Release-Prüfstand](RELEASE-STATUS-0.2-alpha.9.md).
Der folgende Text dokumentiert die Implementierung und damalige Vorbereitung.

Aktueller GC-/Update-Folgestand: CSV enthält zusätzlich `layout_ns`,
`gui_tick_ns` und Aufrufzahlen. Stichproben enthalten bis zu zwölf reine
Methodennamen je Stack; `runtime-gc.csv` enthält Collector, GC-Anlass und
Heapbelegung. `jdk.ZAllocationStall` wird gesondert erfasst. Keine Argumente
oder Objektinhalte. [Aktueller Stand](ALPHA9-GC-UPDATE.md).


Privater Sandbox-Teststand für Core und Enhanced, 17.11.2026. Nicht veröffentlicht.
**Korrigierter Teststand:** AWT-Fenster wählen jetzt automatisch Blt. Der echte
Bildschirmtest ist bestanden; für die neue Calon-Abnahme ist kein manueller
Präsentationsparameter erforderlich. Wasserupdates und die Diagnose wurden
gezielt ergänzt; siehe [Code und Nachweise](ALPHA9-CALON-FIXES.md).

Grundlage: [bestätigte Calon-Aufnahme und Messgrenzen](CALON-MOTION-ANALYSIS.md).
Die bisherigen Messungen belegen einzelne lange Frames und den Copy/GDI-Ausgabepfad.
Die Folgeaufnahme belegt drei GC-Pausen und weitere Update-Spitzen; ihre vollständige
Zuordnung und die Wirksamkeit der neuen Wasserbegrenzung bleiben zu messen.

## Änderungen in beiden Editionen

- AWT-/Java2D-Fenster und deren Kinder verwenden automatisch Blt, auch in Sandboxie.
  D3D11 wählt bei anderen geeigneten Hosts Flip Discard mit zwei Puffern, wenn DXGI Tearing unterstützt.
  VSync aus bleibt `Present(0, …)`; VSync ein benutzt das gewählte Intervall.
  Tearing wird nur nach erfolgreicher Featureabfrage und nur bei Intervall 0
  im tatsächlichen Fenstermodus aktiviert. Resize behält die Erstellungsflags.
- Nicht unterstützte Systeme oder fehlgeschlagene Flip-Erstellung verwenden den
  bisherigen Blt-Pfad. Für einen gezielten A/B-Test ist der Prozessparameter
  `FORGE_D3D11_PRESENT=blt` verfügbar. D3D9 bleibt unverändert.
- MSAA wird vor Flip aufgelöst; sRGB bleibt erhalten. Der Test hat zusätzlich
  einen bestehenden sRGB-Readbackfehler gefunden: BGRA-sRGB-Zuordnungen lagen hinter
  einer wirkungslosen Präprozessorprüfung auf einen Enumwert. Die Zuordnungen sind
  jetzt verfügbar; Readback verwendet das bekannte typisierte Renderformat.
- Die maximale D3D11-Framewarteschlange wird bei Flip auf zwei begrenzt. Kein
  zusätzlicher Waitable-Object-Limiter: Der vorhandene FPS-Limiter bleibt zuständig.
  Kein geändertes FPS-Limit, keine Glättung oder Verfälschung der Simulationszeit.

Die Auswahl folgt den [DXGI-Flip-Anforderungen](https://learn.microsoft.com/en-us/windows/win32/direct3ddxgi/for-best-performance--use-dxgi-flip-model)
und den [Regeln für Tearing, VSync und Resize](https://learn.microsoft.com/en-us/windows/win32/direct3ddxgi/variable-refresh-rate-displays).
Ein Wechsel des Present-Modells ist noch kein Nachweis besserer Calon-Framezeiten.

## Kurze Aufnahme

Enhanced: **Forge → Diagnose → 30 Sekunden Rucklerdiagnose aufnehmen**.
Core: **Spieleinstellungen → Forge Core → Rucklerdiagnose · 30 s aufnehmen**.
Ein weiterer Klick beendet die Aufnahme; nach spätestens 30 Sekunden speichert
ein Hintergrundthread den Bericht. Keine dauerhafte Hintergrundaufzeichnung.

Im Datenordner entsteht `diagnostics/frames-<zufällige Kennung>/` mit:

- `frames.csv`: tatsächliche Frameabstände, Limiter, Update, Render und HUD;
  zusätzlich Wasserreflexion/-brechung und Vegetation samt Aufrufzählern;
  unter D3D11 Terrain-Lade-/Entladequeues, Render und Present samt Modus.
- `summary.json`: P99, Maximum, Überschreitungen des doppelten eingestellten
  Framebudgets und der Grenzen 16,67 / 33,33 / 50 ms; Überlaufzähler.
- `runtime-events.csv`: Zeiten ausgewählter GC-/Safepoint-Ereignisse.
- `runtime-methods.csv`: Häufigkeit gesampelter oberster Methoden des Spielthreads.
- `runtime-samples.csv`: relative Zeitpunkte dieser Methodenstichproben.
- `runtime-allocations.csv`: Allokationsstichproben mit geschätztem Gewicht, Klasse,
  oberster Methode und Spielthread-Markierung; keine Objektinhalte oder Threadnamen.
- `runtime-summary.json`: Stichprobenanzahlen und ausgelassene Einträge.
- `README.txt`: Einheiten, verschachtelte Phasen und Messgrenzen.

Der Ring enthält höchstens 16.384 Frames. Bei Überlauf werden die ältesten
ersetzt; Export und Zusammenfassung nennen die Zahl. UI und Spielthread schreiben
keine Berichtsdateien. JFR wird intern gestartet, zeitlich auf 35 Sekunden und
mit einem 16-MiB-Aufzeichnungslimit begrenzt. Der externe Attach-Schutz bleibt an.
Roh-JFR wird nur temporär für die Auswertung angelegt und anschließend entfernt;
es gehört nicht zum exportierten Bericht. Kein automatischer Upload.

Keine Profile, Logindaten, Chats, Objekt-/Spielernamen, Netzwerkpakete oder
Kommandozeilen im Bericht. Die Ereignisauswahl ist eine feste Positivliste.
Bei nicht verfügbarem JFR oder nativen Messfunktionen bleiben die Java-Framezeiten
nutzbar; fehlende Messungen werden gekennzeichnet. D3D9 bekommt die gemeinsame
Java-Diagnose, jedoch keine neuen nativen Terrain-/Present-Messfunktionen.

`present_ns` enthält Resolve und den CPU-seitigen Present-Aufruf, keine GPU-Zeit.
Terrain und HUD können in den größeren Update-/Renderphasen liegen: Werte nicht
zusammenaddieren. Die erfasste direkte Messarbeit ist eine Untergrenze des
Aufnahmeaufwands; JFR kann zusätzlich Scheduling und Laufzeit beeinflussen.
Methodenstichproben sind Hinweise und keine vollständige CPU-Zuordnung.

## Calon-Abnahme

1. Enhanced alpha.9 mit D3D11 und den übernommenen Einstellungen starten.
2. Die bekannte Flugstrecke zunächst ohne Video und ohne Diagnose fliegen.
3. Kurze Diagnose starten, nach der Vorbereitung dieselbe Strecke fliegen.
4. Bei verbleibenden Rucklern den Bericht und einen separaten PresentMon-Lauf
   ohne Aufnahme vergleichen. FPS-/VSync-/Auflösungseinstellungen festhalten.
5. Im Bericht den automatisch gewählten Blt-Modus des AWT-Fensters prüfen;
   anschließend Core testen. Beide Editionen verwenden identische gemeinsame Klassen/DLLs.

Die Spieltests des korrigierten Standes sind noch offen. Kein neuer Original32-Vergleich, kein Wine-Test,
keine Vollbild-/Alt-Tab-Abnahme und kein Leistungsversprechen für andere GPUs.
Es wurden keine zusätzlichen Serverabfragen und keine Bewegungsänderungen eingebaut.
