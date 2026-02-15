# UpschTV — цифровая операционная система подразделения

Репозиторий содержит стартовый набор проектной документации и базовый каркас монорепозитория для разработки системы управления подразделением: диспетчерская, караулы, техника, выезды, ГСМ, отчётность, аналитика, TV-panel и Telegram-интеграция.

## Что уже подготовлено

- Техническое задание в формате, близком к ГОСТ.
- Архитектурная спецификация (модули, потоки данных, NFR, безопасность).
- ER-диаграмма и UML use-case диаграмма (Mermaid).
- Предлагаемая структура монорепозитория.
- Пошаговый план миграции с Google-таблиц.
- Рабочий каркас директорий `apps/*`, `services/*`, `packages/*`, `infra/*`, `db/*`.
- Начальный `Prisma`-schema и черновик `OpenAPI` контракта.

## Документы

- `docs/technical-specification-gost.md`
- `docs/system-architecture.md`
- `docs/er-diagram.mmd`
- `docs/uml-use-cases.mmd`
- `docs/repository-structure.md`
- `docs/migration-plan.md`
- `docs/api/openapi.yaml`

## Текущая структура

```text
apps/
services/
packages/
infra/
db/prisma/schema.prisma
docs/
```

## Следующие шаги

1. Инициализировать реальные приложения (Next.js / NestJS) в `apps/*` и `services/*`.
2. Подключить PostgreSQL и применить первые миграции Prisma.
3. Реализовать Auth + RBAC и модуль `dispatch-service` как MVP.
4. Синхронизировать OpenAPI с DTO/контроллерами и добавить contract tests.
5. Настроить CI/CD и проверки качества (lint, test, typecheck, security scan).
