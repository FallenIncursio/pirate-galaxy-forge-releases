# Core / Enhanced 0.2.0-alpha.14 – zur Veröffentlichung freigegeben

Stand: 20.11.2026. Spielbasis 1002133, Starter 14, Core-Sequenz 13 / Enhanced 95.
Der Nutzer meldet bisher störungsfreien Betrieb und hat die Veröffentlichung
beider Editionen, den Quell-Push und beide Updatekanäle ausdrücklich beauftragt.
Die Kanäle werden erst nach erfolgreicher Prüfung der öffentlichen Downloads
umgestellt. Die getesteten Installer und Pakete werden unverändert verwendet.

## Änderungen

Begrenzte Ressourcen-Downloads mit temporärer Datei und Integritätsprüfung;
Fehler und Abbrüche erreichen abhängige Ladeaufträge. Fehler optionaler lokaler
Login-Dateien verhindern die Anmeldemaske nicht mehr. Der Starter bestätigt erst
die Loginbereitschaft und bietet nach 45 s ohne Fortschritt Diagnose, Weiterwarten,
Neustart und Reparatur. Lokale Threadaufnahmen und HTTP-Status helfen bei der
Zuordnung. Die Reparatur erhält Profile, Einstellungen und geschützte Anmeldungen.

[Implementierung, Grenzen und 32-Bit-Vergleich](ALPHA14-STARTUP-RECOVERY.md).
Die konkrete Ursache auf betroffenen Spielerrechnern ist noch nicht nachgewiesen.

## Geprüfter Stand

- Build `.build/editions/alpha14-final-build`: 133 gemeinsame Klassen bytegleich
  in Core und Enhanced; native D3D9-/D3D11-Eingaben gegenüber alpha.13 unverändert.
- `.build/editions/alpha14-final-tests`: 60 Suiten und sechs Negativkontrollen
  bestanden, einschließlich nativer GUI-/Fokusproben beider Renderer/Editionen.
- Je Edition 19 Ressourcen-Ladetests, 13 Metadatenprüfungen, acht Signal-/Snapshot-
  Prüfungen und 50 Starterprüfungen. Erfolg, HTTP 503, Prüfsummenfehler, stockender
  Datenstrom, Dienstwechsel, lokale Dateifehler und abhängige Aufgaben geprüft.
- Je Edition sieben zusätzliche Prozessprüfungen mit echter 45-Sekunden-Frist:
  Die künstliche Java-Sequenz liefert einen Hänger, automatische Threadaufnahmen
  und einen Export; ihre spätere Loginmeldung beendet den Hängerzustand ohne Neustart.
- Je Edition 30 Zuverlässigkeits- und 32 Updaterprüfungen, außerdem signierter
  Starterwechsel 13 → 14. Neue Hängeroberfläche für beide Editionen visuell geprüft.
- Reale lokale Installer/Updatepakete in eigenen Sandboxie-Containern geprüft:
  56 alpha.13-Upgradeprüfungen (`C:\PGF14R1`), 53 Neuinstallations-/Alpha73-Prüfungen
  (`C:\PGF14R2`), einschließlich Profil-/Credential-Erhalt, Reparatur, Rückfall,
  Editionsisolation und Deinstallation. Ausschließlich künstliche Profile.

Der erste Start des zweiten Testcontainers erreichte das 20-s-Zeitlimit des
Testwrappers. Der Test wurde ohne geerbte Ausgabepipes einzeln neu gestartet und
vollständig bestanden; der erste Fehlversuch bleibt privat protokolliert.
Diese automatisierten Prüfungen verwendeten keine Spielverbindung, echten Profile
oder Spielerberichte. Ein Server-Deployment war nicht erforderlich.

## Sandbox-Abnahme und Artefakte

Enhanced wurde am 20.11.2026 über den tatsächlich installierten Starter 14 mit
D3D11 bis in die verbundene Spielsitzung gestartet. Drei Profile, Einstellungen,
eine geschützte Anmeldung und die Windows-Lautstärke wurden übernommen und
geprüft. Die Loginbereitschaft wurde bestätigt; beim Veröffentlichungsauftrag
lag keine Startfehler- oder Hängermeldung vor. Der Nutzer meldet „Bisher läuft
alles“. Eine genaue Testdauer und vollständige Funktionsabnahme sind damit nicht
belegt. Der laufende Client wird für die Veröffentlichung nicht geschlossen.

Die unabhängige Hängeraufsicht ist aktiv. Die Reparatur- und Hängerfälle stammen
aus isolierten automatischen Prüfungen; am Nutzerclient wurde kein Hänger erzwungen.

Signierte Kandidaten: `.build/alpha14-release-candidates/{core,enhanced}`.
Öffentliche Auswahl je Edition: Setup, Starter, signiertes Manifest, Update-ZIP,
Lizenzhinweise, Bibliotheksquellen und SHA256-Prüfsummen. Private Spielkopien,
Profile, Anmeldedaten, Rohlogs und Speicherabbilder gehören nicht dazu.

Hashgebundene Belege: `distribution/tests/startup-recovery-alpha14.json`,
`distribution/tests/editions-0.2-alpha.14-readiness.json`,
`distribution/tests/editions-0.2-alpha.14-launch.json` und
`distribution/tests/editions-0.2-alpha.14-release-candidates.json`.
Die ursprünglichen Vorbereitungsbelege bleiben historische, bytegebundene Belege.

Offen bleiben eine gesonderte Core-Spielsitzung, betroffene externe Rechner,
andere GPUs, Wine und Langzeittests. Kamerabhängige Helligkeit und die native
Sirius-Absturzursache werden nicht als behoben ausgegeben. Die Spielerhänger
sind ohne deren Diagnose noch nicht abschließend zugeordnet.
