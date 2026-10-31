# Shine — port for Minecraft 26.3 (Fabric)

Port of the [Shine](https://modrinth.com/mod/shine) visual-effects mod (tapeQ) to **Minecraft 26.3** on **Fabric Loader**.

## What this is

Selective bloom post-processing for Minecraft, with per-block source strength overrides, an in-game config screen (YACL), Mod Menu integration, and optional Sodium compatibility mixins.

This is a source port of the 1.21.11 release adapted to Minecraft 26.3. It is **not** an official release by tapeQ.

## Requirements

- Minecraft 26.3
- Fabric Loader **0.19.5** (or newer 0.19.x)
- Fabric API **0.163.0+26.3** (or newer 26.3 build)
- **Sodium** for 26.3 (recommended; the mod ships Sodium compile-stub mixins and works best with Sodium)
- Yet Another Config Lib **3.9.7+26.3-fabric** (config screen)
- Mod Menu **21.0.0** (optional, for in-game config entry)
- Java 25, Gradle 9.7.1 (for building)

## Changes made for the 26.3 port

- **Toolchain:** Fabric Loom 1.18 (`net.fabricmc.fabric-loom`), Loader 0.19.5, Fabric API 0.163.0+26.3, Java 25, Gradle 9.7.1.
- **Mappings:** Minecraft 26.1+ ships unobfuscated, so Yarn mappings were removed and the build uses `loom.officialMojangMappings()` (Mojang names).
- **Dependency configurations:** `modImplementation` / `modCompileOnly` / `modLocalRuntime` replaced with `implementation` / `compileOnly` / `runtimeOnly` (Loom 1.18 on unobfuscated versions).
- **Rendering events:** `WorldRenderEvents.START_MAIN` / `BEFORE_ENTITIES` moved to `LevelRenderEvents` in `net.fabricmc.fabric.api.client.rendering.v1.level`; `WorldTerrainRenderContext` → `LevelTerrainRenderContext`.
- **Mixin config:** `compatibilityLevel` set to `JAVA_25`.
- **fabric.mod.json:** depends updated to `minecraft ~26.3`, `fabric-loader >=0.19.5`, `fabric-api >=0.163.0+26.3`, `yet_another_config_lib_v3 >=3.9.7+26.3-fabric`, `java >=25`.

All shader files, mixin targets and selection/encoding logic were left as-is because 26.3 uses Mojang names (no remapping needed).

## Building

```bash
./gradlew build
```

The built jar appears in `build/libs/`. Install it in `mods/` alongside Fabric API, YACL and (recommended) Sodium for Minecraft 26.3.

## Notes

- This repository was prepared in an environment without access to Maven Central / Fabric Maven and without a Java toolchain, so the project **could not be compiled or run here**. Dependency coordinates (especially the YACL Modrinth artifact version id) and a few mixin target signatures (Indigo renderer, Sodium, vanilla chunk/liquid/model block renderers) should be verified against the actual 26.3 client jar at build time; fix any remaining compile errors iteratively with `./gradlew build`.
- The mod requires Sodium for best results; without Sodium the vanilla chunk renderer mixins apply instead.

## Credits

Original mod: **Shine** by tapeQ — https://modrinth.com/mod/shine (source: https://github.com/tapeQz/Shine)
Third-party credits (shader code, artwork) remain as in the original mod (`THIRD_PARTY_NOTICES.txt` in the built jar).

License: PolyForm Shield License 1.0.0 (original mod is All Rights Reserved; this port is a derivative adaptation for personal/educational use — check the original license before redistributing).
