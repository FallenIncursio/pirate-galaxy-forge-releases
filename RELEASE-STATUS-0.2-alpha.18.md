# Release-Prüfstand: Enhanced 0.2.0-alpha.18

21.11.2026. BP-Drop-Anzeige für Enhanced, Spielversion **1002133**.
Core bleibt **0.2.0-alpha.17**. Veröffentlichung, Quell-Push und Downloadprüfung
am 21.11.2026 beauftragt. Enhanced-Sequenz 99; Core-Kanal bleibt auf Sequenz 16.

## Geprüfte Dateien

Build: `.build/editions/alpha18-scan-drops-final-build`.
Tests: `.build/editions/alpha18-scan-drops-final-tests`.
Grundlage des uncommitteten Arbeitsstandes:
`aea17f865437740526f06caba5ee2efd6cda04dc`.
Die Buildbelege binden die Änderungen zusätzlich über die einzelnen Quellhashes.

| Edition | SHA-256 des Game-JARs |
|---|---|
| Core, unverändert | `918093c4e935e8f8af3eab689b956736843c73573332a574e82752eda0612310` |
| Enhanced | `dd443e65ba06700bbeed616dd9cb4295ab9862c7b9d9edbe990fc489de711af1` |

135 gemeinsame Klassen sind identisch. Core enthält keine BP-Drop-Klassen,
Ressourcen oder Scanner-Hooks und benötigt den neuen Enhanced-Patcher nicht.
Alle nativen D3D9-/D3D11-Inputs sind gegenüber alpha.17 unverändert.

## Automatische Abnahme

- Beide Editionsgates bestanden: 62 Hauptprüfungen, 25 Einträge in der
  Enhanced-Feature-Prüfung sowie 16 Python-Vertrags-/Importerprüfungen.
- Neue Drop-Prüfung: **8.834 Checks**, darunter Laden und Verifizieren der echten
  Scannerklasse sowie native Typ-/Rangfelder,
  der gepackte Katalog, Besitzstände, Sirius-Planetenfilter, Pilotenbindung,
  verzögerte RPC-Antworten und das Wiederholungslimit. RPC-Antworten stammen aus
  Testdaten, nicht vom Spielserver.
- D3D9 und D3D11: jeweils **1.818 native Enhanced-Bedienchecks**, einschließlich
  Scanner-Scrollen, Zugriff auf Originalinformationen, Teilezahlen ohne
  Abschneiden am Scrollbalken, Komponentenfokus, Wiederaufbau und Einstellungen
  mit Übernehmen/Verwerfen. Auflösungen 1024×768, 1920×1080, 3440×1440; HUD-Größen
  bis 200 %. Gerenderte Scanneransichten visuell geprüft.
- Zehn Negativkontrollen bestanden; darunter falsche Original-/Eingabehashes,
  falsche Patchzahl und verbotene Anwendung des Scanner-Patches auf Core.
  Der Scanner-Patcher verändert ausschließlich die deklarierte `aox`-Klasse.

## Releasepakete

Signierte Enhanced-Kandidaten unter `.build/alpha18-final-candidates` sind
geprüft: 59 Neuinstallations-/Alpha-73-Prüfungen, 64 alpha.17-Upgrade-/Reparatur-
prüfungen und 24 Installer-Oberflächenprüfungen. Wiederanlauf, Rollback,
Profil-/Anmelde- und Renderer-Erhalt wurden mit künstlichen Testdaten geprüft. Core-alpha.17
dient unverändert als Editionsvergleich. Separate Belege folgen in
`distribution/tests/editions-0.2-alpha.18-release-candidates.json` und nach
Upload in `distribution/tests/editions-0.2-alpha.18-publication.json`.
Private Spielcaches, Profile und Anmeldungen gehören nicht in Releasepakete.

## Korrektur nach dem ersten Start

Der erste private Enhanced-Kandidat unter `C:\PGF18S` wurde zurückgewiesen:
`java.lang.VerifyError: Bad local variable type` in `aox.do` verhinderte den
vollständigen Spielstart. Die bisherigen UI-Proben prüften die Zusatzanzeige,
luden aber nicht die tatsächlich gepatchte Scannerklasse.

Der neue Hook verwendet einen Wrapper mit stabilen Argumenten und lässt
Originalmethode und Stackframes unverändert. Die native `aix`-Zielauflösung
bleibt erhalten. Der neue Verifikationstest weist den ersten Kandidaten
nachweislich zurück und besteht mit dem korrigierten Game-JAR. Beide vollständigen
Editionsgates einschließlich D3D9-/D3D11-Oberflächen sind erneut bestanden.
Die neue Prüfung ist verbindlicher Teil von `ScanDropTests`.

## Lange BP-Namen vollständig anzeigen

Der anschließende Spieltest mit dem Startfix zeigte die BP-Liste und Teilezahlen
korrekt, aber Namen wie „NP Mesomersynthese-Materialisierer“ wurden abgeschnitten.
MyGUI bricht lange Wörter nur an Leerzeichen um; zusätzlich war die Namenshöhe
auf zwei Zeilen begrenzt. Enhanced misst jetzt die wirkliche Schriftbreite,
bricht auch an Bindestrichen beziehungsweise Unicode-Zeichengrenzen um und
vergrößert jede Zeile passend zum Text. Die Teilezahl steht immer darunter.
Die Scrollbalkenbreite wird bei der abschließenden Canvasgröße nur einmal abgezogen.

Die neue native Prüfung weist die vorige Darstellung anhand der tatsächlichen
Textbreite zurück. Mit dem Fix sind Breite, Höhe, vollständiger Text, Abstand zur
Teilezahl, Scrollen und beide Informationsreiter geprüft und visuell kontrolliert.
Gegenüber dem Startfix ändert sich nur `pg64/client/ScanDropUi.class` im Game-JAR;
Core und sämtliche nativen Bibliotheken bleiben bytegleich.

Auf neuen Startauftrag PID 40116 regulär beendet und den Namensfix mit D3D11
in `PGForgeAlpha18BpNames` gestartet (PID 24584, Container `C:\PGF18D`,
Startkopie `C:\PGF18P\E\versions\0.2.0-alpha.18`). Profil, Einstellungen,
geschützte Anmeldung und Windows-Mixer 8 % / nicht stumm geprüft.
Spieloberfläche und Scanner sichtbar; 56 geladene Dateihashes bestätigt.
Beleg: `distribution/tests/scan-drops-alpha18-namefit-launch.json`.
Die anschließende Rückmeldung ist im finalen Stand korrigiert: volle Zeilenbreite
ohne reservierten Scrollbalken bei kurzen Listen; einzelne und kurze Listen
beginnen oben unter der Überschrift. Native Tests erfassen einen, drei und viele
Einträge samt Scrollen. Der laufende Spielclient bleibt beim vorigen Namensfix
(`8bafdc34…`); die finale Anordnung wurde nicht in diese Sitzung eingespielt.

## Noch offen

Normale Scans und Teilezahlen sind im D3D11-Spieltest sichtbar. Wechselnde
Sirius-Planeten und die vollständige Ingame-Abnahme bleiben offen. Die native
Layoutprüfung ersetzt keinen vollständigen Spieltest.
Death-Squad-Sonderrollen und unklare Event-/Missionsbedingungen werden nicht
geraten. Keine neue Wine-/macOS- oder Langzeit-Leistungsmessung. Kein neuer
quantitativer Leistungsnachweis für diese reine Zusatzanzeige.

[Funktionsumfang, Quellen und manueller Testplan](ALPHA18-SCAN-DROPS.md).
