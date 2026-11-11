# Verity — Minecraft Java 1.21.8 · Fabric

Неофициальный Fabric-мод с ИИ-спутником Verity. В обычной форме он дружелюбен к владельцу, следует за ним и общается через отдельное окно чата. При низком доверии меняет внешний вид и может атаковать владельца.

## Скачать

**[GitHub Release — Verity 0.2.0](https://github.com/doniel1488-code/Verity-Fabric/releases/tag/v0.2.0)**

Release публикуется автоматически только после успешной компиляции, remap и проверки всех обязательных ресурсов внутри JAR. Пока Release не появился, открой [GitHub Actions](https://github.com/doniel1488-code/Verity-Fabric/actions) и скачай артефакт успешной сборки.

## Требования

- Minecraft Java Edition **1.21.8**.
- Fabric Loader **0.17.2** или совместимый.
- Fabric API для Minecraft 1.21.8.
- Java **21**.
- Собственный API-ключ Groq для ИИ-чата.
- Для мультиплеера мод должен стоять и на Fabric-сервере, и у клиентов. Paper/Spigot не поддерживаются.

## Ресурсы мода

В JAR входят все необходимые ресурсы:

- Иконка Verity в списке модов Fabric.
- Текстура обычной Verity и отдельная текстура хоррор-формы.
- Модель и текстура Коробки Verity.
- Рецепт крафта Коробки Verity.
- Четыре OGG-звука: обычное окружение, хоррор-окружение, получение урона и призыв.
- Русская локализация `ru_ru` и английская `en_us`.

## Язык интерфейса

Мод использует язык, выбранный в Minecraft. Для русского интерфейса открой **Настройки → Язык → Русский**. При выбранном английском языке Minecraft будет использовать перевод `en_us`.

## Установка

1. Установи Fabric Loader для Minecraft 1.21.8.
2. Установи Fabric API для Minecraft 1.21.8.
3. Скачай `verity-fabric-0.2.0.jar` из [Releases](https://github.com/doniel1488-code/Verity-Fabric/releases/tag/v0.2.0).
4. Положи JAR в `.minecraft/mods`.
5. Запусти игру один раз, чтобы мод создал конфигурацию.
6. Выбери русский язык Minecraft, если хочешь русский интерфейс.
7. Открой `.minecraft/config/verity-fabric.json`, укажи свой Groq API-ключ в поле `apiKey`, сохрани файл и перезапусти игру.

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

Вставь свой ключ в `apiKey`. Ключ не включён в репозиторий или JAR и хранится только в локальном конфиге. Не публикуй конфиг с заполненным ключом. Доступность модели и ограничения запросов зависят от текущего аккаунта Groq.

## Сборка из исходников

Нужны JDK 21 и Gradle 8.14.3. Исходный проект хранится в `source/v0.2.0/chunks/` как части XZ-архива. После распаковки примени compatibility patch из `source/patches/0001-fix-1218-item-tooltip.patch` — он удаляет устаревший tooltip override, несовместимый с 1.21.8.

Linux / macOS / Git Bash:

```bash
cat source/v0.2.0/chunks/part-*.b64 | base64 --decode > Verity-Fabric-source.tar.xz
xz -t Verity-Fabric-source.tar.xz
tar -xJf Verity-Fabric-source.tar.xz
patch -p1 -d VerityFabric < source/patches/0001-fix-1218-item-tooltip.patch
cd VerityFabric
gradle --no-daemon clean build
```

Готовый JAR: `build/libs/verity-fabric-0.2.0.jar`.

## Автоматические проверки

GitHub Actions восстанавливает исходники, применяет 1.21.8 patch, проверяет локализации, PNG-текстуры, модель предмета, рецепт и OGG-звуки, затем компилирует и remap-ит мод. После сборки те же проверки выполняются уже внутри JAR. Только после успешного результата запускается публикация GitHub Release.

## Статус

**0.2.0 — предварительный релиз.** Компиляция и проверка ресурсов автоматизированы. Призыв, следование, хоррор-поведение, звуки и реальные запросы Groq нужно дополнительно проверить непосредственно в клиенте Minecraft 1.21.8.

## Лицензия

MIT. Это независимая реализация, не связанная с создателем оригинальной Verity.
