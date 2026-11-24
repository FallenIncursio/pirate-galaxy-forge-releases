> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Core und Enhanced 0.2.0-alpha.4 — Release- und Prüfstand

**Veröffentlicht und öffentlich geprüft am 15.11.2026.** Beide Releases und
Updatekanäle liefern alpha.4: Core Sequenz 4, Enhanced Sequenz 85; Starterrevision 12.
Alle 14 öffentlichen Dateien wurden erneut heruntergeladen und anhand ihrer
Prüfsummen geprüft. Release- und Kanalmanifeste sind RSA-verifiziert; die normalen
Update-URLs und beide README-Installerlinks liefern die erwarteten Dateien.
Der Nutzer bestätigte zuvor den Enhanced-D3D11-Ranglistentest mit „funktioniert“.
Frühere Releases und der ältere Enhanced-Kanal bleiben unverändert.

Binärquellencommit: `66385c73ecdb122d073a62742059f506b9eb6f1e`. Die nachfolgende Veröffentlichungserfassung
ändert keine getesteten Programmdateien. Beleg im Quellrepo:
`distribution/tests/editions-0.2-alpha.4-publication.json`.

Der erste vollständige Teststart deckte einen Verifikationsfehler im neuen
Ranglisten-Patch auf. Der unveröffentlichte Kandidat wurde durch einen Neubau mit
neu berechneten JVM-Frames ersetzt; alle im Korrekturledger erfassten Spielklassen sind Teil
der JVM-Ladeprüfung. Siehe [Startkorrektur](../technical/ALPHA4-CODE-CHANGES.md).

## Änderungen

Beide Editionen erhalten die gemeinsame Ranglisten-Ladekorrektur mit Fehler-/
Timeoutzustand ohne zusätzliche Fußzeile, die korrigierte D3D11-HUD-Fensterzuordnung,
korrekte Erkennung der D3D11-Kantenglättung und die bewegte originale Shopvorschau
samt Bereinigung beim Artikelwechsel und Schutz gegen verspätete Auswahlantworten. Enhanced erhält zusätzlich
die wiederherstellbare Energiekugelmarkierung. Die Produktgrenzen bleiben erhalten.

[Code und Patchverträge](../technical/ALPHA4-CODE-CHANGES.md) ·
[Kumulative Funktionen und 32-Bit-Vergleich](../overview/FEATURES.md).

## Prüfung und Abnahmegrenzen

Die Prüfung ist an `.build/editions/alpha4-ranking-ready-{build,tests}` und
`.build/alpha4-ranking-ready-candidates` gebunden. Der historische Vorbereitungsbeleg
`distribution/tests/editions-0.2-alpha.4-ranking-readiness.json` bleibt unverändert.
Die anschließende Nutzerbestätigung steht in `alpha4-user-acceptance.json`, der
Freigabebeleg in `editions-0.2-alpha.4-release-candidates.json` unter demselben Ordner.

- 40 Java-/UI-Suiten, darunter acht native UI-Suiten für D3D9/D3D11, sowie die
  Enhanced-Funktionstests bestanden.
- Sieben synthetische Java-8-Protokollpakete mit je 51 Prüfpunkten pro Edition;
  Ranglistensteuerung einschließlich schneller Wechsel und interner Folgeaufträge
  mit dem ursprünglichen Spiel-Scheduler geprüft.
- 56 Installations-/Upgrade-/Reparaturprüfungen ab alpha.3 und 24 Prüfungen der
  Installer-Oberfläche mit den finalen Paketbytes bestanden.
- Die unveränderten Starter-/Updaterquellen bleiben durch 29 bzw. 32 Prüfungen
  je Edition abgedeckt. Drei native Fehlerstarts je finalem Starter geprüft.
- Beide Editionen in der neuen Sandbox installiert; D3D11-Geräte- und
  Selector-Prüfung bestanden. Enhanced anschließend mit übernommenen Einstellungen,
  Profilen und verschlüsselten Anmeldedaten gestartet. Windows-Mixerlautstärke
  erhalten; verbundene Spielsitzung und gefüllte Pilotenrangliste beobachtet.
- Der Nutzer bestätigte den gezielt für Clanrangliste und Divisionswechsel
  gestarteten Enhanced-D3D11-Stand und gab die Veröffentlichung frei. Eine
  vollständige Einzelabnahme aller Funktionen wird daraus nicht abgeleitet.

Die gezielten nativen Regressionen prüfen HUD-Auswahl, Übernehmen und erneutes Laden
nach Renderfensterwechsel, unveränderte Ranglistengeometrie und sechs Antriebsspur-
Auswahlwechsel. Der alte Animationszustand reproduzierte den Shopfehler; der neue
Aufbau erholt sich davon.

Offen bleiben eine gesonderte Core-Spielsitzung mit diesen finalen Bytes, vollständige
HUD-/Shopfarben-/Kantenglättungs-/Energiekugelabnahme, weitere Planeten- und
Erebos-Orbit-Wechsel sowie längere Sitzungen. Weitere GPUs/Treiber und Wine sind
separat zu prüfen. Die allgemeine Nutzerbestätigung ersetzt diese Einzelprüfungen nicht.

Die Kantenglättung wird nicht zwangsweise eingeschaltet. Zum Bildvergleich dieselbe
Auflösung, HUD-Skalierung und Grafikoption verwenden; 4x-MSAA benötigt GPU-Leistung.
Ein Ranking-Timeout stellt keine erfolgreiche Serverantwort dar. Shop-GPU-Tests
verwenden ein diagnostisches Material und ersetzen nicht die originale Farbabnahme.

Die Hinweise auf lokale Kandidaten in unveränderten Paketbeilagen beschreiben den
damaligen Teststand. Maßgeblich für den Veröffentlichungsstatus sind die aktuellen
Release-Seiten und signierten Updatekanäle.
