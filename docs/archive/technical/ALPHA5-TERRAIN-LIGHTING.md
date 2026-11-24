> Historischer Stand. Versionen, Freigaben und Tests gelten für den damaligen Zeitpunkt. [Aktuelle Übersicht](../../../README.md).

# Alpha.5: Terrain-LOD und Shaderbeleuchtung

Alpha.5-Fixstand vom 16.11.2026, entwickelt auf `a5c33fe679227439e8b80ba91dd2d9120d2624a5`.
Der Nutzer hat den Enhanced-D3D11-Molikar-Test bestätigt und das Update freigegeben.
Quell- und Artefakthashes stehen in
`editions/native-builds/alpha5-molikar-*.json`; aktueller Testbeleg:
`distribution/tests/molikar-alpha5.json`. Der frühere
`distribution/tests/terrain-lighting-alpha5.json` bleibt als Beleg des ersten
alpha.5-Teststands erhalten; dieser zeigte auf Molikar noch den unten beschriebenen Fehler.

## Molikar: bestätigte Ursache und zusätzlicher Fix

Die private 25-Sekunden-Aufnahme zeigt starke Helligkeitswechsel beim Drehen.
Mit den originalen `mizar2`-Terrainressourcen lässt sich das im Offline-Replay
reproduzieren. Der Original32-Client bindet in Highest/Highest1 an Slot 6
`refmap_12.png`; der bisherige D3D11-Client bindet `planetsurface_falloff.png`.
Eine eindimensionale Helligkeitsrampe wurde als zweidimensionale Reflexionskarte
abgetastet. Das erzeugt die großen hellen/schwarzen Flecken bei Kamerabewegung.

Im gepinnten OGRE-Patch verwendet `MaterialTranslator::translate` für
`set_texture_alias` jetzt `mTextureAliases[name] = value`. Das bisherige
`insert` behielt die zuerst eingelesene Zuweisung des Vorfahren und ignorierte
die spätere planetenspezifische Zuweisung. Der ursprüngliche Parser
`parseSetTextureAlias` verwendet ebenfalls die überschreibende Zuweisung.
Es wird weder eine Planetentextur ersetzt noch die Helligkeit pauschal verändert.
Der Parser gehört zum gemeinsamen Core; Enhanced verwendet dieselbe DLL.

72 Ansichten (24 Drehwinkel × 10/20/40 Grad Neigung) wurden mit originalem
32-Bit-Java, Original-JAR und originalen x86-DLLs sowie beiden D3D11-Ständen
verglichen. Kamera, Terrain und kontrolliertes Licht sind gleich. Dies ist
kein Nachspielen der Kontositzung oder des vollständigen Tag-/Nachtzyklus.
Alle 34 Texturbelegungen stimmen nach dem Fix mit Original32 überein.
Die mittlere absolute RGB-Abweichung auf Referenzpixeln über 10 fällt im Mittel
von 43,90 auf 16,81; alle 72 Ansichten verbessern sich. Restabweichungen bleiben
bei Filterung, Rasterisierung und Geometrie; keine vollständige Bildgleichheit.

Der synthetische Test mit echten Materialparsern und Vererbung über mehrere
Dateien zeigt vor dem Fix 13 Fehler bei 21 Prüfungen, danach keinen. 807.456
beobachtete Terrain-Zeichnungen haben keine falsche Material-LOD; neun explizite
Qualitätsauswahlen bestehen. Weitere Prüfungen mit den finalen nativen Dateien:
5.208 Shaderfälle (maximal eine RGB-Stufe zur x64-D3D9-Referenz), sieben
COLOR-Profilfälle, 160 Bereinigungszyklen, unveränderte elf Calon-Bilder und fünf
Wasser-Fallback-Bilder, 49 Enhanced-Overlayprüfungen mit acht Szenenzyklen.

Aktueller Neubau: `.build/alpha5-molikar-render`. Replay und private Rohbilder:
`.build/molikar`. Testwerkzeuge sind nicht Teil der Spielpakete. Der neue
Enhanced-D3D11-Molikar-Test wurde vom Nutzer bestätigt. Weitere Planeten, eine
separate Core-Spielsitzung und andere GPUs bleiben gesondert.

## Frühere gemeinsame Änderungen

`native-terrain/src/src/OgrePagingLandScapeRenderable.cpp` berechnet die
Material-LOD unter der Ogre-14-Standardstrategie `distance_sphere` wieder aus
`mDistanceToCam`: quadrierte Entfernung zum Kachelzentrum mal inverser Kamera-LOD-Bias.
Das entspricht dem alten D3D9-Zweig. Die beim Port eingeführte generische Strategie
verwendete den übergeordneten Szenenknoten, den Kugelradius und ihre eigene
Bias-Auswertung. Dadurch konnten benachbarte Kacheln eine falsche Materialtechnik
und damit andere Glanz-, Nebel- oder Schattenberechnungen erhalten.
Ausdrücklich andere LOD-Strategien behalten ihre bisherige Auswertung.
Geometrie-LOD, Sichtweite und Originalmaterialien werden nicht neu abgestimmt.

`JniBootstrap.cpp` erhält bei der Cg-Konvertierung die ursprüngliche Profilfolge
hinter `hlslv`/`hlslf`. Die Cg-Patchdatei entscheidet anhand des ersten ursprünglich
angegebenen D3D-Pixelprofils, ob COLOR0/COLOR1 beim Eintritt in den Pixelshader auf
0–1 begrenzt werden. Das entspricht den dokumentierten Regeln für `ps_1_1` bis
`ps_2_0`; TEXCOORD, `ps_3_0` und Programme ohne altes Pixelprofil bleiben davon
unberührt. Die bisherige Sonderbehandlung anhand von Planet-Shadernamen entfällt.
[Microsoft: Shader-Eingänge unter D3D9](https://learn.microsoft.com/en-us/windows/win32/direct3dhlsl/dx-graphics-hlsl-writing-shaders-9).

Der `LegacyTechniqueResolver` ordnet die expliziten Forge-Qualitäten Highest/Ultra
dem ursprünglichen Default-Schema zu und erhält die passende unterstützte LOD.
Das normale Spiel verwendet bei höchster Qualität bereits `Default`; der
zusätzliche Resolverfehler ist daher nicht die alleinige Erklärung der Meldung.

Der JNI-Selektor hält außerdem `_ConfigOption._getpossibleValues` und dessen
Destruktor für die reflektierte MSAA-Abfrage verfügbar. Alle 1.437 bisherigen
ogre4j-Exporte bleiben erhalten. `build_alpha70.py` isoliert `git apply` für die
entpackten Upstreamquellen vom umgebenden Git-Checkout; anschließend wird weiterhin
der vollständige Quellbaum gegen den gepinnten Patch geprüft.

## Erster alpha.5-Vergleich vor der Molikar-Nachkorrektur

| Prüfung | Alpha.4 | Alpha.5 |
|---|---:|---:|
| Falsche Material-LOD bei 142.272 beobachteten Terrain-Zeichnungen | 18.144 | 0 |
| Fehler bei neun Highest/Ultra/Medium-LOD-Auswahlen | 2 | 0 |
| Shader-Fälle mit mehr als zwei RGB-Stufen Abweichung zur x64-D3D9-Referenz | 112 von 5.208 | 0 von 5.208 |
| Maximale RGB-Abweichung im Shader-Vergleich | 63 | 1 |
| Fehler bei sieben isolierten COLOR-/TEXCOORD-/Profilprüfungen | 5 | 0 |

Die Terrainprüfung rendert echte lokale Kalabesh-Ressourcen mit drei Kameraposen
und drei LOD-Biaswerten. Die Referenz verwendet die **originalen 32-Bit-DLLs und
eine 32-Bit-Java-Laufzeit**, nicht nur Forge mit D3D9. Beide Wege verwenden die
originalen Spielwrapper. Ein ausschließlich im Test verwendeter Adapter bildet
die alten direkten Kameraaufrufe auf SceneNodes ab und erzeugt das Renderziel.
Positionen und Quaternionen sind identisch; Richtungsabweichung maximal 1,2e-7.
Der Adapter wird nicht ausgeliefert. Die LOD-Zähler zählen wiederholte Zeichnungen,
nicht unterschiedliche Kacheln oder betroffene Planeten.

Neun Bilder je Variante wurden verglichen. Die mittlere absolute RGB-Abweichung
zur Original32-Referenz sinkt in allen neun Ansichten leicht: vorher 8,75–10,82,
danach 8,69–10,47 auf einer 0–255-Skala. Gemessen wird auf Referenzpixeln mit
mindestens einem Kanal über 10, ohne nachträgliche Farbkorrektur. Texturfilterung,
Rasterisierung und Geometriedetails unterscheiden sich weiterhin. Die Bilder
belegen **keine vollständige Helligkeits- oder Bildgleichheit**.

Die 5.208 Shader-Fälle sind dagegen kontrollierte Einzeltests mit 31 originalen
Shaderfamilien, sieben Blickwinkeln, Licht/Nebel, manuellen/automatischen
Konstanten und dem originalen Falloff-Verlauf. Dieser Vergleich nutzt den
beibehaltenen **x64-D3D9-Renderer**, flache Testgeometrie und festgelegte Texturen.
Er ist kein 32-Bit-Komplettszenenvergleich und keine Ingame-Abnahme aller Planeten.

Die vorhandenen Korrekturen wurden mit den neuen DLLs erneut geprüft:
160 Materiallebensdauerzyklen ohne zurückbleibende RTSS-Einträge; elf Calon-
Himmel-/Reflexions-/Wasserbilder und fünf Wasser-Fallback-Fälle pixelgleich zum
vorherigen geprüften Fixstand; Enhanced-Overlays mit 49 Prüfungen und acht
Szenenzyklen erfolgreich. Die neuen DLLs behalten alle bisherigen Exporte.

## Reproduktion

Aktuelle native Ausgabe: `.build/alpha5-molikar-render`; Konfiguration und vollständige
Upstream-/Abhängigkeitsbelege liegen dort. Der Build benötigt die bereits
dokumentierten gepinnten privaten Eingaben, keine Daten einer laufenden Sitzung.

```powershell
python project/client-runtime-modernization/ogre14/build_alpha70.py engine --config .build/alpha5-molikar-render/config.json
python project/client-runtime-modernization/ogre14/build_alpha70.py bindings --tests d3d11 --config .build/alpha5-molikar-render/config.json
```

`regressions/terrain-lighting/CMakeLists.txt` baut den Testadapter, den isolierten
Farbtest und optional den D3D9-Shadervergleich. Parameter: `OGRE_SOURCE`,
`OGRE_BUILD`, `JDK`, optional `LEGACY_OGRE_LIBRARY`. `run_parity.py --help`
beschreibt die expliziten Original-JAR-, Java-, DLL- und Asseteingaben. D3D11
benötigt zusätzlich `--d3d11 --media <shader-media> --bridge <Testadapter>`.
Der Ausgabeordner muss neu sein. Die WorldLightingProbe erhält für 5.208 Fälle
als viertes Argument `angles`; die lokale Assetmappe enthält die Originalshader
und `planetsurface_falloff.png`. Ohne `angles` bleiben die bisherigen 744 Fälle.

Rohbilder, Shaderdateien und Spielressourcen bleiben ausschließlich lokal unter
`.build/alpha5-parity`. Kein Netzwerk, kein Konto und keine sichtbare Spielsitzung
werden für diese Tests benötigt. Öffentliche Metadaten enthalten nur Hashes und
zusammengefasste Ergebnisse.

## Grenzen und nächste Abnahme

In beiden Editionen D3D11 auf mindestens zwei verschieden beleuchteten Planeten
prüfen: Kamera langsam drehen, neigen und zoomen; Boden, Felsen, Gebäude und
Übergänge beobachten. Danach Orbit/Landung und Grafikqualität wechseln.
Calon-Wasser, Schatten, Nebel und Enhanced-Anzeigen mitprüfen. Vergleichsbilder
aus Original32 müssen dieselbe Position, Kamera, Qualität und Beleuchtung haben.
Weitere GPUs/Treiber, Wine und längere Spielsitzungen bleiben separate Tests.
Keine Gamma-Korrektur pro Planet, zusätzliche Serverabfragen oder FPS-Zusage.
