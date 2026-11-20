# alpha.16: Cacheübernahme und nachvollziehbare Updatefehler

Die erste ausgewertete Startdiagnose zeigte einen Fehler während der Aktivierung
und anschließend einen Start von alpha.10. Der genaue auslösende Dateipfad fehlte
im Export. Eine getrennte Reproduktion bestätigte einen Updaterfehler:
`CarryRemoteCache` übernimmt den optionalen Cache, `ValidateInstalled` verlangte
anschließend dessen Release-Prüfsumme. Die Datei `files/r1034324255` ist zwischen
Spielbasis 1002132 und 1002133 von 2332 auf 2541 Bytes verändert. Ihre übernommenen
alten Bytes lösen den Aktivierungsfehler reproduzierbar aus. Auch spätere legitime
Serveränderungen am Cache konnten dieselbe Prüfung scheitern lassen.

## Umsetzung

Alle Pfade für installierte Daten verwenden dieselbe Regel: kanonische optionale
REMOTE-Dateien sind veränderlich; ihre Prüfung erfolgt im originalen Ressourcen-
loader. Die optional-Markierung ist ausschließlich für `files/r<Integer>` und versionierte Sprachcache-Dateien
`lang/lang[1]_<Spielbuild>_<Sprache>.properties` erlaubt.
Kern, gepatchte JARs, native Bibliotheken, Laufzeit, Startkonfiguration und signierte
Payload werden weiterhin geprüft. LOCAL-Dateien sind keine REMOTE-Ressourcen.
Profile, Rendererwechsel und geschützte Anmeldung werden weiter separat übernommen.

Bei Updatefehlern bleibt die bisherige Installation erhalten. Ein sichtbarer Dialog
bietet Wiederholung, Diagnose und bei passender geprüfter Spielbasis einen ausdrücklich
gewählten Start der vorhandenen Version. Der Starter vergleicht dafür den signierten
Spielquellenkatalog mit seiner gepinnten Spielbasis. Er startet keine bekannte veraltete
Basis stillschweigend. Offlineverwendung einer verifizierten kompatiblen Installation
bleibt möglich. Die Integrität wird beim tatsächlichen Start erneut geprüft.

Schema-4-Berichte enthalten getrennte Versionsfelder sowie bis zu vier Fehler mit
Phase, fester Kategorie und bis zu zwölf Methodenframes ohne Dateipfade, Parameter
oder freie Exception-Meldungen. Schema 1/2/3 bleibt serverseitig unterstützt. Lokale
alte Diagnosen werden beim erneuten Export in das neue Schema übernommen; fehlende
neue Felder bleiben unbekannt. Rohlogs werden weiterhin nur lokal gespeichert.

## Grenzen und Vergleich

Der Fehler betrifft den Forge-Updater und damit beide Editionen. Der originale
32-Bit-Client verwendet diesen Updater nicht. Java- und native Spielmechanik werden
für alpha.16 nicht geändert. Es gibt keine zusätzlichen Gameplay-Serverabfragen.
Die Diagnose beweist keinen GPU-Fehler; der beobachtete Renderframe bestätigt keinen
sichtbaren Login. Die konkrete Ursache eines eventuell verbleibenden Hängers im
alten Client lässt sich aus dem ersten Bericht ohne Thread-Aufnahmen nicht ableiten.

Ein bestandener Cache-Upgrade-Test beweist nicht, dass sämtliche Ladehänger auf
anderen Rechnern behoben sind. Kamerabhängige Helligkeit, native Sirius-Ursache,
weitere GPUs, Wine/macOS und Langzeit-Gameplay bleiben separate offene Themen.

[Prüfstand](RELEASE-STATUS-0.2-alpha.16.md)
