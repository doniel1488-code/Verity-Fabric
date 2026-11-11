# Verity — Fabric 1.21.8

AI-companion horror mod for Minecraft Java 1.21.8 (Fabric).

## Project files
The full Gradle source project is in [source/Verity-Fabric-source.tar.xz](source/Verity-Fabric-source.tar.xz). Extract it, then open the `VerityFabric` directory.

## Build locally
Requirements: JDK 21 and Gradle 8.14.3.

```bash
gradle --no-daemon clean build
```

The remapped JAR is created in `build/libs/verity-fabric-0.1.0.jar`.

## Install and configure
1. Install Fabric Loader for Minecraft 1.21.8 and Fabric API.
2. Build the project or download the JAR from the Actions artifact after a successful run.
3. Put the JAR in `.minecraft/mods`.
4. Launch once, close Minecraft, then edit `.minecraft/config/verity-fabric.json`.
5. Set your own Groq key in `apiKey`. The default model is `openai/gpt-oss-20b`.

The API key is stored locally and is not included in the source archive, JAR, or repository. Never commit your config file or share the key publicly.

## In game
- Use a Verity Box on a block to summon the companion.
- Press `V` near Verity to open the AI chat.
- Feed Verity a golden carrot to restore trust.
- At low trust the companion becomes hostile (can be disabled in the config).

## Current status
Early prototype. GitHub Actions compiles the project on every push and uploads the JAR as a workflow artifact. A tag like `v0.1.0` creates a GitHub Release. The first CI run is the authoritative compile check; in-game behaviour still needs playtesting.

## License
MIT. This is an independent implementation and is not affiliated with the original Verity creator.
