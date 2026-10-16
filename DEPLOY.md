# DEPLOY — sarrz demo

**Репо:** `apilot/sarrz-demo` → https://apilot.github.io/sarrz-demo/

## Состав
- `index.html` — демо-макет (апгрейд sarrz.ru; noindex, nofollow — уже вшит; favicon — inline SVG data-URI, отдельного файла нет и не нужно)
- `assets/` ×11: og_image.jpg (превью для мессенджеров), 5 фото webp с прода (hero-workshop, eng-drawing, ship-plant, ship-trawl, ship-truck), 2 лого png (белый + синий), `fonts/` ×3 cerapro-*.woff2
- Внешних запросов 0 — шрифты и фото локальные, папка полностью автономна (self-check file:// пройден 15.10.2026: 0 внешних, h-scroll 0 @390, вес страницы ~376KB)

## Шаги (без git — только веб-интерфейс)
1. Создать публичный репо `sarrz-demo` на GitHub (аккаунт apilot)
2. «Add file → Upload files» → перетащить `index.html` и папку `assets/` целиком в корень репо → Commit changes
3. Settings → Pages → Branch: main, / (root) → Save
4. Подождать 1–2 мин (CDN-кэш до 3 мин)

## Проверка после деплоя
```bash
curl -s https://apilot.github.io/sarrz-demo/ | grep -c noindex   # → 1
curl -s -o /dev/null -w "%{http_code}" https://apilot.github.io/sarrz-demo/assets/hero-workshop.webp  # → 200
curl -s https://apilot.github.io/sarrz-demo/ | grep -c "8-800-555-94-80"  # → ≥4
```
+ вручную (инкогнито, телефон, LTE): CTA «Запросить КП» и 8-800 видны в первом экране @390; бургер открывает белую панель с синим лого; квиз 3 вопроса → «Заявка принята».

## og:image — одно действие после публикации
В `<head>` index.html, над тегом `og:image`, оставлен HTML-комментарий: заменить относительный `assets/og_image.jpg` на абсолютный `https://apilot.github.io/sarrz-demo/assets/og_image.jpg` (иначе превью в мессенджерах не подхватится).

## Запасной хостинг
Timeweb Cloud Apps (*.twc1.net). НЕ Netlify/Vercel (поддомены глючат из РФ).

## После переговоров
Репо удалить (или скрыть) — демо не должно индексироваться рядом с sarrz.ru.

## Контекст (не для клиента)
- Письмо адресовать **Шурыгину И.В.** (гендиректор-совладелец по ЕГРЮЛ; Зиновьев на сайте — публичное лицо). Почта: zakaz@sarrz.ru
- Продукт — **апгрейд, не ремейк** (сайт свежий, подрядчик «Сайтмедиа»): мобильный CTA в первом экране, вес 3 MB → ~1 MB + lazy-load, фото объектов открыты для Яндекс.Картинок/Google Images (сейчас robots запрещает ВСЕ картинки), подбор резервуара по 3 параметрам
- Фото/шрифт — с текущего прода; пересъёмка на едином фоне не входила в скоуп демо
