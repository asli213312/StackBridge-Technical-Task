# StackBridge Technical Task

Простой веб-сервис на Python с reverse-proxy через Nginx, упакованный в Docker как результат тестового задания.

---

## 📋 Описание

Проект состоит из двух сервисов:
- **Backend** — HTTP-сервер на Python, отвечает на запросы текстом *"Hello from Effective Mobile!"*
- **Nginx** — reverse-proxy, принимает запросы на порту 80 и проксирует их на backend

- ## Запуск

```bash
# 1. Клонировать репозиторий
git clone https://github.com/asli213312/StackBridge-Technical-Task
cd StackBridge-Technical-Task

# 2. Запустить проект
docker-compose --profile prod up -d

# 3. Проверить работу
curl http://localhost
```

Ожидаемый ответ: `"Hello from Effective Mobile!"` (курсивом)

---

## 🏗 Архитектура

```
Пользователь (порт 80) → Nginx → Backend (порт 8080)
```

### Схема взаимодействия

```
┌─────────────┐      ┌─────────────┐      ┌─────────────┐
│  Пользователь│ ────▶│    Nginx    │ ────▶│   Backend   │
│   (браузер) │      │   :80       │      │   :8080     │
└─────────────┘      └─────────────┘      └─────────────┘
                            │                       │
                            └─────── Docker-сеть "app"
```

- Backend не публикует порт на хост (доступен только внутри Docker-сети)
- Nginx проксирует все запросы на backend

---

## 🔧 Режимы запуска

| Профиль | Команда | Описание |
| :--- | :--- | :--- |
| **dev** | `docker-compose --profile dev up -d` | Конфиг Nginx монтируется через volume (для разработки) |
| **prod** | `docker-compose --profile prod up -d --build` | Конфиг Nginx внутри образа (для продакшена) |

---

## 📁 Структура проекта

```
StackBridge-Technical-Task/
├── backend/
│   ├── Dockerfile          # сборка Python-образа
│   └── app.py              # HTTP-сервер
├── nginx/
│   ├── Dockerfile          # сборка Nginx с конфигом
│   └── nginx.conf          # конфигурация reverse-proxy
├── .env                    # переменные окружения продакшена
├── .env.dev                # переменные окружения разработки
├── docker-compose.yaml     # основной compose-файл
└── README.md
```

---

## 🛠 Технологии

| Технология | Версия |
| :--- | :--- |
| Python | 3.11 |
| Nginx | 1.25.3-alpine |
| Docker | 20.10+ |
| Docker Compose | 2.20+ |

---
