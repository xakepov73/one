# Стартовые шаблоны структуры проекта (Python / Node.js / Go)

Этот документ — быстрый ориентир для новичка: какую структуру взять на старте и зачем нужен каждый файл.

---

## 1) Python (FastAPI) — рекомендуемый старт

Подходит, если хотите быстрый API, хорошую типизацию и простой вход в backend.

```text
my-service/
├─ pyproject.toml
├─ README.md
├─ .gitignore
├─ .env.example
├─ src/
│  └─ app/
│     ├─ __init__.py
│     ├─ main.py
│     ├─ config.py
│     ├─ api/
│     │  ├─ __init__.py
│     │  └─ health.py
│     ├─ services/
│     │  ├─ __init__.py
│     │  └─ health_service.py
│     └─ models/
│        ├─ __init__.py
│        └─ health.py
├─ tests/
│  ├─ __init__.py
│  └─ test_health.py
└─ scripts/
   ├─ run-dev.sh
   └─ test.sh
```

### Что делает каждый файл/папка

- `pyproject.toml` — зависимости, конфигурация форматтера/линтера/тестов в одном месте.
- `README.md` — как запускать проект, как тестировать, где код.
- `.gitignore` — исключает мусор (`.venv`, `__pycache__`, локальные артефакты).
- `.env.example` — шаблон переменных окружения без секретов.
- `src/app/main.py` — точка входа приложения (инициализация FastAPI, роутов).
- `src/app/config.py` — централизованная загрузка и валидация конфигурации.
- `src/app/api/` — HTTP-слой (роуты, валидация входа/выхода).
- `src/app/services/` — бизнес-логика, не привязанная к веб-фреймворку.
- `src/app/models/` — схемы данных (Pydantic/DTO/domain entities).
- `tests/` — автотесты (юнит/интеграционные).
- `scripts/` — короткие команды для одинакового запуска у всех.

### Почему это удобно новичку

- Ясное разделение: API ↔ логика ↔ модели.
- Легко искать код по ответственности.
- Меньше "магии" и проще масштабировать.

---

## 2) Node.js (TypeScript + Express/Fastify)

Подходит, если команда сильна в JavaScript/TypeScript и нужен универсальный backend.

```text
my-service/
├─ package.json
├─ tsconfig.json
├─ README.md
├─ .gitignore
├─ .env.example
├─ src/
│  ├─ index.ts
│  ├─ config/
│  │  └─ env.ts
│  ├─ routes/
│  │  └─ health.route.ts
│  ├─ controllers/
│  │  └─ health.controller.ts
│  ├─ services/
│  │  └─ health.service.ts
│  └─ types/
│     └─ health.ts
├─ test/
│  └─ health.test.ts
└─ scripts/
   ├─ dev.sh
   └─ test.sh
```

### Зачем это нужно

- `package.json` — зависимости и команды (`dev`, `build`, `test`).
- `tsconfig.json` — строгая типизация и правила компиляции.
- `src/index.ts` — вход в приложение.
- `routes/` — маршрутизация (HTTP-пути).
- `controllers/` — разбор запроса/ответа, без бизнес-правил.
- `services/` — бизнес-правила и use-case.
- `types/` — общие типы и интерфейсы.
- `test/` — тесты, чтобы не ломать поведение при изменениях.

---

## 3) Go (net/http + chi)

Подходит, если нужна простота деплоя, производительность и строгая структура пакетов.

```text
my-service/
├─ go.mod
├─ go.sum
├─ README.md
├─ .gitignore
├─ .env.example
├─ cmd/
│  └─ api/
│     └─ main.go
├─ internal/
│  ├─ config/
│  │  └─ config.go
│  ├─ transport/http/
│  │  ├─ router.go
│  │  └─ health_handler.go
│  ├─ service/
│  │  └─ health_service.go
│  └─ domain/
│     └─ health.go
├─ pkg/
│  └─ logger/
│     └─ logger.go
└─ tests/
   └─ health_test.go
```

### Зачем это нужно

- `cmd/api/main.go` — минимальный `main`, только сборка зависимостей и запуск.
- `internal/` — приватный код сервиса (не для внешнего импорта).
- `transport/http/` — HTTP-слой (роутер, handlers).
- `service/` — бизнес-логика.
- `domain/` — доменные сущности/контракты.
- `pkg/` — переиспользуемые утилиты (если действительно общие).
- `tests/` — внешние/интеграционные сценарии.

---

## Что изучить новичку в первую очередь (в любом стеке)

1. `README.md` — как поднять проект локально.
2. Файл конфигурации (`pyproject.toml`, `package.json`, `go.mod`) — чем проект живёт.
3. Точку входа (`main.py` / `index.ts` / `main.go`) — как всё запускается.
4. Первый маршрут `health` и связанный сервис — самый короткий путь понять архитектуру.
5. Первый тест — как команда проверяет корректность изменений.

## Практический совет по выбору

- Берите **Python/FastAPI**, если нужен максимально быстрый старт и понятная структура для новичков.
- Берите **Node/TS**, если фронтенд и бэкенд в одном языке.
- Берите **Go**, если важны простота эксплуатации и производительность.

