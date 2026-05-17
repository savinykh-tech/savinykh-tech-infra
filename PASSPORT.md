# ПАСПОРТ ИНФРАСТРУКТУРЫ И НАВЫКОВ (17.05.2026)

## Сервер
- Хост: Aeza VPS, тариф HELs-1
- ОС: Ubuntu 24.04.1 LTS
- Ядро: BBR (TCP Congestion Control)
- CPU: 1 core, RAM: 2 GB, NVMe: 30 GB
- Свободно: ~18 ГБ

## Сеть и безопасность
- SSH порт: 4422
- UFW: открыты 4422, 80, 443, 2053, 2083, 8443, 853; порт 53 временно открыт (⚠️ требуется закрыть, переход на DoT)
- Fail2Ban: активен
- Вход: по SSH-ключу (ed25519), пароль как запасной
- Приватный ключ: сохранён на Google Диск (архив с паролем)
- Бэкапы: ручной `save.sh` (системные файлы) + n8n (архивация backups → Telegram)
- Пароли: удалены из переменных окружения Portainer, все секреты только в n8n Credentials

## Сервисы (Docker)
| Сервис | Порт | Статус |
|--------|------|--------|
| n8n | 3000 (через Caddy) | Running |
| caddy | 80/443 | Running |
| adguard | 53, 853 (DoT) | Running (53 открыт — подлежит закрытию) |
| 3x-ui (Xray) | 2053/2083/8443 | Running |
| jarvis (Flask) | 5000 (внутренний) | Running |
| watchtower | - | Running |
| portainer | 9000 (через proxy) | Running |

## Конфигурация Docker
- Управление: Portainer (https://savinykh-tech.ru/manage)
- docker-compose.yaml: `/home/jarvis_admin/docker-compose.yaml`
- Контейнер n8n: примонтирована папка `/home/jarvis_admin` как `/host` (Bind)
- Контейнер n8n: примонтирован `/usr/bin/curl` с хоста (Bind, Read-only)
- Переменная NODES_EXCLUDE="[]" добавлена для доступа к Execute Command

## Бэкапы
- **Локальный:** `~/save.sh` (сохраняет системные конфиги в `~/backups/YYYYMMDD_HHMM/`)
- **Удалённый:** воркфлоу n8n «Бэкап конфигов Docker» (один узел Execute Command)
  - Команда: `tar -czf /host/full-backup-$(date +%Y%m%d).tar.gz -C /host backups && curl ...`
  - Отправка: Telegram бот Jarvis, chat_id=487903609
  - Частота: ручной запуск после изменений
- **Воркфлоу n8n:** ключевые воркфлоу экспортируются в JSON вручную как дополнительная страховка

## Навыки
### Уверенно
- Базовые команды Linux, SSH-ключи
- Docker run/stop, docker-compose up/down
- n8n: HTTP-запросы, пагинация, фильтрация, Telegram, Credentials, Execute Command
- JSON, Git (add, commit, push, remote)
- Монтирование папок и файлов в контейнеры (через Portainer)
- tar, curl, chown внутри контейнеров

### Изучаю
- CLI-утилиты (htop, journalctl, du, df, docker logs)
- Docker Compose (глубоко)

### Не знаю
- Python, PostgreSQL
- Cloud (S3)
- crontab
