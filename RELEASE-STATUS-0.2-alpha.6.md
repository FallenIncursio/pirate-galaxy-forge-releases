# Core und Enhanced 0.2.0-alpha.6 — Veröffentlichung mit bekanntem Absturz

## Veröffentlichung geprüft

Core und Enhanced **0.2.0-alpha.6** sind veröffentlicht. Alle 14 öffentlichen Downloads,
beide RSA-Updatekanäle und README-Installerlinks wurden heruntergeladen und geprüft.
Sequenzen: Core 6 / Enhanced 87. Binärquellencommit: `5d32b3597ce0bc34b0e6ea37478c3f3aa9e241db`.
Beleg: `distribution/tests/editions-0.2-alpha.6-publication.json`. Frühere Releasepakete bleiben unverändert.
Der bekannte native Material-/Shader-Absturz ist in dieser Ausgabe noch enthalten
und öffentlich dokumentiert. Analyse und Fix sind als nächster Schritt beauftragt;
keine automatische Veröffentlichungsfreigabe für den nachfolgenden Fix.

## Historischer Vorbereitungs- und Diagnosestand

## Aktueller Befund: nativer Absturz, noch nicht behoben

Am 16.11.2026 ist Enhanced/D3D11 nach 753,7 Sekunden mit einer
Speicherzugriffsverletzung in der OGRE-/RTSS-Materialbereinigung abgestürzt.
Die vorher bestandenen Offlineprüfungen decken diesen Livefall nicht ab.
**Veröffentlichung trotz dieses bekannten Fehlers am 16.11.2026 ausdrücklich beauftragt. Keine Behauptung vollständiger Stabilitätsabnahme.** Die betroffenen nativen Dateien sind
gemeinsamer Code; ein entsprechender Absturz in Core wurde nicht beobachtet.
[Befund und vorgeschlagene nächste Prüfung](ALPHA6-CRASH-MATERIAL-CLEANUP.md).

Auf Nutzerauftrag wurde derselbe unveränderte Kandidat wieder gestartet. Eine
nach dem Absturz gehaltene Instanzsperre wurde gezielt in der Testbox bereinigt.
Profile, Einstellungen und geschützte Anmeldung bleiben am selben Datenort;
Windows-Mixer 8 %, nicht stumm, bestätigt. Hangar, Spielserververbindung,
16 Selector-Zyklen und 33 geladene native DLL-Hashes gegen den D3D11-Lock geprüft.
Privater Neustartbeleg: `work/alpha6-crash-20261116-185147/restart-verified.json`.
Es wurde kein Fix eingebaut, nichts veröffentlicht oder gepusht.

## Historie: erster Sandbox-Start

Enhanced wurde am 16.11.2026 mit D3D11 gestartet. Die vorherige alpha.5-Sitzung
wurde auf Nutzerauftrag regulär beendet. 19 aktuelle Profil-/Einstellungsdateien,
drei Spielprofile und eine verschlüsselte Anmeldung sind übernommen; Windows-Mixer
8 %, nicht stumm, im neuen Prozess bestätigt. Anmeldung, Serververbindung,
Ingame-Szene und die geladenen nativen Dateien sind geprüft. Die eigentliche
Remnant-/Aggrobeacon-Abnahme steht aus. Core wurde noch nicht als Spiel gestartet.
Nichts veröffentlicht oder gepusht. Privater Startbeleg im Chat-Arbeitsordner:
`work/alpha6-enhanced-launch/verified.json`.

## Historischer Vorbereitungsstand vor diesem Start

Stand: 16.11.2026. **Nicht veröffentlicht. Ingame-Abnahme offen.**
Reserviert: Core-Sequenz 6, Enhanced-Sequenz 87; Starterrevision 12 bleibt erhalten.
Öffentliche Downloads und beide Updatekanäle bleiben auf alpha.5.

## Änderungen seit alpha.5

- Beide Editionen / D3D11: spätes Laden von Partikelmaterialien repariert,
  einschließlich Aggrobeacon, Rauch-, Projektil- und Lavaeffekten. Keine roten
  Ersatzflächen während einer noch fehlenden Materialbindung.
- Beide Editionen / D3D11: Schiffskopien behalten ihr tatsächliches Material
  einschließlich Gruppe und dynamischer Farbe.
- Enhanced: Remnant-Auftritte nur für XC/SC; MN/DL behalten ihre HP-/Effektanzeige.
  Die Beschränkung gilt auch für den älteren Ersatzimpuls. Core bleibt ohne Bossintro.

[Ursachen, Implementierung und Tests](ALPHA6-REMNANT-MATERIALS.md) ·
[Kumulative Funktionen und Original32-Vergleich](FEATURES.md).

## Technische Prüfung

- Beide Editionen aus der gepinnten Alpha-73-Basis neu gebaut; 113 gemeinsame
  Klassen sind identisch. 40 Editions-/Java-/native Oberflächensuiten sowie sechs
  Negativkontrollen bestanden, einschließlich Core-Hilfe und Enhanced-Einstieg.
- 76 Bossprüfungen bestanden. 45 native Materialprüfungen bestanden;
  die alpha.5-Gegenprobe zeigt 39 Fehler. Acht Szenenwechsel enthalten.
- 160 Material-/Shader-Bereinigungszyklen, 49 Overlayprüfungen und unveränderte
  elf Calon-Himmels-/fünf Wasserbilder mit den neuen nativen Dateien geprüft.
- Acht native DLLs neu gebaut und mit unveränderter Exportschnittstelle belegt.
  Lose DLLs und Basic-JAR-Dateien werden gegen den Editions-Lock geprüft.
  D3D9-DLLs bleiben unverändert; die Introänderung gilt in Enhanced für beide Renderer.

Build: `.build/editions/alpha6-final-build`; Tests: `.build/editions/alpha6-final-tests`;
Native Ausgabe: `.build/alpha6-render`.
Finale private Pakete: `.build/alpha6-final-sandbox`.
Kurze D3D11-Startanfragen: `C:\PGF6M\C\data\launch.json` und
`C:\PGF6M\E\data\launch.json`; neue Box `PGForgeAlpha6Materials` unter `C:\PGF6B`.
Die vorbereiteten Kopien enthalten noch keine übernommenen Nutzerprofile.
Vor dem angeforderten Spielstart die dann aktuellen Einstellungen, Profile,
geschützte Anmeldung und Windows-Lautstärke übernehmen.

## Noch ausstehend

Der laufende Nutzerclient wird durch diese Vorbereitung nicht ersetzt. Die neue
Version wurde noch nicht am Spielserver angemeldet. Für die Sandbox-Abnahme:

1. Enhanced: MN/DL ohne Intro; XC/SC mit Intro, auch nach Tarnung/erneutem Auftauchen.
   Bossleiste, Effekte und manuelle Zielwahl weiter prüfen.
2. Aggrobeacon mehrfach einsetzen, bei mehreren betroffenen Schiffen und mit
   unterschiedlicher Kameradistanz. Das korrekte Icon muss erscheinen.
3. Zwischen Orbit und Planet wechseln und dieselben Effekte erneut auslösen.
   Rauch, Schuss-/Strahleffekte und Lava auf fehlende Materialien prüfen.
4. Core separat mit D3D11 prüfen; es enthält nur die gemeinsamen Materialkorrekturen.

Installer-/Update-/Reparaturprüfungen werden vor der beauftragten Veröffentlichung mit den signierten Paketen ausgeführt. Weitere GPUs, Wine, vollständige Ingame-Abnahme und quantitative Langzeittests bleiben offen. Keine pauschale Behebung aller ursprünglichen Assetwarnungen behaupten.
