# Nightfall Client (Etappe 1: Fundament)

Fabric-Client fuer Minecraft Java 1.21.11 (Yarn-Mappings, Loom 1.14, Java 21).

## Build
1. JDK 21 installieren.
2. Gradle-Wrapper erzeugen (einmalig, falls `gradlew` fehlt): `gradle wrapper --gradle-version 9.2.1`
   oder die Wrapper-Dateien (`gradlew`, `gradlew.bat`, `gradle/wrapper/gradle-wrapper.jar`) aus der Fabric-Example-Mod kopieren.
3. `./gradlew build`  ->  `build/libs/NightfallClient-1.21.11.jar` (zusammen mit Fabric API in den mods-Ordner)
4. Zum Testen: `./gradlew runClient`

Falls eine Version in `gradle.properties` nicht aufgeloest wird, die aktuelle Version von https://fabricmc.net/develop eintragen.

## Bedienung
- **RIGHT SHIFT**: ClickGUI (in einer Welt). Linksklick Modul an/aus, Rechtsklick Einstellungen.
- Panel-Kopf ziehen = verschieben, Rechtsklick = einklappen, Mausrad = scrollen.
- Oben: Suche, Profile (Klick laden, Rechtsklick loeschen, + neu, Save), HUD Editor.
- Keybind pro Modul: unten in den Einstellungen (Klick, Taste druecken, Backspace loescht).
- Konfiguration: `.minecraft/config/nightfall/profiles/*.json`

## Stellen, die bei API-Abweichungen zuerst geprueft werden sollten
- `Input.handle()`: `getWindow().getHandle()`
- `HudRenderCallback` (NightfallClient): ggf. `HudElementRegistry` verwenden
- `ctx.getMatrices()` (`pushMatrix/translate/scale/popMatrix`, 2D-Matrix seit 1.21.6)
- `Screen#renderBackground(DrawContext,int,int,float)` und `mouseScrolled(...)`-Signaturen
- `PositionedSoundInstance.master(...)` in `ClickGuiScreen.sound`
- `World#getTimeOfDay()` in `TimeHud`, `MinecraftClient#getCurrentFps()` in `FpsHud`
