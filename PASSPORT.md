# ПАСПОРТ ИНФРАСТРУКТУРЫ И НАВЫКОВ (15.05.2026)

## Сервер
- Хост: Aeza VPS, тариф HELs-1
- ОС: Ubuntu 24.04.1 LTS
- Ядро: BBR (TCP Congestion Control)
- CPU: 1 core, RAM: 2 GB, NVMe: 30 GB
- Свободно: 18 ГБ

## Сеть и безопасность
- SSH порт: 4422
- UFW: открыты 4422, 80, 443, 2053, 2083, 8443, 853; порт 53 временно открыт (⚠️ требуется закрыть, переход на DoT)
- Fail2Ban: активен
- Вход: по SSH-ключу (ed25519), пароль как запасной
- Приватный ключ: сохранён на Google Диск в архиве с паролем
- Бэкапов НЕТ (⚠️ в ближайших планах)

## Сервисы (Docker)
| Сервис | Порт | Статус |
|--------|------|--------|
| n8n | 3000 (через Caddy) | Running |
| caddy | 80/443 | Running |
| adguard | 53, 853 (DoT) | Running (53 открыт — подлежит закрытию) |
| 3x-ui (Xray) | 2053/2083/8443 | Running |
| jarvis (Flask) | 5000 (внутренний) | Running |
| watchtower | - | Running |
| portainer | - | Running |

## Навыки
### Уверенно
- Базовые команды Linux
- SSH-ключи
- Docker run/stop
- n8n: HTTP, пагинация, фильтрация, Telegram, Credentials
- JSON

### Изучаю
- Git (освоен на уровне add, commit, push)
- Docker Compose (базово)

### Не знаю
- Python, PostgreSQL
- CLI-утилиты (htop, journalctl, du, df, docker logs)
- Cloud (S3)
- crontab

## Безопасность (чек-лист)
- [x] SSH нестандартный порт
- [x] Fail2Ban
- [x] UFW
- [x] Вход по ключу
- [x] Приватный ключ сохранён на Google Диск (в архиве с паролем)
- [ ] Бэкапы (следующий шаг — n8n workflow)
- [x] Токены в Credentials
- [ ] Пароль sudo не отключен (проверить)
- [ ] Закрыть порт 53 (настроить DoT для микрота и телефона)
