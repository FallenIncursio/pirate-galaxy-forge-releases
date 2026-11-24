# Enhanced alpha.28 – Reparaturfelder nach Herkunft

Veröffentlicht nach bestätigtem Enhanced-D3D11-Sandbox-Test für Spielversion 1002133.
Core bleibt alpha.17 / Sequenz 16. Der laufende Nutzerclient blieb geöffnet.

## Bedienung

Unter **Forge → Anzeige → Kampf & Effekte** gibt es zwei Auswahlen:

- **Reparaturfelder: Spieler** – eigenes Schiff, Mitspieler, gegnerische Spieler
  und zugeordnete Spielertürme.
- **Reparaturfelder: PvE-Gegner** – lokal als NPC zugeordnete Feldquellen.

Beide bieten Original, Leicht reduziert, Stark reduziert und Nur Kontur.
Stark reduziert entspricht dem bisherigen Reduziert. Leicht reduziert bewahrt
mehr Leuchten und die originale Animation. Nur Kontur zeigt die Feldgrenze.
Unbekannte Herkunft bleibt original sichtbar. Originale Reichweite, Wirkung,
Animation und das separate Effektsymbol werden nicht verändert.

Explizit gespeicherte alte Einstellungen gelten zunächst für beide Kategorien.
Neue Profile verwenden Spieler Original / PvE Stark reduziert. Übernehmen speichert
beide Werte atomar; Verwerfen und Seitenwechsel folgen dem bestehenden Entwurf.

## Implementierung

Der bestehende, gehashte Enhanced-Hook in `att.do(ti,jv)` erhält zusätzlich das
zugehörige Objekt `att.bQK`. Kein neuer Serveraufruf, keine Änderung an Core.
`aeo.EU()` liefert `avatar` oder `parentavatar`. Bei empfangenen `tm`-Effekten
hat eine gültige `TriggerUserID` Vorrang vor dem Empfänger; ohne gesicherte
Absenderinformation wird nicht vom Empfänger auf den Verursacher geschlossen.
Die Effektfarbe ist keine Spieler-/NPC-Klassifikation. Die zwei ursprünglichen
Reparaturfeldmodelle bleiben die einzige zugelassene Modellgruppe.

Pro Feld werden Herkunft und Darstellungsmodus geführt. Java hält nur schwache
Objektverweise und höchstens 256 Bindungen; Besitzeränderungen werden alle
200 ms lokal nachgeführt. Native Szenen- und Partikelidentitäten werden geprüft.
Fehler räumen die eigenen Veränderungen im Renderthread auf.

Die gespeicherten IDs bleiben Original=0, Stark=1, Kontur=2; Leicht erhält ID 3.
`repair.fields.groups` speichert beide Werte in einer atomaren Transaktion.
`repair.fields.visuals` bleibt für die Migration und einen Rückfall erhalten.
Die Reihenfolge der sichtbaren Auswahl ist unabhängig von diesen IDs.

Die starke Dämpfung bleibt `0,40 / Überlagerungen`. Leicht verwendet
`0,70 / (1 + 0,65 × (Überlagerungen − 1))`. Das sind Shaderfaktoren und keine
Prozentangaben zur wahrgenommenen Helligkeit. Nur tatsächlich reduzierte Auren
gehen in die Überlagerungszahl ein. Originalfelder und Konturen schwächen
reduzierte Nachbarfelder nicht zusätzlich ab. Materialcaches unterscheiden
Reduktionsstufe und Überlagerungszahl; D3D9 und D3D11 werden getrennt gebaut.

## Diagnose

Der freiwillige lokale Export enthält zusätzlich `repair-fields.json`:
Modi, Spieler-/PvE-/unbekannte Bindungen, nachträgliche Zuordnungen, Überläufe,
Fehlerklasse sowie aktuelle native Feld-/Aurazähler. Keine Namen, Nutzer-IDs,
Koordinaten, Rohobjekte oder zusätzlichen Uploads. Die aktuellen nativen Werte
werden im Renderthread abgenommen; der Export liest nur den gespeicherten Stand.

## Prüfungen und Sandbox-Abnahme

Automatisierte Prüfungen umfassen Migration, getrennte Speicherung, ungültige
Werte, Besitzer-/Empfängerunterscheidung, Turmbesitzer, unbekannte Herkunft,
begrenzte Bindungen und bereinigte Diagnose. Negative Patchkontrollen verhindern
Core-Anwendung, abweichende Spielklassen und unerwartete Hookanzahlen.

Die nativen Renderproben verwenden originale Reparaturpartikel auf drei
Hintergründen mit 1/3/6/10 überlagerten Feldern. Sie prüfen Bildunterschiede,
Animation, getrennte Materialien, gemischte Modi, Besitzeränderung, Reichweite,
Szenenwechsel und Aufräumen. UI-Prüfungen verwenden originale MyGUI-Widgets
mit Übernehmen/Verwerfen und 100/150/200 % HUD-Skalierung.

Der Nutzer bestätigt den D3D11-Sandbox-Test. Zusätzliche gezielte Fälle für weitere Abnahmen:

1. Spieler Original / PvE Stark reduziert gleichzeitig auf einem Planeten.
2. Eigenes, fremdes und feindliches Spielerfeld sowie Reparaturfeldtürme.
3. Leicht/Stark/Kontur während aktiver und überlappender Felder umschalten.
4. Dialog schließen/öffnen, Neustart und Planetenwechsel; Einstellungen erhalten.
5. Bei einer falschen Zuordnung den Diagnosebericht exportieren.

Offline-GPU- und UI-Prüfungen ersetzen diese Ingame-Abnahme nicht.
