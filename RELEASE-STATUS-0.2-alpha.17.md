# Core / Enhanced 0.2.0-alpha.17 – zur Veröffentlichung freigegeben

Spielversion **1002133**, Starter **17**, Core-Sequenz **16**, Enhanced-Sequenz
**98**. Am 21.11.2026 bestätigt der Nutzer den neuen Enhanced-Sandbox-Stand und
beauftragt beide Releases, Quell-Push, Updatekanäle und öffentliche Downloadprüfung.
Die folgenden Vorbereitungs- und Testbelege bleiben an ihre jeweiligen Bytes
gebunden. Neue signierte Installer werden aus dem bestätigten Widgetstand erstellt.
Vollständige OTB-Matchabläufe und Serverwertung sind damit nicht bestätigt.

## Laufender Sandbox-Test: neues Enhanced-alpha.17-OTB-Widget

Am 21.11.2026 auf Nutzerauftrag den vorherigen Sandbox-Client regulär beendet
(Exit 0) und das neue geprüfte Enhanced-Paket mit D3D11 gestartet. Box
`PGForgeAlpha17OtbWidget`, Container `C:\PGF17X2`, Kandidat
`C:\PGF17Y2\E\versions\0.2.0-alpha.17`, Spiel PID 45092.
Direkter privater Kandidatenstart über den nativen Host, kein neuer Installer-
oder Startertest. Vor weiteren Aktionen Prozess und Startzeit frisch prüfen.

Drei Profile, Einstellungen und eine geschützte Anmeldung aus der zuletzt
beendeten Sitzung übernommen (19 Dateien, Hashvergleich und Credential-Reader
bestanden). Windows-Mixer 8 %, nicht stumm. 16 Selector-Zyklen und 54 geladene
Dateihashes geprüft; D3D11, Sandboxie, Anmeldung und sichtbarer Orbit bestätigt.
Game-JAR `ebe020a4b209298bd2278679ddc194a33089ec3e85646238d6217cd6508f2b99`.
Normale current.json/preferences.json und kopierte Quellprofile unverändert.

Client zum Test offen lassen. Vorschau: Forge → Anzeige → Widgets → OTB-Warnung
testen. Echte OTB-Warnübergänge mit diesem Widget noch nicht live abgenommen;
Serverwertung bleibt unbekannt. Beleg
`distribution/tests/editions-0.2-alpha.17-otb-widget-launch.json`, private Daten
im Chatordner `work/alpha17-otb-widget-launch`. Nichts veröffentlicht, gepusht,
committet oder an Updatekanälen geändert. Alte signierte Kandidaten enthalten
das neue Widget weiterhin nicht; vor Veröffentlichung neu bündeln und prüfen.

## Aktueller Sandbox-Stand: Enhanced mit Werten, Countdown und Vorschau

Enhanced zeigt Systemnutzungen seit lokalem Messbeginn, beide Signalalter und
einen Warn-Countdown. In den letzten 15 Sekunden gibt es eine gelbe Vorwarnung,
bei Ablauf ein deutlich hinterlegtes Warnband mit dunkler Schrift und Warnzeichen.
Serverwertung bleibt unbekannt. Die Anzeige weicht dem originalen OTB-HUD und
der Verbindungsanzeige aus, ohne Eingaben oder Fokus zu übernehmen.

Anzeige → Widgets → OTB-Warnung testen öffnet eine Fünf-Sekunden-Vorschau mit
beschrifteten Beispieldaten. Wiederholen, Rückkehr, Seitenwechsel und Schließen
sind geprüft; echte Messung, Diagnose, gespeicherte Einstellungen und noch nicht
übernommene Änderungen bleiben durch die Vorschau unberührt.
Keine zusätzlichen Serverabfragen. Core und die nativen DLLs bleiben unverändert.

- Finaler Build: `.build/editions/alpha17-otb-widget-rc-build`.
- Finaler Testlauf: `.build/editions/alpha17-otb-widget-rc-tests`.
- 62 Suiten und sechs Negativkontrollen; 698 OTB-Checks bestanden.
- D3D9 und D3D11: jeweils 1.239 Enhanced-Bedienprüfungen, drei Auflösungen und
  mehrere HUD-Skalierungen; native Textbreiten, passive Eingabe und Vorschau geprüft.
- Namensfix weiterhin enthalten; 93 Zielanzeigenchecks je Edition bestanden.
- Core-JAR bytegleich zum vorherigen OTB-/Namensstand; 135 gemeinsame Klassen
  identisch. In Enhanced ändern sich ausschließlich sieben Widget-/UI-Klassen.
- Neue vollständige private Sandbox-Pakete: `C:\PGF17W`, je
  `Pirate-Galaxy-Forge-<Core|Enhanced>-0.2.0-alpha.17`.
- Maßgeblicher neuer Beleg: `distribution/tests/otb-widget-alpha17.json`;
  Gesamtstand: `distribution/tests/editions-0.2-alpha.17-readiness.json`.

Bei der Paketvorbereitung blieb der damalige Client unverändert. Anschließend
wurde auf Nutzerauftrag das neue Widget mit Profilübernahme in einer frischen
Sandbox gestartet; siehe Startbeleg oben. Ein echtes OTB mit dem neuen Widget
bleibt noch zu testen. Die nachfolgenden Live- und Installerbelege gelten nur
für den vorherigen Stand. Alte signierte Kandidaten
`.build/alpha17-otb-candidates` enthalten die neue Anzeige **nicht** und müssen
vor einer Veröffentlichung neu gebündelt und installationsgeprüft werden.
Dieser Auftrag bereitet private Spielpakete zur Sandbox-Abnahme vor.
Keine Veröffentlichung, kein Commit, Push oder Kanalwechsel.

## Live-OTB: lokale Aktivität bestätigt, Restabnahme offen

52 Messpunkte über 4:09 Minuten: 17 angenommene Systemnutzungen und 425
Bewegungssignale, keine Resets nach dem Anlauf oder gemeldete Queue-Verluste.
Widget sichtbar, Serverwertung weiterhin unbekannt. Längste Signalpause nur
13 Sekunden; Warnübergang bei 60 Sekunden, Tod/Wiederbelebung und Matchende
noch nicht live geprüft. Gezielte Namensfix-Abnahme ebenfalls offen.
[Live-Analyse](OTB-LIVE-ALPHA17-2026-11-20.md), Beleg
`distribution/tests/otb-alpha17-live-20261120.json`. Client unverändert geöffnet.

## Aktuell gestarteter OTB-/Namenstest

Am 20.11.2026 den neuen Enhanced-Kandidaten über Starter 17 mit D3D11 in der
frischen Box `PGForgeAlpha17OtbNames` gestartet. Profil und Einstellungen frisch
übernommen: drei Profile, eine geschützte Anmeldung samt Gerätezuordnung,
Windows-Mixer 8 % ohne Stummschaltung. Vorheriger normaler Client regulär beendet;
seine Installation und Profile unverändert. 16 Selector-Zyklen, 51 geladene
Dateihashes, Sandboxie und tatsächliches D3D11 bestätigt. Anmeldung, Serververbindung
und sichtbarer Orbit geprüft; Client bleibt zum Test geöffnet.

Startbeleg: `distribution/tests/editions-0.2-alpha.17-otb-launch.json`.
Echter OTB-Matchtest und Namensfix-Abnahme sind noch ausstehend. Nichts
veröffentlicht, gepusht oder an den öffentlichen Updatekanälen geändert.

## Aktueller Sandbox-Stand: lokale OTB-Erkennung und Namensfix

Neue Umsetzung auf Nutzerauftrag vom 20.11.2026. Core bleibt bytegleich zum
geprüften Namensfix; Enhanced ergänzt die lokale OTB-Beobachtung und optionale
Frühwarnung. Die Serverwertung bleibt ausdrücklich unbekannt. Details:
[Lokale OTB-Erkennung](ALPHA17-LOCAL-OTB.md).

Aktueller Build: `.build/editions/alpha17-otb-final-build`.
Abschließende Prüfung: `.build/editions/alpha17-otb-final-tests`.
- 62 Suiten und sechs Negativkontrollen bestanden; 520 OTB-Prüfungen.
- Native D3D9-/D3D11-Prüfungen beider Editionen; Enhanced mit je 597 UI-Checks.
- Namensfix: 93 Zielanzeigenchecks je Edition und native initiale Namenslayouts.
- Core-JAR bytegleich zum Namensfix; 135 gemeinsame Klassen identisch,
  native DLLs unverändert. OTB-Erweiterung ausschließlich Enhanced.
- Neue vollständige private Spielpakete: `C:\PGF17O`, je
  `Pirate-Galaxy-Forge-<Core|Enhanced>-0.2.0-alpha.17`.
- Neue signierte lokale Installer/Updatepakete: `.build/alpha17-otb-candidates`.
- 64 Installations-/Upgrade-/Reparatur-/Rollbackchecks in eigener Sandbox
  bestanden: `.build/alpha17-otb-installer-tests`, Upgrade von alpha.16.
  Profile, Einstellungen und DPAPI-Erhalt mit Testdaten geprüft.
- Maßgebliche Belege: `distribution/tests/editions-0.2-alpha.17-readiness.json`
  und `distribution/tests/local-otb-alpha17.json`, an die neuen Hashes gebunden.
  Frühere Readiness unverändert als `.build/alpha17-initial-readiness.json` gesichert.
- Die eigens gestarteten Prüfprozesse sind beendet. Der laufende normale Client
  bleibt geöffnet; keine echten Anmeldedaten oder Profile für Tests verwendet.
- Laufende Spielabnahme ausstehend; keine Übernahme echter Profile und kein
  authentifizierter Spielstart in dieser Vorbereitung.

Die nachfolgenden früheren Paket-/Installationsbelege gelten weiterhin nur für
ihre damaligen Bytes. Laufender normaler Client bleibt unangetastet.
Keine Veröffentlichung, kein Commit, Push oder Kanalwechsel.

## Historie: Veröffentlichung wegen Namensregression angehalten

Nach der zunächst positiven Rückmeldung meldet der Nutzer abgeschnittene
Allianz-Namen, die sich erst nach Anklicken korrigieren. Der private Kandidat
ist dadurch nicht zur Veröffentlichung geeignet. Die Vorprüfung hat noch
keinen Commit, Push, Upload oder Kanalwechsel ausgeführt.

Die gemeinsame Callback-Schutzprüfung wurde eingegrenzt, damit initiale
Namens-/Symboländerungen erhalten bleiben. Neue Build-/Prüfbelege werden
separat erzeugt; die folgenden Belege gelten ausschließlich für die alten
Paketbytes und werden nicht auf die Nachbesserung übertragen.
Der laufende Sandbox-Client bleibt unverändert geöffnet.

## Geprüfter Nachfix für den nächsten Sandbox-Test

- Build: `.build/editions/alpha17-name-build`; Spielbasis 1002133.
- Prüfungen: `.build/editions/alpha17-name-tests`: 62 Suiten und sechs
  Negativkontrollen bestanden; 93 Zielanzeigenchecks je Edition.
- Sechs native Namenslayouts je Edition/Renderer: lange und farbige Namen,
  Umlaute, initiale Symbolbereinigung sowie Breiten vor/nach Auswahl geprüft.
- Core und Enhanced unter D3D9 und D3D11 bestanden. 135 gemeinsame Klassen
  identisch; gegenüber dem ersten alpha.17-JAR nur `awa.class` geändert.
- Neue vollständige private Sandbox-Pakete: `C:\PGF17N`, je
  `Pirate-Galaxy-Forge-<Core|Enhanced>-0.2.0-alpha.17`.
- Hashgebundener Nachweis: `distribution/tests/target-name-regression-alpha17.json`.

Der Nachfix wurde noch nicht im echten Spiel gestartet. Die bisherige
Live-Abnahme deckt ihn nicht ab. Die alten signierten Installer enthalten ihn
nicht; neue signierte Pakete samt passenden Installationsprüfungen sind vor
einer Veröffentlichung erforderlich. Nichts veröffentlicht oder gepusht.

## Historischer Sandbox-Start des ersten Kandidaten

Am 20.11.2026 über den unveränderten, lokal geprüften Installer und Starter 17
mit D3D11 gestartet. Box `PGForgeAlpha17Targets`, Container `C:\PGF17Q`;
Starter PID 53168, Spiel PID 52744. Anmeldung und Orbit sichtbar bestätigt;
der Client bleibt für den Nutzer geöffnet. Startdiagnose ohne Startfehler,
UI-/Zielanzeigenzähler bereits im Diagnoseverlauf vorhanden.

Der normale alpha.16-Client wurde auf ausdrücklichen Auftrag regulär mit
Exitcode 0 geschlossen. Drei Profile, eine geschützte Anmeldung und aktuelle
Einstellungen frisch übernommen; der echte Credential-Reader bestätigt die
Nutzbarkeit ohne Ausgabe von Anmeldedaten. Windows-Mixer wieder 8 %, nicht stumm.
16 Selectorzyklen und 47 geladene Dateihashes geprüft. Normale Installation,
Windows-Shell-Folder und fremde Sandbox-Konfigurationen unverändert.
Beleg: `distribution/tests/editions-0.2-alpha.17-launch.json`.
Die konkrete Gameplay-Abnahme der Zielanzeigenkorrektur steht weiterhin aus.

## Änderungen

- Unabhängige Lebens-/Schildbalken und Schutz vor verspäteten Aktualisierungen
  geschlossener Zielanzeigen in beiden Editionen.
- Stille reine Widget-Existenzprüfungen; echte Zugriffsfehler bleiben sichtbar.
- Begrenzte UI-/Audio-Zähler in Live-Logs und Schema-4-Diagnoseexporten.
  Fehlgeschlagene Sounds sind nun anhand bereinigter Ressourcennamen zuzuordnen.

Die gemeinsame Implementierung ist in Core und Enhanced byteidentisch.
Native Rendererdateien bleiben auf dem bisher gepinnten Stand.

## Historische Artefakte und Testbelege des ersten Kandidaten

- Java-Build: `.build/editions/alpha17-build`.
- Gemeinsame Regressionen und native UI-Prüfungen:
  `.build/editions/alpha17-verified-tests`.
- Starter-/Exporttests: `.build/alpha17-startup-tests`.
- JVM-/Starter-Integration: `.build/alpha17-observability-tests`.
- Signierte lokale Installer-/Updatekandidaten: `.build/alpha17-candidates`.
- Isolierte Installationsprüfung: `.build/alpha17-installer-tests`.
- Vollständige private Spielpakete für beide Renderer: `C:\PGF17A`.
- Hashgebundener Gesamtbeleg: `distribution/tests/editions-0.2-alpha.17-readiness.json`.

Abgeschlossen: 62 Editionssuites und sechs Negativkontrollen, native UI unter
D3D9/D3D11, 73 Starter-/Exportchecks je Edition, neun JVM-/Starterchecks je
Edition sowie 14 ungültige Berichtsfälle. Die echte Sandboxie-Installation
von alpha.16 auf alpha.17 besteht 64 Prüfungen einschließlich Profilübernahme,
Reparatur, Rollback und Editionstrennung mit ausschließlich künstlichen Daten.
Native Soundfehler werden für beide Editionen und Renderer korrekt gezählt;
die unveränderte Original-Zielklasse reproduziert den behobenen Nullzugriff.

Der Testbericht lag wegen des Benutzerprofilpfads unter `user/current` statt
`drive/C`. Er wurde unverändert an den erwarteten Beobachtungspfad kopiert;
anschließend prüfte der bestehende Testläufer die Paket- und Installationshashes.
Die Pfadauflösung und identischen Berichtsbytes sind im Gesamtbeleg festgehalten.

Der Gesamtbeleg ist maßgeblich für die Vorbereitung und die geprüften Paketbytes.
Die öffentliche Installation bleibt unverändert. Die unveränderlichen Kandidaten
enthalten keine echten Profile oder Anmeldedaten; diese wurden beim oben
dokumentierten Start ausschließlich in die private Sandbox-Kopie übernommen.
Für die Live-Diagnose Starter 17 aus dem geprüften Installer verwenden. Der
direkte Java-/Hoststart des privaten Spielpakets ersetzt keinen Startertest.
Diese abschließenden Prüfnotizen ändern die bereits gebauten Paketbytes nicht.

## Offene Befunde und Grenzen

Die Materialprüfung reproduziert einen D3D11-Vererbungsfehler bei
`Skyscraper.ground`; ein isolierter Syntax-Gegenversuch beseitigt ihn. Dieser
separate native Rendererfix ist in alpha.17 noch nicht enthalten. Drei weitere
Materialreferenzen bleiben im geprüften Cache ohne Definition. Bekannte
Originalskriptfehler werden nicht als neue Downloadkorruption ausgegeben.

Keine Behauptung einer Behebung aller Audiofehler, aller fehlenden Widgets,
kamerabhängiger Helligkeit oder der offenen Sirius-Absturzursache. Der erste
Kandidat war in Enhanced bis zum authentifizierten Orbit geprüft. Für den
Namens-Nachfix steht der erneute Spieltest noch aus. Wine/macOS und fremde GPUs nicht erneut geprüft.
Installer/Starter haben weiterhin keine Windows-Authenticode-Signatur; lokale
Updatepakete verwenden die bestehende RSA-Signaturidentität.

[Implementierung, Materialvergleich und Testablauf](ALPHA17-TARGET-UI-AUDIO.md)
