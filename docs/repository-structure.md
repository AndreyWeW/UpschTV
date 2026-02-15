# Рекомендуемая структура репозитория

```text
upsch-platform/
  apps/
    web-dispatcher/        # Next.js приложение для диспетчера и начальника караула
    web-tv-panel/          # Fullscreen readonly клиент
    api-gateway/           # NestJS gateway (BFF/edge)
    worker-reports/        # Генерация PDF/Excel, фоновые задачи
    telegram-bot/          # Интеграционный сервис Telegram
  services/
    auth-service/
    dispatch-service/
    personnel-service/
    guards-service/
    vehicles-service/
    fuel-service/
    equipment-service/
    document-service/
    analytics-service/
    notification-service/
  packages/
    config/                # shared конфиги (eslint, tsconfig, env schema)
    ui/                    # общий UI-kit
    types/                 # shared DTO/types
    sdk/                   # API client SDK
    utils/                 # переиспользуемые утилиты
  infra/
    docker/
    k8s/
    nginx/
    terraform/
  db/
    prisma/
      schema.prisma
      migrations/
    seeds/
  docs/
  .github/
    workflows/
```

## Принципы
- Monorepo с чёткими границами доменов;
- Общие типы через `packages/types`;
- Контракты API фиксируются OpenAPI;
- Любые breaking changes проходят через версионирование API;
- Отдельные сервисы для тяжёлых задач и интеграций.
