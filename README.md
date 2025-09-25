
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


## 🔧 Правила работы с кодом и гайд по GitHub

### Основные правила
1. **В `main` ничего не пушим!**  
   Все изменения делаем в отдельной ветке → потом создаём Pull Request (PR).

2. **Создаём ветку от `main`:**
   ```bash
   git checkout -b feature/название-задачи

Примеры:

* `feature/add-csv-loader`
* `bugfix/fix-clickhouse`
* `docs/add-architecture`

3. **Делаем коммиты небольшими и понятными:**

   ```bash
   git commit -m "etl: добавлен загрузчик CSV"
   ```

   Используем префиксы: `backend:`, `frontend:`, `ml:`, `etl:`, `docs:`, `devops:`.

4. **Pull Request (PR):**

   * Описать: что изменилось и зачем.
   * Если задача есть в Issues → указать `Closes #номер`.
   * Ждём хотя бы одного ревью от команды.

5. **Слияние (merge):**
   После апрува объединяем ветку через **Squash & Merge** → история в `main` остаётся чистой.

---

### Мини-гайд для новичков

1. Склонировать репозиторий (делается один раз):

   ```bash
   git clone https://github.com/Fomikk/LCT-Pyatnashka-MISISxMIPT.git
   cd LCT-Pyatnashka-MISISxMIPT
   ```

2. Создать ветку для своей задачи:

   ```bash
   git checkout -b feature/название-задачи
   ```

3. Внести изменения → сохранить файлы → закоммитить:

   ```bash
   git add .
   git commit -m "frontend: добавлен компонент пайплайна"
   ```

4. Отправить ветку на GitHub:

   ```bash
   git push origin feature/название-задачи
   ```

5. Перейти на сайт GitHub → появится кнопка **Compare & Pull Request** → создать PR.

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
