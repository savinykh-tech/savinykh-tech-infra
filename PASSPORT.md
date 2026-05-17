# ПАСПОРТ ИНФРАСТРУКТУРЫ И НАВЫКОВ (18.05.2026)

## Сервер
- Хост: Aeza VPS, тариф HELs-1
- ОС: Ubuntu 24.04.1 LTS
- Ядро: BBR (TCP Congestion Control)
- CPU: 1 core, RAM: 2 GB, NVMe: 30 GB
- Свободно: ~18 ГБ

## Сеть и безопасность
- SSH порт: 4422
- UFW: открыты 4422, 80, 443, 853, 2053, 2083, 8443
- Fail2Ban: активен
- Вход: по SSH-ключу (ed25519), пароль как запасной
- Приватный ключ: сохранён на Google Диск (архив с паролем)
- DNS: AdGuard Home работает по DNS-over-TLS (порт 853) и DoH (443). Порт 53 полностью закрыт.
- Микрот: переведён на DoH (https://savinykh-tech.ru/dns-query) + резерв Cloudflare (1.1.1.1)
- Пароли: удалены из переменных окружения, секреты только в n8n Credentials

## Сервисы (Docker)
| Сервис | Порт | Статус |
|--------|------|--------|
| n8n | 3000 (через Caddy) | Running |
| caddy | 80/443 | Running |
| adguard | 853 (DoT), 443 (DoH) | Running |
| 3x-ui (Xray) | 2053/2083/8443 | Running |
| jarvis (Flask) | 5000 (внутренний) | Running |
| watchtower | - | Running |
| portainer | 9000 (через proxy) | Running |

## Конфигурация Docker
- Управление: Portainer (https://savinykh-tech.ru/manage)
- docker-compose.yaml: `/home/jarvis_admin/docker-compose.yaml`
- Контейнер n8n: примонтирована папка `/home/jarvis_admin` как `/host` (Bind)
- Контейнер n8n: примонтирован `/usr/bin/curl` с хоста (Bind, Read-only)

## Бэкапы
- **Локальный:** `~/save.sh` (сохраняет системные конфиги в `~/backups/`)
- **Удалённый:** воркфлоу n8n (архивирует папку `backups` → отправляет в Telegram)
- **Частота:** ручной запуск после изменений, в перспективе crontab

## Навыки
### Уверенно
- Базовые команды Linux, SSH-ключи
- Docker run/stop, монтирование файлов и папок в контейнеры
- n8n: HTTP-запросы, пагинация, фильтрация, Credentials, Execute Command, отправка файлов
- Git (add, commit, push, remote)
- DNS-over-TLS/DoH, базовая сетевая безопасность (UFW, Fail2Ban)
- Работа с WinBox (MikroTik)

### Изучаю
- CLI-утилиты (journalctl, docker logs, htop, df, du)
- Docker Compose (глубоко)

### Не знаю
- Python, PostgreSQL
- Cloud (S3)
- crontab
