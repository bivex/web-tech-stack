Вот что удалось выяснить по стеку технологий **notion.com** через DevTools / JavaScript:

---

## Frontend

**React + Next.js**
- Все JS-бандлы идут через `/_next/static/chunks/` — явный признак Next.js
- Присутствует `window.__NEXT_DATA__` и `webpackChunk_N_E` (Next.js специфичный Webpack runtime)
- Рендеринг: **SSR** (Server-Side Rendering) — в данных есть флаг `__N_SSP: true` (getServerSideProps)
- Next.js Image component (`data-nimg`) и link prefetch подтверждены в DOM
- HTTP/2 (`nextHopProtocol: h2`)

**CSS**
- **CSS Modules** — классы с характерными хэш-суффиксами (например `class_4a3f`)
- Стилей нет Tailwind/Emotion/styled-components
- 26 подключённых CSS-файлов от Next.js билда
- CSS-переменные (собственная дизайн-система, `--color-primary: #097fe8`)

**Шрифты**
- Кастомный шрифт **NotionInter** (Regular, Medium, SemiBold, Bold) — собственный вариант Inter, хостится на notion.com

---

## CMS / Контент

- **Contentful** — 39 изображений и видео загружаются с `images.ctfassets.net` и `videos.ctfassets.net`. Весь контент маркетингового сайта управляется через Contentful

---

## Мониторинг и ошибки

- **Sentry** — обнаружен через `_sentryTraceData` и `_sentryBaggage` в pageProps (трассировка ошибок)

---

## A/B тестирование / Фичи-флаги

- Собственный механизм экспериментов через `experimentProps` в pageProps. Активные флаги, например: `marketing_top_nav_2025`, `marketing_ubp_pricing`, `marketing_agents_homepage_26`

---

## Сторонние сервисы (внешние скрипты)

| Сервис | Назначение |
|---|---|
| **Transcend** (`transcend-cdn.com/airgap.js`) | Управление согласием на cookies / GDPR |
| **Adora** (`adora-cdn.com`) | Product adoption / пользовательские подсказки |
| **Google Sign-In** (`accounts.google.com/gsi/client`) | Аутентификация через Google |
| **Decagon** | AI-поддержка в хелп-центре (обнаружен в экспериментах) |

---

## Инфраструктура

- Протокол: **HTTP/2**
- Судя по структуре (`_next/`, отсутствие сторонних CDN для JS), скорее всего деплой на **Vercel** или собственной инфраструктуре
- Сжатие: страница весит ~60 KB в сжатом виде

---

**Кратко:** Notion использует **React + Next.js (SSR)** с **CSS Modules**, контент хранится в **Contentful**, ошибки мониторятся через **Sentry**, есть собственная система A/B тестов, consent management через **Transcend**, шрифт — кастомный **NotionInter**.
