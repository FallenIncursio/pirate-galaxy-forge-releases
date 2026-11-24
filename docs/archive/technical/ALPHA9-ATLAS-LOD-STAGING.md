> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# alpha.9: Schriftatlanten, manuelle LODs und gestufter Vegetationsaufbau

Aktuelle Veröffentlichung und Testgrenzen: [Release-Prüfstand](../verification/RELEASE-STATUS-0.2-alpha.9.md).
Der folgende Text dokumentiert die Implementierung und damalige Vorbereitung.

Privater Folgestand für Core und Enhanced, 18.11.2026. Nicht veröffentlicht.
Ausgangspunkt ist die jüngste Calon-Aufnahme mit fünf Schriftspitzen und vier
Vegetationsspitzen. Sie beweist keine einzelne Ursache für sämtliche Mini-Ruckler.

## Schrift-Lebensdauer

`FontManager` hält benutzte GUI-Fonts einschließlich der Basis einer vergrößerten
HUD-Schrift. Die Begrenzung beträgt 32 Fonts und 64 MiB Atlasdaten. Die zuletzt
verwendeten Fonts bleiben bevorzugt erhalten. Ungenutzte Spielressourcen können
weiter bereinigt werden, ohne dabei die Schrift kurzlebiger Zielanzeigen erneut
zu rasterisieren. Es werden Font-Ressourcen gehalten, keine veralteten Texturzeiger.

Explizites Entladen funktioniert weiterhin. Entfernte oder ersetzte Ressourcen
werden bei der nächsten Benutzung aus dem Bestand entfernt. GUI-Shutdown gibt den
gesamten Bestand frei. Die native Objektgröße des Schriftmanagers bleibt für
die bestehende Java-Anbindung unverändert; acht Konstruktor-/Destruktorzyklen
mit dieser Anbindung sind geprüft. Der bisher uninitialisierte vertikale Font-Offset wird
mit null initialisiert; konfigurierte Werte behalten Vorrang.

Eine native Prüfung umfasst 32 Bereinigungszyklen bei tatsächlich wirksamen
100 %, 115 % und 200 % HUD, Größenwechsel, erzwungenes Neuladen, die
Begrenzung, Ressourcenentfernung und Shutdown: 148 Prüfungen bestanden.

Zusätzliche Gegenprobe mit echter `targetinfo.layout`, 115 % HUD und D3D11:

| Zustand nach Ressourcenbereinigung | Vorherige DLL | Neuer Stand |
|---|---:|---:|
| Vier Layout-Erstellungen | 31,20–32,38 ms | 0,17–0,30 ms |
| Rasterisierungen im gesamten Acht-Zyklen-Test | 10 | 2 beim ersten Laden |

Die alte DLL reproduziert den Fehler unter derselben Probe. Die neue DLL besteht
die Prüfung anhand der Ressourcenereignisse; die Laufzeiten sind lokale Messwerte,
keine zugesagte Framerate. Der erste Aufbau bleibt erwartungsgemäß teuer.

## Tatsächlich ausgewählte Vegetations-LODs

`prepareStaticSource` bereitet jetzt Grundmodell und sämtliche von `BatchPage`
auswählbaren manuellen LOD-Entities vor. Dieselben Regeln gelten für Windseiten.
Die vorhandenen Grenzen von 64 MiB CPU-Schattenpuffern und 8 MiB pro Puffer bleiben
erhalten. Dynamische und animierte Quellen werden weiterhin ausgelassen.
Mesh-Unload gibt die zugehörige Cache-Buchführung frei.

Zu große LOD-Indizes werden auf die letzte vorhandene Stufe begrenzt. Vorher konnte
die Auswahl genau einen Eintrag hinter dem Ende liegen. Prüfungen verwenden den
echten `BatchPage`-/`WindBatchPage`-Auswahlpfad mit Grundmodell, manueller Stufe
und zu großen Indizes. Der frühere direkte Grundmesh-Test deckte das nicht ab.

## Seiten in mehreren Schritten aufbauen

Optionale Baum- und Windseiten erhalten einen fortsetzbaren CPU-Aufbau. Pro Schritt
werden kleine Vertex-/Indexblöcke transformiert. Quellpuffer werden vor jeder
Rückkehr entsperrt; Grafikpuffer bleiben niemals über Framegrenzen gemappt.
Uploads erfolgen auf dem Spiel-/Renderthread. Erst eine vollständig gebaute Seite
wird an die Szene angehängt und kann sichtbar werden.

Alle Vegetationsschichten teilen ein weiches Budget von 2 ms je OGRE-Frame.
Mehrere Updates desselben Frames bekommen kein neues Budget. Zusätzlich sind
temporäre Ausgabedaten auf insgesamt 64 MiB begrenzt. Quellen werden während eines
Aufbaus gehalten; Windparameter werden vor dem möglichen Entfernen der Entity
gesichert. Entladen, Loader-Wechsel und Loader-Zerstörung verwerfen angefangene
Arbeit. Explizites Vorladen beendet auch bereits angefangene Seiten.

Eine sofort benötigte Seite darf vollständig fertiggebaut werden. Auch einzelne
Treiberuploads, Material-/Shaderarbeit und außergewöhnlich große Seiten können das
Budget überschreiten. Es ist deshalb ausdrücklich kein hartes Framezeitlimit.
Gras benutzt weiterhin seinen bisherigen Aufbau. Sichtweite, Pflanzendichte,
Planetenkonfigurationen und Windparameter wurden nicht reduziert.

Beim Vergleich eines Venar-Modells wurde zusätzlich ein uninitialisierter vierter
Tangentenwert nachgewiesen. Beide Aufbauwege übernehmen diesen Wert jetzt aus dem
Quellmodell. Er beschreibt die Orientierung des Tangentenraums; zufälliger
Grafikspeicher ist dafür kein gültiger Ersatz.

## Abdeckung und offene Abnahme

Die native D3D11-Prüfung vergleicht vollständigen und gestuften Aufbau, mehrere
Vertexkanäle, Farben, Wind, Indizes, wiederholte Abbrüche, leere Seiten,
LOD-Auswahl, Loader-Wechsel, Seitenwiederverwendung und reguläres Ende.
49 echte Quellmeshes werden privat geprüft: 43 von Calon, sechs von Venar.
294 unbeschattete Quell-Lesevorgänge vor Vorbereitung, null danach. Der gestufte
Aufbau erzeugt dieselben Geometriebytes wie der korrigierte vollständige Aufbau.
Originalressourcen und rohe Messdateien gehören nicht in die Release-Repos.

Beide Editionen verwenden dieselben neuen D3D11-Bibliotheken. D3D9-Paketbibliotheken
bleiben unverändert. Die bisherige 62-spaltige Diagnose bleibt kompatibel;
`forests_build_ns` enthält die im jeweiligen Frame ausgeführten Aufbauschritte.
Keine zusätzlichen Serverabfragen, Profiländerungen oder automatische Anmeldung.

Vor Freigabe dieselbe Calon-Strecke wiederholt fliegen, neue Gegner/Zielanzeigen,
Kamerawechsel und Orbit/Rückkehr prüfen. Mit und ohne Diagnose vergleichen;
Venar und einen schwächer bewachsenen Planeten ergänzen. Wasser-Einzelausreißer,
andere Grafikkarten und längere Sitzungen bleiben offen. Kein neuer kontrollierter
32-Bit-Flugvergleich und keine Behauptung vollständiger Rucklerfreiheit.

Verbindlicher Build-/Paketstand: [Prüfstatus](../verification/RELEASE-STATUS-0.2-alpha.9.md).
Sanitisierter Beleg: `distribution/tests/calon-alpha9-atlas-lod-fixes.json`.
