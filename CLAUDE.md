# CLAUDE.md — trip-kareila

Single-file проект. Единственный редактируемый файл: `index.html`.
Стек: HTML5 + Tailwind CSS CDN + Alpine.js 3.14.1 CDN. Без сборки, деплой на GitHub Pages.

## Поездка

- Даты: 24–26 июля 2026 (пт–вс)
- Место: Бухта Терву, Ладожское озеро
- Координаты базы: 61.308498, 30.110127
- Старт: Офис Яндекса «Бенуа», СПб (59.984872, 30.406674)
- Участников: 13

## Цветовая палитра (Tailwind custom)

| Токен  | HEX       | Роль                  |
|--------|-----------|-----------------------|
| f950   | #0f1c14   | самый тёмный фон      |
| f900   | #1a2e22   | основной фон          |
| f800   | #243b2e   | карточки              |
| f700   | #2e4a38   | бордеры               |
| f600   | #3a5c46   |                       |
| f500   | #4a6741   | вторичный текст dim   |
| f400   | #6a8f60   | section-label         |
| f300   | #8db082   | описания              |
| f200   | #b5ceaf   | основной текст        |
| f100   | #dcebd9   |                       |
| gold   | #d4a853   | акцент, CTA           |

## Структура секций (index.html)

| Строка | Секция                        | id           | Alpine компонент                        |
|--------|-------------------------------|--------------|-----------------------------------------|
| 164    | Navigation                    | —            | —                                       |
| 189    | Hero                          | —            | `countdown()` (inline x-data на div)   |
| 273    | About / О поездке             | about        | `x-data` на карточке активностей        |
| 336    | Location / Локация            | location     | —                                       |
| 447    | Timeline / Программа          | timeline     | —                                       |
| 528    | Weather / Погода              | weather      | `weather()`                             |
| 579    | Budget / Бюджет               | budget       | —                                       |
| 628    | Shopping / Список покупок     | shopping     | `Object.assign(shoppingList(), {open})` |
| 747    | Checklist / Чек-лист          | checklist    | `checklist()`                           |
| 802    | Rules / Правила               | rules        | —                                       |
| 883    | FAQ                           | faq          | `faqData()`                             |
| 917    | Footer                        | —            | —                                       |
| 940    | Scripts                       | —            | все JS-функции                          |

## JS-функции (все в одном `<script>` от строки 940)

| Строка | Функция         | Назначение                              |
|--------|-----------------|-----------------------------------------|
| 943    | shoppingList()  | список покупок + Google Sheets sync     |
| 1024   | checklist()     | чек-лист с localStorage                 |
| 1102   | faqData()       | аккордеон FAQ                           |
| 1135   | countdown()     | обратный отсчёт в Hero                  |
| 1167   | weather()       | прогноз погоды с Open-Meteo             |

## Ключевые URL и данные

- Apps Script URL: `https://script.google.com/macros/s/AKfycbyN7lW_CE0lSyuMYl3D8aRA89FZZbDU3Jx0ycYa-DPenL6c1b0hdlbynJaD_pJNMPoL/exec`
- Google Sheet: `https://docs.google.com/spreadsheets/d/1k63rHPiJNTwJ3lyR71YmOA_pqNLpV1UULX4aHiTZjGU`
- Open-Meteo API: forecast с `start_date=2026-07-24&end_date=2026-07-26`, данные появятся ~8 июля
- Splitwise: `https://www.splitwise.com/join/BY8BfUjKyqb+zdnvq?v=e`
- Организатор TG: @ruslansd
- Организатор YM: `https://yandex.ru/chat/p/31b78ff0-5a99-4b6e-b42d-b4646166fedb?utm_source=invite`

## localStorage

| Ключ               | Назначение                        |
|--------------------|-----------------------------------|
| trip_buyer_name    | имя покупателя в списке покупок   |
| trip_checklist_v2  | состояние чек-листа (bool[])      |

## Типы элементов чек-листа

| type      | цвет    | иконка | кто                        |
|-----------|---------|--------|----------------------------|
| required  | красный | ❗     | Паспорт (обязательно)      |
| critical  | зелёный | 🌟     | Хорошее настроение         |
| important | золотой | ⚡     | Дождевик, обувь            |
| normal    | серый   | —      | всё остальное              |

## Важные нюансы

- CORS для Apps Script: используем `mode: 'no-cors'` для POST, GET работает нормально
- Shopping list: коллапсится кнопкой, данные грузятся при открытии, polling каждые 30с
- Checklist readiness: логика 80%+бонус если паспорт И настроение отмечены, иначе макс 50%
- Номера секций в разметке: 01–09 (04 = Погода, дублей нет)
- Hero image: `https://tervu.ru/wp-content/uploads/2019/03/dostoprimechatelnosti-lahdenpohya-e15.jpg`
