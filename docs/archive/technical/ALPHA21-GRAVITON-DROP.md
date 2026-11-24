> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Enhanced alpha.21: Gravitonen-Dropstatus

Enhanced für Spielversion **1002133**, Starter **17**, Update-Sequenz **102**.
Core bleibt **0.2.0-alpha.17 / Sequenz 16**. Der Nutzer bestätigt den D3D11-
Sandbox-Test der lesbaren Anzeige und hat die Veröffentlichung freigegeben.
Profile und Einstellungen bleiben bei Updates erhalten.

## Bedienung

**Forge → Anzeige → Widgets → Gravitonen-Dropstatus** schaltet die Anzeige ein
oder aus. Erst „Übernehmen“ speichert; „Verwerfen“ erhält die bisherige Auswahl.
„Gravitonen-Vorschau“ zeigt vier beschriftete Beispiele, ohne echte Beobachtungen
oder Einstellungen zu verändern. Standardmäßig ist die Anzeige eingeschaltet.

Der sechste Slot im ausgeklappten Gravitonenfach zeigt:

| Anzeige | Bedeutung |
| --- | --- |
| Originalsymbol; Name im Tooltip | Ein Drop ist im aktuellen Sichtbereich erkannt. |
| Mehrere Drops | Mehr als ein sichtbarer Graviton-Drop; keine Besitzbehauptung. |
| `~6h`, `~3h` | Einzeilige, auf volle Stunden aufgerundete Restzeit. |
| `~45m` | Unter einer Stunde: auf volle Minuten aufgerundete Restzeit. |
| `~frei` | Lokale Wartezeit abgelaufen; ein neuer Drop wäre nach der Schätzung möglich. |
| `—` | Keine brauchbare Zeitbasis vorhanden. |

Der Countdown ist zentriert, weiß und fett auf einem dunklen, deckenden
Hintergrund. Die Schrift wird mit der echten Spielschrift an die Slotbreite
angepasst. Keine zweite Textzeile; das Fach und die fünf Originalslots bleiben
gleich groß. Zum Beispiel zeigt die Kurzansicht bei 2 Std. 14 Min. `~3h`; der
Tooltip behält **2 Std. 14 Min.** bei. Aufrundung suggeriert keine frühere
Bereitschaft; erst bei abgelaufener Restzeit erscheint `~frei`.

Mauszeiger über dem Slot zeigt Details. Der Slot verbraucht oder sammelt nichts
ein und übernimmt keinen Tastaturfokus. Die ursprünglichen fünf Gravitonen bleiben
bedienbar. Das Gravitonenfach lässt sich weiterhin einklappen; auch bei leerem
Bestand wird der Status im ausgeklappten Fach angezeigt.

## Was die Zeit bedeutet

Die sechs Stunden werden **ab lokal erkanntem eigenen Einsammeln geschätzt**.
Dropzeit, ursprüngliche Drop-Zuordnung und serverseitige Berechtigung sind damit
nicht bestätigt. Deshalb steht bei Restzeit und Bereitschaft immer `~`.
Ohne beobachtetes Einsammeln oder gültigen gespeicherten Anker bleibt die Zeit
unbekannt. Ein sichtbarer Drop allein startet keinen persönlichen Countdown.

Das bekannte Serverfeld `last_graviton_dropped` wird zunächst nur diagnostisch
beobachtet. Seine tatsächliche Übermittlung, Einheit, Uhr und Bedeutung sind
noch nicht verifiziert. Benutzungs-Abklingzeiten werden ausdrücklich nicht als
Drop-Wartezeit verwendet. Keine zusätzliche Spielserverabfrage.

Zeitbasis getrennt nach Pilot und Server speichern; während der Sitzung monotone
Zeit verwenden. Neustart berücksichtigt vergangene Zeit. Ungültige, zukünftige
oder alte Werte und größere Uhrsprünge führen zu „unbekannt“. Vorgänge in anderen
Clients können die lokale Schätzung überholen. Kein garantiertes Drop-Versprechen.

## Diagnose und Sandbox-Abnahme

Unter **Forge → Diagnose** lässt sich die Gravitonen-Diagnose separat abschalten.
„Bereinigten Bericht speichern“ enthält `graviton-drop.json`: höchstens 256
Ereignisse, erkannte Typen/Zustände und die zwei geprüften Serverfeld-Quellen.
Keine Namen, Kontodaten, Chattexte oder Roh-PropertyMaps; kein automatischer Upload.

Für weiterführende Drop- und Zeitbasisprüfungen:

1. Anzeige und Vorschau bei 100/115/150/200 % prüfen; Ein-/Ausschalten mit
   Übernehmen/Verwerfen, leeres Inventar und eingeklapptes Fach kontrollieren.
2. Einen echten Drop sichten: Name/Symbol prüfen. Erst eigenes Einsammeln darf
   einen geschätzten Timer setzen. Fremdes Einsammeln und bloßes Verschwinden
   dürfen keinen neuen eigenen Anker erzeugen.
3. Orbit/Planetenwechsel: Sichtung muss verschwinden, gespeicherte Schätzung
   erhalten bleiben. Pilot/Server wechseln und getrennte Zeitbasis prüfen.
4. Bericht vor/nach Sichten und Einsammeln exportieren. Erst diese Daten können
   eine spätere belastbare Interpretation des Serverfelds ermöglichen.

Die automatischen Tests benutzen synthetische Daten mit originalen Klassen und
echten nativen Widgets. Sie bestätigen keine serverseitige Sechs-Stunden-Regel
und ersetzen keinen echten Drop-Test. Prüfergebnisse und Paketbindung stehen in
[RELEASE-STATUS-0.2-alpha.21.md](../verification/RELEASE-STATUS-0.2-alpha.21.md).
