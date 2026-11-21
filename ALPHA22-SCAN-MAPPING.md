# Enhanced alpha.22: Bauplan-Zuordnungen und Scannerdiagnose

Enhanced alpha.22 für Spielversion 1002133, nach bestätigtem D3D11-Sandbox-Test
zur Veröffentlichung freigegeben. Core bleibt alpha.17 / Sequenz 16.

## Korrekturen

Der Import verarbeitet Gegnerlisten und Fraktionswechsel innerhalb einer
Quellenzeile getrennt. Levelangaben wie `R97,98` bleiben erhalten; verschiedene
Gegner übernehmen dieselben angegebenen Level, keine größeren Levelbereiche.
Die Reihenfolge zusammengehöriger Planeten- und Gegnerzeilen bleibt erhalten.
Fehlende Planetentitel werden ausschließlich anhand zweier geprüfter Bildpfade
ergänzt. Der falsche Antares-Titel und normale Drohnen-Dropzweige werden über
begründete, an die gepinnten Quelldateien gebundene Korrekturen behandelt.

Beispiele: Wache auf Erebos, Interceptor/Minelayer auf Erebos, Marauder/Resurrector
in Gemini, Mantis-/Imperial-Sniper auf dem Mond und Custodian/Repogrub in Draconis.
Wache verwendet ausschließlich den nativen Schlüssel `mantis1.sentry.name`;
die gleich übersetzte Angriffsdrohne bekommt diese Einträge nicht.
Seltene Gegnervarianten benötigen das originale native `rare`-Merkmal.

Die 41 hashgeprüften Prelude-Dateien vom 31.10.2026 ergeben **4.748 Regeln für
1.323 Baupläne**: 195 zusätzliche Regeln und 35 zusätzliche Baupläne gegenüber
alpha.21. Alle bisherigen 4.553 Regeln bleiben erhalten. Der Import wird für alle
Gebiete ausgeführt; unabhängige Regressionen prüfen alle 20 statischen Planeten
sowie Sirius-Klassen und den tatsächlich empfangenen Sirius-Planetenpool.

Die Oberfläche bleibt unverändert: mögliche Baupläne und eigener Sammelstand.
Keine neuen Tooltips oder erklärenden Felder. Vorhandene Anzeige-/Nur-fehlende-
Einstellungen bleiben wirksam. Keine zusätzlichen Serverabfragen.

## Diagnose

Nach problematischen Scans unter **Forge → Diagnose** den bestehenden bereinigten
Bericht exportieren. Er enthält zusätzlich `scanner-drops.json` mit höchstens
128 lokalen Beobachtungen: Planet, zulässiger nativer Gegnerschlüssel, Level,
Fraktion, Seltenheitsmerkmal, Treffer-/Anzeigeanzahl, Sirius-Poolgröße und
Zuordnungsgrund. Keine Spielernamen, Ziel-IDs, Koordinaten, Zugangsdaten, Rohlogs
oder kompletten Objekte. Keine Dateien pro Frame; der Export erfolgt auf Wunsch.
Identischer Zustand wird während eines geöffneten Scans nicht erneut erfasst.

`no_identity_rule` unterscheidet einen fehlenden Gegnereintrag von `no_rank_rule`.
`variant_required`, `pool_unavailable` und `pool_excludes_rules` trennen
Variantenbedingungen und Sirius-Datenlage. Bei ausgeblendeten vollständigen BPs
bleibt die ungefilterte Trefferzahl erhalten. Katalog-/Scanfehler sind separat
erkennbar, ohne beliebige Exception-Texte in den Bericht zu übernehmen.

`project/client-scan-drops/catalog-coverage.json` dokumentiert alle 1.625
berücksichtigten Quellenzeilen einschließlich begründeter Ausschlüsse. Ein
Import mit fehlender oder veränderter Quelldatei schlägt fehl.

## Verbleibende Grenzen

Dies ist keine vollständige serverseitige Droptabelle und keine Dropchance.
Death-Squad-, Landeplatz-, Koordinaten-, Kostüm- und manche Missionsbedingungen
sind nicht sicher aus den bisher geprüften nativen Feldern bestimmbar. Solche
Zeilen bleiben ausgeschlossen und im Abdeckungsbericht sichtbar. Insbesondere
sind DS-Abasis/Ignomes/Odion auf Calon noch separat zu verifizieren. Ein Scan
dieser Gegner im Teststand liefert dafür Level-/Identitätsdiagnose, bestätigt
aber allein noch keine serverseitige Dropberechtigung.

Unbelegte Angaben wie „Pyro?“ werden nicht als gesicherte Drops importiert.
Giza, Soris und Amarna bleiben ausgeschlossen. Für A110 ist die Katalogidentität
als Event markiert; sie wird nicht stillschweigend in eine normale Dropregel
umgewandelt. Fehlende Angaben im Quellsnapshot werden nicht erfunden.

## Manueller Sandbox-Test

1. Erebos-Wache scannen: beide ne0n-Schiffe anzeigen; keine Namensabschneidung.
2. Erebos-Interceptor und Minelayer auf passenden Leveln scannen; benachbarte
   Level dürfen keinen höheren blauen Bauplan erben.
3. Auf weiteren Planeten normale und seltene Gegner vergleichen; besondere
   Farb-BPs dürfen nur bei der seltenen Variante erscheinen.
4. Auf Calon Abasis/Ignomes/Odion scannen und den bereinigten Bericht exportieren,
   insbesondere bei vermissten DS-Einträgen.
5. Sirius-Klassen/Planetenwechsel, Nur-fehlende-Filter sowie Ein-/Ausschalten
   prüfen. Giza/Soris/Amarna dürfen keine globale Drop-Liste erhalten.

Der Nutzer bestätigt den D3D11-Sandbox-Test. Daraus folgt keine vollständige
Abnahme aller Gegner/Level oder der oben ausgeschlossenen Sonderbedingungen.
