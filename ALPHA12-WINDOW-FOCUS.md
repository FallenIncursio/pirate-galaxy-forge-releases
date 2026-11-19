# alpha.12: Tastaturfokus der Spielfenster

Stand vom 19.11.2026, Spielbasis 1002133. Gemeinsamer Fix für Core und Enhanced;
D3D9 und D3D11. Fokus-Test in Enhanced/D3D11 vom Nutzer bestätigt; Veröffentlichung freigegeben.

## Änderung

Normale MyGUI-Fenster beginnen wieder mit `mNeedKeyFocus = false`. Das entspricht
dem gemessenen Verhalten der ursprünglichen 32-Bit-Bibliothek. Ein Klick auf eine
Fensterfläche oder einen gewöhnlichen Button überträgt den Tastaturfokus damit
nicht mehr auf das Elternfenster. Die Komponententasten bleiben verfügbar, ohne
erneut auf den Planeten klicken zu müssen.

Editierbare Felder behalten ihren eigenen Tastaturfokus. Explizit angeforderter
Fensterfokus und die unabhängige Modalprüfung bleiben erhalten. Kein globaler
Fokus-Reset pro Frame, kein zusätzliches Weiterreichen bereits verbrauchter
Eingaben und keine Änderung am Komponenten-Dispatcher oder an Serveranfragen.

Die Korrektur liegt ausschließlich in der gemeinsamen MyGui.dll. Beide Renderer
werden aus dem aktuellen gemeinsamen GUI-Quellstand neu gebaut. Der D3D9-Build
benötigt dafür C++17 für die bestehenden Diagnosezähler und die ältere einparametrige
OGRE-Textursuche. Die D3D11-Textursuche bleibt unverändert. Bestehende ABI-Exporte
bleiben erhalten; die alten JNI-Wrapper werden mit den neuen DLLs geprüft.
Lose und in Basic eingebettete DLLs werden gemeinsam über native Locks gebunden.

## Aufklärung des D3D11-Testabbruchs

Der neue Analyse-Test hatte `Gui.delete()` ohne vorheriges `Gui.shutdown()`
aufgerufen. Der historische native Destruktor löscht nur die Singleton-Zuordnung;
`shutdown()` meldet die Grafik-Listener ab und zerstört die GUI-Manager.
Ohne diesen Aufruf blieb ein Listener auf ein bereits gelöschtes Objekt registriert.

Der gesicherte Stack führt über `RenderSystem::fireEvent`,
`D3D11RenderSystem::fireDeviceEvent` und die Zerstörung des Renderfensters bis zu
`Root::~Root`. Die korrigierte Reihenfolge `shutdown -> delete -> Root-Abbau`
beendet bereits die unveränderte alpha.11-D3D11-Probe mit Exit 0. Die neuen
Fokusproben geben ihren Erfolgsbeleg erst nach dem vollständigen Abbau aus.
Dieser Testfehler ist kein belegter Absturz des laufenden Nutzerclients.

Die bestehenden Core-/Enhanced-Oberflächenproben verwendeten diese Reihenfolge
bereits. D3D11-spezifische Zusatzproben im gemeinsamen nativen Testhelfer sind
beim D3D9-Build nun entsprechend abgegrenzt.

## Regression und Grenzen

`WindowFocusProbe` prüft echte Spiel-Skins und native Eingaben: normale Fenster,
Buttons, Verschieben, Texteingabe, Schließen, Wiederöffnen, modale Fenster,
expliziten Fensterfokus, Freigabe nach Zerstörung sowie 100/115/150 Prozent HUD.
Neun Fensterzyklen je Edition/Renderer; normale Ziffern, F6 und Ziffernblock;
zusätzlich begrenzte Hotkey-Queue, Wiederholungsschutz und Verwerfen bei verlorenem
Spielkontext. Kein Login, keine Desktop-Eingaben und kein Serverkontakt.

Die vorherigen D3D9-/D3D11-DLLs scheitern gezielt am Fensterstandard, beide neuen
DLLs bestehen die Probe mit sauberem Prozessabschluss. Vollständige Editions- und
Paketbelege sowie offene Punkte stehen im zugehörigen Release-Prüfstand.

Der Nutzer bestätigt den Fokusfix nach dem Enhanced/D3D11-Sandbox-Test. Die
Bestätigung ist keine einzeln protokollierte Vollabnahme aller Fenster und Eingaben.
Die Logs enthalten bekannte Tracking-, UI- und Szenenmeldungen, aber keine neue
Exception oder Absturzspur. Wine und andere GPUs sind nicht neu geprüft. Kamerabhängige Helligkeitswechsel, OTB-Endwertung und Wiederbelebungsabnahme
bleiben unverändert offen. Der laufende Nutzerclient wird nicht neu gestartet.

[Release-Prüfstand](RELEASE-STATUS-0.2-alpha.12.md) ·
[Kumulative Funktionen](FEATURES.md).
