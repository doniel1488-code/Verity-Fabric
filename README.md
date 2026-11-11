# Verity — Minecraft Java 1.21.8 · Fabric

Неофициальный Fabric-мод с ИИ-спутником Verity. В обычной форме он дружелюбен к владельцу, но при низком доверии может перейти к хоррор-поведению.

## Скачать

**[Verity 0.2.0 — GitHub Release](https://github.com/doniel1488-code/Verity-Fabric/releases/tag/v0.2.0)**

Релиз публикуется автоматически только после успешной сборки, remap и проверки ресурсов внутри JAR. Пока Release не появился, можно посмотреть [GitHub Actions](https://github.com/doniel1488-code/Verity-Fabric/actions) и скачать артефакт успешной сборки.

## Требования

- Minecraft Java Edition **1.21.8**.
- Fabric Loader **0.17.2** или совместимее.
- Fabric API для Minecraft 1.21.8.
- Java **21**.
- Собственный API-ключ Groq для ИИ-диалога.
- Для мультиплеера мод должен стоять на Fabric-сервере и у клиентов. Paper/Spigot не поддерживаются.

## Что входит в мод

- Иконка Verity в списке модов.
- Текстура обычной Verity и отдельная демоническая текстура.
- Коробка призыва: своя текстура, модель предмета и рецепт крафта.
- Четыре OGG-звука: обычное окружение, хоррор-окружение, получение урона и призыв.
- Русская локализация `ru_ru` и английская `en_us`.
- Следование за владельцем, сохранение владельца и уровня доверия.
- Отдельное окно ИИ-чата с памятью последних сообщений и контекстом игрового мира.
- Ответы через OpenAI-совместимый Groq API.
- При доверии 20/100 и ниже Verity меняет форму и становится опасным. Механику можно отключить в конфиге.

## Установка

1. Установи Fabric Loader для Minecraft 1.21.8.
2. Установи Fabric API для Minecraft 1.21.8.
3. Скачай `verity-fabric-0.2.0.jar` из [Releases](https://github.com/doniel1488-code/Verity-Fabric/releases/tag/v0.2.0).
4. Положи JAR в папку `.minecraft/mods`.
5. Запусти игру один раз, чтобы мод создал конфигурацию.
6. В настройках Minecraft выбери язык **Русский**. Мод содержит `ru_ru`; при английском языке Minecraft использует `en_us`.
7. Открой `.minecraft/config/verity-fabric.json`, укажи собственный Groq API-ключ в поле `apiKey`, сохрани файл и перезапусти игру.

## Управление

| Действие | Как выполнить |
|---|---|
| Призвать Verity | Используй Коробку Verity по блоку |
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

Вставь собственный ключ в `apiKey`. Ключ не включён в репозиторий или JAR и хранится только в локальном конфиге. Не публикуй конфиг с заполненным ключом.

## Сборка из исходников

Нужны JDK 21 и Gradle 8.14.3.

### Windows PowerShell

Из корня репозитория:

```powershell
$b64 = (Get-ChildItem source/v0.2.0/chunks/part-*.b64 | Sort-Object Name | Get-Content -Raw) -join ""
[IO.File]::WriteAllBytes("Verity-Fabric-source.tar.xz", [Convert]::FromBase64String($b64))
tar -xJf Verity-Fabric-source.tar.xz
cd VerityFabric
gradle --no-daemon clean build
```

### Linux / macOS / Git Bash

```bash
cat source/v0.2.0/chunks/part-*.b64 | base64 --decode > Verity-Fabric-source.tar.xz
xz -t Verity-Fabric-source.tar.xz
tar -xJf Verity-Fabric-source.tar.xz
cd VerityFabric
gradle --no-daemon clean build
```

Готовый JAR: `build/libs/verity-fabric-0.2.0.jar`.

## Проверка ресурсов

Скрипт `scripts/verify_resources.py` проверяет:

- обе локализации и необходимые переводные ключи;
- PNG-текстуры и их размеры;
- четыре OGG-файла;
- JSON модели, звуков и рецепта;
- ссылки звуковых событий на существующие файлы.

GitHub Actions запускает проверку исходников до компиляции и повторно проверяет ресурсы уже внутри собранного JAR.

## Статус

**0.2.0 — предварительный релиз.** Компиляция и проверка ресурсов автоматизированы; призыв, поведение, анимации, звуки и реальные запросы к Groq нужно дополнительно проверить в клиенте Minecraft 1.21.8.

## Лицензия

MIT. Это независимая реализация, не связанная с создателем оригинальной Verity.
