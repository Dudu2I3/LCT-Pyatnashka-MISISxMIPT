# 🤖 ETL AI Assistant Backend - MVP

Простой MVP бэкенд для автоматизации ETL-задач с ИИ-ассистентом.

## 🚀 Быстрый запуск

### Вариант 1: Docker Compose (рекомендуется)
```bash
# Клонируйте репозиторий
git clone <repo-url>
cd etl-ai-assistant

# Запустите все сервисы
docker-compose up -d

# Проверьте статус
docker-compose ps
```

**Доступные сервисы:**
- Backend API: http://localhost:8080
- Airflow UI: http://localhost:8081 (admin/admin)
- PostgreSQL: localhost:5432
- ClickHouse: localhost:8123
- Простой UI: http://localhost:8080/static/index.html

### Вариант 2: Локальная разработка
```bash
# Установите зависимости
pip install -r requirements.txt

# Запустите только бэкенд (остальные сервисы должны быть запущены отдельно)
uvicorn app.main:app --reload --port 8080
```

## 📋 API Эндпойнты

### Health Checks
- `GET /api/v1/health/` - Общий статус
- `GET /api/v1/health/airflow` - Статус Airflow
- `GET /api/v1/health/databases` - Статус БД

### Анализ данных
- `POST /api/v1/analysis/file` - Анализ файлов (CSV/JSON/XML)
- `POST /api/v1/analysis/db` - Анализ таблиц БД

### Рекомендации
- `POST /api/v1/recommend/storage` - Рекомендации по хранению

### DDL Генерация
- `POST /api/v1/ddl/generate` - Генерация DDL скриптов

### ETL Пайплайны
- `POST /api/v1/pipelines/draft` - Создание пайплайна
- `POST /api/v1/pipelines/publish` - Публикация в Airflow
- `POST /api/v1/pipelines/trigger/{dag_id}` - Запуск DAG
- `GET /api/v1/pipelines/status/{dag_id}` - Статус DAG

## 🛠️ Структура проекта

```
app/
├── main.py                 # Точка входа FastAPI
├── core/
│   └── config.py          # Конфигурация
├── api/v1/                # API маршруты
│   ├── router.py
│   ├── routes_health.py
│   ├── routes_analysis.py
│   ├── routes_recommend.py
│   ├── routes_ddl.py
│   └── routes_pipelines.py
├── schemas/               # Pydantic схемы
├── services/              # Бизнес-логика
├── connectors/            # Коннекторы к источникам
└── integrations/          # Интеграции (Airflow)
```

## 🔧 Конфигурация

Создайте `.env` файл (см. `.env.example`):
```bash
ENV=dev
CORS_ALLOW_ORIGINS=*
AIRFLOW_BASE_URL=http://localhost:8081
POSTGRES_DSN=postgresql+psycopg2://user:password@localhost:5432/etl_db
CLICKHOUSE_HOST=localhost
CLICKHOUSE_PORT=8123
```

## 🧪 Тестирование

1. Откройте http://localhost:8080/static/index.html
2. Используйте простой UI для тестирования всех эндпойнтов
3. Или используйте Swagger UI: http://localhost:8080/api/docs

## 📦 Что включено

- ✅ FastAPI с автоматической документацией
- ✅ Коннекторы: PostgreSQL, ClickHouse, файлы (CSV/JSON/XML)
- ✅ Интеграция с Airflow (заглушка)
- ✅ Health checks для всех сервисов
- ✅ Простой веб-интерфейс для тестирования
- ✅ Docker Compose для локальной разработки

## 🔄 Следующие шаги

1. **ML-инженер**: Реализовать LLM-сервис для анализа и рекомендаций
2. **DevOps**: Настроить продакшн инфраструктуру (K8s, мониторинг)
3. **Frontend**: Создать полноценный React UI
4. **Дата-инженер**: Добавить сложные трансформации и коннекторы

## 🐛 Устранение неполадок

- Если Airflow не запускается: `docker-compose logs airflow-webserver`
- Если БД недоступны: `docker-compose logs postgres clickhouse`
- Проверьте статус: `GET /api/v1/health/`


