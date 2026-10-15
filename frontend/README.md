# Noir Bijoux — frontend

React 19 + TypeScript + React Router + Vite + Tailwind CSS. Визуальное оформление сохранено; изменения касаются данных каталога, компонентов конструктора и путей к изображениям.

## Запуск в PowerShell

```powershell
cd C:\Projects\NOIR_BIJOUX\frontend
Copy-Item .env.example .env
npm ci
npm run dev
```

Сайт: `http://localhost:5173`. В другом окне PowerShell запустите API из `backend/` (инструкции — `backend/docs/ПРАКТИКА_15_NOIR_BIJOUX.md`).

## API и запасные данные

Каталог загружает `GET /api/products`, конструктор — `GET /api/components?type=...`. Если API не запущен, страница использует те же локальные данные из `app/data/`, поэтому интерфейс остаётся доступным. Адрес задаётся через `VITE_API_URL` в `.env`.

Демо-авторизация, избранное, корзина и история заказов на frontend пока хранятся в `localStorage`; backend API для пользователей, сборок и заказов подготовлен отдельно.

## PNG-assets

Публичные PNG должны находиться в `public/assets/`. Полный список путей — `public/assets/README.md`. В текущей копии проекта сами новые PNG не приложены, поэтому отображаются прежние SVG-заполнители из `app/assets/`; после добавления PNG они автоматически заменят заполнители. В базе хранятся только пути `/assets/...`, а не бинарные изображения.

Имена из исходного списка нормализованы так: пробел в `bracelet-dark-star .png` убран; написание `stone-pearle.png` сохранено.

## Команды

| Команда | Назначение |
|---|---|
| `npm ci` | установить версии из lock-файла |
| `npm run dev` | режим разработки, порт 5173 |
| `npm run typecheck` | проверка типов |
| `npm run build` | production-сборка |
| `npm start` | запустить production-сборку |

## Маршруты

`/` — главная · `/catalog` — каталог · `/product/:slug` — изделие · `/about` — мастер · `/constructor` — выбор типа · `/constructor/necklace`, `/bracelet`, `/earrings`, `/ring` — конструктор · `/cart` · `/checkout` · `/login` · `/register` · `/profile/history` · `/profile/favorites` · `/profile/settings`.

## Docker и GitHub Actions

Frontend — самостоятельный проект: `Dockerfile` собирает production-образ, `.github/workflows/build.yml` запускает typecheck/build и публикует образ в GitHub Container Registry после push в `main`. По умолчанию `VITE_API_URL=/api` (нужен reverse proxy на backend). Для раздельных production-доменов задайте build argument или Actions variable `VITE_API_URL` с публичным URL API, например `https://api.example.com/api`.
