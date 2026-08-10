---
name: security-review-checklist
description: Инструкция по проверке требований для специалиста по кибербезопасности.
---
### 4.4. Инструкция по проверке требований для специалиста по кибербезопасности
- Пиши на русском языке
- Данный документ предназначен для проверки требований, сгенерированных ИИ-агентом, с фокусом на информационную безопасность, защиту данных, соответствие стандартам и нормативным требованиям.
- Ты должен проверять требования из рабочей директории
- Делай акцент на безопасность архитектуры, защиту персональных данных, соответствие стандартам ИБ и выявление потенциальных угроз
- Отчет после проверки требования должен появится в папке reports (если ее нету, создать!), формат названия файла - {навзание требования которые ты проверял}_security_review.md
- Используй актуальные знания о киберугрозах, стандартах безопасности (ISO 27001, NIST, OWASP) и нормативных требованиях

---

#### 4.4.1. Методология специалиста по кибербезопасности

Шесть столпов информационной безопасности:

##### 4.4.1.1. **Конфиденциальность (Confidentiality)**
Обеспечение доступа к информации только авторизованным лицам и системам.

##### 4.4.1.2. **Целостность (Integrity)**
Гарантия того, что данные не были изменены неавторизованным образом и остаются точными и полными.

##### 4.4.1.3. **Доступность (Availability)**
Обеспечение доступности информации и информационных систем для авторизованных пользователей при необходимости.

##### 4.4.1.4. **Аутентичность (Authenticity)**
Подтверждение подлинности пользователей, устройств и информации.

##### 4.4.1.5. **Неотрицаемость (Non-repudiation)**
Предотвращение отказа от совершенных действий или транзакций.

##### 4.4.1.6. **Подотчетность (Accountability)**
Возможность привязать действия и события к конкретным лицам или системам.

---

#### 4.4.2. Процесс проверки информационной безопасности

##### 4.4.2.1. Этап 1: Анализ угроз и рисков

**Цель**: Выявление потенциальных угроз информационной безопасности и оценка рисков

**1.1. Threat Modeling (Моделирование угроз)**
- [ ] **STRIDE анализ**: Spoofing, Tampering, Repudiation, Information Disclosure, DoS, Elevation of Privilege
- [ ] **PASTA (Process for Attack Simulation and Threat Analysis)**: структурированный подход к анализу угроз
- [ ] **DREAD оценка**: Damage, Reproducibility, Exploitability, Affected Users, Discoverability
- [ ] **Kill Chain анализ**: этапы атаки от разведки до достижения цели
- [ ] **MITRE ATT&CK Framework**: тактики, техники и процедуры атакующих

**1.2. Risk Assessment (Оценка рисков)**
- [ ] **Идентификация активов**: критически важные данные и системы
- [ ] **Анализ уязвимостей**: потенциальные слабые места в архитектуре
- [ ] **Оценка воздействия**: потенциальный ущерб от реализации угроз
- [ ] **Вероятность реализации**: likelihood различных сценариев атак
- [ ] **Приоритизация рисков**: матрица рисков по критичности

**1.3. Compliance Assessment (Оценка соответствия)**
- [ ] **GDPR/152-ФЗ**: защита персональных данных
- [ ] **PCI DSS**: стандарт безопасности индустрии платежных карт
- [ ] **ISO 27001/27002**: международные стандарты ИБ
- [ ] **NIST Cybersecurity Framework**: рамочный документ по кибербезопасности
- [ ] **Отраслевые требования**: специфические стандарты для домена

##### 4.4.2.2. Этап 2: Архитектура безопасности

**2.1. Security by Design**
- [ ] **Defense in Depth**: многоуровневая защита
- [ ] **Zero Trust Architecture**: "никому не доверяй, всех проверяй"
- [ ] **Principle of Least Privilege**: минимальные необходимые привилегии
- [ ] **Separation of Duties**: разделение критических функций
- [ ] **Fail Secure**: безопасное поведение при сбоях

**2.2. Identity and Access Management (IAM)**
- [ ] **Authentication**: многофакторная аутентификация (MFA)
- [ ] **Authorization**: ролевая модель доступа (RBAC/ABAC)
- [ ] **Account Management**: жизненный цикл учетных записей
- [ ] **Privileged Access Management (PAM)**: управление привилегированными доступами
- [ ] **Single Sign-On (SSO)**: централизованная аутентификация

**2.3. Network Security Architecture**
- [ ] **Network Segmentation**: микросегментация и изоляция
- [ ] **Firewalls**: правила и политики межсетевых экранов
- [ ] **VPN**: защищенные каналы связи
- [ ] **IDS/IPS**: системы обнаружения и предотвращения вторжений
- [ ] **DDoS Protection**: защита от атак типа "отказ в обслуживании"

##### 4.4.2.3. Этап 3: Защита данных

**3.1. Data Classification (Классификация данных)**
- [ ] **Публичные данные**: общедоступная информация
- [ ] **Внутренние данные**: корпоративная информация
- [ ] **Конфиденциальные данные**: чувствительная информация
- [ ] **Строго конфиденциальные**: критически важные данные
- [ ] **Персональные данные**: PII согласно GDPR/152-ФЗ

**3.2. Data Protection (Защита данных)**
- [ ] **Encryption at Rest**: шифрование данных в хранилищах
- [ ] **Encryption in Transit**: шифрование данных при передаче
- [ ] **Key Management**: управление криптографическими ключами
- [ ] **Data Masking**: маскирование чувствительных данных
- [ ] **Data Loss Prevention (DLP)**: предотвращение утечек данных

**3.3. Privacy by Design**
- [ ] **Data Minimization**: сбор минимально необходимых данных
- [ ] **Purpose Limitation**: использование данных только по назначению
- [ ] **Consent Management**: управление согласиями пользователей
- [ ] **Right to be Forgotten**: право на удаление данных
- [ ] **Privacy Impact Assessment (PIA)**: оценка влияния на приватность

##### 4.4.2.4. Этап 4: Application Security

**4.1. OWASP Top 10 Analysis**

- [ ] **A01: Broken Access Control**: нарушения контроля доступа
- [ ] **A02: Cryptographic Failures**: ошибки в криптографии
- [ ] **A03: Injection**: инъекционные атаки (SQL, NoSQL, LDAP)
- [ ] **A04: Insecure Design**: небезопасный дизайн
- [ ] **A05: Security Misconfiguration**: неправильная конфигурация безопасности
- [ ] **A06: Vulnerable Components**: уязвимые компоненты
- [ ] **A07: Identification and Authentication Failures**: сбои аутентификации
- [ ] **A08: Software and Data Integrity Failures**: нарушения целостности
- [ ] **A09: Security Logging and Monitoring Failures**: недостатки логирования
- [ ] **A10: Server-Side Request Forgery**: SSRF атаки

**4.2. Secure Development Lifecycle (SDL)**
- [ ] **Security Requirements**: требования безопасности на раннем этапе
- [ ] **Threat Modeling**: моделирование угроз в дизайне
- [ ] **Secure Coding**: безопасная разработка
- [ ] **Security Testing**: тестирование безопасности (SAST/DAST)
- [ ] **Security Code Review**: ревью кода с точки зрения безопасности

**4.3. API Security**
- [ ] **Authentication & Authorization**: OAuth 2.0, JWT, API Keys
- [ ] **Rate Limiting**: ограничение количества запросов
- [ ] **Input Validation**: валидация входных данных
- [ ] **Output Encoding**: кодирование выходных данных
- [ ] **API Gateway Security**: централизованная защита API

##### 4.4.2.5. Этап 5: Infrastructure Security

**5.1. Cloud Security**
- [ ] **Shared Responsibility Model**: разделение ответственности с провайдером
- [ ] **Cloud Security Posture Management (CSPM)**: мониторинг конфигурации
- [ ] **Container Security**: безопасность контейнеров и образов
- [ ] **Serverless Security**: безопасность функций и событий
- [ ] **Multi-Cloud Security**: единые политики безопасности

**5.2. DevSecOps Integration**
- [ ] **Security as Code**: автоматизация проверок безопасности
- [ ] **Infrastructure as Code Security**: безопасность IaC templates
- [ ] **CI/CD Pipeline Security**: защита конвейера разработки
- [ ] **Secrets Management**: управление секретами в автоматизации
- [ ] **Compliance as Code**: автоматизация проверок соответствия

**5.3. Endpoint Security**
- [ ] **Device Management**: управление устройствами (MDM/EMM)
- [ ] **Antimalware Protection**: защита от вредоносного ПО
- [ ] **Patch Management**: управление обновлениями безопасности
- [ ] **USB Control**: контроль съемных носителей
- [ ] **Remote Access Security**: безопасность удаленного доступа

##### 4.4.2.6. Этап 6: Monitoring and Incident Response

**6.1. Security Monitoring**
- [ ] **SIEM (Security Information and Event Management)**: корреляция событий
- [ ] **SOAR (Security Orchestration and Response)**: автоматизация реагирования
- [ ] **Threat Intelligence**: анализ индикаторов компрометации
- [ ] **User and Entity Behavior Analytics (UEBA)**: анализ поведения
- [ ] **Continuous Security Monitoring**: непрерывный мониторинг

**6.2. Incident Response Planning**
- [ ] **Incident Response Team**: состав и роли команды реагирования
- [ ] **Incident Classification**: классификация инцидентов по серьезности
- [ ] **Response Procedures**: процедуры реагирования на инциденты
- [ ] **Forensic Readiness**: готовность к расследованию
- [ ] **Business Continuity**: обеспечение непрерывности бизнеса

---

#### 4.4.3. Security Review артефактов

##### 4.4.3.1. User Stories Security Review

**Security-focused проверка:**
- [ ] **Sensitive Data Handling**: обработка чувствительных данных в пользовательских сценариях
- [ ] **Authentication Requirements**: требования аутентификации для ролей
- [ ] **Authorization Boundaries**: границы авторизации между ролями
- [ ] **Privacy Considerations**: вопросы приватности в пользовательских историях
- [ ] **Compliance Requirements**: требования соответствия в бизнес-процессах

##### 4.4.3.2. Use Cases Security Analysis

**Security проверка сценариев:**
- [ ] **Security Preconditions**: предварительные условия безопасности
- [ ] **Security Exception Flows**: обработка исключений безопасности
- [ ] **Data Validation**: валидация данных в сценариях
- [ ] **Audit Trail**: требования к аудиту действий
- [ ] **Error Handling**: безопасная обработка ошибок

##### 4.4.3.3. Component Security Architecture

**Архитектурная security проверка:**
- [ ] **Trust Boundaries**: границы доверия между компонентами
- [ ] **Security Zones**: зоны безопасности в архитектуре
- [ ] **Attack Surface**: анализ поверхности атаки
- [ ] **Secure Communication**: защищенные каналы связи
- [ ] **Security Components**: компоненты безопасности (WAF, Firewall, etc.)

##### 4.4.3.4. Sequence Diagrams Security Flow

**Security flow анализ:**
- [ ] **Authentication Flow**: потоки аутентификации в диаграммах
- [ ] **Authorization Checks**: проверки авторизации в каждом вызове
- [ ] **Sensitive Data Flow**: потоки чувствительных данных
- [ ] **Error Propagation**: распространение ошибок безопасности
- [ ] **Session Management**: управление сессиями в потоках

##### 4.4.3.5. Data Security in ERD

**Data security анализ:**
- [ ] **Sensitive Data Identification**: идентификация чувствительных данных
- [ ] **Encryption Requirements**: требования к шифрованию на уровне БД
- [ ] **Access Control**: контроль доступа к таблицам и полям
- [ ] **Data Retention**: политики хранения и удаления данных
- [ ] **Backup Security**: безопасность резервных копий

##### 4.4.3.6. API Security Review

**API security проверка:**
- [ ] **Authentication Schemes**: схемы аутентификации API
- [ ] **Authorization Scopes**: области авторизации для эндпоинтов
- [ ] **Input Validation**: валидация входных параметров
- [ ] **Rate Limiting**: ограничения скорости запросов
- [ ] **Error Responses**: безопасные ответы на ошибки

---

#### 4.4.4. Security Risk Matrix

##### 4.4.4.1. Критичность угроз
| Уровень | Описание | Воздействие | Требуемые меры |
|---------|----------|-------------|----------------|
| **Critical** | Критические уязвимости | Полная компрометация системы | Немедленное исправление |
| **High** | Высокие риски | Значительный ущерб | Исправление в течение 24-48 часов |
| **Medium** | Средние риски | Ограниченный ущерб | Исправление в течение недели |
| **Low** | Низкие риски | Минимальное воздействие | Исправление в плановом порядке |

##### 4.4.4.2. CVSS Scoring
Используется Common Vulnerability Scoring System для оценки уязвимостей:
- **Base Score**: базовые характеристики уязвимости
- **Temporal Score**: изменения во времени
- **Environmental Score**: влияние на конкретную среду

##### 4.4.4.3. Compliance Risk Assessment
| Стандарт | Требование | Статус соответствия | Риск несоответствия |
|----------|------------|-------------------|-------------------|
| GDPR Art. 25 | Privacy by Design | ❌ Не реализовано | High |
| ISO 27001 A.9.1 | Access Control Policy | ✅ Реализовано | Low |
| NIST CSF ID.AM | Asset Management | ⚠️ Частично | Medium |

---

#### 4.4.5. Security Controls Framework

##### 4.4.5.1. Preventive Controls (Превентивные меры)
- [ ] **Access Controls**: системы контроля доступа
- [ ] **Encryption**: криптографическая защита
- [ ] **Network Security**: защита сетевой инфраструктуры
- [ ] **Security Awareness**: обучение безопасности
- [ ] **Vulnerability Management**: управление уязвимостями

##### 4.4.5.2. Detective Controls (Детективные меры)
- [ ] **Security Monitoring**: мониторинг безопасности
- [ ] **Intrusion Detection**: обнаружение вторжений
- [ ] **Audit Logging**: аудит и логирование
- [ ] **Vulnerability Scanning**: сканирование уязвимостей
- [ ] **Behavioral Analysis**: анализ поведения

##### 4.4.5.3. Corrective Controls (Корректирующие меры)
- [ ] **Incident Response**: реагирование на инциденты
- [ ] **Disaster Recovery**: восстановление после катастроф
- [ ] **Patch Management**: управление исправлениями
- [ ] **Malware Remediation**: устранение вредоносного ПО
- [ ] **Security Updates**: обновления безопасности

---

#### 4.4.6. Privacy and Data Protection

##### 4.4.6.1. GDPR Compliance Checklist
- [ ] **Lawful Basis**: правовые основания обработки данных
- [ ] **Data Subject Rights**: права субъектов данных
- [ ] **Data Protection Impact Assessment (DPIA)**: оценка влияния на защиту данных
- [ ] **Privacy by Design and Default**: приватность по умолчанию
- [ ] **Data Breach Notification**: уведомление о нарушениях
- [ ] **Data Protection Officer (DPO)**: назначение DPO
- [ ] **International Data Transfers**: международные передачи данных

##### 4.4.6.2. 152-ФЗ "О персональных данных" (Россия)
- [ ] **Согласие на обработку**: получение согласий
- [ ] **Уведомление Роскомнадзора**: уведомление регулятора
- [ ] **Локализация данных**: требования к локализации
- [ ] **Технические меры защиты**: реализация технических мер
- [ ] **Организационные меры**: организационные меры защиты

##### 4.4.6.3. Data Classification Policy
```
┌─────────────────┬──────────────────┬─────────────────┬──────────────────┐
│ Классификация   │ Описание         │ Требования ИБ   │ Время хранения   │
├─────────────────┼──────────────────┼─────────────────┼──────────────────┤
│ Public          │ Публичные данные │ Целостность     │ Неограниченно    │
│ Internal        │ Внутренние       │ Доступность     │ 7 лет            │
│ Confidential    │ Конфиденциальные │ + Шифрование    │ 5 лет            │
│ Restricted      │ Строго секретные │ + Аудит         │ 3 года           │
│ Personal Data   │ Персональные     │ + Согласие      │ По закону        │
└─────────────────┴──────────────────┴─────────────────┴──────────────────┘
```

---

#### 4.4.7. Penetration Testing Requirements

##### 4.4.7.1. Security Testing Types
- [ ] **SAST (Static Application Security Testing)**: статический анализ кода
- [ ] **DAST (Dynamic Application Security Testing)**: динамическое тестирование
- [ ] **IAST (Interactive Application Security Testing)**: интерактивное тестирование
- [ ] **SCA (Software Composition Analysis)**: анализ компонентов ПО
- [ ] **Manual Penetration Testing**: ручное тестирование на проникновение

##### 4.4.7.2. Testing Scope
- [ ] **External Perimeter**: внешний периметр организации
- [ ] **Internal Network**: внутренняя сеть
- [ ] **Web Applications**: веб-приложения
- [ ] **Mobile Applications**: мобильные приложения
- [ ] **API Endpoints**: программные интерфейсы
- [ ] **Wireless Networks**: беспроводные сети
- [ ] **Social Engineering**: социальная инженерия

##### 4.4.7.3. Testing Methodology
- [ ] **OWASP Testing Guide**: методология тестирования OWASP
- [ ] **NIST SP 800-115**: руководство NIST по техническому тестированию
- [ ] **PTES (Penetration Testing Execution Standard)**: стандарт выполнения
- [ ] **OSSTMM (Open Source Security Testing Methodology Manual)**: открытая методология
- [ ] **ISSAF (Information Systems Security Assessment Framework)**: рамочный документ

---

#### 4.4.8. Incident Response and Forensics

##### 4.4.8.1. Incident Response Lifecycle
1. **Preparation**: подготовка к инцидентам
2. **Identification**: выявление инцидентов
3. **Containment**: сдерживание угрозы
4. **Eradication**: устранение угрозы
5. **Recovery**: восстановление систем
6. **Lessons Learned**: извлечение уроков

##### 4.4.8.2. Forensic Requirements
- [ ] **Evidence Preservation**: сохранение доказательств
- [ ] **Chain of Custody**: цепочка доказательств
- [ ] **Timeline Analysis**: анализ временной линии
- [ ] **Memory Forensics**: анализ оперативной памяти
- [ ] **Network Forensics**: сетевая криминалистика
- [ ] **Digital Evidence**: цифровые доказательства

##### 4.4.8.3. Business Continuity & Disaster Recovery
- [ ] **Recovery Time Objective (RTO)**: цель времени восстановления
- [ ] **Recovery Point Objective (RPO)**: цель точки восстановления
- [ ] **Business Impact Analysis (BIA)**: анализ влияния на бизнес
- [ ] **Backup Strategy**: стратегия резервного копирования
- [ ] **Alternative Sites**: альтернативные площадки

---

#### 4.4.9. Security Metrics and KPIs

##### 4.4.9.1. Security Performance Indicators
- [ ] **Mean Time to Detection (MTTD)**: среднее время обнаружения
- [ ] **Mean Time to Response (MTTR)**: среднее время реагирования
- [ ] **Security Incident Volume**: количество инцидентов безопасности
- [ ] **Vulnerability Remediation Time**: время устранения уязвимостей
- [ ] **Security Training Completion**: завершение обучения безопасности

##### 4.4.9.2. Risk Metrics
- [ ] **Risk Score Trends**: тренды показателей риска
- [ ] **Control Effectiveness**: эффективность контролей
- [ ] **Compliance Score**: показатель соответствия
- [ ] **Security ROI**: возврат инвестиций в безопасность
- [ ] **Cost of Incidents**: стоимость инцидентов

---

#### 4.4.10. Emerging Security Threats

##### 4.4.10.1. Current Threat Landscape
- [ ] **AI/ML Security**: безопасность искусственного интеллекта
- [ ] **IoT Security**: безопасность интернета вещей
- [ ] **Supply Chain Attacks**: атаки на цепочки поставок
- [ ] **Quantum Computing Threats**: угрозы квантовых вычислений
- [ ] **Deepfakes**: технологии глубокой подделки

##### 4.4.10.2. Zero Trust Implementation
- [ ] **Identity Verification**: верификация личности
- [ ] **Device Verification**: верификация устройств
- [ ] **Network Microsegmentation**: микросегментация сети
- [ ] **Continuous Monitoring**: непрерывный мониторинг
- [ ] **Least Privilege Access**: минимальные привилегии

---

#### 4.4.11. Чек-лист безопасности

##### 4.4.11.1. Архитектура безопасности
- [ ] Defense in Depth реализована на всех уровнях
- [ ] Zero Trust принципы применены последовательно
- [ ] Границы доверия четко определены и защищены
- [ ] Принцип минимальных привилегий соблюден
- [ ] Разделение обязанностей реализовано

##### 4.4.11.2. Защита данных
- [ ] Классификация данных проведена полностью
- [ ] Шифрование применено для всех чувствительных данных
- [ ] Управление ключами реализовано безопасно
- [ ] DLP меры внедрены и функционируют
- [ ] Privacy by Design принципы соблюдены

##### 4.4.11.3. Application Security
- [ ] OWASP Top 10 уязвимости проанализированы
- [ ] Secure Development Lifecycle внедрен
- [ ] Security testing интегрировано в CI/CD
- [ ] Input validation реализована повсеместно
- [ ] Error handling не раскрывает системную информацию

##### 4.4.11.4. Infrastructure Security
- [ ] Network segmentation реализована корректно
- [ ] Endpoint protection развернута на всех устройствах
- [ ] Patch management процессы автоматизированы
- [ ] Cloud security posture оптимизирована
- [ ] Container security меры внедрены

##### 4.4.11.5. Compliance & Governance
- [ ] Применимые стандарты соответствия идентифицированы
- [ ] Privacy requirements выполняются полностью
- [ ] Audit trails настроены для всех критических действий
- [ ] Risk assessment проведена и документирована
- [ ] Security policies разработаны и внедрены

##### 4.4.11.6. Monitoring & Response
- [ ] SIEM/SOAR решения развернуты и настроены
- [ ] Incident response план разработан и протестирован
- [ ] Security metrics определены и отслеживаются
- [ ] Threat intelligence интегрирована в мониторинг
- [ ] Forensic readiness обеспечена

---

#### 4.4.12. Шаблон отчета специалиста по кибербезопасности

```markdown
## Security Review: [Название проекта]

### Исполнительное резюме
- **Общий уровень безопасности**: [Critical/High/Medium/Low Risk]
- **Критические уязвимости**: [Количество]
- **Соответствие стандартам**: [Процент соответствия]
- **Рекомендуемые действия**: [Приоритетные меры]

### Анализ угроз и рисков

#### 1. Threat Modeling Results: [Risk Score/10]
**Выявленные угрозы:**
- 🔴 **Critical**: [Список критических угроз]
- 🟡 **High**: [Список высоких угроз]
- 🟢 **Medium/Low**: [Остальные угрозы]

**STRIDE Analysis:**
| Категория | Выявленные угрозы | Вероятность | Воздействие | Риск |
|-----------|------------------|-------------|-------------|------|
| Spoofing | [Описание] | High | High | Critical |
| Tampering | [Описание] | Medium | High | High |

#### 2. Vulnerability Assessment: [Score/10]
**OWASP Top 10 Analysis:**
- ✅ **Covered**: [Защищенные категории]
- ❌ **Gaps**: [Пробелы в защите]
- ⚠️ **Partial**: [Частично реализованные меры]

#### 3. Compliance Status: [Score/10]
**Standards Compliance:**
| Стандарт | Требования | Соответствие | Пробелы |
|----------|------------|-------------|---------|
| GDPR | Art. 25, 32 | 85% | Privacy by Design |
| ISO 27001 | Controls | 90% | Incident Response |
| OWASP | Top 10 | 70% | Input Validation |

### Архитектура безопасности

#### 4. Security Architecture: [Score/10]
**Defense in Depth:**
- ✅ **Implemented**: [Реализованные уровни]
- ❌ **Missing**: [Отсутствующие защиты]
- 💡 **Recommendations**: [Улучшения архитектуры]

**Zero Trust Implementation:**
- [ ] Identity Verification: [Статус]
- [ ] Device Trust: [Статус]
- [ ] Network Segmentation: [Статус]
- [ ] Continuous Monitoring: [Статус]

#### 5. Data Protection: [Score/10]
**Data Security Measures:**
- ✅ **Encryption**: [Что защищено]
- ❌ **Gaps**: [Незащищенные данные]
- 🔐 **Key Management**: [Состояние]

**Privacy Compliance:**
- [ ] GDPR Article 25: [Status]
- [ ] Data Minimization: [Status]
- [ ] Consent Management: [Status]
- [ ] Right to be Forgotten: [Status]

#### 6. Application Security: [Score/10]
**Secure Development:**
- ✅ **SDL Integration**: [Что внедрено]
- ❌ **Security Gaps**: [Пробелы в разработке]
- 🔍 **Testing Coverage**: [Покрытие тестирования]

### Critical Security Issues

#### Immediate Actions Required (24-48 hours)
1. **[Critical Issue 1]**: [Описание и меры]
2. **[Critical Issue 2]**: [Описание и меры]

#### High Priority (1 week)
1. **[High Issue 1]**: [Описание и план]
2. **[High Issue 2]**: [Описание и план]

#### Medium Priority (1 month)
1. **[Medium Issue 1]**: [Описание и график]
2. **[Medium Issue 2]**: [Описание и график]

### Risk Matrix

| Risk ID | Threat | Likelihood | Impact | Risk Level | Mitigation |
|---------|--------|------------|--------|------------|------------|
| R001 | Data Breach | High | Critical | Critical | Implement DLP |
| R002 | API Abuse | Medium | High | High | Rate limiting |

### Security Controls Assessment

#### Preventive Controls: [Score/10]
- [ ] Access Controls: [Effectiveness]
- [ ] Encryption: [Coverage]
- [ ] Network Security: [Implementation]

#### Detective Controls: [Score/10]
- [ ] SIEM/Monitoring: [Capability]
- [ ] IDS/IPS: [Coverage]
- [ ] Audit Logging: [Completeness]

#### Corrective Controls: [Score/10]
- [ ] Incident Response: [Readiness]
- [ ] Disaster Recovery: [Testing]
- [ ] Patch Management: [Process]

### Recommendations Roadmap

#### Phase 1: Critical Security (0-3 months)
1. [Критические исправления безопасности]
2. [Обязательные compliance требования]
3. [Защита от известных угроз]

#### Phase 2: Enhanced Security (3-6 months)
1. [Усиление мониторинга]
2. [Автоматизация security процессов]
3. [Расширенная защита данных]

#### Phase 3: Advanced Security (6-12 months)
1. [Zero Trust реализация]
2. [AI/ML security внедрение]
3. [Proactive threat hunting]

### Compliance Action Plan

#### GDPR Compliance
- [ ] **Immediate**: [Критические требования]
- [ ] **Short-term**: [Планируемые меры]
- [ ] **Long-term**: [Стратегические изменения]

#### Industry Standards
- [ ] **ISO 27001**: [План сертификации]
- [ ] **SOC 2**: [Аудит готовность]
- [ ] **PCI DSS**: [Соответствие платежным стандартам]

### Conclusion

**Общая оценка безопасности**: [Уровень зрелости безопасности]

**Готовность к производству**: [Да/Нет с условиями/Нет]

**Ключевые блокеры**: [Критические проблемы безопасности]

**Рекомендуемые следующие шаги**: [Конкретные действия]

---
*Security Review выполнен: [Дата] | Классификация: [Конфиденциально] | Следующий обзор: [Дата]*
```

---

**Следуйте данной инструкции для комплексной проверки требований с точки зрения информационной безопасности, обеспечивая защиту от современных киберугроз и соответствие нормативным требованиям.**
