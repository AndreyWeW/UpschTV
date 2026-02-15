# Архитектура системы

## 1. Архитектурный стиль
Рекомендуемая модель: модульная микросервисная архитектура с единым API Gateway.

## 2. Компоненты

### Клиенты
- Dispatcher Web (React/Next.js)
- Officer Web/Mobile (адаптивный frontend)
- Admin Console
- Management Analytics Views
- TV Panel (readonly)
- Telegram Bot

### Backend
- API Gateway (REST + auth middleware)
- Auth Service (JWT, refresh, RBAC)
- Dispatch Service
- Personnel Service
- Guard Shift Service
- Vehicles Service
- Fuel Service
- Equipment Service
- Document Service
- Analytics Service
- Notification Service (WebSocket + Telegram)
- Audit Logging Service

### Данные
- PostgreSQL (основная транзакционная БД)
- Объектное хранилище (сканы, вложения, фото)
- Redis (кэш, очереди, pub/sub)

## 3. Взаимодействие

1. Клиент вызывает API Gateway.
2. Gateway валидирует JWT и контекст прав.
3. Запрос маршрутизируется в доменный сервис.
4. Сервис пишет данные в PostgreSQL и отправляет событие в шину (Redis pub/sub или broker).
5. Notification Service транслирует обновления в WebSocket и/или Telegram.
6. Analytics Service агрегирует оперативные и исторические метрики.

## 4. Базовые API (v1)

- `GET /dispatches`
- `POST /dispatches`
- `PUT /dispatches/:id`
- `GET /statistics`
- `GET /vehicles`
- `POST /fuel`
- `GET /dashboard`

## 5. WebSocket каналы

- `active_dispatches`
- `fuel_status`
- `daily_summary`

## 6. Безопасность

- JWT access + refresh;
- RBAC (dispatcher/chief/admin/management/viewer);
- Audit trail для критичных операций;
- TLS termination на Nginx;
- Ротация секретов;
- Ограничение частоты запросов (rate limiting).

## 7. Нефункциональные ориентиры

- API p95 < 300 ms;
- Real-time push < 1 sec;
- До 100 concurrent пользователей;
- Непрерывные backup + проверка восстановления.

## 8. Масштабирование

- Горизонтальное масштабирование stateless сервисов;
- Read replicas для аналитических чтений;
- Отделение OLTP от тяжёлых отчётов;
- Очереди для задач экспорта PDF/Excel.

## 9. Observability

- Централизованные логи;
- Метрики (latency, errors, throughput);
- Трассировка (request correlation id);
- Алерты по SLA и инцидентам.
