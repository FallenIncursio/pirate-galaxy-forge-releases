> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Alpha.13: Ressourcen, Absturzdiagnose und Updatevorbereitung

Stand 19.11.2026. Gemeinsame Änderungen für Core und Enhanced, Spielbasis 1002133.
Veröffentlichung von Core und Enhanced einschließlich beider Updatekanäle freigegeben.
Die laufende Testsitzung bleibt geöffnet.

## Ausgangsbefund und Original32

Sechs zum Analysezeitpunkt verfügbare private Berichte enthalten keine ausreichende
native Fehlerstelle. Der neueste betrifft Enhanced alpha.9 beim Sirius-Landeanflug
und den Prozesscode 0xc0000409. Dieser Code allein bestimmt die Ursache nicht.
Ein Ressourcen-NPE ist im Bericht genannt, aber der alte Diagnosesammler konnte
Exception-Namen und Stackzeilen verschiedener Ereignisse vermischen.

Die Klassen ds, dp, azc, aze und fw sind im geprüften Original32, alpha.9 und
alpha.12 bytegleich. Die Offlineprobe bestätigt zwei Originalfehler: fehlender
Ressourcendienst liefert null; jh-Fehler werden ohne Grenze rekursiv wiederholt.
Der bekannte RTSS-Materiallebensdauerfix seit alpha.7 bleibt enthalten. Die neue
Härtung wird nicht als nachgewiesene Behebung des nativen Sirius-Absturzes bezeichnet.
Rohberichte und Originalklassen bleiben außerhalb der Quellrepo.

## Ressourcenlader

`modules/shared/src/pg64/client/ResourceRequests.java` besitzt je ds-Instanz eine
volatile Dienstbindung. Jede Bindung bekommt eine neue Identität, auch beim
erneuten Binden desselben Proxys. Vor und nach der RPC sowie vor jedem erneuten
Versuch wird die Identität geprüft. Alte Antworten werden verworfen.

- Regulär genau eine vorhandene Metadatenanfrage; keine neuen Hintergrundabfragen.
- Ausschließlich jh oder eine kurze entsprechende Ursachenverkettung: höchstens
  vier Versuche mit 125, 250 und 500 ms Pause. Kein rekursiver Aufrufstack.
- Fehlender Dienst und sonstige Exceptions führen zu einem Ladefehler; sie werden
  nicht zu einer dauerhaften UNAVAILABLE-Markierung umgedeutet.
- Echte null-Antwort des Dienstes behält die ursprüngliche Nichtvorhanden-Semantik.
- Interrupt bleibt gesetzt und beendet Anfrage/Wartezeit. Auch die beiden
  verschluckten Sleep-Interrupts des äußeren ds-Metadatenladewegs sind korrigiert.
- Ein laufender RPC behält seinen vorhandenen Transport-Timeout. Die Änderung
  erzeugt keine zusätzlichen Executor-Threads und erzwingt keinen Prozessabbruch.

`EditionFixes` patcht Konstruktor, Dienstbindung, Abfragemethode und zwei Warteorte.
Original-/Eingabehash und fünf erwartete Änderungen stehen in `edition-fixes.tsv`.
Ein unbekannter Input oder geänderte Patchstellen brechen den Build ab. Die
originalen Inhaltsdownloads, Ressourcenprüfungen und UI-Szenen bleiben erhalten.
Dienstgeneration ist keine erfundene serverseitige Planetengeneration.

## Diagnose und Datenschutz

`StartupDiagnostics` hält acht begrenzte Java-Ereignisse mit UTC/relativer Zeit,
Ausgabestrom, Ereignisart und höchstens zwölf zugehörigen Stacknamen. Parserzustand
ist pro stdout/stderr getrennt. Ein neues Ereignis startet einen neuen Stack;
Klassen mit `$` werden erhalten. Meldungstexte, Threadnamen, Argumente und
Quelldateipfade werden nicht in den technischen Bericht übernommen.

64 begrenzte Phasen mit Dauer bleiben im lokalen Kontext. Der Bericht nennt den
Prozess-Exit separat und kennzeichnet Java-Ereignisse nicht als bestätigte
Absturzursache. Das öffentliche Drahtformat bleibt Schema 2 und wird gegen den
vorhandenen Dienstvertrag getestet; keine Servermigration/Deployment erforderlich.

Vorhandene, zur Prozess-ID und Laufzeit passende WER-Minidumps werden kurz erneut
gesucht. Native Exception und FAST_FAIL-Untercode werden zusätzlich zur bereits
vorhandenen Modul-/PDB-/Offsetauswertung gelesen. Keine Interpretation des
Untercodes als automatische Sicherheits- oder Stackoverflow-Diagnose.

Neue JVM-Startvorlagen schreiben `hs_err_pid%p.log` in den lokalen Diagnoseordner.
Nur der begrenzte Kopf der passenden PID-Datei wird ausgewertet: Exception und
gegebenenfalls Modulname plus relativer Offset. Keine Arguments-/Speicherbereiche.
Speicherabbilder bleiben optional; Rohlogs/JVM-Fehlerdateien werden nicht automatisch
versendet. Es wird keine globale WER-Konfiguration geändert. Ohne vom System/JVM
erzeugte Datei kann weiterhin native Evidenz fehlen.

## Updater

Neue signierte Release-ZIPs nutzen DEFLATE Level 6. Sonstige deterministische
Archive und historische Releasebytes behalten ihr bisheriges Format. Der lokale
alpha.12-Vergleich ergab rund 63 % weniger Volumen; die tatsächlichen alpha.13-
Größen stehen im Kandidatenbeleg. Keine Übertragung dieser Ersparnis auf gesamte
Installationsdauer oder Spiel-FPS.

Paket und Java-Archiv behalten unter ihrem Inhalts-Hash eine Teil-Datei samt
kleinem Validator. Normaler HTTPS-Transport sendet Range/If-Range nur mit starkem
ETag. Eine 206-Antwort muss Bereich, Gesamtgröße, Restlänge und ETag exakt bestätigen;
200 ersetzt die Teil-Datei vollständig. Fehlerhafte Bereiche/Hashes werden verworfen.
Der vollständige signierte SHA-256 bleibt zwingend vor Übernahme in den Archivcache.
Ein Verbindungsabbruch kann einmal im normalen Transport fortgesetzt werden.
curl/GitHub-Fallback startet bewusst frisch; Teilbytes verschiedener Transportwege
werden nicht ungeprüft kombiniert. Eine fortschreitende langsame Verbindung ist
kein Stillstand; zusätzlich gilt eine gesamte Transferzeitgrenze.

Bei vorhandener Installation kann der Nutzer bis vor der Aktivierung das Update
verschieben. Blockierende HTTP-Lesevorgänge können dabei abgebrochen werden;
fortsetzbare Teilbytes bleiben für den nächsten Versuch. Die bisherige Installation
bleibt aktiv und wird vor Start normal geprüft. Für Erstinstallation/Reparatur wird
kein nicht vorhandener funktionierender Vorgänger versprochen.

Fehlende REMOTE-Caches (`r` plus kanonische signed-int-Dateinamen) werden nur aus
dem letzten Renderer derselben Edition übernommen. Keine LOCAL-/Anmeldedateien
über diesen Weg, keine Überschreibung vorhandener Ziele, keine Verzeichnisrekursion
oder Links. Größe/Anzahl sind begrenzt. Die ursprüngliche Inhaltsprüfung bleibt aktiv.

Eine bestehende Laufzeit wird gegen die neue signierte Inventarliste beim Kopieren
verifiziert. Abweichungen führen zur Archiveinrichtung. Keine Hardlinks und kein
Vertrauen in das alte Laufzeitmanifest. Hashes werden beim Kopieren/Entpacken
berechnet; unabhängige Aktivierungs- und Startprüfungen bleiben erhalten.

## Prüfungen und Grenzen

Die kanonischen Tests sind `ResourceRequestsTests`, `ReliabilityTests`,
`StartupTests`, `CrashReportTests`, `EditionUpdaterTests` und die bestehenden
Starter-/Installer-/Editionsprüfungen. Netzwerkfixtures verwenden nur eigene
Loopback-Antworten; die HTTP-Testumleitung existiert nicht im Produktbuild.

Ein bisher latent unvollständiger Klassenpfad der EditionFixes-Negativkontrollen
wurde korrigiert. Die Kontrollen nutzen jetzt wie der echte Build die aktuelle
Originalbasis und Spielabhängigkeiten; sie dürfen nicht an einem fremden
ClassNotFoundException scheitern.

Enhanced/D3D11 wurde mit übernommenen Profilen angemeldet bis auf die
Planetenoberfläche gestartet; der Nutzer meldet bisher keine Probleme. Eine
kontrollierte Abnahme sämtlicher Lande-/Verbindungswechsel ist damit nicht belegt.
Noch ausstehend: gezielter Sirius-Landeabsturztest, Langzeittest,
Erfahrungen mit real betroffenen langsamen Anschlüssen, Wine und andere GPUs.
Kamerabhängige Helligkeit, OTB-Endwertung und reale Wiederbelebung bleiben separat.
Ergebnisse und finale Artefakte: [Prüfstand](../verification/RELEASE-STATUS-0.2-alpha.13.md).
