
# Интеллектуальный цифровой инженер данных

MVP сервиса для автоматизации **ETL-задач** с использованием LLM.  
Цель проекта — упростить работу с данными: подключение источников, построение пайплайнов, выбор хранилища и автоматизация обновлений.

---

## 📌 Стек технологий
- **Backend:** FastAPI (Python)
- **Frontend:** React
- **ETL/оркестрация:** Apache Airflow (обязательно), допускаются Prefect/Dagster
- **Хранилища:** PostgreSQL, ClickHouse, HDFS
- **ML/AI:** LLM для анализа данных и генерации SQL/DDL/рекомендаций
- **Контейнеризация:** Docker / Docker Compose
- **(Опционально) Оркестрация контейнеров:** Kubernetes

---

## 🔧 Правила работы с кодом (Git Flow)
1. **Не пушим напрямую в `main`.** Все изменения — только через Pull Request.
2. Создаём ветку от `main`:
   ```bash
   git checkout -b feature/<кратко-о-фиче>
   # примеры: feature/add-csv-loader, bugfix/fix-ch-ddl, docs/architecture-diagram


3. Делаем атомарные коммиты с понятными сообщениями:

   ```bash
   git commit -m "etl: добавлен загрузчик CSV и тесты"
   ```

   Рекомендуемый префикс: `backend:`, `frontend:`, `ml:`, `etl:`, `docs:`, `devops:`.
4. Открываем PR в `main`:

   * Описание: **что**, **зачем**, **как тестировать**.
   * Ссылки на Issues (напр. `Closes #12`).
   * Минимум **1 ревью** от участника команды.
5. После апрува — **merge** через Squash & Merge (чистая история).
6. CI должен быть зелёным до слияния (когда добавим GitHub Actions).

---

## ✅ Как работать с задачами (Issues + Project Board)

1. Все задачи фиксируем в **GitHub Issues**.
2. Каждую Issue связываем с **Project Board** (Kanban: *To Do → In Progress → Review → Done*).
3. Шаблон Issue (кратко):

   * **Описание:** что нужно сделать и почему.
   * **Готово когда:** измеримые критерии приёмки.
   * **Затронутые модули:** файлы/папки.
   * **Связано:** ссылки на PR/другие Issues.
4. К одной задаче — одна ветка и один PR.

---

## ▶️ Локальный запуск (черновик)

> Раздел будет дополняться по мере появления кода и Docker-окружения.

1. Клонировать репозиторий:

   ```bash
   git clone https://github.com/Fomikk/LCT-Pyatnashka-MISISxMIPT.git
   cd LCT-Pyatnashka-MISISxMIPT
   ```
2. (Позже) установить зависимости и переменные окружения:

   ```bash
   # пример
   python -m venv .venv && source .venv/bin/activate
   pip install -r requirements.txt
   cp .env.example .env
   ```
3. (Позже) запустить Docker-сервисы:

   ```bash
   docker-compose up -d
   ```
4. Проверка сервисов:

   * Backend: [http://localhost:8000](http://localhost:8000)
   * Airflow: [http://localhost:8080](http://localhost:8080)
   * Frontend: [http://localhost:3000](http://localhost:3000)

---

## 📂 Структура репозитория

```
/backend   → API (FastAPI/Django)
/frontend  → UI (React/Vue)
/ml        → LLM, анализ данных, генерация SQL/DDL
/etl       → пайплайны (Airflow/Prefect/Dagster)
/docs      → схемы (.drawio/.png), отчёты, презентации, скриншоты
```

---

## 🧭 Дорожная карта (MVP)

* Подключение файловых источников (CSV/JSON/XML) → `etl`, `ml`
* Автоанализ структуры и генерация DDL → `ml`
* Рекомендация хранилища (CH/HDFS/PG) → `ml`
* Базовый пайплайн в Airflow (без сложных трансформаций) → `etl`
* UI для ввода источников/цели + визуализация пайплайна → `frontend`
* Backend-API для связи UI ↔ LLM/ETL → `backend`
* Docker Compose для локального запуска → `devops`

---

## 🧪 Качество, тесты и стиль

* Тесты: `pytest` (минимум smoke-тесты на ключевые модули).
* Линтеры: `ruff`/`flake8`, форматирование `black`.
* Типы: `mypy` где возможно.
* Запуск (будет уточнено):

  ```bash
  pytest -q
  ruff check .
  black --check .
  mypy .
  ```

---


## 📎 Полезные ссылки

* **Project Board:** (добавить ссылку после создания)
* **Docs:** `/docs`
* **Архитектура:** `/docs/architecture.drawio` и `/docs/architecture.png` (после добавления)
* **Коммуникация:** Telegram-чат команды

---

## 👥 Команда

* Team Lead / Backend: Никитенко Егор
* Frontend: Джабраилов Павел
* ML/AI: Фоменко Артём
* ETL/Data Engineer: Кабанов Виталий
* DevOps: Хабибуллин Данияр

---

## 📄 Лицензия

Проект распространяется по лицензии **MIT** (см. `LICENSE`).

```
```
