# Core und Enhanced 0.2.0-alpha.10 — Veröffentlichung beauftragt

Auftrag: OTB-Widget und lokale Diagnose in Enhanced verbessern; gemeinsamen
Wiederbelebungsdialog in Core und Enhanced absichern. Laufenden Client erhalten.
Der Nutzer hat die Veröffentlichung einschließlich beider Updatekanäle freigegeben.
Ein neuer OTB-Spieltest ist derzeit nicht möglich und wird nicht als bestanden
ausgewiesen. Auch die praktische Wiederbelebungsabnahme bleibt offen.

## Änderungen und Herkunft

- Beide Editionen: geerbte NullPointerException im Wiederbelebungsdialog behoben;
  fehlende Timer bleiben unbekannt, später eintreffende Werte werden übernommen.
- Enhanced: kompakte Erklärung bei unvollständigen Aktivitätsdaten; unabhängige
  Aktualität der Zähler; begrenztes, abschaltbares lokales OTB-Journal.
- Gemeinsame native Bibliotheken, Renderer und die alpha.9-Optimierungen bleiben
  unverändert. Keine neue Leistungs-, Sicherheits- oder Serverfreigabe behauptet.

[Umsetzung, Diagnoseformat und Grenzen](ALPHA10-OTB-RESURRECTION.md) ·
Beobachteter Livefehler: Diagnose vom 18.11.2026 im Quellrepo dokumentiert.

## Vorbereitung

Maßgeblicher Java-Build: `.build/editions/alpha10-build3`.
Tests: `.build/editions/alpha10-tests/result.json`.
Unabhängiger OTB-/Core-Vergleich: `.build/editions/alpha10-contract.json`.

- 50 Editionssuiten und sechs Negativkontrollen bestanden.
- 481 OTB-Prüfungen gegen das neue Enhanced-JAR bestanden, einschließlich
  Einzelzähler-Alter, beobachteter Datenlücke, paralleler Änderungen und Journal.
- Je 16 Prüfungen des Cooldown-Helfers in Core und Enhanced bestanden.
  Die gepatchte Originalklasse wurde geladen/verifiziert; der reale
  Wiederbelebungsdialog ist weiterhin ein separater Spieltest.
- Native Oberfläche D3D9 und D3D11: jeweils 54 Core- und 1.152 Enhanced-Prüfungen;
  1024/1920/3440 Pixel und 100/150/200 % HUD. Acht OTB-Zustände,
  Ein-/Ausschalten der Diagnose, Fokusfreiheit und Wiederaufbau geprüft.
  Diagnoseansichten bei 100/200 % zusätzlich visuell kontrolliert.
- Core-JAR gegenüber alpha.9: genau zwei geänderte Einträge, die ursprüngliche
  Dialogklasse und der neue gemeinsame Helfer. Beide in Enhanced bytegleich.
  Zehn OTB-Helferklassen ausschließlich Enhanced; elf Original-OTB-Modell-/API-
  Klassen und alle nativen Eingaben gegenüber alpha.9 unverändert.
- Neue Helfer auf direkte Transportaufrufe und replizierte Schreibzugriffe
  geprüft. Das ist eine Bytecodeprüfung, kein neuer Live-Netzwerkmitschnitt.

Paketverzeichnis: `C:\PGF10A`, je
`Pirate-Galaxy-Forge-<Core|Enhanced>-0.2.0-alpha.10`.
Der Paketierungsbeleg `C:\PGF10A\result.json` und die jeweiligen `candidate.json`
belegen den Abschluss; der sanitisierte zusammengefasste Nachweis steht unter
`distribution/tests/editions-0.2-alpha.10-readiness.json`.
Pakete sind privat, Updates deaktiviert, keine Profile oder Anmeldedaten importiert.
D3D9- und D3D11-Startkonfigurationen werden lokal vorbereitet; kein Spielstart.

Die neuen Updatekanäle verwenden Core-Sequenz 9 und Enhanced-Sequenz 91.
Starterrevision und Mindeststarter bleiben 12. Die Aktivierung erfolgt nach der
Prüfung der öffentlichen Downloads. Vorheriger Stand: alpha.9, Sequenzen 8/90.

## Offene praktische Abnahme

Neue Spielbytes noch nicht mit dem Nutzer gestartet. OTB-Endwertung, reguläre
Wiederbelebung im Spiel, andere GPUs und Wine sind nicht neu abgenommen.
Der vorhandene alpha.9-Prozess bleibt offen. Profile, Anmeldung, Einstellungen
und Windows-Lautstärke werden in diesem Vorbereitungsauftrag nicht verändert.
