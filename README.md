# Verity — Minecraft Java 1.21.8 · Fabric

Неофициальный Fabric-мод с ИИ-спутником Verity. В обычной форме он дружелюбен к владельцу, следует за ним и общается через отдельный чат. При низком доверии меняет внешний вид и может стать агрессивным.

## Скачать

**[GitHub Release — Verity 0.2.1](https://github.com/doniel1488-code/Verity-Fabric/releases/tag/v0.2.1)**

Прямой файл: [verity-fabric-0.2.1.jar](https://github.com/doniel1488-code/Verity-Fabric/releases/download/v0.2.1/verity-fabric-0.2.1.jar).

## Требования

- Minecraft Java Edition **1.21.8**.
- Fabric Loader **0.17.2** или совместимый.
- Fabric API для Minecraft **1.21.8**.
- Java **21**.
- Собственный API-ключ Groq для ИИ-чата.
- Для мультиплеера мод должен стоять на Fabric-сервере и у клиентов. Paper/Spigot не поддерживаются.

## Ресурсы мода

В релизный JAR включены и автоматически проверены:

- Иконка Verity в списке модов Fabric.
- Обычная и хоррор-текстуры сущности.
- Модель и текстура Коробки Verity.
- Рецепт крафта Коробки Verity.
- Четыре OGG-звука: обычное окружение, хоррор-окружение, получение урона и призыв.
- Русская локализация `ru_ru` и английская `en_us`.

## Язык интерфейса

Мод использует язык, выбранный в самом Minecraft. Для русского интерфейса открой **Настройки → Язык → Русский**. При выбранном английском языке Minecraft использует `en_us`.

## Установка

1. Установи Fabric Loader для Minecraft 1.21.8.
2. Установи Fabric API для Minecraft 1.21.8.
3. Скачай JAR из раздела [Releases](https://github.com/doniel1488-code/Verity-Fabric/releases/tag/v0.2.1).
4. Положи его в `.minecraft/mods`.
5. Запусти игру один раз, чтобы мод создал конфигурацию.
6. Выбери русский язык Minecraft, если нужен русский интерфейс.
7. Открой `.minecraft/config/verity-fabric.json`, укажи собственный Groq API-ключ в поле `apiKey`, сохрани файл и перезапусти игру.

## Управление

| Действие | Как выполнить |
|---|---|
| Призвать спутника | Используй Коробку Verity по блоку |
| Открыть диалог | Нажми `V`, находясь рядом с Verity |
| Отправить сообщение | `Enter` |
| Закрыть диалог | `Esc` |
| Восстановить доверие | Покорми Verity золотой морковью |

## Рецепт Коробки Verity

В верстаке:

```text
  Золотой слиток
Золотой слиток  Аметист  Золотой слиток
  Редстоун
```

Точный рецепт: `data/verity/recipe/verity_box.json`.

## Настройка ИИ

После первого запуска появится файл `.minecraft/config/verity-fabric.json`:

```json
{
  "provider": "groq",
  "baseUrl": "https://api.groq.com/openai/v1",
  "model": "openai/gpt-oss-20b",
  "apiKey": "",
  "maxHistory": 16,
  "enableHorrorEvents": true
}
```

Вставь свой ключ в `apiKey`. Ключ не включён в репозиторий или JAR и хранится только в локальном конфиге. Не публикуй конфиг с заполненным ключом.

## Сборка из исходников

Нужны JDK 21 и Gradle 8.14.3.

### Windows PowerShell

Из корня репозитория:

```powershell
$b64 = (Get-ChildItem "source/v0.2.0/verified-chunks/part-*.b64" | Sort-Object Name | Get-Content -Raw) -join ""
[IO.File]::WriteAllBytes("Verity-Fabric-source.tar.xz", [Convert]::FromBase64String($b64))
tar -xJf Verity-Fabric-source.tar.xz
git apply source/patches/0002-fix-item-registry-key.patch
cd VerityFabric
gradle --no-daemon clean build
```

### Linux / macOS / Git Bash

```bash
cat source/v0.2.0/verified-chunks/part-*.b64 | base64 --decode > Verity-Fabric-source.tar.xz
xz -t Verity-Fabric-source.tar.xz
tar -xJf Verity-Fabric-source.tar.xz
cd VerityFabric
gradle --no-daemon clean build
```

Готовый JAR: `build/libs/verity-fabric-0.2.0.jar`.

## Автоматические проверки

GitHub Actions восстанавливает исходники, проверяет локализации, PNG-текстуры, модель предмета, рецепт и OGG-звуки, затем компилирует и remap-ит мод. После сборки те же проверки выполняются уже внутри JAR. Публикация релиза запускается отдельным commit message с маркером `[publish-release]`; workflow собирает JAR заново и создаёт тег/релиз после успешной проверки.

## Статус

**0.2.1 — предварительный релиз.** Исправлен вылет при регистрации Коробки Verity: `RegistryKey` задаётся до создания `Item`. CI проверяет это до компиляции и повторно проверяет ресурсы внутри JAR. Игровое поведение, анимации и реальные запросы Groq всё ещё требуют проверки в клиенте Minecraft 1.21.8.

## Лицензия

MIT. Это независимая реализация, не связанная с создателем оригинальной Verity.
