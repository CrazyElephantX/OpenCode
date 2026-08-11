# Пример скилов и агентов для OpenCode

Предлагайте своих, делайте пулреквесты с улучшениями.

## Агенты

| Агент | Файл | Краткое описание |
|-------|------|------------------|
| Владелец продукта | [`agents/product-owner.md`](agents/product-owner.md) | Формирует продуктовое видение, приоритизирует backlog, пишет User Story и Acceptance Criteria, считает бизнес-ценность инициатив |
| Бизнес аналитик | [`agents/business-analyst.md`](agents/business-analyst.md) | Анализирует бизнес-процессы (AS-IS/TO-BE), собирает и документирует бизнес-требования (BRD), строит BPMN и Use Case |
| Системный аналитик | [`agents/system-analyst.md`](agents/system-analyst.md) | Переводит бизнес-требования в технические спецификации: backend-логика, ERD, Sequence, OpenAPI, AsyncAPI, NFR |
| Проверка ИБ | [`agents/security-reviewer.md`](agents/security-reviewer.md) | Проверяет требования и спецификации на соответствие ИБ-стандартам (ISO 27001, NIST, OWASP, 152-ФЗ) |

## Скилы

| Скил | Каталог | Краткое описание |
|------|---------|------------------|
| asyncapi-spec | [`skills/asyncapi-spec/`](skills/asyncapi-spec/SKILL.md) | Создание спецификации для Kafka Message Broker в формате AsyncAPI (YAML) |
| backend-logic | [`skills/backend-logic/`](skills/backend-logic/SKILL.md) | Создание спецификации описания логики работы Backend |
| backlog-prioritization | [`skills/backlog-prioritization/`](skills/backlog-prioritization/SKILL.md) | Приоритизация backlog по RICE, WSJF, MoSCoW и Value/Effort матрице |
| business-case | [`skills/business-case/`](skills/business-case/SKILL.md) | Составление бизнес-кейса инициативы с расчетом ROI, TCO и рисков |
| business-process-bpmn | [`skills/business-process-bpmn/`](skills/business-process-bpmn/SKILL.md) | Моделирование бизнес-процессов AS-IS/TO-BE в BPMN 2.0 |
| erd-model | [`skills/erd-model/`](skills/erd-model/SKILL.md) | Создание ER диаграмм (PlantUML) с готовым SQL скриптом для базы данных |
| nfr-requirements | [`skills/nfr-requirements/`](skills/nfr-requirements/SKILL.md) | Создание нефункциональных требований (производительность, надежность, безопасность, масштабируемость) |
| openapi-spec | [`skills/openapi-spec/`](skills/openapi-spec/SKILL.md) | Написание спецификации в формате OpenAPI (REST API) |
| product-roadmap | [`skills/product-roadmap/`](skills/product-roadmap/SKILL.md) | Построение продуктового роадмапа в формате Now/Next/Later или по релизам |
| security-review-checklist | [`skills/security-review-checklist/`](skills/security-review-checklist/SKILL.md) | Инструкция по проверке требований для специалиста по кибербезопасности |
| sequence-diagram | [`skills/sequence-diagram/`](skills/sequence-diagram/SKILL.md) | Создание Sequence диаграмм (PlantUML) |
| stakeholder-map | [`skills/stakeholder-map/`](skills/stakeholder-map/SKILL.md) | Построение карты стейкхолдеров и матрицы RACI |
| user-story | [`skills/user-story/`](skills/user-story/SKILL.md) | Написание User Story по INVEST с критериями приемки в формате Gherkin |


## Как настрокить
- [ТЕКСТ.OpenCode для системного аналитика. Пишем требования и ревьюим спецификации с AI-агентом](https://bv-dev.ru/opencode-dlya-sistemnogo-analitika/)

### Видео с первоначальной настройкой
- [YouTube](https://youtu.be/trrhfhvMcIU)
- [RuTube](https://rutube.ru/video/private/b361fecc8027c87244e041c036bcaf07/?p=z0DuraOOOtphYB3zYcqfQg)
- [VkVideo](https://vkvideo.ru/video-79866382_456239069)
- [boosty](https://boosty.to/crazyelephant/posts/ee9e24d0-99ad-4849-9d89-8c40cdb61a58)

## Основные команды
- `curl -fsSL https://opencode.ai/install | bash` — установка
- `opencode auth login` — авторизация у провайдера модели
- `opencode` — запуск TUI в папке проекта
- `opencode run "запрос" --agent plan --format json` — одноразовый запрос без интерфейса
- `opencode agent create` — интерактивное создание агента
- `opencode run --agent system-analyst "запрос"` — запуск агента из CLI
- `opencode github install` — подключение автопроверок на каждый Pull Request

# Дополнительные материалы
- подробнее о скилах: https://opencode.dev/docs/skills/
- подробнее об агентах: https://opencode.dev/docs/agents/

# Поддержать меня
- [boosty](boosty: https://boosty.to/crazyelephant)