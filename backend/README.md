# 🤖 ETL AI Assistant - MVP для автоматизации ETL-задач

Интеллектуальный цифровой инженер данных на базе ИИ для автоматизации рутинных ETL-процессов.

## 🎯 Описание проекта

Этот проект представляет собой MVP ИИ-ассистента для автоматизации ETL-задач, который позволяет пользователям без специальных знаний настраивать конвейеры обработки данных через простой веб-интерфейс.

### Ключевые возможности:
- ✅ Подключение к различным источникам данных (CSV, JSON, XML, PostgreSQL, ClickHouse)
- ✅ Анализ структуры данных с помощью ИИ
- ✅ Рекомендации по оптимальному хранению данных
- ✅ Автоматическая генерация DDL-скриптов
- ✅ Создание ETL-пайплайнов с интеграцией в Airflow
- ✅ Работа по расписанию
- ✅ Простой веб-интерфейс для настройки

## 🚀 Быстрый запуск

### Локальный запуск с Docker Compose

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
- 🌐 **API Backend**: http://localhost:8080
- 📚 **API Документация**: http://localhost:8080/api/docs
- 🖥️ **Веб-интерфейс**: http://localhost:8080/static/index.html
- 🔄 **Airflow**: http://localhost:8081 (admin/admin)
- 🐘 **PostgreSQL**: localhost:5432 (user/password)
- 🏠 **ClickHouse**: localhost:8123 (default/)

### Разработка

```bash
# Установка зависимостей
pip install -r requirements.txt

# Запуск только бэкенда (для разработки)
python run_dev.py
```

## 📋 API Endpoints

### Health Checks
- `GET /api/v1/health/` - общий статус системы
- `GET /api/v1/health/airflow` - статус Airflow
- `GET /api/v1/health/databases` - статус баз данных

### Анализ данных
- `POST /api/v1/analysis/file` - анализ файлов (CSV/JSON/XML)
- `POST /api/v1/analysis/db` - анализ таблиц БД
- `POST /api/v1/analysis/profile` - профилирование источника

### Рекомендации и DDL
- `POST /api/v1/recommend/storage` - рекомендации по хранению
- `POST /api/v1/ddl/generate` - генерация DDL-скриптов

### ETL Пайплайны
- `POST /api/v1/pipelines/draft` - создание черновика пайплайна
- `POST /api/v1/pipelines/publish` - публикация в Airflow
- `POST /api/v1/pipelines/trigger/{dag_id}` - запуск пайплайна
- `GET /api/v1/pipelines/status/{dag_id}` - статус пайплайна

## 🏗️ Архитектура решения

### Компоненты системы:

1. **FastAPI Backend** - основной API сервер
2. **PostgreSQL** - метаданные и конфигурация
3. **ClickHouse** - аналитические данные
4. **Airflow** - оркестрация ETL-процессов
5. **LLM Service** - интеграция с языковыми моделями
6. **Web UI** - простой интерфейс для пользователей

### Поддерживаемые источники данных:
- 📄 **Файлы**: CSV, JSON, XML
- 🐘 **PostgreSQL** - оперативные данные
- 🏠 **ClickHouse** - аналитические данные
- 🔄 **Kafka** - потоковые данные (заглушка)
- 📁 **HDFS** - большие данные (заглушка)

### Поддерживаемые целевые системы:
- 🐘 **PostgreSQL** - для оперативных данных
- 🏠 **ClickHouse** - для аналитики с партицированием
- 📁 **HDFS** - для больших данных в Parquet формате

## 🧠 ИИ-функциональность

Система использует LLM для:
- Анализа структуры данных и качества
- Генерации рекомендаций по хранению
- Создания оптимизированных DDL-скриптов
- Генерации кода ETL-пайплайнов

## 📊 Тестовые данные

В проекте включены примеры тестовых данных:
- `test_data/sample.csv` - CSV с данными сотрудников
- `test_data/sample.json` - JSON с расширенной структурой
- `test_data/sample.xml` - XML с иерархической структурой

## 🔧 Конфигурация

Основные настройки в `.env`:
```env
ENV=dev
POSTGRES_DSN=postgresql+psycopg2://user:password@postgres:5432/etl_db
CLICKHOUSE_HOST=clickhouse
AIRFLOW_BASE_URL=http://airflow-webserver:8080
LLM_BASE_URL=http://llm:8000
```

## 📈 Мониторинг

Система включает:
- Health checks для всех компонентов
- Логирование через Loguru
- Метрики производительности
- Кэширование результатов анализа

## 🚀 Развертывание в облаке

Для продакшена рекомендуется:
- Kubernetes для оркестрации контейнеров
- Настройка мониторинга (Prometheus/Grafana)
- Использование внешних LLM сервисов
- Настройка backup и disaster recovery

## 📝 Примеры использования

### 1. Анализ CSV файла
```bash
curl -X POST "http://localhost:8080/api/v1/analysis/file" \
  -H "Content-Type: application/json" \
  -d '{
    "file_path": "/app/test_data/sample.csv",
    "file_type": "csv",
    "connection": {}
  }'
```

### 2. Генерация DDL для ClickHouse
```bash
curl -X POST "http://localhost:8080/api/v1/ddl/generate" \
  -H "Content-Type: application/json" \
  -d '{
    "target_system": "clickhouse",
    "table_name": "analytics_data",
    "sample": {
      "columns": [
        {"name": "id", "dtype": "int", "nullable": false},
        {"name": "ts", "dtype": "timestamp", "nullable": false},
        {"name": "value", "dtype": "float", "nullable": true}
      ]
    }
  }'
```

### 3. Создание ETL пайплайна
```bash
curl -X POST "http://localhost:8080/api/v1/pipelines/draft" \
  -H "Content-Type: application/json" \
  -d '{
    "source": {"type": "csv", "path": "/data/input.csv"},
    "destination": {"type": "clickhouse", "table": "analytics"},
    "schedule_cron": "0 * * * *"
  }'
```

## 🤝 Вклад в проект

1. Fork репозитория
2. Создайте feature branch
3. Внесите изменения
4. Добавьте тесты
5. Создайте Pull Request

## 📄 Лицензия

MIT License - см. файл LICENSE для деталей.

## 🆘 Поддержка

При возникновении проблем:
1. Проверьте логи: `docker-compose logs`
2. Проверьте статус сервисов: `docker-compose ps`
3. Создайте issue в репозитории

---

**Разработано для хакатона по созданию ИИ-ассистента для автоматизации ETL-задач**


