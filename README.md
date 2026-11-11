# Verity — Fabric 1.21.8

Неофициальная самостоятельная реализация ИИ-спутника Verity для Minecraft Java Edition 1.21.8 + Fabric.

## Статус сборки


**CI build прошёл успешно:** [GitHub Actions #19](https://github.com/doniel1488-code/Verity-Fabric/actions/runs/43055005795). JAR и sources JAR доступны в Artifacts этого запуска. Сборка выполнена на Java 21 и прошла Gradle compile/remap. Игровой тест в клиенте Minecraft ещё не проводился.

## Исходники

Gradle-проект хранится в каталоге `source/` как несколько Base64-частей одного XZ-архива. GitHub Actions собирает их в архив и распаковывает перед компиляцией.

### Восстановление исходников в Windows PowerShell

```powershell
$b64 = (Get-ChildItem source/verity-source-part-*.b64 | Sort-Object Name | Get-Content -Raw) -join ""
[IO.File]::WriteAllBytes("Verity-Fabric-source.tar.xz", [Convert]::FromBase64String(($b64 -replace "\\s", "")))
tar -xJf Verity-Fabric-source.tar.xz
```

### Linux / macOS / Git Bash

```bash
cat source/verity-source-part-*.b64 | base64 --decode > Verity-Fabric-source.tar.xz
xz -t Verity-Fabric-source.tar.xz
tar -xJf Verity-Fabric-source.tar.xz
```

После распаковки открой каталог `VerityFabric`.

## Сборка

Требуются JDK 21 и Gradle 8.14.3.

```bash
cd VerityFabric
gradle --no-daemon clean build
```

Готовый remapped JAR: `build/libs/verity-fabric-0.1.0.jar`.

## Установка и настройка ИИ

1. Установи Fabric Loader для Minecraft 1.21.8 и Fabric API соответствующей версии.
2. Скачай JAR из [успешного Actions run](https://github.com/doniel1488-code/Verity-Fabric/actions/runs/43055005795) → Artifacts → `Verity-Fabric-Minecraft-1.21.8`.
3. Помести JAR в `.minecraft/mods`.
4. Запусти игру один раз и закрой её.
5. Открой `.minecraft/config/verity-fabric.json` и заполни `apiKey` собственным ключом Groq.

По умолчанию используется OpenAI-совместимый endpoint Groq и модель `openai/gpt-oss-20b`.

**API-ключ не вшит в исходники, JAR или репозиторий.** Не публикуй конфиг с ключом, не отправляй его в issues и не добавляй в Git.

## Управление

- Используй предмет **Коробка Verity** по блоку, чтобы призвать спутника.
- Нажми **V** рядом с Verity, чтобы открыть ИИ-чат.
- Покорми Verity золотой морковью, чтобы восстановить доверие.
- При низком доверии спутник может стать агрессивным; эту механику можно выключить в конфиге.

## Лицензия

MIT. Это независимая реализация, не связанная с создателем оригинальной Verity.
