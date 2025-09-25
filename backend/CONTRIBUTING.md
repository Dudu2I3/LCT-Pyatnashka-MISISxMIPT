# 🤝 Руководство по разработке

## 🚀 Быстрый старт

### Локальная разработка
```bash
# 1. Клонируйте репозиторий
git clone <repo-url>
cd etl-ai-assistant

# 2. Установите зависимости
pip install -r requirements.txt

# 3. Запустите внешние сервисы
docker-compose -f docker-compose.dev.yml up -d

# 4. Запустите бэкенд
python run_dev.py
```

### Полный запуск (все сервисы)
```bash
docker-compose up -d
```

## 🏗️ Архитектура

### Backend (FastAPI)
- **API:** `/api/v1/`
- **Документация:** `/api/docs`
- **Health checks:** `/api/v1/health/`

### Основные компоненты
- `app/api/` - REST API эндпойнты
- `app/services/` - бизнес-логика
- `app/connectors/` - коннекторы к источникам данных
- `app/schemas/` - Pydantic модели
- `app/integrations/` - интеграции (Airflow, LLM)

## 🔧 Разработка

### Добавление нового эндпойнта
1. Создайте схему в `app/schemas/`
2. Добавьте сервис в `app/services/`
3. Создайте роут в `app/api/v1/`
4. Зарегистрируйте в `app/api/v1/router.py`

### Добавление нового коннектора
1. Создайте класс в `app/connectors/`
2. Добавьте методы подключения и анализа
3. Обновите сервисы анализа

### Тестирование
```bash
# Запуск тестов
pytest

# Проверка линтера
flake8 app/
black app/
```

## 📋 API Эндпойнты

### Health Checks
- `GET /api/v1/health/` - общий статус
- `GET /api/v1/health/airflow` - статус Airflow
- `GET /api/v1/health/databases` - статус БД

### Анализ данных
- `POST /api/v1/analysis/file` - анализ файлов
- `POST /api/v1/analysis/db` - анализ БД

### Рекомендации
- `POST /api/v1/recommend/storage` - рекомендации по хранению

### DDL
- `POST /api/v1/ddl/generate` - генерация DDL

### Пайплайны
- `POST /api/v1/pipelines/draft` - создание пайплайна
- `POST /api/v1/pipelines/publish` - публикация в Airflow
- `POST /api/v1/pipelines/trigger/{dag_id}` - запуск DAG
- `GET /api/v1/pipelines/status/{dag_id}` - статус DAG

## 🔄 Workflow

### Git Flow
1. Создайте feature ветку: `git checkout -b feature/new-feature`
2. Внесите изменения
3. Создайте PR в main ветку
4. После ревью - мерж в main

### Коммиты
Используйте conventional commits:
- `feat:` - новая функциональность
- `fix:` - исправление бага
- `docs:` - документация
- `refactor:` - рефакторинг
- `test:` - тесты

## 🐛 Отладка

### Логи
- Backend: консоль PyCharm/терминал
- Docker: `docker-compose logs <service>`

### Частые проблемы
1. **Порт занят:** измените порт в конфигурации
2. **Docker не запускается:** проверьте Docker Desktop
3. **БД недоступна:** проверьте `docker-compose ps`

## 📚 Полезные ссылки

- [FastAPI документация](https://fastapi.tiangolo.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [Airflow документация](https://airflow.apache.org/docs/)
- [Pydantic](https://pydantic-docs.helpmanual.io/)
