---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: todos
---

# Estado dos Documentos

Índice de controle. Nesta fase **todos** os documentos estão em `DRAFT`.
**Nenhum documento está `FROZEN`.** Nenhuma onda foi congelada.

| Status | Significado |
|--------|-------------|
| `DRAFT` | Em elaboração; não serve de contrato |
| `REVIEW` | Pronto para auditoria humana |
| `FROZEN` | Contrato; implementação pode confiar |
| `SUPERSEDED` | Substituído |

## Resumo

| Estado | Quantidade |
|--------|-----------|
| DRAFT | 126 |
| REVIEW | 0 |
| FROZEN | 0 |
| SUPERSEDED | 0 |

Total de documentos em `docs/`: **126**

## Documentos por diretório


### `docs/00-governance/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `ASSUMPTIONS.md` | DRAFT | 0.1.0 | F0 |
| `DECISION-POLICY.md` | DRAFT | 0.1.0 | F0 |
| `DECISION-REGISTRY.md` | DRAFT | 0.1.0 | F0 |
| `DOCUMENT-STATUS.md` | DRAFT | 0.1.0 | F0 |
| `FREEZE-POLICY.md` | DRAFT | 0.1.0 | F0 |
| `GLOSSARY.md` | DRAFT | 0.1.0 | F0 |
| `OPEN-QUESTIONS.md` | DRAFT | 0.1.0 | F0 |
| `PROJECT-CONSTITUTION.md` | DRAFT | 0.1.0 | F0 |
| `RISK-REGISTER.md` | DRAFT | 0.1.0 | F0 |

### `docs/01-product/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `COMPETITOR-LANDSCAPE.md` | DRAFT | 0.1.0 | F1 |
| `CORE-JOURNEYS.md` | DRAFT | 0.1.0 | F1 |
| `FUTURE-SCOPE.md` | DRAFT | 0.1.0 | F1 |
| `MONETIZATION.md` | DRAFT | 0.1.0 | F1 |
| `MVP-SCOPE.md` | DRAFT | 0.1.0 | F1 |
| `NON-GOALS.md` | DRAFT | 0.1.0 | F1 |
| `PERSONAS.md` | DRAFT | 0.1.0 | F1 |
| `POST-MVP-SCOPE.md` | DRAFT | 0.1.0 | F1 |
| `PRODUCT-METRICS.md` | DRAFT | 0.1.0 | F1 |
| `PRODUCT-PRINCIPLES.md` | DRAFT | 0.1.0 | F1 |
| `PRODUCT-VISION.md` | DRAFT | 0.1.0 | F1 |

### `docs/02-architecture/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `COMPONENT-BOUNDARIES.md` | DRAFT | 0.1.0 | F2 |
| `CONTAINER-ARCHITECTURE.md` | DRAFT | 0.1.0 | F2 |
| `ENVIRONMENT-STRATEGY.md` | DRAFT | 0.1.0 | F2 |
| `PORTABILITY-STRATEGY.md` | DRAFT | 0.1.0 | F2 |
| `PROVIDER-ABSTRACTION.md` | DRAFT | 0.1.0 | F2 |
| `REPOSITORY-STRATEGY.md` | DRAFT | 0.1.0 | F2 |
| `SCALABILITY-STRATEGY.md` | DRAFT | 0.1.0 | F2 |
| `SYSTEM-CONTEXT.md` | DRAFT | 0.1.0 | F2 |

### `docs/03-domain/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `BOUNDED-CONTEXTS.md` | DRAFT | 0.1.0 | F1 |
| `DOMAIN-INVARIANTS.md` | DRAFT | 0.1.0 | F1 |
| `DOMAIN-MAP.md` | DRAFT | 0.1.0 | F1 |
| `ENTITY-CATALOG.md` | DRAFT | 0.1.0 | F1 |

### `docs/04-data/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `BACKUP-RESTORE.md` | DRAFT | 0.1.0 | F3 |
| `CONCEPTUAL-DATA-MODEL.md` | DRAFT | 0.1.0 | F3 |
| `DATA-CLASSIFICATION.md` | DRAFT | 0.1.0 | F3 |
| `DATA-LIFECYCLE.md` | DRAFT | 0.1.0 | F3 |
| `GEO-DATA-MODEL.md` | DRAFT | 0.1.0 | F3 |

### `docs/05-offline-sync/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `CONFLICT-RESOLUTION.md` | DRAFT | 0.1.0 | F4 |
| `LOCAL-DATABASE-STRATEGY.md` | DRAFT | 0.1.0 | F4 |
| `MEDIA-SYNC.md` | DRAFT | 0.1.0 | F4 |
| `OFFLINE-FIRST-CONTRACT.md` | DRAFT | 0.1.0 | F4 |
| `SYNC-FAILURE-MODES.md` | DRAFT | 0.1.0 | F4 |
| `SYNC-PROTOCOL.md` | DRAFT | 0.1.0 | F4 |

### `docs/06-maps-location/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `GEO-PRIVACY.md` | DRAFT | 0.1.0 | F5 |
| `GPS-STRATEGY.md` | DRAFT | 0.1.0 | F5 |
| `LOCATION-SHARING.md` | DRAFT | 0.1.0 | F5 |
| `MAP-ARCHITECTURE.md` | DRAFT | 0.1.0 | F5 |
| `MAP-PROVIDER-MATRIX.md` | DRAFT | 0.1.0 | F5 |
| `ONLINE-OFFLINE-MAP-STRATEGY.md` | DRAFT | 0.1.0 | F5 |

### `docs/07-api/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `API-ENDPOINT-MATRIX.md` | DRAFT | 0.1.0 | F6 |
| `API-ERROR-CONTRACT.md` | DRAFT | 0.1.0 | F6 |
| `API-IDEMPOTENCY.md` | DRAFT | 0.1.0 | F6 |
| `API-PORTABILITY.md` | DRAFT | 0.1.0 | F6 |
| `API-PRINCIPLES.md` | DRAFT | 0.1.0 | F6 |
| `API-SECURITY.md` | DRAFT | 0.1.0 | F6 |
| `API-VERSIONING.md` | DRAFT | 0.1.0 | F6 |

### `docs/08-security-privacy/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `AUTH-OPTIONS.md` | DRAFT | 0.1.0 | F6 |
| `GEO-PRIVACY-THREAT-MODEL.md` | DRAFT | 0.1.0 | F6 |
| `INCIDENT-RESPONSE.md` | DRAFT | 0.1.0 | F6 |
| `PRIVACY-LGPD-CHECKLIST.md` | DRAFT | 0.1.0 | F6 |
| `SECRETS-POLICY.md` | DRAFT | 0.1.0 | F6 |
| `SECURITY-BASELINE.md` | DRAFT | 0.1.0 | F6 |
| `THREAT-MODEL.md` | DRAFT | 0.1.0 | F6 |

### `docs/09-social/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `COMMUNITY-MODEL.md` | DRAFT | 0.1.0 | F7 |
| `EVENTS-MODEL.md` | DRAFT | 0.1.0 | F7 |
| `FEED-MODEL.md` | DRAFT | 0.1.0 | F7 |
| `FOLLOW-FRIEND-MODEL.md` | DRAFT | 0.1.0 | F7 |
| `GROUP-MODEL.md` | DRAFT | 0.1.0 | F7 |
| `MESSAGING-MODEL.md` | DRAFT | 0.1.0 | F7 |
| `MODERATION.md` | DRAFT | 0.1.0 | F7 |
| `PROFILE-MODEL.md` | DRAFT | 0.1.0 | F7 |
| `REPORT-BLOCK.md` | DRAFT | 0.1.0 | F7 |
| `SOCIAL-MODEL.md` | DRAFT | 0.1.0 | F7 |

### `docs/10-gamification/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `ACHIEVEMENTS.md` | DRAFT | 0.1.0 | F8 |
| `ANTI-FRAUD.md` | DRAFT | 0.1.0 | F8 |
| `CHALLENGES.md` | DRAFT | 0.1.0 | F8 |
| `RANKINGS.md` | DRAFT | 0.1.0 | F8 |

### `docs/11-commerce/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `AFFILIATE-PROGRAM.md` | DRAFT | 0.1.0 | F8 |
| `ATTRIBUTION.md` | DRAFT | 0.1.0 | F8 |
| `COMMERCE-FRAUD.md` | DRAFT | 0.1.0 | F8 |
| `COMMISSIONS-PAYOUTS.md` | DRAFT | 0.1.0 | F8 |
| `OFFERS.md` | DRAFT | 0.1.0 | F8 |
| `PARTNER-PORTAL.md` | DRAFT | 0.1.0 | F8 |
| `PARTNER-STORES.md` | DRAFT | 0.1.0 | F8 |

### `docs/12-billing/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `BILLING-ARCHITECTURE.md` | DRAFT | 0.1.0 | F8 |
| `ENTITLEMENTS.md` | DRAFT | 0.1.0 | F8 |
| `FREE-PRO-MODEL.md` | DRAFT | 0.1.0 | F8 |

### `docs/13-intelligence/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `ENVIRONMENTAL-DATA.md` | DRAFT | 0.1.0 | F3/F8 |
| `FISHING-INTELLIGENCE.md` | DRAFT | 0.1.0 | F3/F8 |
| `PRIVACY-PRESERVING-AGGREGATION.md` | DRAFT | 0.1.0 | F3/F8 |

### `docs/14-operations/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `ASYNC-JOBS.md` | DRAFT | 0.1.0 | F9 |
| `ENVIRONMENTS.md` | DRAFT | 0.1.0 | F9 |
| `FEATURE-FLAGS.md` | DRAFT | 0.1.0 | F9 |
| `OBSERVABILITY.md` | DRAFT | 0.1.0 | F9 |
| `RUNBOOK-BASELINE.md` | DRAFT | 0.1.0 | F9 |

### `docs/15-quality/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `COMMERCE-TEST-MATRIX.md` | DRAFT | 0.1.0 | F9 |
| `OFFLINE-TEST-MATRIX.md` | DRAFT | 0.1.0 | F9 |
| `PRIVACY-TEST-MATRIX.md` | DRAFT | 0.1.0 | F9 |
| `QUALITY-GATES.md` | DRAFT | 0.1.0 | F9 |
| `TEST-STRATEGY.md` | DRAFT | 0.1.0 | F9 |

### `docs/16-roadmap/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `DEPENDENCY-MAP.md` | DRAFT | 0.1.0 | F10 |
| `DOCUMENTATION-FREEZE-WAVES.md` | DRAFT | 0.1.0 | F10 |
| `IMPLEMENTATION-SLICE-ROADMAP.md` | DRAFT | 0.1.0 | F10 |

### `docs/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `README.md` | DRAFT | 0.1.0 | F0 |

### `docs/adr/`

| Documento | Status | Versão | Onda |
|-----------|--------|--------|------|
| `ADR-0001-MOBILE-STACK.md` | PROPOSED | — | variável |
| `ADR-0002-WEB-STACK.md` | PROPOSED | — | variável |
| `ADR-0003-API-BOUNDARY.md` | **ACCEPTED** | — | variável |
| `ADR-0004-DATABASE-POSTGRES-POSTGIS.md` | PROPOSED | — | variável |
| `ADR-0005-BACKEND-HOSTING-VERCEL.md` | PROPOSED | — | variável |
| `ADR-0006-BACKEND-FRAMEWORK.md` | **OPEN** | — | variável |
| `ADR-0007-ORM-QUERY-LAYER.md` | **OPEN** | — | variável |
| `ADR-0008-AUTHENTICATION.md` | **OPEN** | — | variável |
| `ADR-0009-ONLINE-MAPS-GOOGLE.md` | PROPOSED | — | variável |
| `ADR-0010-OFFLINE-MAPS.md` | **OPEN — BLOQUEANTE** | — | variável |
| `ADR-0011-OFFLINE-SYNC.md` | PROPOSED | — | variável |
| `ADR-0012-GEO-PRIVACY.md` | **ACCEPTED** | — | variável |
| `ADR-0013-MEDIA-STORAGE.md` | PROPOSED | — | variável |
| `ADR-0014-BILLING.md` | **OPEN** | — | variável |
| `ADR-0015-ASYNC-JOBS.md` | **OPEN** | — | variável |
| `ADR-0016-OBSERVABILITY.md` | **OPEN** | — | variável |
| `ADR-0017-MONOREPO.md` | PROPOSED | — | variável |
| `ADR-0018-SOCIAL-GRAPH.md` | PROPOSED | — | variável |
| `ADR-0019-MESSAGING.md` | **OPEN** | — | variável |
| `ADR-0020-AFFILIATE-ATTRIBUTION.md` | PROPOSED | — | variável |
| `ADR-0021-PARTNER-PORTAL.md` | PROPOSED | — | variável |
| `README.md` | DRAFT | — | variável |

## Regras

1. Documento novo entra nesta tabela no mesmo commit em que é criado.
2. Mudança de `Status` aqui e no cabeçalho do próprio documento devem ser simultâneas.
3. `FROZEN` só por onda, conforme `FREEZE-POLICY.md`.
4. Divergência entre esta tabela e o cabeçalho do documento é falha do gate `DOC-CONSISTENCY`.
