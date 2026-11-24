> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Calon: Liveprüfung der Schriftatlas-/LOD-/Vegetations-Fixes

Am 18.11.2026 die neue Nutzerdiagnose aus Enhanced alpha.9 mit D3D11 ausgewertet:
7.080 Frames über 29,989 Sekunden. Derselbe geprüfte Kandidat wie im Startbeleg
`distribution/tests/editions-0.2-alpha.9-atlas-lod-launch.json`; beide nativen
Messmodule in allen Frames aktiv. Kein Neustart oder Produktionscode-Eingriff.
Sanitisierter Beleg: `distribution/tests/calon-alpha9-atlas-lod-live.json`.
Rohdaten und GUI-Log bleiben privat unter `work/alpha9-atlas-lod-live` im Chatordner.

## Die gezielten Fixes wirken

| Messgröße | Vorheriger Vegetationstest | Neuer Atlas-/LOD-Test |
|---|---:|---:|
| Zielanzeigenaufbau, Maximum pro Frame | 24,258 ms | 1,021 ms |
| Zielanzeigen-Layoutaufrufe | 10 | 10 |
| Vegetation, Maximum pro Frame | 15,147 ms | 2,917 ms |
| Vegetationsframes über 5 ms | 35 | 0 |
| Seitenaufbau, Maximum pro Frame | 14,753 ms | 2,899 ms |
| Quellenlesen, Maximum pro Frame | 4,502 ms | 0,031 ms |
| Leseversuche ohne CPU-Schatten | 1.220 | 0 |

Kein erneuter großer Zielanzeigen-Schriftaufbau in dieser Aufnahme. Der CPU-Schatten-
bestand liegt konstant bei 5.537.382 Bytes, weit unter 64 MiB. Optionale Seitenarbeit
verteilt sich über mehr Frames; daher ist ein höheres Vegetations-P99 trotz kleinerer
Spitzen erwartbar. Es wurden 38 Vorladeaufträge und 2.235 Pflanzeninstanzen erfasst,
zuvor 51 und 3.963. Die Strecke/Spielsituation war nicht kontrolliert identisch;
die Zahlen sind keine allgemeine prozentuale Leistungszusage.

## Verbleibende Ausreißer

| Gesamte Frameabstände | Vorher | Jetzt |
|---|---:|---:|
| P99 | 6,110 ms | 6,447 ms |
| Maximum | 39,441 ms | 49,362 ms |
| Über doppeltem 240-FPS-Budget (8,33 ms) | 36 | 23 |
| Über 16,67 ms | 9 | 8 |
| Über 33,33 ms | 2 | 2 |
| Über 50 ms | 0 | 0 |

Die behobenen Pfade sind deutlich günstiger, die Gesamtaufnahme ist noch nicht
ruckelfrei. `frame_delta` misst Abstände; `frame_total` misst den instrumentierten
Schleifendurchlauf. Beide gehören nicht automatisch zur gleichen verursachenden
Zeile. Neun Durchläufe über 16,67 ms enthalten folgende Hinweise:

- Bei 2,174 s: Timerupdate 29,780 ms, davon 14,339 ms in der verschachtelten
  Schriftphase. JFR trifft `HudCooldown.styleNative`. Im zeitlich passenden GUI-Log
  werden `ForgeComfort_PG_TextFontBoldSmall_16` und dessen 2x-Variante gerastert.
  Kein Wiederauftreten dieses großen Timerereignisses innerhalb der 30 Sekunden.
- Bei 3,042 / 9,625 / 11,624 / 22,644 s: JFR trifft `NativeLibrary.findEntry0`
  unter Audio-Pitch, Audio-Position, Partikelposition und Partikelbreite. Das spricht
  für späte native Methodenbindung. Eine Stichprobe beweist nicht, dass die gesamte
  jeweilige Updatephase (bis 47,700 ms) in dieser Funktion verbracht wurde.
- Bei 13,311 s: Renderphase 31,563 ms; Stichprobe in `Root._renderOneFrame`.
  `present_ns` dieses Frames nur 0,441 ms. Native Unterursache bleibt offen.
- Die übrigen langen Durchläufe sind mit den vorhandenen Unterphasen/Stichproben
  nicht vollständig zugeordnet. Vegetation, Zielanzeigen und Wasser erklären
  sie nicht. Wasserreflexion diesmal maximal 3,208 ms.

Keine GC-, Safepoint- oder Allokationswarteereignisse exportiert. Die direkte
Diagnoseaktivierung kostet im ersten Frame weiterhin 10,233 ms und muss beim
Bewerten des Messstarts berücksichtigt werden. Keine GPU-Zeitmessung enthalten.

## Nächste Prüfung

Die gleiche Strecke in dieser bereits warmen Sitzung erneut fliegen. So lässt
sich prüfen, ob Timer-/JNI-Spitzen nur bei der ersten Nutzung entstehen. Einen
Kontrollflug ohne Diagnose ergänzen. Der Erststart bleibt dennoch relevant.

Im Code `HudCooldown.prepare` und `ForgeComfort.cpp::prepareNative` nachverfolgen,
ob die Vorbereitung tatsächlich im richtigen Ladezeitpunkt stattfindet und die
effektive HUD-Schriftvariante lädt. `font(nullptr,...)` durchläuft den tatsächlichen
Widget-Schriftwechsel nicht. Danach gezielt Audio-/Partikel-Bindungen vorwärmen bzw.
deren Auflösung messen; keine globalen Ressourcenbereinigungen deaktivieren und
keine willkürlichen Spiel-/Audiofunktionen mit ungültigen Objekten aufrufen.

Keine allgemeine Releasefreigabe, keine neue Core-Liveaufnahme, kein kontrollierter
32-Bit-Vergleich. Dieser Schritt dokumentiert die Diagnose und ändert keinen Code.
