# Alpha.7: Lebensdauer bei der Materialbereinigung

Gemeinsamer D3D11-Fix für Core und Enhanced 0.2.0-alpha.7.
Die Veröffentlichung beider Editionen wurde am 17.11.2026 ausdrücklich beauftragt.

## Ursache und Nachweis

Der beobachtete Absturz führte über `MaterialManager._remove__StringR` und
`com.splitscreen.att$6.go()` in `ShaderGenerator::SGPass::~SGPass`. Dieser
Destruktor entfernte einen Shader-Zustand über einen rohen `mDstPass`-Zeiger.
Wurde der Pass zuvor durch Materialersetzung, Technik- oder Passlöschung
freigegeben, konnte der spätere Zugriff bereits wiederverwendeten Speicher treffen.
Ein Zeiger ungleich null ist dafür kein gültiger Lebensdauernachweis.

Ein D3D11-Test mit echten Materialien und Shadern reproduziert diese Fehlerklasse
in fünf Fällen: sämtliche Techniken löschen, `copyDetailsTo`, Passlöschung,
Technikzuweisung und eine überlebende Kopie der Anwendungsbindungen. Nach korrektem
Leeren der Renderqueue und verzögerter Passlöschung wird der Speicher durch normale
OGRE-Allokationen wiederverwendet; ausschließlich neu zugewiesener Speicher wird
beschrieben. Der anschließende Materialabbau führt mit alpha.5 und alpha.6 zu
Speicherzugriffsverletzungen. Damit bestand der Defekt bereits vor den alpha.6-Fixes.

Das reproduziert den fehlerhaften Lebensdauerpfad. Welche frühere Ingame-Operation
den Pass in der ursprünglichen Sitzung ungültig machte, ist mangels Heapabbild
nicht vollständig rekonstruiert; Aggrobeacon oder das Remnant-Intro sind damit
nicht als Auslöser bewiesen.

## Korrektur

Die Bindungen eines Ziel-Passes besitzen nun eine private Lebensdauermarke. Die
Shader-Hülle hält darauf nur einen schwachen Verweis. Sobald die Bindungen oder
der Pass verschwinden, ist die Marke ungültig und die spätere Bereinigung greift
nicht mehr auf diesen Pass zu. Kopierte Bindungen bekommen ihre eigene Marke;
sie verlängern die Lebensdauer des ursprünglichen Besitzers nicht.

Bei einem noch lebenden Pass wird der Shader-Zustand weiterhin ausdrücklich
freigegeben. Das ist auch beim Beenden des Shader-Generators erforderlich,
bevor dessen Shader-Fabriken verschwinden. Die private Zuordnung wird bei jeder
Hüllenzerstörung entfernt. Öffentliche Klassenlayouts und Exportschnittstellen
bleiben erhalten; die Prüfung liegt im gemeinsamen D3D11-Code beider Editionen.
Sie läuft beim Erzeugen und Bereinigen der Hüllen, nicht für jedes gezeichnete Objekt.

## Prüfung und Grenzen

Die gezielte Gegenprobe umfasst 800 korrigierte Zyklen in acht Szenarien,
einschließlich Shader-Neuerzeugung, gelöschter Bindungen und Beenden mit aktivem
Material. Fünf negative Fälle stürzen mit alpha.5 und alpha.6 ab; mit dem Fix
bleiben alle acht Szenarien erfolgreich. Testquelle:
`project/client-runtime-modernization/ogre14/regressions/material-cleanup`.

Der abschließende Paketprüfstand und die übrigen Regressionen werden in
[RELEASE-STATUS-0.2-alpha.7.md](RELEASE-STATUS-0.2-alpha.7.md) festgehalten.
Enhanced wurde mit den korrigierten Dateien in der Sandbox gestartet. Der Nutzer
berichtet bisher keine weiteren Abstürze; Dauer und Wechselzahl wurden nicht
angegeben. Eine gesonderte Core-Spielsitzung ist nicht bestätigt.
Die laufende alpha.7-Testsitzung und die veröffentlichten alpha.6-Dateien werden
durch die Veröffentlichung nicht ersetzt. Keine pauschale Behebung aller
Absturzursachen, keine neue Sicherheitsfunktion und keine FPS-Zusage.
