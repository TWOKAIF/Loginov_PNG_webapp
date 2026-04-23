# PNG-webapp — шаблон

HTML/CSS/JS мини-аппа для Telegram. Клиент вводит текст, выбирает шрифт/цвет/размер, превью на canvas, «Скачать» отправляет JSON в бота через `Telegram.WebApp.sendData`.

Шаблон поставляется с демо-плейсхолдером «Александр Логинов». Не использовать напрямую — клонировать через `../setup_new_client.py`.

## Что клиентское (меняется под каждого)

- `index.html`:
  - `<title>` и `meta apple-mobile-web-app-title`
  - `@font-face` (3 шрифта) → пути в `fonts/`
  - `:root { --red }` — акцентный цвет палитры
  - Блок `#color_chips` — кружки палитры
  - `<select id="s_font">` → `<option>` списка шрифтов
  - JS-объект `FONTS` и `state.font` по умолчанию
  - Сброс в `#btn_reset` — значения по умолчанию
- `instruction.html`: имя клиента, список шрифтов, палитра, ссылка на бота
- `manifest.json`: `name`, `short_name`
- `sw.js`: префикс `CACHE` + список `ASSETS` (имена шрифтов)
- `icon-192.png`, `icon-512.png`: аватар бота / PWA
- `fonts/`: файлы шрифтов клиента

## Что общее (не трогать)

- Canvas-логика, `SCALE=5`, `MIN_W/MIN_H=400`, `MAX_PX=16777216` — см. `НАРАБОТКИ_iOS_PNG.md`
- iOS-модалка с долгим нажатием (не использовать `navigator.share` для файлов!)
- `releaseCanvas()` после использования canvas
- Отказ от `ctx.shadowColor/shadowBlur` — только `filter: drop-shadow`

## Важно про `sw.js`

При любом обновлении **бампать версию кеша**: `CACHE='client-png-v1'` → `v2`. Иначе старая версия зависает в PWA клиента.

## Локальный просмотр

```bash
python3 -m http.server 5173
# http://localhost:5173
```
