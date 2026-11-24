> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Alpha.9: GC-Pausen und lange Spielupdates

Privater Core-/Enhanced-Teststand vom 17.11.2026. Nicht veröffentlicht.

## Befund aus der neuen Calon-Aufnahme

5.565 Frames in 30 Sekunden, P99 16,750 ms, Maximum 52,366 ms. 56 Frames
überschreiten 16,67 ms, neun 33,33 ms. Die vier GC-Pausen dauern 46,680,
35,974, 28,667 und 26,103 ms. Der längste Frame überlappt die längste Pause.
Das zeitgleich lange Wasserupdate ist deshalb kein Nachweis für 47 ms reine
Wasserzeichenzeit. Die Unterphasen sind verschachtelt und werden nicht addiert.

Alle vier Methodenstichproben im nativen Layout-Lader liegen in langen
Update-Frames. Darunter sind Updates von 37,638, 31,780 und 30,513 ms ohne
überlappende GC-Pause. Weitere Spitzen, insbesondere Vegetation bis 22,751 ms,
sind damit nicht vollständig erklärt. Eine einzelne Methodenstichprobe beweist
nicht die gesamte Dauer oder den genauen Anteil des XML-Parsers.

Die gewichteten Allokationsstichproben des Spielthreads schätzen 149,632 MiB
in 30 Sekunden. Auffällig sind Finalizer-Registrierung (20,502 MiB), native
Zeigerträger, Winkelupdates und wiederholte Regex-Kompilierung. Das sind
Stichprobenschätzungen, keine vollständige Objektzählung. Die alte Aufnahme
enthält nur die oberste Methode; vollständige Aufrufketten lassen sich daraus
nicht nachträglich rekonstruieren. Die neue Diagnose erweitert diesen Nachweis.

## Änderungen

- **Speicherbereinigung:** Beide privaten Kandidaten verwenden generationales
  ZGC statt G1. Die bisherige Heap-Spanne von 512 MiB bis 8 GiB bleibt erhalten.
  Attach-Schutz, explizite Sammlung und native Finalizer bleiben aktiv. Die
  Buildvorlage entfernt die alten G1-Schalter ausdrücklich, bevor sie die neue
  Richtlinie einsetzt; die tatsächlichen Startflags werden mit der JVM geprüft.
  ZGC führt wesentliche Sammelarbeit nebenläufig aus und benötigt dafür CPU-
  und Heap-Spielraum. Es ist keine Garantie für einen ruckelfreien Frame.
  [OpenJDK-/Oracle-Dokumentation](https://docs.oracle.com/en/java/javase/24/gctuning/z-garbage-collector.html).
- **Winkelupdates:** Der belegte Pfad `at.do(Radian,float)` ersetzt bislang für
  jeden Aufruf den nativen Winkel und dessen Java-Zeigerträger. Der neue D3D11-
  Wertpfad schreibt das Ergebnis derselben nativen Float-Multiplikation in den
  bestehenden eigenen Winkel. Geliehene, gelöschte, abgeleitete oder identische
  Quell-/Zielobjekte behalten den bisherigen Pfad. Keine native Adresse wird
  länger gespeichert. Die D3D9-Bibliotheken bleiben bytegleich und verwenden
  den geprüften bisherigen Winkelpfad.
- **HUD-Text:** Die zwei konstanten Muster in `oc.ct` werden einmal kompiliert.
  Matcher und Texte bleiben aufrufbezogen; auch die ursprüngliche Behandlung
  mehrstelliger Prozent-Platzhalter bleibt erhalten.
- **Layout-Laden:** MyGUI hält bis zu 16 geparste Layout-Vorlagen vor. Bei jedem
  Laden werden Ressource und vollständiger Inhalt erneut gelesen und exakt
  verglichen. Änderungen, fehlende oder fehlerhafte Dateien werden dadurch
  nicht verdeckt. Höchstens 128 KiB XML je Vorlage und 2 MiB XML-Eingaben
  insgesamt bleiben gespeichert, zusätzlich die begrenzten Parsebäume.
  Ressourcen-Reset und Abmeldung des Layout-Laders leeren den Cache. Aktive
  Aufrufe behalten ihre eigene Dokumentreferenz. Widgets werden weiterhin neu
  erzeugt; es werden keine Widget-/Szenenzeiger zwischengespeichert. Lesen,
  Texturladen und Widget-Erzeugung können weiterhin Arbeit verursachen.
- **Enhanced:** Optionale Forge-Widget-Abfragen verwenden die bereits vorhandene
  stille native Registry-Suche. Die wiederholte Erzeugung eines Enumerators und
  das Durchlaufen aller Wurzelfenster entfallen. Dieser zusätzliche Fix gehört
  zu Enhanced; die übrigen Änderungen sind gemeinsam.
- **Diagnose:** Zusätzlich Layout- und GUI-Updatezeiten samt Aufrufzahlen,
  maximal zwölf Methodennamen je Stichproben-Stack, GC-Anlass/-Collector,
  Heap-Belegung und ZGC-Allokationswartezeiten. Keine Argumente, Objektinhalte,
  Anmeldedaten oder automatischen Uploads. Roh-JFR wird weiterhin gelöscht.

## Prüfung und Grenzen

- 48 Editionssuiten und sechs vorhandene Negativkontrollen bestanden;
  119 gemeinsame Klassen sind bytegleich. Native UI-Prüfungen mit D3D9/D3D11.
- Je Edition 12.026 Winkel-/Textprüfungen, einschließlich 10.000 zufälliger
  Float-Bitmuster, geliehener/gelöschter nativer Objekte und Allokationsmessung.
  D3D9-Fallback: 12.015 Prüfungen. Die alten Winkel- bzw. Textmethoden scheitern
  jeweils an ihrer eigenen Gegenprobe.
- 212 Cache-Prüfungen und 79 Prüfungen im tatsächlichen ResourceManager:
  Wiederverwendung, Inhaltsänderung gleicher Länge, Fehler, Reset und Freigabe.
  Die vorherige MyGUI-DLL scheitert an der Wiederverwendungs-Gegenprobe.
- 86 vergleichbare UI-Bilder sind pixelgleich zum vorherigen privaten Stand.
  Das ist UI-Parität, kein neuer Original32- oder Calon-Flugvergleich.
- Synthetischer 12-s-Vergleich mit tatsächlichen nativen Java-Objekten:
  G1 maximal 3,7223 ms GC-Pause, ZGC 0,0185 ms. Der gleiche ZGC-Prüfpfad
  läuft in der echten Sandbox mit maximal 0,0238 ms und ohne erfasste
  Allokationswartezeit. Beide Hostläufe erzeugen unterschiedlich viele Frames
  innerhalb der Zeitgrenze; dies ist kein identischer Gameplay-Benchmark.
- Je Edition 357 Diagnoseprüfungen im dokumentierten Lauf. Stichprobenzahlen
  können zwischen Läufen variieren. Alte und neue Startflags werden getrennt
  geprüft, der Original-Protokollzugriff bleibt durch Negativkontrollen abgesichert.

Gegenüber der 32-Bit-Basis ändern diese Korrekturen die lokale Ausführung,
nicht Bewegung, Spielzeit, Serverabfragen oder Kampfdaten. Keine gemessene
Original32-Leistungsparität. Ein neuer Calon-Test, längere Szenenwechsel,
andere Rechner/Grafikkarten und Wine bleiben offen. Eine vollständige Beseitigung
aller Mini-Ruckler wird vor diesem Spieltest nicht behauptet.

Maßgebliche Kandidaten und Belege: [aktueller Prüfstand](../verification/RELEASE-STATUS-0.2-alpha.9.md).
