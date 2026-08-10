---
name: asyncapi-spec
description: Создание спецификации требований для Kafka Message Broker в формате AsyncAPI .
---
### 4.7. Спецификация для Kafka Message Broker в формате AsyncAPI 

**Инструкции по описанию брокера сообщений Kafka**

**Язык выполнения:** Русский язык
**Формат результата:** AsyncAPI спецификация в YAML формате
**Место сохранения:** Папка проекта с именем `{feature-name}_asyncapi.yaml`
**Стандарт:** AsyncAPI 2.6.0 или выше

#### 4.7.1. Содержание
1. [Формат выходного файла](#формат-выходного-файла)
2. [Шаблон описания Kafka архитектуры](#шаблон-описания-kafka-архитектуры)
3. [Метрики качества](#метрики-качества)
4. [Валидационные правила](#валидационные-правила)
5. [Методология проектирования](#методология-проектирования)
6. [Примеры описания Kafka](#примеры-описания-kafka)
7. [Критерии качества](#критерии-качества)
8. [Чек-лист для ИИ агента](#чек-лист-для-ии-агента)

---

#### 4.7.2. Формат выходного файла

##### 4.7.2.1. Обязательная структура AsyncAPI YAML файла:

```yaml
# {feature-name}_asyncapi.yaml
asyncapi: '2.6.0'
info:
  title: '{Feature Name} Kafka Events API'
  version: '1.0.0'
  description: |
    Описание асинхронных событий для {feature-name} через Apache Kafka
    
    ## Назначение
    {Описание назначения системы событий}
    
    ## Архитектурная роль
    {Роль в общей архитектуре системы}
    
  contact:
    name: 'Development Team'
    email: 'dev-team@company.com'
  license:
    name: 'MIT'

servers:
  kafka-cluster:
    url: '{kafka-broker-urls}'
    protocol: kafka
    description: 'Production Kafka cluster'
    bindings:
      kafka:
        schemaRegistryUrl: 'http://schema-registry:8081'
        schemaRegistryVendor: 'confluent'
    security:
      - saslScram: []

defaultContentType: application/json

channels:
  'domain.entity.events':
    description: 'События жизненного цикла {entity}'
    bindings:
      kafka:
        topic: 'domain.entity.events'
        partitions: 12
        replicas: 3
        configs:
          retention.ms: 2592000000  # 30 дней
          cleanup.policy: 'delete'
          compression.type: 'snappy'
    publish:
      summary: 'Отправка событий {entity}'
      operationId: 'publishEntityEvent'
      bindings:
        kafka:
          groupId: 'entity-producers'
          clientId: 'entity-service'
          acks: 'all'
          key:
            type: string
            description: 'ID сущности для партиционирования'
      message:
        $ref: '#/components/messages/EntityEvent'
    subscribe:
      summary: 'Получение событий {entity}'
      operationId: 'subscribeEntityEvent'
      bindings:
        kafka:
          groupId: 'entity-consumers'
          clientId: 'consumer-service'
      message:
        $ref: '#/components/messages/EntityEvent'

components:
  messages:
    EntityEvent:
      name: 'EntityEvent'
      title: 'Событие сущности'
      summary: 'Событие изменения состояния сущности'
      contentType: application/json
      headers:
        type: object
        properties:
          eventType:
            type: string
            enum: ['CREATED', 'UPDATED', 'DELETED']
          source:
            type: string
            description: 'Источник события'
          timestamp:
            type: string
            format: date-time
      payload:
        $ref: '#/components/schemas/EntityEventPayload'
      examples:
        - name: 'entityCreated'
          summary: 'Создание сущности'
          headers:
            eventType: 'CREATED'
            source: 'entity-service'
            timestamp: '2024-01-15T10:30:00Z'
          payload:
            entityId: 'uuid-here'
            status: 'ACTIVE'
            createdAt: '2024-01-15T10:30:00Z'

  schemas:
    EntityEventPayload:
      type: object
      required:
        - entityId
        - status
        - createdAt
      properties:
        entityId:
          type: string
          format: uuid
          description: 'Уникальный идентификатор сущности'
        status:
          type: string
          enum: ['ACTIVE', 'INACTIVE', 'PENDING']
          description: 'Статус сущности'
        createdAt:
          type: string
          format: date-time
          description: 'Время создания события'
        metadata:
          type: object
          description: 'Дополнительные данные'
          additionalProperties: true
      example:
        entityId: 'f47ac10b-58cc-4372-a567-0e02b2c3d479'
        status: 'ACTIVE'
        createdAt: '2024-01-15T10:30:00Z'
        metadata:
          source: 'web-app'
          userId: 'user-123'

  securitySchemes:
    saslScram:
      type: scramSha512
      description: 'SASL/SCRAM authentication'

  parameters:
    EntityId:
      description: 'Идентификатор сущности'
      schema:
        type: string
        format: uuid

# Дополнительная конфигурация Kafka (в секции x-kafka-config)
x-kafka-config:
  cluster:
    brokers: 3
    replication:
      default: 2
      critical_topics: 3
    resources:
      broker_memory: '4Gi'
      broker_cpu: '2'
      broker_storage: '100Gi'
  
  producers:
    default_config:
      acks: 'all'
      retries: 10
      batch.size: 100000
      linger.ms: 5
      enable.idempotence: true
      compression.type: 'snappy'
    
  consumers:
    default_config:
      auto.commit.enable: false
      max.poll.records: 500
      session.timeout.ms: 30000
      fetch.min.bytes: 1
      
  monitoring:
    metrics:
      - 'kafka.server:type=BrokerTopicMetrics,name=MessagesInPerSec'
      - 'kafka.consumer:type=consumer-fetch-manager-metrics'
      - 'kafka.producer:type=producer-metrics'
    alerts:
      - name: 'high_consumer_lag'
        condition: 'consumer_lag > 10000'
        severity: 'critical'
      - name: 'broker_down'
        condition: 'broker_availability < 100%'
        severity: 'critical'
        
  security:
    authentication:
      protocol: 'SASL_SSL'
      mechanism: 'SCRAM-SHA-512'
    acls:
      - principal: 'User:entity-service'
        operations: ['Write', 'Describe']
        resources: ['Topic:domain.entity.events']
      - principal: 'User:consumer-service'
        operations: ['Read', 'Describe']
        resources: ['Topic:domain.entity.events', 'Group:entity-consumers']
```

##### 4.7.2.2. Правила именования файлов:
- `{feature-name}_asyncapi.yaml` - для основных фич
- `{domain}_events_asyncapi.yaml` - для доменных решений
- `{system-name}_kafka_asyncapi.yaml` - для системных интеграций

**Примеры:**
- `banking_transfer_asyncapi.yaml`
- `ecommerce_orders_asyncapi.yaml`
- `notification_events_asyncapi.yaml`

##### 4.7.2.3. Обязательные секции AsyncAPI:
1. **asyncapi**: версия спецификации (2.6.0+)
2. **info**: метаданные API
3. **servers**: конфигурация Kafka кластера
4. **channels**: топики и их конфигурация
5. **components**: схемы сообщений, security schemes
6. **x-kafka-config**: расширенная конфигурация Kafka (опционально)

---

#### 4.7.3. Шаблон описания Kafka архитектуры

##### 4.7.3.1. Обязательная структура (9 основных блоков):

| № | Блок | Описание | Обязательность |
|---|------|----------|----------------|
| 1 | **Общий обзор** | Назначение Kafka в системе, роль в архитектуре | ✅ Обязательно |
| 2 | **Топики и схемы** | Структура топиков, схемы сообщений, партиционирование | ✅ Обязательно |
| 3 | **Продьюсеры** | Сервисы-отправители, стратегии отправки | ✅ Обязательно |
| 4 | **Консьюмеры** | Сервисы-получатели, группы консьюмеров | ✅ Обязательно |
| 5 | **Конфигурация кластера** | Настройки брокеров, репликация, отказоустойчивость | ✅ Обязательно |
| 6 | **Схемы данных** | Avro/JSON схемы, Schema Registry, версионирование | ✅ Обязательно |
| 7 | **Безопасность** | Аутентификация, авторизация, шифрование | 🔶 Рекомендуется |
| 8 | **Мониторинг и алерты** | Метрики, логирование, SLA | 🔶 Рекомендуется |
| 9 | **Производительность** | Throughput, latency, оптимизации | 🔶 Рекомендуется |

---

#### 4.7.4. Метрики качества

##### 4.7.4.1. Целевые показатели:
- **Полнота структуры**: 6/6 обязательных блоков = 100%
- **Покрытие топиков**: Описание всех основных топиков системы
- **Схемы данных**: 100% топиков имеют описание схем
- **Группы консьюмеров**: Четкое разделение ответственности
- **Отказоустойчивость**: Минимум 2x репликация критичных топиков

##### 4.7.4.2. Система оценки:
- **Production-ready**: 95-100% соответствие + безопасность + мониторинг
- **Отличное качество**: 85-94% соответствие метрикам
- **Хорошее качество**: 70-84% соответствие метрикам  
- **Требует доработки**: <70% соответствие метрикам

---

#### 4.7.5. Валидационные правила

##### 4.7.5.1. Автоматические проверки:

###### 4.7.5.1.1. Структурная валидация
```
✓ Все 6 обязательных блоков присутствуют
✓ Каждый топик имеет описание схемы
✓ Продьюсеры и консьюмеры четко идентифицированы
✓ Указана стратегия партиционирования
```

###### 4.7.5.1.2. Архитектурная валидация
```
✓ Топики логически связаны с доменами системы
✓ Схемы данных соответствуют API спецификациям
✓ Группы консьюмеров не пересекаются по ответственности
✓ Репликация настроена для критичных топиков
```

###### 4.7.5.1.3. Производственная валидация
```
✓ Указаны retention policies для всех топиков
✓ Описана стратегия обработки ошибок
✓ Настроен мониторинг и алертинг
✓ Документированы процедуры disaster recovery
```

---

#### 4.7.6. Методология проектирования

##### 4.7.6.1. Шаг 1: Анализ доменных событий
**Источники для анализа:**
- User Stories и Use Cases
- Sequence диаграммы
- Архитектурная диаграмма системы
- API спецификации (для синхронных операций)

##### 4.7.6.2. Шаг 2: Выделение событий
**Типы событий:**
- **Domain Events**: изменения состояния бизнес-сущностей
- **Integration Events**: межсервисное взаимодействие
- **System Events**: технические события (логи, метрики)
- **Command Events**: асинхронные команды

##### 4.7.6.3. Шаг 3: Проектирование топиков
**Принципы именования:**
```
{domain}.{entity}.{event-type}
Примеры:
- banking.transfer.created
- banking.transfer.completed
- ecommerce.order.placed
- notification.email.sent
```

##### 4.7.6.4. Шаг 4: Определение схем
**Форматы схем:**
- **Avro**: строгая типизация, эволюция схем
- **JSON Schema**: гибкость, простота
- **Protobuf**: производительность, совместимость

##### 4.7.6.5. Шаг 5: Планирование партиций
**Стратегии партиционирования:**
- По ID пользователя (user-based)
- По ID сущности (entity-based)
- По временным меткам (time-based)
- Round-robin (равномерное распределение)

##### 4.7.6.6. Шаг 6: Настройка консьюмеров
**Паттерны потребления:**
- **Single Consumer**: обработка в порядке
- **Consumer Group**: параллельная обработка
- **Multiple Groups**: различная бизнес-логика

---

#### 4.7.7. Примеры описания Kafka

##### 4.7.7.1. Пример 1: Банковская система переводов

###### 4.7.7.1.1. Общий обзор
**Назначение:** Асинхронная обработка банковских переводов с гарантиями доставки и аудитом операций.
**Роль в архитектуре:** Центральная шина событий между микросервисами Banking, Notification, Audit, Fraud Detection.

###### 4.7.7.1.2. Топики и схемы

**2.1. Топик: `banking.transfer.events`**
```yaml
Назначение: События жизненного цикла переводов
Партиции: 12 (по account_id % 12)
Replication Factor: 3
Retention: 30 дней
Cleanup Policy: delete
```

**Схема сообщения (Avro):**
```json
{
  "type": "record",
  "name": "TransferEvent",
  "namespace": "com.bank.events",
  "fields": [
    {"name": "transferId", "type": "string"},
    {"name": "fromAccountId", "type": "string"},
    {"name": "toAccountId", "type": "string"},
    {"name": "amount", "type": {"type": "fixed", "name": "Decimal", "size": 16}},
    {"name": "currency", "type": "string"},
    {"name": "status", "type": {"type": "enum", "symbols": ["PENDING", "PROCESSING", "COMPLETED", "FAILED"]}},
    {"name": "timestamp", "type": {"type": "long", "logicalType": "timestamp-millis"}},
    {"name": "userId", "type": "string"},
    {"name": "comment", "type": ["null", "string"], "default": null}
  ]
}
```

**2.2. Топик: `banking.notifications.requests`**
```yaml
Назначение: Запросы на отправку уведомлений
Партиции: 6 (по user_id % 6)
Replication Factor: 2
Retention: 7 дней
```

**2.3. Топик: `banking.audit.log`**
```yaml
Назначение: Аудит всех операций для compliance
Партиции: 1 (строгий порядок)
Replication Factor: 3
Retention: 7 лет (compliance требования)
Cleanup Policy: compact
```

###### 4.7.7.1.3. Продьюсеры

**3.1. Transfer Service (Главный продьюсер)**
```yaml
Сервис: transfer-service
Топики: banking.transfer.events
Стратегия: 
  - Идемпотентность: включена
  - Acks: all (гарантия записи на все реплики)
  - Retries: 10
  - Batch Size: 100KB
  - Linger: 5ms
Обработка ошибок:
  - Retry с exponential backoff
  - Dead Letter Queue: banking.transfer.dlq
```

**Пример кода:**
```java
@Service
public class TransferEventProducer {
    
    @Value("${kafka.topic.transfer-events}")
    private String transferEventsTopic;
    
    public void publishTransferEvent(TransferEvent event) {
        kafkaTemplate.send(transferEventsTopic, event.getFromAccountId(), event)
            .addCallback(
                result -> log.info("Event sent: {}", event.getTransferId()),
                failure -> log.error("Failed to send event", failure)
            );
    }
}
```

**3.2. Notification Service**
```yaml
Сервис: notification-service  
Топики: banking.notifications.requests
Стратегия: Fire-and-forget (acks=1)
```

###### 4.7.7.1.4. Консьюмеры

**4.1. Fraud Detection Service**
```yaml
Группа: fraud-detection-group
Топики: banking.transfer.events
Стратегия:
  - Auto Commit: false (ручное подтверждение)
  - Max Poll Records: 50
  - Session Timeout: 30s
  - Partition Assignment: cooperative-sticky
Логика:
  - Анализ на мошенничество
  - Публикация результата в fraud.detection.results
```

**4.2. Audit Service**
```yaml
Группа: audit-group
Топики: 
  - banking.transfer.events
  - banking.notifications.requests
Стратегия:
  - Earliest offset (обработка всех событий)
  - Batch processing (100 записей за раз)
  - Idempotent processing
```

**4.3. Notification Consumer**
```yaml
Группа: notification-consumers
Топики: banking.notifications.requests
Параллелизм: 3 instance
Retry Policy:
  - Max retries: 5
  - Backoff: exponential (1s, 2s, 4s, 8s, 16s)
  - DLQ: banking.notifications.dlq
```

###### 4.7.7.1.5. Конфигурация кластера

**5.1. Брокеры**
```yaml
Количество брокеров: 3
Размещение: 3 различные AZ
Конфигурация:
  - log.retention.hours: 168 (7 дней по умолчанию)
  - log.segment.bytes: 1GB
  - num.network.threads: 8
  - num.io.threads: 8
  - socket.send.buffer.bytes: 102400
  - socket.receive.buffer.bytes: 102400
```

**5.2. Zookeeper**
```yaml
Узлы: 3 (кворум)
Конфигурация:
  - tickTime: 2000
  - initLimit: 10  
  - syncLimit: 5
  - maxClientCnxns: 60
```

**5.3. Репликация**
```yaml
Критичные топики (transfers, audit): RF=3, min.insync.replicas=2
Обычные топики (notifications): RF=2, min.insync.replicas=1
Тестовые топики: RF=1
```

###### 4.7.7.1.6. Схемы данных

**6.1. Schema Registry**
```yaml
URL: http://schema-registry:8081
Compatibility: BACKWARD
Версионирование: автоматическое
Subjects:
  - banking.transfer.events-value (v1, v2)
  - banking.notifications.requests-value (v1)
  - banking.audit.log-value (v1)
```

**6.2. Эволюция схем**
```json
// v1 -> v2: добавление поля metadata
{
  "type": "record",
  "name": "TransferEvent",
  "fields": [
    // ... существующие поля ...
    {"name": "metadata", "type": ["null", "string"], "default": null}
  ]
}
```

###### 4.7.7.1.7. Безопасность

**7.1. Аутентификация**
```yaml
Протокол: SASL_SSL
Механизм: SCRAM-SHA-512
Пользователи:
  - transfer-service: RW доступ к banking.transfer.*
  - notification-service: RW доступ к banking.notifications.*
  - audit-service: R доступ ко всем топикам
  - fraud-detection: R доступ к banking.transfer.events
```

**7.2. Авторизация (ACL)**
```bash
# Transfer Service
kafka-acls --add --allow-principal User:transfer-service \
  --operation Write --topic banking.transfer.events

# Fraud Detection
kafka-acls --add --allow-principal User:fraud-detection \
  --operation Read --topic banking.transfer.events \
  --group fraud-detection-group
```

**7.3. Шифрование**
```yaml
In-transit: TLS 1.3
At-rest: LUKS disk encryption
Schema Registry: mTLS + basic auth
```

###### 4.7.7.1.8. Мониторинг и алерты

**8.1. Ключевые метрики**
```yaml
Broker метрики:
  - kafka.server:type=BrokerTopicMetrics,name=MessagesInPerSec
  - kafka.server:type=BrokerTopicMetrics,name=BytesInPerSec
  - kafka.server:type=ReplicaManager,name=LeaderCount

Consumer Lag:
  - kafka.consumer:type=consumer-fetch-manager-metrics,client-id=*

Producer метрики:
  - kafka.producer:type=producer-metrics,client-id=*
```

**8.2. Алерты**
```yaml
Критичные:
  - Consumer Lag > 10000 сообщений
  - Broker недоступен > 1 минуты
  - Disk usage > 85%

Предупреждения:
  - Producer errors > 1%
  - Replication lag > 5 секунд
  - Consumer group rebalance
```

**8.3. Дашборды**
```yaml
Grafana панели:
  - Kafka Cluster Overview
  - Topic Performance
  - Consumer Groups Status
  - Producer Performance
  - Error Rates
```

###### 4.7.7.1.9. Производительность

**9.1. Throughput характеристики**
```yaml
Целевые показатели:
  - Transfers: 10,000 msg/sec
  - Notifications: 5,000 msg/sec
  - Audit: 15,000 msg/sec

Latency (p99):
  - Producer: < 50ms
  - Consumer: < 100ms
  - End-to-end: < 200ms
```

**9.2. Оптимизации**
```yaml
Producer:
  - Batch size: 100KB
  - Linger: 5ms
  - Compression: snappy

Consumer:
  - Fetch size: 1MB
  - Max poll records: 500
  - Parallel processing

Broker:
  - Log segment: 1GB
  - Log flush: async
  - Page cache: 70% RAM
```

---

##### 4.7.7.2. Пример 2: E-commerce платформа

###### 4.7.7.2.1. Общий обзор
**Назначение:** Event-driven архитектура для e-commerce с обработкой заказов, инвентаря и уведомлений.
**Роль в архитектуре:** Основная шина событий между Order Service, Inventory Service, Payment Service, Notification Service.

###### 4.7.7.2.2. Топики и схемы

**2.1. Топик: `ecommerce.orders.events`**
```yaml
Назначение: События жизненного цикла заказов
Партиции: 8 (по order_id hash)
Replication Factor: 2
Retention: 14 дней
```

**Схема (JSON Schema):**
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "properties": {
    "orderId": {"type": "string", "format": "uuid"},
    "customerId": {"type": "string", "format": "uuid"},
    "status": {"enum": ["PLACED", "CONFIRMED", "SHIPPED", "DELIVERED", "CANCELLED"]},
    "items": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "productId": {"type": "string"},
          "quantity": {"type": "integer", "minimum": 1},
          "price": {"type": "number", "minimum": 0}
        }
      }
    },
    "totalAmount": {"type": "number", "minimum": 0},
    "timestamp": {"type": "string", "format": "date-time"}
  },
  "required": ["orderId", "customerId", "status", "items", "totalAmount", "timestamp"]
}
```

**2.2. Топик: `ecommerce.inventory.updates`**
```yaml
Назначение: Обновления остатков товаров
Партиции: 4 (по product_id hash)
Replication Factor: 2
Retention: 7 дней
Cleanup Policy: compact (latest state)
```

**2.3. Топик: `ecommerce.payments.events`**
```yaml
Назначение: События платежей
Партиции: 6
Replication Factor: 3 (критичные данные)
Retention: 365 дней (compliance)
```

###### 4.7.7.2.3. Продьюсеры

**3.1. Order Service**
```yaml
Топики: ecommerce.orders.events
Конфигурация:
  - acks: all
  - enable.idempotence: true
  - retries: Integer.MAX_VALUE
  - max.in.flight.requests.per.connection: 5

Outbox Pattern:
  - Транзакционная запись в БД + Kafka
  - Eventual consistency гарантии
```

**3.2. Inventory Service**
```yaml
Топики: ecommerce.inventory.updates
Стратегия: Компактированный топик для актуального состояния
```

###### 4.7.7.2.4. Консьюмеры

**4.1. Payment Service**
```yaml
Группа: payment-processors
Топики: ecommerce.orders.events
Фильтр: status = "PLACED"
Логика: Инициация платежа
Результат: Публикация в ecommerce.payments.events
```

**4.2. Inventory Service**  
```yaml
Группа: inventory-updaters
Топики: ecommerce.orders.events
Логика: Резервирование/освобождение товаров
Идемпотентность: По order_id + item_id
```

**4.3. Notification Service**
```yaml
Группа: notification-senders
Топики: 
  - ecommerce.orders.events
  - ecommerce.payments.events
Параллелизм: 5 consumers
Retry: 3 попытки с backoff
```

###### 4.7.7.2.5. Конфигурация кластера

**5.1. Развертывание**
```yaml
Окружение: Kubernetes
Brokers: 3 pods
Resources:
  - CPU: 2 cores
  - Memory: 4GB
  - Storage: 100GB SSD per broker
```

**5.2. Настройки производительности**
```yaml
log.retention.bytes: 10GB per partition
log.segment.bytes: 512MB
compression.type: snappy
num.replica.fetchers: 4
```

###### 4.7.7.2.6. Мониторинг

**6.1. Business метрики**
```yaml
- Orders processed per minute
- Payment success rate
- Inventory sync delay
- Customer notification delivery rate
```

**6.2. Technical метрики**
```yaml
- Consumer lag per topic
- Producer throughput
- Error rates by service
- Partition distribution
```

---

#### 4.7.8. Критерии качества для ИИ

##### 4.7.8.1. Архитектурная зрелость
- **Обязательно**: Все 6 основных блоков заполнены
- **Продакшн**: Добавлены блоки безопасности, мониторинга, производительности
- **Enterprise**: Добавлены disaster recovery, compliance, governance

##### 4.7.8.2. Техническая детализация
- **Топики**: Ясная схема партиционирования и retention политики
- **Схемы**: Валидные Avro/JSON Schema с примерами
- **Конфигурация**: Realistic настройки для целевой нагрузки
- **Безопасность**: ACL, аутентификация, шифрование

##### 4.7.8.3. Операционная готовность
- **Мониторинг**: Ключевые метрики и алерты определены
- **Обработка ошибок**: DLQ, retry policies, circuit breakers
- **Производительность**: SLA, throughput, latency требования
- **Disaster Recovery**: Backup, restore, failover процедуры

##### 4.7.8.4. Интеграция с системой
- **Domain Events**: Соответствуют бизнес-логике из Use Cases
- **API Integration**: Дополняют REST API архитектуру
- **Data Flow**: Согласованы с Sequence диаграммами
- **Services**: Соответствуют компонентной архитектуре

---

#### 4.7.9. Чек-лист для ИИ агента

##### 4.7.9.1. Обязательная проверка:
- [ ] ✅ AsyncAPI YAML файл создан с правильным именем
- [ ] ✅ Версия AsyncAPI указана (2.6.0+)
- [ ] ✅ Секция info заполнена полностью
- [ ] ✅ Servers содержит конфигурацию Kafka
- [ ] ✅ Channels описывают все топики
- [ ] ✅ Каждый channel имеет publish/subscribe операции
- [ ] ✅ Components содержат схемы сообщений
- [ ] ✅ Определена стратегия партиционирования в bindings
- [ ] ✅ Настроена репликация в kafka bindings
- [ ] ✅ Описаны retention policies в configs
- [ ] ✅ Схемы данных валидны (JSON Schema)
- [ ] ✅ Указаны группы консьюмеров в bindings
- [ ] ✅ AsyncAPI YAML синтаксис корректен

##### 4.7.9.2. Качественная проверка:
- [ ] 🎯 Топики логически связаны с доменами
- [ ] 🎯 Схемы поддерживают эволюцию (backward compatibility)
- [ ] 🎯 Обработка ошибок через DLQ описана
- [ ] 🎯 Идемпотентность обработки обеспечена
- [ ] 🎯 Producer acknowledgements настроены корректно
- [ ] 🎯 Consumer offset management определен

##### 4.7.9.3. Production-ready проверка:
- [ ] 🚀 Безопасность: SASL/SSL, ACL настроены
- [ ] 🚀 Мониторинг: метрики и алерты определены
- [ ] 🚀 Производительность: SLA и оптимизации описаны
- [ ] 🚀 Backup и disaster recovery процедуры
- [ ] 🚀 Schema Registry настроен
- [ ] 🚀 Consumer lag мониторинг
- [ ] 🚀 Dead Letter Queue обработка
- [ ] 🚀 Capacity planning (партиции, brokers)

##### 4.7.9.4. Интеграционная проверка:
- [ ] 🔗 События соответствуют Use Cases
- [ ] 🔗 Схемы совместимы с API спецификациями
- [ ] 🔗 Сервисы-продьюсеры есть в архитектурной диаграмме
- [ ] 🔗 Consumer groups не конфликтуют по ответственности
- [ ] 🔗 Временные характеристики реалистичны
- [ ] 🔗 Объемы данных соответствуют масштабу системы

**Цель**: Создавать YAML файлы с описанием Kafka архитектуры, готовые для production развертывания с полным покрытием функциональных и нефункциональных требований.

##### 4.7.9.5. Финальная проверка AsyncAPI YAML:
- [ ] 📄 Файл сохранен с расширением .yaml
- [ ] 📄 Имя файла соответствует конвенции именования
- [ ] 📄 AsyncAPI структура соответствует спецификации
- [ ] 📄 Все строковые значения заключены в кавычки
- [ ] 📄 Отступы выполнены пробелами (не табами)
- [ ] 📄 JSON Schema корректно определены в components
- [ ] 📄 Kafka bindings настроены для channels
- [ ] 📄 Security schemes определены при необходимости
- [ ] 📄 Examples включены для каждого типа сообщения

---

#### 4.7.10. Дополнительные рекомендации

##### 4.7.10.1. Стиль документирования:
- **Структурированность**: Используйте YAML для конфигураций
- **Конкретность**: Указывайте точные числа партиций, retention, throughput
- **Примеры**: Включайте реальные схемы Avro/JSON Schema
- **Визуализация**: ASCII диаграммы для topology

##### 4.7.10.2. Производственные аспекты:
- **Именование**: Следуйте конвенциям {domain}.{entity}.{event}
- **Партиционирование**: Обоснуйте выбор ключа партиционирования
- **Retention**: Учитывайте compliance и storage costs
- **Версионирование**: Планируйте эволюцию схем заранее

##### 4.7.10.3. Интеграция с DevOps:
- **Infrastructure as Code**: Terraform/Helm конфигурации
- **CI/CD**: Schema validation в pipeline
- **Monitoring**: Prometheus/Grafana метрики
- **Alerting**: PagerDuty/Slack интеграции

##### 4.7.10.4. Disaster Recovery:
- **Backup**: MirrorMaker 2.0 для репликации
- **Recovery**: RTO/RPO требования
- **Testing**: Chaos engineering практики
- **Documentation**: Runbooks для операционной команды
