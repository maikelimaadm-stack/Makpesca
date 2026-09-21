---
Status: REVIEW
Version: 0.2.0
Last Updated: 2026-09-21
Owners: Maike Lima (autoridade humana final)
Related ADRs: todos
Wave: cross-cutting (controle vivo; registrada em F0)
Lifecycle: LIVING
---

# Documentação MAKPESCA — Índice Oficial

Este arquivo é o **índice oficial** da documentação e o mapa de **SSOTs**
(Single Source of Truth). Se dois documentos discordarem, vale o SSOT indicado aqui.

Fase atual: **MP-DOC-00 v2 R1 — Fundação Documental, candidatura de F0**.
`IMPLEMENTATION-READY-GATE` = **BLOCKED**. `HUMAN APPROVAL` (F0) = **PENDING**.

**Product Owner / autoridade humana final: Maike Lima**
(SSOT: [PROJECT-CONSTITUTION](00-governance/PROJECT-CONSTITUTION.md) Art. 15).

**Offline core ≠ basemap offline.** O offline core é constitucional (Art. 4); a base
cartográfica offline é decisão separada e ainda aberta (Art. 4-A, ADR-0010).

## 1. Mapa de SSOTs

| Assunto | SSOT |
|---------|------|
| Regras inegociáveis do projeto | `00-governance/PROJECT-CONSTITUTION.md` |
| **Ownership e autoridade final** | `00-governance/PROJECT-CONSTITUTION.md` Art. 15 |
| **Composição das ondas (Core/Living)** | `00-governance/FREEZE-POLICY.md` §7 |
| **Contagens e resumos derivados** | `00-governance/DECISION-POLICY.md` §8 |
| Como se decide | `00-governance/DECISION-POLICY.md` |
| Como se congela | `00-governance/FREEZE-POLICY.md` |
| Estado de cada documento | `00-governance/DOCUMENT-STATUS.md` |
| Registro de decisões | `00-governance/DECISION-REGISTRY.md` |
| Vocabulário | `00-governance/GLOSSARY.md` |
| Riscos | `00-governance/RISK-REGISTER.md` |
| Dúvidas abertas | `00-governance/OPEN-QUESTIONS.md` |
| Premissas não verificadas | `00-governance/ASSUMPTIONS.md` |
| Visão de produto | `01-product/PRODUCT-VISION.md` |
| Escopo do MVP | `01-product/MVP-SCOPE.md` |
| O que o produto não é | `01-product/NON-GOALS.md` |
| Monetização | `01-product/MONETIZATION.md` |
| Arquitetura de containers | `02-architecture/CONTAINER-ARCHITECTURE.md` |
| Portabilidade / saída de provider | `02-architecture/PORTABILITY-STRATEGY.md` |
| Abstração de providers | `02-architecture/PROVIDER-ABSTRACTION.md` |
| Estrutura de repositório | `02-architecture/REPOSITORY-STRATEGY.md` |
| Domínios e contextos | `03-domain/BOUNDED-CONTEXTS.md` |
| Entidades | `03-domain/ENTITY-CATALOG.md` |
| Invariantes de domínio | `03-domain/DOMAIN-INVARIANTS.md` |
| Modelo conceitual de dados | `04-data/CONCEPTUAL-DATA-MODEL.md` |
| Modelo geoespacial | `04-data/GEO-DATA-MODEL.md` |
| Classificação de dados | `04-data/DATA-CLASSIFICATION.md` |
| Contrato offline | `05-offline-sync/OFFLINE-FIRST-CONTRACT.md` |
| Protocolo de sync | `05-offline-sync/SYNC-PROTOCOL.md` |
| Conflitos | `05-offline-sync/CONFLICT-RESOLUTION.md` |
| Sync de mídia | `05-offline-sync/MEDIA-SYNC.md` |
| Arquitetura de mapa | `06-maps-location/MAP-ARCHITECTURE.md` |
| Mapa online vs offline | `06-maps-location/ONLINE-OFFLINE-MAP-STRATEGY.md` |
| **Geo-privacy (regra de negócio)** | `06-maps-location/GEO-PRIVACY.md` |
| **Geo-privacy (ameaças)** | `08-security-privacy/GEO-PRIVACY-THREAT-MODEL.md` |
| Compartilhamento de localização | `06-maps-location/LOCATION-SHARING.md` |
| Princípios de API | `07-api/API-PRINCIPLES.md` |
| Erros de API | `07-api/API-ERROR-CONTRACT.md` |
| Idempotência | `07-api/API-IDEMPOTENCY.md` |
| Superfície de API | `07-api/API-ENDPOINT-MATRIX.md` |
| Baseline de segurança | `08-security-privacy/SECURITY-BASELINE.md` |
| Modelo de ameaças | `08-security-privacy/THREAT-MODEL.md` |
| LGPD | `08-security-privacy/PRIVACY-LGPD-CHECKLIST.md` |
| Modelo social | `09-social/SOCIAL-MODEL.md` |
| Comunidades | `09-social/COMMUNITY-MODEL.md` |
| Grupos | `09-social/GROUP-MODEL.md` |
| Mensagens | `09-social/MESSAGING-MODEL.md` |
| Eventos | `09-social/EVENTS-MODEL.md` |
| Moderação | `09-social/MODERATION.md` |
| Gamificação | `10-gamification/RANKINGS.md`, `ACHIEVEMENTS.md`, `CHALLENGES.md` |
| Lojas parceiras | `11-commerce/PARTNER-STORES.md` |
| Afiliados | `11-commerce/AFFILIATE-PROGRAM.md` |
| Atribuição | `11-commerce/ATTRIBUTION.md` |
| PRO / entitlements | `12-billing/ENTITLEMENTS.md` |
| Billing | `12-billing/BILLING-ARCHITECTURE.md` |
| Inteligência de pesca | `13-intelligence/FISHING-INTELLIGENCE.md` |
| Dados ambientais | `13-intelligence/ENVIRONMENTAL-DATA.md` |
| Observabilidade | `14-operations/OBSERVABILITY.md` |
| Ambientes | `14-operations/ENVIRONMENTS.md` |
| Estratégia de testes | `15-quality/TEST-STRATEGY.md` |
| Gates | `15-quality/QUALITY-GATES.md` |
| Ondas de freeze | `16-roadmap/DOCUMENTATION-FREEZE-WAVES.md` |
| Roadmap de slices | `16-roadmap/IMPLEMENTATION-SLICE-ROADMAP.md` |
| Decisões arquiteturais | `adr/` |

## 2. Índice completo

### 00 — Governança
- [PROJECT-CONSTITUTION.md](00-governance/PROJECT-CONSTITUTION.md)
- [DECISION-POLICY.md](00-governance/DECISION-POLICY.md)
- [FREEZE-POLICY.md](00-governance/FREEZE-POLICY.md)
- [DOCUMENT-STATUS.md](00-governance/DOCUMENT-STATUS.md)
- [DECISION-REGISTRY.md](00-governance/DECISION-REGISTRY.md)
- [GLOSSARY.md](00-governance/GLOSSARY.md)
- [RISK-REGISTER.md](00-governance/RISK-REGISTER.md)
- [OPEN-QUESTIONS.md](00-governance/OPEN-QUESTIONS.md)
- [ASSUMPTIONS.md](00-governance/ASSUMPTIONS.md)
- [F0-FREEZE-CANDIDATE-REPORT.md](00-governance/F0-FREEZE-CANDIDATE-REPORT.md)

### 01 — Produto
- [PRODUCT-VISION.md](01-product/PRODUCT-VISION.md)
- [PRODUCT-PRINCIPLES.md](01-product/PRODUCT-PRINCIPLES.md)
- [PERSONAS.md](01-product/PERSONAS.md)
- [CORE-JOURNEYS.md](01-product/CORE-JOURNEYS.md)
- [MVP-SCOPE.md](01-product/MVP-SCOPE.md)
- [POST-MVP-SCOPE.md](01-product/POST-MVP-SCOPE.md)
- [FUTURE-SCOPE.md](01-product/FUTURE-SCOPE.md)
- [NON-GOALS.md](01-product/NON-GOALS.md)
- [COMPETITOR-LANDSCAPE.md](01-product/COMPETITOR-LANDSCAPE.md)
- [MONETIZATION.md](01-product/MONETIZATION.md)
- [PRODUCT-METRICS.md](01-product/PRODUCT-METRICS.md)

### 02 — Arquitetura
- [SYSTEM-CONTEXT.md](02-architecture/SYSTEM-CONTEXT.md)
- [CONTAINER-ARCHITECTURE.md](02-architecture/CONTAINER-ARCHITECTURE.md)
- [COMPONENT-BOUNDARIES.md](02-architecture/COMPONENT-BOUNDARIES.md)
- [PORTABILITY-STRATEGY.md](02-architecture/PORTABILITY-STRATEGY.md)
- [PROVIDER-ABSTRACTION.md](02-architecture/PROVIDER-ABSTRACTION.md)
- [REPOSITORY-STRATEGY.md](02-architecture/REPOSITORY-STRATEGY.md)
- [ENVIRONMENT-STRATEGY.md](02-architecture/ENVIRONMENT-STRATEGY.md)
- [SCALABILITY-STRATEGY.md](02-architecture/SCALABILITY-STRATEGY.md)

### 03 — Domínio
- [DOMAIN-MAP.md](03-domain/DOMAIN-MAP.md)
- [BOUNDED-CONTEXTS.md](03-domain/BOUNDED-CONTEXTS.md)
- [ENTITY-CATALOG.md](03-domain/ENTITY-CATALOG.md)
- [DOMAIN-INVARIANTS.md](03-domain/DOMAIN-INVARIANTS.md)

### 04 — Dados
- [CONCEPTUAL-DATA-MODEL.md](04-data/CONCEPTUAL-DATA-MODEL.md)
- [GEO-DATA-MODEL.md](04-data/GEO-DATA-MODEL.md)
- [DATA-CLASSIFICATION.md](04-data/DATA-CLASSIFICATION.md)
- [DATA-LIFECYCLE.md](04-data/DATA-LIFECYCLE.md)
- [BACKUP-RESTORE.md](04-data/BACKUP-RESTORE.md)

### 05 — Offline e Sync
- [OFFLINE-FIRST-CONTRACT.md](05-offline-sync/OFFLINE-FIRST-CONTRACT.md)
- [LOCAL-DATABASE-STRATEGY.md](05-offline-sync/LOCAL-DATABASE-STRATEGY.md)
- [SYNC-PROTOCOL.md](05-offline-sync/SYNC-PROTOCOL.md)
- [CONFLICT-RESOLUTION.md](05-offline-sync/CONFLICT-RESOLUTION.md)
- [MEDIA-SYNC.md](05-offline-sync/MEDIA-SYNC.md)
- [SYNC-FAILURE-MODES.md](05-offline-sync/SYNC-FAILURE-MODES.md)

### 06 — Mapas e Localização
- [MAP-ARCHITECTURE.md](06-maps-location/MAP-ARCHITECTURE.md)
- [ONLINE-OFFLINE-MAP-STRATEGY.md](06-maps-location/ONLINE-OFFLINE-MAP-STRATEGY.md)
- [GPS-STRATEGY.md](06-maps-location/GPS-STRATEGY.md)
- [GEO-PRIVACY.md](06-maps-location/GEO-PRIVACY.md)
- [LOCATION-SHARING.md](06-maps-location/LOCATION-SHARING.md)
- [MAP-PROVIDER-MATRIX.md](06-maps-location/MAP-PROVIDER-MATRIX.md)

### 07 — API
- [API-PRINCIPLES.md](07-api/API-PRINCIPLES.md)
- [API-VERSIONING.md](07-api/API-VERSIONING.md)
- [API-ERROR-CONTRACT.md](07-api/API-ERROR-CONTRACT.md)
- [API-IDEMPOTENCY.md](07-api/API-IDEMPOTENCY.md)
- [API-ENDPOINT-MATRIX.md](07-api/API-ENDPOINT-MATRIX.md)
- [API-SECURITY.md](07-api/API-SECURITY.md)
- [API-PORTABILITY.md](07-api/API-PORTABILITY.md)

### 08 — Segurança e Privacidade
- [SECURITY-BASELINE.md](08-security-privacy/SECURITY-BASELINE.md)
- [THREAT-MODEL.md](08-security-privacy/THREAT-MODEL.md)
- [GEO-PRIVACY-THREAT-MODEL.md](08-security-privacy/GEO-PRIVACY-THREAT-MODEL.md)
- [AUTH-OPTIONS.md](08-security-privacy/AUTH-OPTIONS.md)
- [SECRETS-POLICY.md](08-security-privacy/SECRETS-POLICY.md)
- [PRIVACY-LGPD-CHECKLIST.md](08-security-privacy/PRIVACY-LGPD-CHECKLIST.md)
- [INCIDENT-RESPONSE.md](08-security-privacy/INCIDENT-RESPONSE.md)

### 09 — Social
- [SOCIAL-MODEL.md](09-social/SOCIAL-MODEL.md)
- [PROFILE-MODEL.md](09-social/PROFILE-MODEL.md)
- [FEED-MODEL.md](09-social/FEED-MODEL.md)
- [FOLLOW-FRIEND-MODEL.md](09-social/FOLLOW-FRIEND-MODEL.md)
- [COMMUNITY-MODEL.md](09-social/COMMUNITY-MODEL.md)
- [GROUP-MODEL.md](09-social/GROUP-MODEL.md)
- [MESSAGING-MODEL.md](09-social/MESSAGING-MODEL.md)
- [EVENTS-MODEL.md](09-social/EVENTS-MODEL.md)
- [MODERATION.md](09-social/MODERATION.md)
- [REPORT-BLOCK.md](09-social/REPORT-BLOCK.md)

### 10 — Gamificação
- [RANKINGS.md](10-gamification/RANKINGS.md)
- [ACHIEVEMENTS.md](10-gamification/ACHIEVEMENTS.md)
- [CHALLENGES.md](10-gamification/CHALLENGES.md)
- [ANTI-FRAUD.md](10-gamification/ANTI-FRAUD.md)

### 11 — Comércio
- [PARTNER-STORES.md](11-commerce/PARTNER-STORES.md)
- [PARTNER-PORTAL.md](11-commerce/PARTNER-PORTAL.md)
- [OFFERS.md](11-commerce/OFFERS.md)
- [AFFILIATE-PROGRAM.md](11-commerce/AFFILIATE-PROGRAM.md)
- [ATTRIBUTION.md](11-commerce/ATTRIBUTION.md)
- [COMMISSIONS-PAYOUTS.md](11-commerce/COMMISSIONS-PAYOUTS.md)
- [COMMERCE-FRAUD.md](11-commerce/COMMERCE-FRAUD.md)

### 12 — Billing
- [FREE-PRO-MODEL.md](12-billing/FREE-PRO-MODEL.md)
- [BILLING-ARCHITECTURE.md](12-billing/BILLING-ARCHITECTURE.md)
- [ENTITLEMENTS.md](12-billing/ENTITLEMENTS.md)

### 13 — Inteligência
- [FISHING-INTELLIGENCE.md](13-intelligence/FISHING-INTELLIGENCE.md)
- [PRIVACY-PRESERVING-AGGREGATION.md](13-intelligence/PRIVACY-PRESERVING-AGGREGATION.md)
- [ENVIRONMENTAL-DATA.md](13-intelligence/ENVIRONMENTAL-DATA.md)

### 14 — Operações
- [OBSERVABILITY.md](14-operations/OBSERVABILITY.md)
- [ASYNC-JOBS.md](14-operations/ASYNC-JOBS.md)
- [FEATURE-FLAGS.md](14-operations/FEATURE-FLAGS.md)
- [RUNBOOK-BASELINE.md](14-operations/RUNBOOK-BASELINE.md)
- [ENVIRONMENTS.md](14-operations/ENVIRONMENTS.md)

### 15 — Qualidade
- [TEST-STRATEGY.md](15-quality/TEST-STRATEGY.md)
- [OFFLINE-TEST-MATRIX.md](15-quality/OFFLINE-TEST-MATRIX.md)
- [PRIVACY-TEST-MATRIX.md](15-quality/PRIVACY-TEST-MATRIX.md)
- [COMMERCE-TEST-MATRIX.md](15-quality/COMMERCE-TEST-MATRIX.md)
- [QUALITY-GATES.md](15-quality/QUALITY-GATES.md)

### 16 — Roadmap
- [DOCUMENTATION-FREEZE-WAVES.md](16-roadmap/DOCUMENTATION-FREEZE-WAVES.md)
- [IMPLEMENTATION-SLICE-ROADMAP.md](16-roadmap/IMPLEMENTATION-SLICE-ROADMAP.md)
- [DEPENDENCY-MAP.md](16-roadmap/DEPENDENCY-MAP.md)

### ADRs
- [adr/README.md](adr/README.md) — índice e status de todas as decisões.

## 3. Onde estão os diagramas

Todos os diagramas são Mermaid, embutidos nos documentos:

| Diagrama | Documento |
|----------|-----------|
| System Context | `02-architecture/SYSTEM-CONTEXT.md` |
| Container Architecture | `02-architecture/CONTAINER-ARCHITECTURE.md` |
| Offline Sync | `05-offline-sync/SYNC-PROTOCOL.md` |
| Geo Privacy | `06-maps-location/GEO-PRIVACY.md` |
| Media Upload | `05-offline-sync/MEDIA-SYNC.md` |
| Auth (conceitual) | `08-security-privacy/AUTH-OPTIONS.md` |
| Billing (conceitual) | `12-billing/BILLING-ARCHITECTURE.md` |
| Social publication | `09-social/FEED-MODEL.md` |
| Community/group relationship | `09-social/COMMUNITY-MODEL.md` |
| Affiliate attribution | `11-commerce/ATTRIBUTION.md` |
| Partner offer flow | `11-commerce/OFFERS.md` |

## 4. Convenção de cabeçalho

Todo documento relevante começa com:

```
---
Status: DRAFT | REVIEW | FROZEN | SUPERSEDED
Version: x.y.z
Last Updated: AAAA-MM-DD
Owners: ...
Related ADRs: ...
---
```

Nesta fase, **todos** os documentos estão em `DRAFT`. Nada é `FROZEN` automaticamente.
