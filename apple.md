Вот полный анализ стека технологий сайта **apple.com**, собранный через DevTools (JavaScript + Performance API):

---

## Фронтенд

**JavaScript-фреймворки:** Apple не использует React, Vue, Angular, Next.js, jQuery и другие публичные фреймворки. Вместо этого они используют **собственный проприетарный фреймворк** — `AC` (Apple Component / Apple Common). Это глобальный объект `window.AC` с паттерном SharedInstance.

**Скрипты (модульная архитектура):**
- `head.built.js` / `main.built.js` — основные бандлы страницы
- `globalheader.umd.js` — глобальная навигация (UMD-модуль)
- `ac-globalfooter.built.js` — глобальный футер
- `ac-analytics.js` v2.28.1 — собственная аналитика Apple
- `home-gallery.built.js`, `endless-entertainment-gallery.built.js` — компоненты галерей
- `data-relay.js` v1.2.0 + `auto-relay.js` — система передачи данных/метрик

Файлы имеют суффикс `.built.js`, что указывает на **собственную систему сборки** Apple, без публичных бандлеров (Webpack, Vite, Rollup не обнаружены).

---

## CSS

- **CSS Custom Properties** (CSS-переменные) — активно используется дизайн-система с префиксами `--sk-` (скорее всего Silk / Apple Design System) и `--r-` для responsive-токенов
- **CSS Grid + Flexbox** — оба поддерживаются и применяются
- **CSS Container Queries** — используются
- **Adaptive изображения** — 33 элемента `<picture>` для responsive-картинок
- **Собственные шрифты**: Apple Icons (100–900 weight), Apple Legacy Chevron — иконочные шрифты Apple

---

## Аналитика

- **Adobe Analytics (AppMeasurement)** v2.23.0 — данные отправляются на `metrics.apple.com` и `securemetrics.apple.com`
- **Собственная система метрик**: `ac-analytics`, `data-relay` — проприетарные решения Apple

---

## Сеть и инфраструктура

- **HTTP/2** (h2) — весь трафик идёт по HTTP/2
- **CDN**: весь контент раздаётся с `www.apple.com` (Akamai CDN — Apple исторически использует Akamai)
- **Собственный сервер метрик**: `securemetrics.apple.com`

---

## HTML / Разметка

- **XHTML-разметка** (`xmlns="http://www.w3.org/1999/xhtml"`) — документ написан в XHTML-совместимом стиле
- **Open Graph** (`og:` prefix) — поддержка соцсетей
- **Определение возможностей браузера через классы на `<html>`**: классы вроде `js no-touch progressive-image no-reduced-motion desktop retina macos chrome` — т.е. Apple динамически детектирует возможности среды и добавляет классы (похоже на Modernizr-подход, но своя реализация)

---

## Браузерные API

| API | Используется |
|---|---|
| Intersection Observer | ✅ |
| Web Animations API | ✅ |
| CSS Container Queries | ✅ |
| Service Workers | поддержка есть, статус регистрации не определён |
| `<picture>` / responsive images | ✅ 33 элемента |

---

## Итог

Apple.com — это **полностью самописный стек**. Никаких open-source фреймворков (React/Vue/Angular/jQuery) не используется. Ключевые элементы: собственный компонентный фреймворк `AC`, своя система сборки (`.built.js`), своя аналитика, дизайн-система с CSS Custom Properties (`--sk-` токены), Adobe Analytics как единственный сторонний инструмент аналитики.
