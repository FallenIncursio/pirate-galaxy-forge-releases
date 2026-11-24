> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# alpha.10: OTB-Datenlage und Wiederbelebungsdialog

Fixstand für Core und Enhanced auf Basis der veröffentlichten alpha.9.
Veröffentlichung ausdrücklich beauftragt; ein neuer OTB-Spieltest ist aktuell
nicht möglich. Die serverseitige Endwertung und eine Wiederbelebung im Spiel
bleiben unbestätigt.

## Enhanced: OTB erkennen, Datenlücken verständlich anzeigen

Die Livediagnose vom 18.11.2026 zeigte eine korrekte Bindung
an den eigenen OTB-Teilnehmer, aber fehlende System-/Flugzähler und eine stehen
gebliebene Onlinezeit. Allgemeine Teilnehmerdaten wurden währenddessen aktualisiert.

Bei fehlenden Werten zeigt das Widget jetzt **„OTB erkannt · Aktivitätsdaten fehlen“**
mit dem Hinweis **„Keine verlässliche Aktivitätswertung.“** Es schrumpft auf eine
zweizeilige Anzeige. Prozentzahlen und Spalten verschwinden bei fehlenden,
veralteten, noch unbestätigten oder rückläufigen Daten. Eine alte Onlinezeit wird
dadurch nicht mehr als vermeintliche 0-%-Teilnahme präsentiert.

Zeitstempel werden je Aktivitätsschlüssel geführt. Ein aktualisierter Onlinezähler
oder ein Landungsflag macht alte System-/Flugzähler nicht erneut frisch. Die
numerische Auswertung verlangt jeweils nach der Bindung beobachtete, höchstens
30 Sekunden alte Zähler. Stabile Landungs-/Markierungsflags benötigen keine
künstlichen periodischen Änderungen. Ein ausdrücklich positives Aktivitätsflag
hat seinen eigenen Aktualitätsnachweis. Die 30 Sekunden bleiben eine konservative
Anzeigeregel und keine Frist des Servers; unveränderte Zähler können deshalb als
nicht mehr frisch behandelt werden.

Die Anzeige erfolgt weiterhin maximal zweimal pro Sekunde, ohne zusätzliche
Serverabfragen, Modellschreibzugriffe, Eingabeautomation oder eigene Spielaktionen.
Clientkriterien sind keine Zusage zur späteren Belohnung oder OTB-Sperre.

## Begrenzte lokale OTB-Diagnose

Unter **Forge → Diagnose → OTB-Diagnose: an/aus** lässt sich die Aufzeichnung
abschalten. Sie ist standardmäßig bereit, zeichnet aber nur beim erkannten
eigenen OTB und eingeschaltetem OTB-Widget auf. Der Diagnosebereich zeigt ihren
Status und Speicherort. Über „Ordner öffnen“ erreicht man `diagnostics/otb`.

Die Aufzeichnung enthält Feldpräsenz, zulässigen Datentyp, rohe Zählerwerte,
Änderungsanzahl und Alter je Feld, Clientgrenzen, Matchphase, vorhandene Restzeit,
Anzeigestatus und einen getrennten Zeitpunkt allgemeiner Modelländerungen.
Eine lokale Bindungsnummer ersetzt Spieler- und Matchkennungen. Es werden keine
Namen, Chattexte, Profile, Zugangsdaten oder Netzwerkpakete gespeichert. Unbekannte
Objekte werden nur als ungültiger Typ erfasst, niemals über ihr `toString()`.

Ein Messpunkt entsteht alle fünf Sekunden, zusätzlich bei Status- und
Bindungswechseln. Beim Verlassen bzw. Ende der erkannten Phase wird noch der
vorliegende Stand protokolliert. Das ist kein Nachweis, dass spätere Ergebnisdaten
bereits vollständig empfangen wurden. Allgemeine Modelländerungen belegen keine
Aktivitätsbestätigung des Servers.

Dateien: `activity.jsonl` und `activity.previous.jsonl`, je maximal 256 KiB.
Ein einzelner Hintergrundschreiber mit höchstens 64 wartenden Zeilen übernimmt
Dateizugriffe; der Spielthread wartet nicht auf die Festplatte. Schreibfehler
beenden die Aufzeichnung und erscheinen im Diagnosestatus. Die Spielanzeige
funktioniert weiter. Keine automatischen Uploads. Bei abruptem Prozessende können
die letzten noch wartenden Zeilen fehlen; der begrenzte Verlauf ist kein Archiv
aller vergangenen Matches.

## Core und Enhanced: fehlende Cooldowns im Wiederbelebungsdialog

Der ursprüngliche Task `com.splitscreen.axp$21$2.go()` verwendete `py.sr()` vor
der Null-Prüfung eines optionalen Cooldowns. Dieser Fehler war in der gepinnten
32-Bit-Basis und beiden bisherigen Editionen bytegleich vorhanden.

Ein gemeinsamer Helfer prüft Spieler, aktuelles Schiff, Avatar, OTB-Teilnehmer,
Wallet und Timer. Fehlende oder ungültige Timer bleiben unbekannt. Ein gültiger
OTB-Landungszonentimer hat weiterhin Vorrang; der vorhandene globale Cooldown
bleibt der ursprüngliche Fallback. Ohne eigenen Teilnehmer wird keine globale
OTB-Berechtigung abgeleitet. Später eintreffende Timer werden beim nächsten
normalen UI-Update berücksichtigt. Ohne Timer erscheint `…` anstelle einer
erfundenen Restzeit. Der ursprüngliche weitere Dialogablauf bleibt erhalten.

Patchnachweis: `patches/edition-fixes.tsv`, Original- und Eingangshash der Klasse,
ein erwarteter Patch; `EditionFixes` kontrolliert zusätzlich den bisherigen
Lookup, drei Property-Lesezugriffe, die Teilnehmerauflösung, die beiden
Cooldown-Abfragen und den bisherigen Ersatztext. Ein abweichender Ausgangscode
bricht den Build ab. Keine Renderer-, Protokoll- oder serverseitige Spieländerung.

## Prüfung und praktische Abnahme

Automatische Prüfungen umfassen den beobachteten 1002/fehlende-Zähler-Fall,
unabhängige Feldaktualität, stabile Flags, Datenrückschritte, Beobachterabbau,
parallele Modelländerungen, Journalrotation, Schreibfehler und Datensparsamkeit.
Der gemeinsame Timer-Test prüft fehlende, ungültige, später eintreffende und
wechselnde Timer sowie fehlende Teilnehmer/Wallet/Avatar-Kontexte.

Native UI-Prüfungen müssen beide Renderer, mehrere Auflösungen und HUD-Skalen,
den Wechsel zwischen kompakter und numerischer Anzeige, Fokusfreiheit sowie den
Diagnoseschalter abdecken. Die tatsächlichen Ergebnisse stehen im
[Release-Prüfstand](../verification/RELEASE-STATUS-0.2-alpha.10.md).

Noch praktisch zu testen: eigener OTB mit dem neuen Paket, die beiden lokalen
Journaldateien, Matchende/Orbit/Rückkehr und ein regulärer Wiederbelebungsdialog.
Kein absichtliches Provozieren einer Inaktivitätssperre nötig. Die aktuelle
Nutzersitzung wird für diese Vorbereitung nicht beendet oder verändert.
