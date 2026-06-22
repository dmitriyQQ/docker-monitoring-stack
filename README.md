# Prometheus + Grafana + Node Exporter Monitoring Stack

Готовый к развёртыванию стек мониторинга на Docker Compose.  
Собирает метрики хоста, хранит их в Prometheus и визуализирует в Grafana с автоматически загружаемым дашбордом 1860.

## Состав
- **Prometheus** — сбор и хранение метрик
- **Node Exporter** — экспорт системных метрик
- **Grafana** — визуализация (с предустановленным Data Source и дашбордом)

## Быстрый старт
1. Убедитесь, что установлен Docker и плагин Compose.
2. Клонируйте репозиторий:
   ```bash
   git clone <url-твоего-репозитория>
   cd monitoring
   ```
3. Запустите стек:
   ```bash
   docker compose up -d
   ```
4. Откройте:
- Prometheus: http://localhost:9090
- Grafana: http://localhost:3000 (логин admin, пароль задаётся в compose файле)

## Настройка
- Конфигурация Prometheus лежит в prometheus.yml.
- Дашборд Node Exporter Full (ID 1860) загружается автоматически.
- Grafana provisioning описан в grafana/provisioning/.

## Остановка
   ```bash
   docker compose down
   ```
