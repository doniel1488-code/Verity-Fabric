# Verity — Fabric 1.21.8

AI companion / horror prototype for Minecraft Java 1.21.8 (Fabric).

## Source
The full Gradle project is stored in `source/parts/` as ordered XZ archive chunks. GitHub Actions joins them before building. For a local copy:

```bash
cat source/parts/part-*.xz > Verity-Fabric-source.tar.xz
tar -xJf Verity-Fabric-source.tar.xz
```

## Build
Requirements: JDK 21 and Gradle 8.14.3.

```bash
gradle --no-daemon clean build
```

The remapped JAR is created in `build/libs/verity-fabric-0.1.0.jar`.

## Install and configure
1. Install Fabric Loader for Minecraft 1.21.8 and Fabric API.
2. Download the JAR from a successful Actions run artifact or a GitHub Release.
3. Put the JAR in `.minecraft/mods`.
4. Launch once, close Minecraft, then edit `.minecraft/config/verity-fabric.json`.
5. Set your own Groq API key in `apiKey`. The default model is `openai/gpt-oss-20b`.

The API key is read locally at runtime. It is not included in the repository or JAR. Do not commit your config file or share your key publicly.

## In game
- Use a Verity Box on a block to summon the companion.
- Press `V` near Verity to open the AI chat.
- Feed Verity a golden carrot to restore trust.
- At low trust the companion becomes hostile (can be disabled in the config).

## Status
Early prototype. GitHub Actions is the compile check; the mod still needs playtesting in Minecraft 1.21.8.

## License
MIT. This is an independent implementation and is not affiliated with the original Verity creator.
