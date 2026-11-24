> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Calon: Diagnose nach Vegetations-/Zielanzeigen-/Timer-Fix

Am 17.11.2026 neue, vom Nutzer erstellte Diagnose der laufenden Enhanced-alpha.9-
Sitzung PID 3740 ausgewertet. D3D11, aktuelle Startkopie `C:\PGF9Y\E`,
7.086 Frames über 29,994 s. Keine Produktionsänderung, kein Neustart oder Upload.
Beleg: `distribution/tests/calon-alpha9-vegetation-live.json`.
Rohdaten, GUI-Log und isolierte Prüfprogramme bleiben privat im Chatordner unter
`work/alpha9-vegetation-live`.

## Messung und Vergleich

| Größe | Vorheriger GC-Test | Neuer Vegetations-Test |
|---|---:|---:|
| Frameabstand P99 | 6,240 ms | 6,110 ms |
| Größter Frameabstand | 70,461 ms | 39,441 ms |
| Abstände über 16,67 ms | 9 | 9 |
| Abstände über 33,33 ms | 3 | 2 |
| Abstände über 50 ms | 2 | 0 |

Die Strecken und Spielsituationen waren nicht kontrolliert identisch. Daher
kein kausaler Prozentgewinn und keine Abnahme als ruckelfrei. `frame_delta` misst
Abstände, `frame_total` den instrumentierten Schleifendurchlauf; nicht dieselbe
Zeile gleichsetzen. Zehn `frame_total`-Spitzen über 16,67 ms teilen sich auf:
fünf Zielanzeigen, vier Vegetationsaufbauten und eine Wasserreflexion mit
zusätzlicher Vegetation. Native Modulmaske 3 in allen Frames: beide Messmodule aktiv.

## 1. Zielanzeigen: Schriftatlanten werden wiederholt aufgebaut

Zehn Ziel-Layouts in sieben Frames geladen. In fünf Frames kostet die Zielanzeige
20,33–24,26 ms, davon 19,65–22,36 ms in `Widget::setFontName`. XML-Parsing insgesamt
null: der vorhandene Dokumentcache greift. `layout_resource_ns` umfasst auch den
anschließenden Aufbau und darf nicht als reine Dateilesezeit interpretiert werden.

Das MyGUI-Log enthält in genau diesen fünf Sekunden erneut die Atlas-Erzeugungs-
meldungen für `PG_TextFont` und `ForgeHud2x_PG_TextFont`. Die Meldung über das leere
Leerzeichen-Glyph stammt aus `Font::loadResource`, nicht aus jedem normalen Draw.
Die Schrift wird also tatsächlich erneut gerastert, obwohl sie zuvor vorbereitet war.

Isolierter Offline-Test mit den unveränderten Kandidaten-DLLs, echten Ziel-Layouts,
D3D11 und 115 % HUD: nach erstem Laden/Entfernen drei Wiederholungen mit
0,308 / 0,199 / 0,170 ms. Nach `unloadUnreferencedResources(true)` vier Wiederholungen
mit 30,606 / 30,633 / 30,530 / 30,775 ms. Kein Serverkontakt und keine Nutzerdateien
verwendet. Die Bereinigung erzeugt den teuren Neuaufbau reproduzierbar.

Codepfad: `MyGUI_EditText.cpp::setFontName` → `MyGUI_HudScale.cpp::getHudFont` →
`Font::load`/`Font::loadResource`. Die temporäre Vorwärm-Zielanzeige in
`LayoutManager::loadLayout` hält nach ihrem Entfernen keine Font-Referenzen mehr.
Auch der Spielcode `com.splitscreen.cf::fc` besitzt eine Bereinigung ungenutzter
MyGUI-Fonts; der konkrete Aufrufer jedes Entladens wurde im Livebericht nicht erfasst.

Nächster Fix: die wenigen tatsächlich benötigten Basis- und HUD-Schriftatlanten
mit begrenztem, an die GUI-Lebensdauer gebundenem Besitz behalten. Ressourcenwechsel,
Gerätereset, HUD-Skalierung und Shutdown müssen weiter korrekt entladen/neu laden.
Kein Gegnerwidget-Pool und kein pauschales Abschalten der Speicherbereinigung.
Regression: laden → Widget entfernen → Ressourcen bereinigen → erneut laden;
100/115/200 %, Szenenwechsel und Freigabe beim GUI-Ende prüfen.

## 2. Vegetation: Einzelaufbau und unvorbereitete Quellen

51 Vorladeaufträge in 49 Frames, keine gezählten sofortigen Seiten und keine
Budget-Vertagung. Vier lange Frames verbringen 13,18–15,15 ms in Vegetation,
fast vollständig in `page->build` (bis 14,75 ms). Gras und Baum-Einfügen bleiben
je unter 0,5 ms. Die langsamen vier Aufbauten haben keine unbeschatteten Lesezugriffe:
CPU-Kopien allein können diese Spitzen also nicht beseitigen.

Zusätzlich 1.220 Leseversuche ohne CPU-Schatten in 30 Frames, Quellenlesen bis
4,50 ms. Schattenbestand konstant 3.249.918 Bytes, weit unter dem 64-MiB-Limit.
Das ist weder ein ausgeschöpftes Budget noch allein ein Beweis für GPU-Stalls.

Konkrete Code-Lücke: `prepareStaticSource` bereitet nur `entity->getMesh()` vor.
`BatchPage::addEntity` (auch Basis des Windpfads) kann dagegen `getManualLodLevel`
auswählen. Diese Quellen sind nicht automatisch vorbereitet. Der bisherige
49-Mesh-Test ruft direkt `BatchedGeometry` mit dem Grundmodell auf und prüft
somit diesen LOD-Auswahlpfad nicht. Die konkreten live gelesenen Meshnamen sind
noch nicht erfasst; die 1.220 Zugriffe sind nicht einzeln einem LOD zugeordnet.

Nächste Schritte: alle tatsächlich verwendeten statischen LOD-Quellen mit denselben
Lebensdauer-/Budgetregeln vorbereiten und über echte `BatchPage`-/Wind-LOD-Wechsel
prüfen. Danach den teuren Seitenaufbau weiter in Geometrietransformation,
Puffererzeugung/Upload und Material-/Shader-Arbeit aufteilen. CPU-Arbeit schrittweise
über Frames vorbereiten; native Renderobjekte weiter auf dem Spielthread erstellen.
Unfertige Seiten unsichtbar halten und beim Szenenwechsel verwerfen. Das derzeitige
2-ms-Zulassungsbudget prüft nur vor dem synchronen `_loadPage` und begrenzt deshalb
nicht die Dauer einer einzelnen Seite. Sichtweite/Dichte unverändert lassen.

## 3. Weitere Befunde und Grenzen

- Enhanced-Timer maximal 0,253 ms, kein großer Timerausreißer. Vorbereitung liegt
  vor dieser Flugaufnahme; null Vorbereitungscalls belegen kein fehlendes Vorwärmen.
- Eine Wasserreflexion kostet 19,982 ms. Derselbe Frame enthält 8,083 ms Vegetation.
  Keine pauschale Senkung der Wasserqualität; Ursache dieses Einzelereignisses offen.
- Ein paralleler ZGC-Major-Durchlauf dauert 255 ms, die fünf tatsächlichen
  Stop-Pausen jedoch nur 0,0077–0,0146 ms. Keine Allokationswartezeit exportiert.
  Die gesamte parallele GC-Dauer darf nicht als 255-ms-Spielpause dargestellt werden.
- Direkte Diagnosezeit im ersten Frame 11,36 ms. Aktivierungsarbeit muss vor die
  gezählte Flugmessung oder als eigene Aufwärmphase gekennzeichnet werden.
  Kontrollflug ohne Diagnose bleibt erforderlich.
- Present maximal 0,901 ms; keine durchgehend langsame Bildausgabe in dieser Messung.
- Keine neue Vergleichsaufnahme anderer Planeten oder des Original32-Clients.

Priorität: Schrift-Lebensdauer, vollständige LOD-Vorbereitung, danach aufgeteilte
Seitenaufbauten und engere Messung des Wasser-Einzelereignisses. Die laufende Sitzung
bleibt erhalten. Dieser Analysebeleg ist kein neuer Fixbuild und keine Releasefreigabe.
