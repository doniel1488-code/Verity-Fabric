# Verity — Minecraft 1.21.8 · Fabric

Клиентско-серверный Fabric-мод с ИИ-спутником Verity, диалогом через Groq API и постепенным переходом к хоррор-поведению.

## Скачать

**[Релиз Verity 0.2.0](https://github.com/doniel1488-code/Verity-Fabric/releases/tag/v0.2.0)**

JAR прикрепляется к релизу автоматически после успешной сборки и проверки ресурсов в GitHub Actions. Пока релиз не опубликован, смотри [сборки Actions](https://github.com/doniel1488-code/Verity-Fabric/actions).

## Требования

- Minecraft Java Edition **1.21.8**.
- Fabric Loader **0.17.2** или совместимее.
- Fabric API для Minecraft 1.21.8.
- Java **21**.
- Собственный API-ключ Groq для ИИ-диалога.
- Для мультиплеера мод должен быть установлен на Fabric-сервере и клиентах. Paper/Spigot не поддерживаются.

## Возможности и ресурсы

- Сущность Verity с обычной и хоррор-текстурой.
- Иконка мода и собственная текстура Коробки Verity.
- Модель предмета Коробки Verity и рецепт крафта.
- Четыре OGG-звука: обычное окружение, окружение хоррор-формы, урон и призыв.
- Полная русская локализация `ru_ru`; английский перевод `en_us` используется как резервный.
- Следование за владельцем, сохранение владельца и уровня доверия.
- Диалоговое окно с памятью последних сообщений и контекстом мира.
- Ответы ИИ через OpenAI-совместимый Groq API.
- При доверии 20/100 и ниже Verity меняется и становится опасным. Эту механику можно отключить в конфиге.

## Установка

1. Установи Fabric Loader для Minecraft 1.21.8.
2. Установи Fabric API для Minecraft 1.21.8.
3. Скачай `verity-fabric-0.2.0.jar` из [Releases](https://github.com/doniel1488-code/Verity-Fabric/releases/tag/v0.2.0).
4. Положи JAR в папку `.minecraft/mods`.
5. Запусти игру один раз, чтобы мод создал конфигурацию.
6. В настройках Minecraft выбери язык **Русский**, чтобы интерфейс мода отображался на русском.
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

Рецепт также хранится в `data/verity/recipe/verity_box.json`.

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

```bash
cat source/verity-source-part-01.b64 source/verity-source-part-02-repair/part-*.b64 source/verity-source-part-03.b64 source/verity-source-part-04.b64 source/verity-source-part-05.b64 source/verity-source-part-06.b64 source/verity-source-part-07.b64 source/verity-source-part-08.b64 source/verity-source-part-09.b64 source/verity-source-part-10.b64 source/verity-source-part-11.b64 source/verity-source-part-12.b64 source/verity-source-part-13.b64 source/verity-source-part-14.b64 | base64 --decode > Verity-Fabric-source.tar.xz
xz -t Verity-Fabric-source.tar.xz
tar -xJf Verity-Fabric-source.tar.xz
cd VerityFabric
gradle --no-daemon clean build
```

Готовый JAR: `build/libs/verity-fabric-0.2.0.jar`.

## Проверка ресурсов

Скрипт `scripts/verify_resources.py` проверяет наличие переводов, корректность JSON, размеры PNG, OGG-звуки, ссылки звуковых событий и рецепт. GitHub Actions запускает эту проверку до компиляции и повторно проверяет ресурсы уже внутри собранного JAR.

## Статус

Версия **0.2.0 — предварительный релиз**. Сборка и проверка ресурсов автоматизированы. Поведение сущности, анимации и реальные запросы к Groq необходимо дополнительно проверить в Minecraft 1.21.8.

## Лицензия

MIT. Это независимая реализация, не связанная с создателем оригинальной Verity.
