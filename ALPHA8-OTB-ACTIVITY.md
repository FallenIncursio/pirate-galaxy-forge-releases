# Enhanced alpha.8: OTB-Aktivitätsprüfung

Das kleine Widget erscheint automatisch im eigenen laufenden OTB. Es zeigt den
Stand der vorhandenen Clientkriterien: Zeit, Systemeinsätze, Flug und Zusatz.
Abschaltbar unter **Forge → Anzeige → Widgets**. „Zusatz“ bedeutet mehr
Systemeinsätze **oder** mehr Flugstrecke; die Grundanforderungen bleiben daneben
erforderlich.

## Bedeutung und Grenzen

„Clientkriterien erfüllt“ und „Im Client aktiv markiert“ garantieren weder eine
Belohnung noch Sperrfreiheit. Die endgültige Wertung trifft der Server.
Ein echtes OTB mit regelmäßig empfangenen Aktivitätswerten und ein Abgleich mit
der Endauswertung sind noch nicht bestätigt. Der Benutzer konnte während der
Vorbereitung kein OTB testen. Fehlende Daten werden als unbekannt angezeigt.

In den letzten fünf Minuten der vorhandenen Matchuhr weist das Widget auf offene
Kriterien hin. Diese fünf Minuten sind eine UI-Hilfe und keine bestätigte
serverseitige Inaktivitätsfrist. Ungeklärte Zählereinheiten werden nicht als
Aktivitätsminuten oder Meter ausgegeben; die Anzeige verwendet Prozente.

## Umsetzung

- Vorhandene lokale Teilnehmermodelle und fünf relevante PropertyMap-Felder.
  Maximal zwei lokale Auswertungen pro Sekunde. Keine zusätzliche Serverabfrage,
  kein neues Ping-Paket, keine Änderung replizierter Werte und keine Automation.
- Auswertung entsprechend der vorhandenen `zn.isActive()`-Logik mit aktuellen
  Clientparametern. Originalmodell und Protokoll bleiben unverändert. Dies
  beweist keine Übereinstimmung mit aktuellen serverseitigen Grenzwerten.
- Fehlende/falsch typisierte Werte, rückläufige Zähler und mehr als 30 Sekunden
  ohne relevante beobachtete Aktualisierung erhalten keine sichere Bewertung.
  Die 30 Sekunden sind eine Schutzregel der Anzeige. Ein erster gespeicherter
  Stand gilt noch nicht als frische Aktualisierung.
- Teilnehmer-, Piloten-, Welt-, Match- und Verbindungswechsel verwerfen die alte
  Zuordnung und entfernen Observer. Die vorhandene Verbindung wird nur gelesen.
- Native HUD-Oberfläche ohne Eingabefokus oder gespeicherte native Zeiger.
  Ausblendung im Orbit, nach Matchende, bei Verbindungsabbruch und im Forge-Dialog.
- Keine neue Telemetrie oder Speicherung von Aktivitäts-Rohdaten.

## Prüfung und Vergleich

461 gezielte Offlineprüfungen umfassen Grenzwerte gegen das Originalprädikat,
Datenlücken, Aktualität, Rückschritte, echte Observer und Verbindungswechsel.
Native MyGUI-Prüfungen unter D3D9 und D3D11 bei 1024×768, 1920×1080 und
3440×1440 mit HUD-Skalierung: je 624 Bedienungs-/Anzeigeprüfungen einschließlich
Apply/Discard, Fokusfreiheit, Abbau/Neuanlage und Abstand zur OTB-Punkte-/Zeitanzeige.

Enhanced wurde mit D3D11 in der Sandbox bis zur verbundenen Planetenoberfläche
gestartet. Profile, Einstellungen, geschützte Anmeldung und Windows-Lautstärke
wurden übernommen; die eingeschaltete OTB-Option war sichtbar. Die anschließende
Veröffentlichungsfreigabe ist keine Bestätigung eines Live-OTB-Endausgangs.

Gegenüber der gepinnten 32-Bit-Basis ist das Widget eine zusätzliche lokale
Anzeige; es repariert oder umgeht keine Aktivitätswertung. Core bleibt auf
alpha.7. Sein Spiel-JAR und alle nativen Bibliotheken bleiben unverändert.
Keine neue allgemeine Sicherheits- oder Leistungsfunktion. Der D3D11-Absturzfix
aus alpha.7 und die bisherigen Korrekturen bleiben enthalten.

[Release-Prüfstand](RELEASE-STATUS-0.2-alpha.8.md) · [Funktionsvergleich](FEATURES.md)
