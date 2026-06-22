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
