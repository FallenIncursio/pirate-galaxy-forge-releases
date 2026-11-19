# Core und Enhanced 0.2.0-alpha.13 — Veröffentlichung freigegeben

Stand: 19.11.2026. Spielversion **1002133**. Der Nutzer meldet bisher störungsfreien
Betrieb von Enhanced/D3D11 und beauftragt beide Releases, Quell-Push und Updatekanäle.
Die laufende Spielsitzung bleibt geöffnet. Die geprüften Paketbytes werden unverändert
übernommen; die darin enthaltenen Beilagen dokumentieren den privaten Buildstand.
Aktuelle Freigabe und Prüfumfang sind auf dieser Seite zusammengefasst.
Core-Sequenz **12**, Enhanced-Sequenz **94**, Starterrevision/Mindestrevision **13**.
Öffentliche Downloads werden vor Aktivierung der Updatekanäle geprüft.

## Umfang

- Gemeinsamer Ressourcenlader: Dienstbindung, begrenzter Retry, Interrupts.
- Getrennte Java-Ereignisse, native Fehlercodes und bereinigte JVM-Fatal-Metadaten.
- Komprimierte Updatepakete, sichere Downloadfortsetzung, Fortschritt und Verschieben.
- Geprüfte Java-Laufzeitübernahme, getrennte REMOTE-Cacheübernahme und weniger Lesewege.
- Sämtliche bisherigen Core-/Enhanced-Fixes, Renderer und Spielbasis erhalten.

[Implementierung, Originalvergleich und Grenzen](ALPHA13-RELIABILITY-UPDATES.md) ·
[Kumulative Funktionen](FEATURES.md) · [Installer/Updater](INSTALLER-UPDATER.md).

## Prüfung

Stand 19.11.2026; alle nachstehenden Prüfungen bestanden:

- 58 Editionssuiten einschließlich nativer D3D9-/D3D11-UI-Prüfungen und sechs
  Build-Negativkontrollen. Ressourcenlader: 13 Prüfungen je Edition; zusätzlich
  zwei Negativproben gegen alpha.12, die den ursprünglichen Fehler bestätigen.
- Je Edition 36 Start-/Diagnoseprüfungen, 30 Zuverlässigkeitsprüfungen mit lokalen
  HTTP-Gegenstellen und 32 Updaterprüfungen. Zusätzlich 113 Absturzbericht- und
  58 Transportprüfungen; keine echten Spielerberichte versendet.
- Signierter Starterwechsel 12 auf 13; der unveränderte öffentliche Starter 12
  prüft und entpackt auch die finalen komprimierten alpha.13-Pakete.
- Je Edition drei Fehlerfälle durch den tatsächlichen nativen Host mit dem
  finalen Starter: Java-Exception, fehlende Hauptklasse und expliziter Exit 1.
- Echte Installer in eigenen Sandboxie-Boxen: 56 Prüfungen beim Upgrade von
  alpha.12 sowie 53 Prüfungen für Core-Neuinstallation und Enhanced von Alpha 73.
  Profil-/Rendererübernahme, geschützte Testanmeldung, Reparatur, Abbruchrecovery,
  Rollback, Deinstallation und Editionstrennung sind abgedeckt. 24 UI-Prüfungen
  der finalen Installer ebenfalls bestanden. Ausschließlich künstliche Testprofile.

Die gebauten Spielarchive unterscheiden sich von alpha.12 nur in
`com/splitscreen/ds.class` und zwei neuen `ResourceRequests`-Klassen.
Native Rendererdateien und alle bisherigen Fixes bleiben unverändert.
Source-/Test- und Artefakthashes stehen in
`distribution/tests/reliability-alpha13.json` und
`distribution/tests/editions-0.2-alpha.13-readiness.json`.

## Spieltest und bekannte Grenzen

Enhanced alpha.13 mit D3D11 ist in der Sandbox angemeldet und auf der Planetenoberfläche
mit HUD sichtbar. Drei Profile, Einstellungen und eine geschützte Anmeldung wurden
übernommen; 56 geladene Dateien, 16 Selector-Zyklen und der Windows-Mixer wurden geprüft.
Der Nutzer bestätigt: „Bisher läuft alles.“ Beim Start keine neue Java-Exception;
bekannte Trackingmeldungen sind im Vorgänger ebenfalls vorhanden.

Der konkrete native Sirius-Landeabsturz bleibt ohne passende native Evidenz offen.
Ressourcenhärtung ist kein Nachweis, dass dieser konkrete Absturz behoben wurde.
Eine separate Core-Spielsitzung, kontrollierte Lande-/Verbindungswechsel, Langzeitprüfung,
reale langsame Anschlüsse, Wine und weitere GPUs sind nicht umfassend abgenommen.
Kamerabhängige Helligkeit, OTB-Endwertung und reale Wiederbelebung bleiben separat.

## Downloadvolumen und Lieferung

| Updatepaket | alpha.12 | alpha.13 | Weniger Downloadvolumen |
| --- | ---: | ---: | ---: |
| Core | 158,407 MB | 58,158 MB | 63,29 % |
| Enhanced | 160,554 MB | 59,140 MB | 63,17 % |

MB dezimal; gemessene ZIP-Dateigrößen. Dies ist keine Zusicherung einer entsprechend
kürzeren gesamten Installation. Bei Erstinstallation können weitere Downloads nötig sein.
Installationsort, Profile und Anmeldedaten bleiben getrennt nach Edition erhalten.
Der Installer ist nicht Authenticode-signiert; Updates nutzen die bestehende RSA-Identität.
Vorherige Releasepakete und der alte Enhanced-Kanal bleiben unverändert.

Maßgebliche Belege im Quellstand: `editions-0.2-alpha.13-release-candidates.json`,
`reliability-alpha13.json`, `alpha13-user-acceptance.json` und nach Abschluss
`editions-0.2-alpha.13-publication.json` unter `distribution/tests`.
