> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Enhanced 0.2.0-alpha.23 – Release-Prüfstand

Sirius-Quarc-Anzeige und gelbe BP-Teilezahlen für Spielversion 1002133.
Enhanced-Sequenz 104 ist aktiv nach bestätigtem D3D11-Sandbox-Test.
Alle sieben öffentlichen Downloads, Prüfsummen, RSA-Manifest und README-Installerlink
sind geprüft. Der Kanal wurde erst nach erfolgreicher Downloadprüfung aktiviert.
Core bleibt alpha.17 / Sequenz 16, der bisherige Nutzerclient bleibt geöffnet.

## Korrigiert

- BP-Teilegruppen (18/14/12/5), Namenssortierung und Merkliste-Hinweis bleiben
  beim Ergänzen gelber Teilezahlen in Karte und Orbit erhalten.
- Fehlende Clan-/Spielerdaten oder Freigabefelder erscheinen als unbekannter
  Quarc-Status. Vorhandener Quarc-Typ oder Exploration ersetzen keine Freigabe.
- Sichtbare Kartenfenster lösen keinen Float-/Integer-Castfehler mehr aus.
  Modell- und Markerfehler werden getrennt behandelt; ein Markerfehler löscht
  keinen gültigen Status im Planetentext.
- Lokale Diagnose Schema 2 trennt Karten-/Orbiteinträge, Snapshot-Verfügbarkeit,
  ausgegebene Teilezahlen, Merkliste und Fehlerbereiche. Keine privaten Inhalte,
  keine Zusatzabfragen und kein automatischer Export.

## Prüfung

- Finale signierte Pakete: 59 Neuinstallations-/Alpha-73-Prüfungen, 64 Upgrade-
  Prüfungen vom bisherigen Enhanced alpha.22 und 24 Installer-UI-Prüfungen bestanden.
  Reparatur, Rollback, Profile, Rendererwahl und geschützte Test-Anmeldedaten geprüft;
  echte Nutzerprofile wurden in diesen Installer-Tests nicht verwendet.
- RSA-Signatur, vollständiges Paket-Inventar und Bibliotheksquellen geprüft.

- 62 Editionsgates und 22 Negativkontrollen bestanden.
- Sirius: 253 Modell-/Cache-/Grenzprüfungen bestanden.
- Diagnose: 20 Export- und Datenschutzprüfungen bestanden.
- Native Enhanced-UI: 3001 Prüfungen auf D3D9 und 3001 auf D3D11, einschließlich
  sichtbarer Kartenpanels und der unbekannten Statuszeile.
- Core: alle Kandidaten-JARs, 138 Helferklassen und native Eingaben unverändert.
  Spiel-JAR: `918093c4e935e8f8af3eab689b956736843c73573332a574e82752eda0612310`.
- Die Schiffskonfigurationsansicht bleibt verworfen; unabhängige Starter-
  Speicherpflege bleibt separat; dieses Release verwendet Starterrevision 17.

Enhanced-Spiel-JAR: `6b412cad726aca4c6f5013215e88375f56dc5dc3c539540de3d2a4217b110761`.

Die automatisierten Prüfungen liefen mit künstlichen Modelldaten und nativer GUI.
Am 22.11.2026 wurde der getestete Stand mit D3D11 in der Sandbox gestartet.
Profilübernahme, geschützte Anmeldung, Einstellungen und Windows-Lautstärke
wurden geprüft; angemeldete Spielszene und Serververbindung bestätigt.
Der Nutzerclient bleibt geöffnet.

Die gemeldeten Sirius-/BP-Fixes wurden im Sandbox-Test vom Nutzer bestätigt.
Vollständige Clanmissionsabläufe und Zustandswechsel durch andere Mitglieder
sind damit nicht vollständig abgedeckt. Fehlende Schlüssel
bleiben bis zur bestätigten Bedeutung ausdrücklich unbekannt.
[Bedienung, Diagnose und Abnahmeschritte](../technical/ALPHA23-SIRIUS-QUARC.md).

Binärquellencommit: `f3a6d61eafcc4e60a5a31698e4819a0f6d1d07e1`. Veröffentlichung und unveränderter Core-Stand
sind im Quellrepository unter `distribution/tests/editions-0.2-alpha.23-publication.json` dokumentiert.
