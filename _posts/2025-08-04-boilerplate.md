---
layout: post
title: Микросервисная архитектура онлайн-магазина: boilerplate
date: 2025-08-04
tags: [go, микросервисы, онлайн-магазин, highload, ddd, api-gateway, boilerplate]
---

# Начинаем разработку user-service

Сегодня приступаю к разработке первого микросервиса — user-service. На старте хочу придерживаться принципа минимализма и сконцентрироваться на базовой функциональности. Никаких JWT токенов, сложных валидаций и прочих излишеств — только минимально рабочий сервис.

# Настройка проекта

Прежде чем писать код, настрою структуру всего проекта и определюсь с процессами разработки.

## Git Flow стратегия

Планирую использовать следующую структуру веток:

```bash
# Основные ветки
main                     # Production-ready код
develop                  # Ветка интеграции

# Feature branches для каждого компонента
feature/api-gateway      # HTTP Gateway и маршрутизация
feature/user-service     # CRUD операции с пользователями
feature/product-service  # CRUD операции с товарами
feature/infrastructure   # Docker Compose, Makefile
feature/load-testing     # Нагрузочное тестирование
```

## Commit Style 

Буду следовать Conventional Commits для структурированной истории:

```bash
feat(gateway): add HTTP routing to services
fix(users): resolve database connection issue  
docs(readme): update setup instructions
test(products): add integration tests
perf(gateway): optimize request routing
refactor(shared): extract common middleware
```

## Версионирование

Semantic Versioning с четким планом релизов:

```bash
v0.1.0 - API Gateway MVP
v0.2.0 - User Service MVP  
v0.3.0 - Product Service MVP
v1.0.0 - Полная интеграция системы
```

# Структура монорепозитория

Решил разрабатывать все микросервисы в одном репозитории для удобства на начальном этапе. Воспользуюсь Go workspaces для управления зависимостями.

## Go Workspace конфигурация

**go.work:**
```go
go 1.21

use (
    ./services/api-gateway
    ./services/user-service
    ./services/product-service
)
```

## Инициализация структуры

Создаю базовую структуру проекта:

```bash
# Создание директорий для сервисов
mkdir -p services/{api-gateway,user-service,product-service}

# Файлы инфраструктуры
touch docker-compose.yml Makefile .gitignore .golangci.yml
```

## .gitignore

Настраиваю игнорирование стандартных файлов:

```txt
# Бинарные файлы
bin/
*.exe

# IDE
.vscode/
.idea/

# Логи и конфигурация
*.log
.env

# Временные файлы
tmp/
*.tmp
```

# Инициализация репозитория

Создаю основные ветки и делаю первый коммит:

```bash
# Создание веток
git checkout -b develop
git checkout -b feature/user-service

# Первый коммит с базовой структурой
git add .
git commit -m "feat: initial project structure with go workspaces"
git push origin feature/user-service
```

# Вопрос с общими компонентами

Пока не определился с тем, как лучше поступить с общими компонентами (логгер, HTTP utils, конфигурация). Рассматриваю два варианта:

1. **Shared модуль** — отдельный пакет для общих компонентов
2. **Дублирование кода** — каждый сервис содержит свою реализацию

На текущем этапе склоняюсь к дублированию для максимальной независимости сервисов. Позже, когда паттерны устоятся, можно будет вынести общий код.

# Следующие шаги

В следующем посте начну непосредственную разработку user-service:

- Базовая архитектура с чистыми слоями
- PostgreSQL для хранения данных
- Redis для кэширования  
- REST API с тремя endpoint'ами
- Structured логирование с Zap
- Docker контейнеризация

Цель — получить работающий сервис за минимальное время без излишних абстракций и преждевременных оптимизаций.