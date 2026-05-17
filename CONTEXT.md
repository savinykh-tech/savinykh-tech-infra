# КОНТЕКСТ ОБУЧЕНИЯ: Роман Савиных

## Цель
- Выйти на удалённый заработок 200 000+ руб./мес. через 12 месяцев
- Основной инструмент: автоматизация на n8n + интеграции
- Обучение: 2-3 часа в день, без выгорания
- Стратегия: «сначала фундамент, потом монетизация»

## Инфраструктура (на 18.05.2026)
- Сервер: Aeza HELs-1 (Ubuntu 24.04, 1 CPU, 2GB RAM, 30GB NVMe)
- Локация: Хельсинки
- SSH: порт 4422, вход по ключу ed25519
- Стек: Docker, n8n, Caddy, AdGuard Home, 3x-ui, Jarvis
- Домен: savinykh-tech.ru (SSL через Caddy)
- Безопасность: UFW, Fail2Ban, порт 53 закрыт, DNS-over-TLS/DoH
- Управление: Portainer (https://savinykh-tech.ru/manage)

## Ключевые автоматизации
- Парсер заявок Servionica (n8n)
- Бот Jarvis (Flask + Telegram)
- Бэкап-воркфлоу (save.sh + n8n → Telegram)

## Git и портфолио
- Репозиторий: https://github.com/savinykh-tech/savinykh-tech-infra
- Документация: CONTEXT.md, PASSPORT.md, PLAN.md, PROGRESS.md

## Текущий этап (18.05.2026)
- Закрыт порт 53, настроен DNS-over-TLS/DoH
- Вся инфраструктура под контролем
- Следующий шаг: CLI-утилиты (journalctl, docker logs, htop)
