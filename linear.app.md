Вот полный стек технологий сайта **linear.app**, определённый через DevTools:

---

## ⚙️ Фреймворк и рендеринг

- **Next.js 16.1.6** — App Router (`appDir: true`), серверный рендеринг с потоковой передачей (`__next_f` streaming)
- **React** — под капотом Next.js (App Router)
- **TypeScript** — судя по структуре кода и named exports

---

## 📦 Бандлер

- **Webpack 5** — стандартный чанк `webpackChunk_N_E` (Next.js дефолт), 79 чанков загружено

---

## 🎨 Стилизация

- **CSS Modules** — классы по паттерну `ComponentName_className__hash` (например `Header_root__x8J2p`, `Button_root__Stmhv`)
- **Styled Components 6.1.18** — обнаружен через `data-styled-version="6.1.18-20"`
- **CSS Custom Properties** — обширная система дизайн-токенов через CSS-переменные (`--header-height`, `--font-size-title1` и т.д.)

---

## 🗂️ Управление состоянием

- **MobX** — обнаружен через `window.__mobxInstanceCount` и `window.__mobxGlobals`

---

## 🧩 UI-библиотеки

- **Radix UI** — примитивы (`data-radix-collection-item`, `data-state`, `data-orientation`) — используется для меню, диалогов и т.д.
- **next/image** — 29 изображений с `data-nimg`

---

## 📊 Мониторинг и аналитика

- **Sentry 10.27.0** — error monitoring (`window.__SENTRY__`, `SENTRY_RELEASE: "linear-web@1.0.0"`)
- **PostHog** — self-hosted на `e.linear.app` (не отправляют данные в облако PostHog), включены только surveys, autocapture отключён

---

## 🖋️ Шрифты

- **Inter Variable** — кастомный вариативный шрифт (`InterVariable.woff2 v4.1`) с хоста `static.linear.app`

---

## 🌗 Темизация

- Dark/Light через атрибут `data-theme` на `<html>`, по умолчанию тёмная тема (`data-theme="dark"`)

---

**Итого:** сайт построен на **Next.js (App Router) + React + TypeScript**, стилизация через **CSS Modules + Styled Components**, состояние — **MobX**, UI-примитивы — **Radix UI**, мониторинг — **Sentry**, аналитика — **PostHog (self-hosted)**.
