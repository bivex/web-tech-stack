Вот полный анализ стека технологий **shopify.com** через DevTools:

---

## Frontend Framework

**React Router v7.13.0 (React Router Framework mode = бывший Remix)**
- Подтверждено через `window.__reactRouterVersion = "7.13.0"`, `window.__reactRouterContext`, `window.__reactRouterManifest`
- В dataLayer прямо указано: `service: "brochure-iii-remix"` — маркетинговый сайт называется "Brochure III Remix"
- **SSR**: `ssr: true`, `isSpaMode: false` — полноценный server-side rendering
- Точки входа: `entry.client-*.js`, `root-*.js`, `route-*.js`, `layout-*.js` — классическая структура Remix/React Router

**React** (последняя версия)
- Файлы: `react-*.js`, `react-dom-*.js`, `jsx-runtime-*.js` на CDN Shopify
- React Fiber подтверждён через `__reactFiber$...` на DOM-элементах

**Сборщик: Vite**
- Характерный паттерн хэшей в именах файлов: `home.v4-Bn7vuk60.css`, `entry.client-CL-IJ7XY.js`, `chunk-JZWAC4HX-BPFHNEQr.js`

---

## CSS

**Tailwind CSS v4**
- Подтверждён по классам в DOM: `flex`, `grid`, `items-center`, `px-margin`, `xl:px-auto-xl`, `bg-section-dark-bg`
- CSS-переменная `--spacing: .25rem` и цвета в формате `oklch(62.3% .214 259.815)` — это точные маркеры Tailwind v4 (не v3)

---

## Графика и анимации

**Three.js v174** — присутствует `window.__THREE__ = "174"`, 2 WebGL-canvas на странице (3D-сцены в hero-секции)

**Rive** (`@rive-app/webgl2@2.34.2`) — интерактивные векторные анимации, загружается WASM-файл `rive.wasm` с unpkg.com

**detect-gpu** (`detect-gpu@5.0.38`) — определение мощности GPU клиента для адаптации графики

---

## Инфраструктура и CDN

- Все статические ресурсы (JS, CSS, шрифты, изображения) хостятся на **cdn.shopify.com** под путём `/shopifycloud/world/brochure/production-homepage/`
- Протокол: **HTTP/2**
- Размер HTML-документа: ~87 KB

---

## Аналитика и маркетинг

| Сервис | Детали |
|---|---|
| **Google Tag Manager** | Кастомный Shopify-эндпоинт `gtm.shopify.com` + стандартный `googletagmanager.com` |
| **dataLayer** | 21 событие при загрузке (component_viewability, page data) |
| **Schema.org** | Структурированные данные `Corporation` для SEO |

---

## Мультиязычность (i18n)

- 61 `hreflang`-ссылка — сайт поддерживает ~30 локалей (en-US, es-AR, de-AT, pt-BR, ru и др.)
- Собственная i18n система: файлы `I18N-*.js`, `i18nInstance-*.js`, `useIntlLocale-*.js`

---

## Прочие технологии

- **Ethereum** (`window.ethereum = true`) — определение Web3/MetaMask кошелька у пользователя
- **CMP** (`window.cmp`) — собственная система управления согласием на cookies (без сторонних OneTrust/Transcend)
- **TypeScript** — судя по структуре кода (types-*.js, enums-*.js) весь код написан на TypeScript
- **AMD define** — присутствует, вероятно для legacy-совместимости

---

**Кратко:** Shopify использует **React Router v7 (Remix) + React + Vite + Tailwind CSS v4** для SSR, **Three.js** и **Rive** для интерактивной графики, собственный CDN (`cdn.shopify.com`) и кастомный GTM-инстанс (`gtm.shopify.com`). Вся система называется внутри **"Brochure"** — это их собственная маркетинговая платформа.
