# StackBridge Technical Task

Простой веб-сервис на Python с reverse-proxy через Nginx, упакованный в Docker.

---

## 📋 Описание

Проект состоит из двух сервисов:
- **Backend** — HTTP-сервер на Python, отвечает на запросы текстом *"Hello from Effective Mobile!"*
- **Nginx** — reverse-proxy, принимает запросы на порту 80 и проксирует их на backend