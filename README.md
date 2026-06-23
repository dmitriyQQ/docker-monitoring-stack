# Полный стек мониторинга и логирования на Docker

Готовый к развёртыванию стек **Prometheus + Node Exporter + Loki + Promtail + Grafana**.
Собирает метрики системы, централизует логи Docker-контейнеров и предоставляет единую панель для визуализации и анализа.

## Возможности

- **Метрики хоста** (CPU, память, диск, сеть) через Node Exporter → Prometheus
- **Логи всех Docker-контейнеров** автоматически собираются Promtail → Loki
- **Преднастроенные дашборды:** Node Exporter Full (ID 1860)
- **Автоматическое добавление источников данных** в Grafana (Provisioning)
- **Единый интерфейс** для метрик и логов с корреляцией по времени
- **Полная автоматизация** — запуск одной командой `docker compose up -d`

## Архитектура

| Компонент     | Назначение                     | Порт |
|---------------|--------------------------------|------|
| Node Ecporter | Сбор системных метрик с хоста  | 9100 |
| Prometheus    | Хранение метрик                | 9090 |
| Loki          | Хранение логов                 | 3100 |
| Promtail      | Читает логи Docker-контейнеров | 9080 |
| Grafana       | Визуализация метрик и логов    | 3000 |

## Быстрый старт
1. Убедитесь, что установлен Docker и плагин Compose.
2. Клонируйте репозиторий:
   ```bash
   git clone https://github.com/dmitriyQQ/docker-monitoring-stack.git 
   cd docker-moitoring-stack
   ```
3. Запустите стек:
   ```bash
   docker compose up -d
   ```
4. Откройте:
- Grafana: http://localhost:3000 (логин admin, пароль задаётся в compose файле)
- Prometheus: http://localhost:9090
- Node-exporter: htpp://localhost:9100 
- Loki: http://localhost:3100
- Promtail http://localhost:9080

## Просмотр логов
1. Grafana -> Explore -> Источник данных Loki
2. Пример запроса:
   ```bash
   {container_name="pometheus"
   ```
Покажет логи контейнера Prometheus

## Метрики
Дашборд Node Exporter Full (Dashboard -> General) показывает:
- Загрузку CPU
- Использование памяти
- Дисковое пространство
- Сетевой трафик

## Настройки сервисов
Изменение конфигураций (./configs):
- prometheus-config.yml - Добавление целей для мониторинга состояния
- loki-config.yml - Настройки хранения логов 
- promtail-config.yml - Нвчтройки источников логов
После изменения конфигураций перезапустите соответсвущие сервисы
   ```bash
   docker compose restart prometheus
   docker compose restart loki promtail
   ```
Пароль Grafana по умолчанию (в данном случае) passwd, что бы задать другой пароль при первом запуске, измените строку в docker-compose.yml:
   ```yaml
   environment:
     - GF_SECURITY_ADMIN_PASSWORD=new_pass
   ```
Или удалите переменную, тогда пароль будет admin
