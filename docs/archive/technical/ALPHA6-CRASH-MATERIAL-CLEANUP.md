> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Alpha.6: Absturz bei der Materialbereinigung

Stand: 16.11.2026. Analyse und Neustart, **noch kein Fix**.

## Gesicherter Befund

Enhanced 0.2.0-alpha.6 mit D3D11 stürzte um 18:51:47 Uhr nach 753,727587 Sekunden
mit `EXCEPTION_ACCESS_VIOLATION (0xc0000005)` ab. Betroffen war der Java-Hauptthread
innerhalb eines nativen Aufrufs von `MaterialManager._remove__StringR`, ausgelöst
durch `com.splitscreen.att$6.go()`. Der protokollierte Prozess-Exitcode war 1.

Die nativen Rücksprungadressen lassen sich anhand der Exporte der tatsächlich
geladenen alpha.6-DLLs folgender Aufrufkette zuordnen, von außen nach innen:

| DLL und relative Adresse | Zugeordnete Funktion |
| --- | --- |
| OgreMain + 0x1510c7 | ResourceManager::removeImpl + 0x2a7 |
| OgreMain + 0x14756f | ResourceGroupManager::_notifyResourceRemoved + 0x3f |
| OgreRTShaderSystem + 0x43223 | ShaderGenerator::removeAllShaderBasedTechniques + 0x193 |
| OgreRTShaderSystem + 0x3d175 | SGTechnique::~SGTechnique + 0x25 |
| OgreRTShaderSystem + 0x41735 | SGTechnique::destroySGPasses + 0x35 |
| OgreRTShaderSystem + 0x3d09f | SGPass::~SGPass + 0x5f |
| OgreMain + 0x1dd3fb | UserObjectBindings::eraseUserAny + 0x3b |
| OgreMain + 0xd469 | Fehlerstelle; nicht exportierte interne Funktion |

Der passende Quellaufruf in `Components/RTShaderSystem/src/OgreShaderGenerator.cpp`,
Zeile 1310 des alpha.6-Builds, lautet:

```cpp
mDstPass->getUserObjectBindings().eraseUserAny(TargetRenderState::UserKey);
```

Die Fundstelle belegt einen ungültigen Speicherzugriff beim Entfernen der
Shader-Bindung. Sie belegt noch nicht, welche frühere Operation den Speicher
ungültig gemacht hat. Die Zuordnung verwendet Exporte und Quellvergleich, keine
vollständige PDB-Symbolisierung. Ein erst nach Prozessende erzeugter Minidump
ist zu klein für eine zuverlässige Rekonstruktion der betroffenen Heapobjekte.

## Wahrscheinliche Ursache und Prüfbedarf

Der konkrete Verdacht ist eine Lebensdauerverletzung: RTSS hält einen rohen
`mDstPass`-Zeiger, obwohl der zugehörige Pass beziehungsweise dessen Bindungen
bereits entfernt, ersetzt oder beschädigt wurden. Der Destruktor dereferenziert
diesen Zeiger bedingungslos. `Material::removeTechnique`, `removeAllTechniques`
und `copyDetailsTo` sowie die verzögerte Pass-Löschung sind relevante Prüfpfade.
Ein Zusammenhang mit den alpha.6-Materialänderungen ist möglich, aber bisher
nicht als Ursache nachgewiesen. Ein defektes Aggrobeacon-Icon oder das Bossintro
ist durch diesen Stack allein ebenfalls nicht als Auslöser belegt.

Empfohlener nächster Fixschritt:

1. Einen gezielten nativen Reproduktionstest erstellen: gerendertes dynamisches
   Material überschreiben beziehungsweise Techniken/Passes entfernen, verzögerte
   Pass-Löschung ausführen und erst danach das Material aus dem Manager entfernen.
   Klone, gleiche Namen mit verschiedenen Gruppen und Beleuchtungspasses einbeziehen.
2. Lebensdauer und Abmeldung von RTSS-Einträgen an Material-/Technik-/Pass-Löschung
   koppeln. Die Reihenfolge muss sicherstellen, dass `SGPass` keine bereits
   ungültigen Pass-Zeiger mehr verwendet. Eine reine Nullprüfung reicht nicht.
3. Mit Diagnose-Symbolen und gezielter Heapprüfung den ursprünglichen Fehler im
   Reproduktionstest nachweisen, dann mit korrigierter Bereinigung ausschließen.
4. Gemeinsame D3D11-Dateien für Core und Enhanced neu bauen; die bisherigen
   Material-, Shader-, Calon- und Terrainprüfungen sowie Live-Szenenwechsel wiederholen.
   Neue Bytes benötigen neue Locks und Paketbelege.

## Neustart und Beweissicherung

Der ursprüngliche Fehlerbericht und die Laufzeitlogs wurden ausschließlich im
privaten Chat-Arbeitsordner gesichert. Nach dem Absturz hielt die Sandbox noch
die Instanzsperre; zwei Startversuche meldeten deshalb eine laufende Instanz.
Erst nach dem gezielten Beenden der Prozesse dieser Testbox ließ sich die
leere Sperrdatei archivieren. Es wurden keine Profile oder Spielstände gelöscht.

Der unveränderte alpha.6-Kandidat läuft wieder mit D3D11. Hangar und
Spielserververbindung wurden beobachtet. Die bestehende geschützte Anmeldung
ist entschlüsselbar, Profile/Einstellungen werden am selben Ort weiterverwendet,
und Windows-Mixer 8 % ohne Stummschaltung wurde bestätigt. 33 geladene native
Dateien stimmen mit dem aktuellen D3D11-Lock überein.

Die genaue Besitz-/Löschsequenz bleibt offen. Dieser Neustart ist kein behobener
Absturz und keine Freigabe zum Veröffentlichen. Keine Paketbytes verändert,
kein Commit, Push oder Upload.
