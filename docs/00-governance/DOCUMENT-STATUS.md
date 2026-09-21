---
Status: REVIEW
Version: 0.2.0
Last Updated: 2026-09-21
Owners: Maike Lima (autoridade humana final)
Related ADRs: todos
Wave: cross-cutting (controle vivo; registrada em F0)
Lifecycle: LIVING
---

# Estado dos Documentos

Índice de controle. **Nenhum documento está `FROZEN`.** Nenhuma onda foi congelada.

## 1. Status

| Status | Significado |
|--------|-------------|
| `DRAFT` | Em elaboração; não serve de contrato |
| `REVIEW` | Pronto para auditoria humana |
| `FROZEN` | Contrato; implementação pode confiar |
| `SUPERSEDED` | Substituído |

## 2. Lifecycle

| Lifecycle | Significado |
|-----------|-------------|
| `FREEZE-CONTROLLED` | Pode ser congelado; pertence ao Core Freeze Set de alguma onda |
| `LIVING` | Registro de controle; **nunca** recebe `FROZEN`; evolui ao longo de F1..F10 |

Definição canônica em [FREEZE-POLICY.md](FREEZE-POLICY.md) §2, §3 e §7 — esse é o SSOT da
composição das ondas. Esta tabela é **derivada**: divergência é falha de `DOC-CONSISTENCY`.

Regra que prende os `LIVING`: podem ser atualizados livremente, mas **não podem contradizer
o Core congelado**. Contradição exige ADR de superseção.

## 3. Resumo

| Estado | Quantidade |
|--------|-----------|
| DRAFT | 112 |
| REVIEW | 15 |
| FROZEN | 0 |
| SUPERSEDED | 0 |
| **Total** | **127** |

Documentos em `docs/`: **126**. Somando `CLAUDE.md` (raiz): **127**.

Os 15 em `REVIEW`: o Core Freeze Set de F0 (7), os Living Control Documents de F0 (7,
incluindo `CLAUDE.md` na raiz) e `QUALITY-GATES.md` (F9, `LIVING`), tocado pela rodada R1.

## 4. Onda F0 — composição

### Core Freeze Set (`FREEZE-CONTROLLED`)

| # | Documento | Status |
|---|-----------|--------|
| 1 | `docs/00-governance/PROJECT-CONSTITUTION.md` | REVIEW |
| 2 | `docs/00-governance/DECISION-POLICY.md` | REVIEW |
| 3 | `docs/00-governance/FREEZE-POLICY.md` | REVIEW |
| 4 | `docs/00-governance/GLOSSARY.md` | REVIEW |
| 5 | `docs/01-product/PRODUCT-VISION.md` | REVIEW |
| 6 | `docs/01-product/PRODUCT-PRINCIPLES.md` | REVIEW |
| 7 | `docs/01-product/NON-GOALS.md` | REVIEW |

### Living Control Documents (`LIVING`, nunca congelam)

| # | Documento | Status |
|---|-----------|--------|
| 8 | `docs/00-governance/DOCUMENT-STATUS.md` | REVIEW |
| 9 | `docs/00-governance/DECISION-REGISTRY.md` | REVIEW |
| 10 | `docs/00-governance/OPEN-QUESTIONS.md` | REVIEW |
| 11 | `docs/00-governance/RISK-REGISTER.md` | REVIEW |
| 12 | `docs/00-governance/ASSUMPTIONS.md` | REVIEW |
| 13 | `docs/README.md` | REVIEW |
| 14 | `CLAUDE.md` (raiz) | REVIEW |

Fora de F0, `docs/15-quality/QUALITY-GATES.md` também é `LIVING` (registro de estado de
gates) e está em `REVIEW` por ter sido reescrito na rodada R1; pertence à onda F9.

## 5. Todos os documentos

`Wave` indica a onda em que o documento é candidato a congelar.
`cross-cutting` = controle vivo, sem onda de congelamento própria.


### `docs/00-governance/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `ASSUMPTIONS.md` | REVIEW | 0.2.0 | cross-cutting | **LIVING** |
| `DECISION-POLICY.md` | REVIEW | 0.2.0 | **F0** | FREEZE-CONTROLLED |
| `DECISION-REGISTRY.md` | REVIEW | 0.2.0 | cross-cutting | **LIVING** |
| `DOCUMENT-STATUS.md` | REVIEW | 0.2.0 | cross-cutting | **LIVING** |
| `FREEZE-POLICY.md` | REVIEW | 0.2.0 | **F0** | FREEZE-CONTROLLED |
| `GLOSSARY.md` | REVIEW | 0.2.0 | **F0** | FREEZE-CONTROLLED |
| `OPEN-QUESTIONS.md` | REVIEW | 0.2.0 | cross-cutting | **LIVING** |
| `PROJECT-CONSTITUTION.md` | REVIEW | 0.2.0 | **F0** | FREEZE-CONTROLLED |
| `RISK-REGISTER.md` | REVIEW | 0.2.0 | cross-cutting | **LIVING** |

### `docs/01-product/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `COMPETITOR-LANDSCAPE.md` | DRAFT | 0.1.0 | F1 | FREEZE-CONTROLLED |
| `CORE-JOURNEYS.md` | DRAFT | 0.1.0 | F1 | FREEZE-CONTROLLED |
| `FUTURE-SCOPE.md` | DRAFT | 0.1.0 | F1 | FREEZE-CONTROLLED |
| `MONETIZATION.md` | DRAFT | 0.1.0 | F1 | FREEZE-CONTROLLED |
| `MVP-SCOPE.md` | DRAFT | 0.1.0 | F1 | FREEZE-CONTROLLED |
| `NON-GOALS.md` | REVIEW | 0.2.0 | **F0** | FREEZE-CONTROLLED |
| `PERSONAS.md` | DRAFT | 0.1.0 | F1 | FREEZE-CONTROLLED |
| `POST-MVP-SCOPE.md` | DRAFT | 0.1.0 | F1 | FREEZE-CONTROLLED |
| `PRODUCT-METRICS.md` | DRAFT | 0.1.0 | F1 | FREEZE-CONTROLLED |
| `PRODUCT-PRINCIPLES.md` | REVIEW | 0.2.0 | **F0** | FREEZE-CONTROLLED |
| `PRODUCT-VISION.md` | REVIEW | 0.2.0 | **F0** | FREEZE-CONTROLLED |

### `docs/02-architecture/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `COMPONENT-BOUNDARIES.md` | DRAFT | 0.1.0 | F2 | FREEZE-CONTROLLED |
| `CONTAINER-ARCHITECTURE.md` | DRAFT | 0.1.0 | F2 | FREEZE-CONTROLLED |
| `ENVIRONMENT-STRATEGY.md` | DRAFT | 0.1.0 | F2 | FREEZE-CONTROLLED |
| `PORTABILITY-STRATEGY.md` | DRAFT | 0.1.0 | F2 | FREEZE-CONTROLLED |
| `PROVIDER-ABSTRACTION.md` | DRAFT | 0.1.0 | F2 | FREEZE-CONTROLLED |
| `REPOSITORY-STRATEGY.md` | DRAFT | 0.1.0 | F2 | FREEZE-CONTROLLED |
| `SCALABILITY-STRATEGY.md` | DRAFT | 0.1.0 | F2 | FREEZE-CONTROLLED |
| `SYSTEM-CONTEXT.md` | DRAFT | 0.1.0 | F2 | FREEZE-CONTROLLED |

### `docs/03-domain/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `BOUNDED-CONTEXTS.md` | DRAFT | 0.1.0 | F1 | FREEZE-CONTROLLED |
| `DOMAIN-INVARIANTS.md` | DRAFT | 0.1.0 | F1 | FREEZE-CONTROLLED |
| `DOMAIN-MAP.md` | DRAFT | 0.1.0 | F1 | FREEZE-CONTROLLED |
| `ENTITY-CATALOG.md` | DRAFT | 0.1.0 | F1 | FREEZE-CONTROLLED |

### `docs/04-data/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `BACKUP-RESTORE.md` | DRAFT | 0.1.0 | F3 | FREEZE-CONTROLLED |
| `CONCEPTUAL-DATA-MODEL.md` | DRAFT | 0.1.0 | F3 | FREEZE-CONTROLLED |
| `DATA-CLASSIFICATION.md` | DRAFT | 0.1.0 | F3 | FREEZE-CONTROLLED |
| `DATA-LIFECYCLE.md` | DRAFT | 0.1.0 | F3 | FREEZE-CONTROLLED |
| `GEO-DATA-MODEL.md` | DRAFT | 0.1.0 | F3 | FREEZE-CONTROLLED |

### `docs/05-offline-sync/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `CONFLICT-RESOLUTION.md` | DRAFT | 0.1.0 | F4 | FREEZE-CONTROLLED |
| `LOCAL-DATABASE-STRATEGY.md` | DRAFT | 0.1.0 | F4 | FREEZE-CONTROLLED |
| `MEDIA-SYNC.md` | DRAFT | 0.1.0 | F4 | FREEZE-CONTROLLED |
| `OFFLINE-FIRST-CONTRACT.md` | DRAFT | 0.1.0 | F4 | FREEZE-CONTROLLED |
| `SYNC-FAILURE-MODES.md` | DRAFT | 0.1.0 | F4 | FREEZE-CONTROLLED |
| `SYNC-PROTOCOL.md` | DRAFT | 0.1.0 | F4 | FREEZE-CONTROLLED |

### `docs/06-maps-location/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `GEO-PRIVACY.md` | DRAFT | 0.1.0 | F5 | FREEZE-CONTROLLED |
| `GPS-STRATEGY.md` | DRAFT | 0.1.0 | F5 | FREEZE-CONTROLLED |
| `LOCATION-SHARING.md` | DRAFT | 0.1.0 | F5 | FREEZE-CONTROLLED |
| `MAP-ARCHITECTURE.md` | DRAFT | 0.1.0 | F5 | FREEZE-CONTROLLED |
| `MAP-PROVIDER-MATRIX.md` | DRAFT | 0.1.0 | F5 | FREEZE-CONTROLLED |
| `ONLINE-OFFLINE-MAP-STRATEGY.md` | DRAFT | 0.1.0 | F5 | FREEZE-CONTROLLED |

### `docs/07-api/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `API-ENDPOINT-MATRIX.md` | DRAFT | 0.1.0 | F6 | FREEZE-CONTROLLED |
| `API-ERROR-CONTRACT.md` | DRAFT | 0.1.0 | F6 | FREEZE-CONTROLLED |
| `API-IDEMPOTENCY.md` | DRAFT | 0.1.0 | F6 | FREEZE-CONTROLLED |
| `API-PORTABILITY.md` | DRAFT | 0.1.0 | F6 | FREEZE-CONTROLLED |
| `API-PRINCIPLES.md` | DRAFT | 0.1.0 | F6 | FREEZE-CONTROLLED |
| `API-SECURITY.md` | DRAFT | 0.1.0 | F6 | FREEZE-CONTROLLED |
| `API-VERSIONING.md` | DRAFT | 0.1.0 | F6 | FREEZE-CONTROLLED |

### `docs/08-security-privacy/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `AUTH-OPTIONS.md` | DRAFT | 0.1.0 | F6 | FREEZE-CONTROLLED |
| `GEO-PRIVACY-THREAT-MODEL.md` | DRAFT | 0.1.0 | F6 | FREEZE-CONTROLLED |
| `INCIDENT-RESPONSE.md` | DRAFT | 0.1.0 | F6 | FREEZE-CONTROLLED |
| `PRIVACY-LGPD-CHECKLIST.md` | DRAFT | 0.1.0 | F6 | FREEZE-CONTROLLED |
| `SECRETS-POLICY.md` | DRAFT | 0.1.0 | F6 | FREEZE-CONTROLLED |
| `SECURITY-BASELINE.md` | DRAFT | 0.1.0 | F6 | FREEZE-CONTROLLED |
| `THREAT-MODEL.md` | DRAFT | 0.1.0 | F6 | FREEZE-CONTROLLED |

### `docs/09-social/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `COMMUNITY-MODEL.md` | DRAFT | 0.1.0 | F7 | FREEZE-CONTROLLED |
| `EVENTS-MODEL.md` | DRAFT | 0.1.0 | F7 | FREEZE-CONTROLLED |
| `FEED-MODEL.md` | DRAFT | 0.1.0 | F7 | FREEZE-CONTROLLED |
| `FOLLOW-FRIEND-MODEL.md` | DRAFT | 0.1.0 | F7 | FREEZE-CONTROLLED |
| `GROUP-MODEL.md` | DRAFT | 0.1.0 | F7 | FREEZE-CONTROLLED |
| `MESSAGING-MODEL.md` | DRAFT | 0.1.0 | F7 | FREEZE-CONTROLLED |
| `MODERATION.md` | DRAFT | 0.1.0 | F7 | FREEZE-CONTROLLED |
| `PROFILE-MODEL.md` | DRAFT | 0.1.0 | F7 | FREEZE-CONTROLLED |
| `REPORT-BLOCK.md` | DRAFT | 0.1.0 | F7 | FREEZE-CONTROLLED |
| `SOCIAL-MODEL.md` | DRAFT | 0.1.0 | F7 | FREEZE-CONTROLLED |

### `docs/10-gamification/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `ACHIEVEMENTS.md` | DRAFT | 0.1.0 | F8 | FREEZE-CONTROLLED |
| `ANTI-FRAUD.md` | DRAFT | 0.1.0 | F8 | FREEZE-CONTROLLED |
| `CHALLENGES.md` | DRAFT | 0.1.0 | F8 | FREEZE-CONTROLLED |
| `RANKINGS.md` | DRAFT | 0.1.0 | F8 | FREEZE-CONTROLLED |

### `docs/11-commerce/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `AFFILIATE-PROGRAM.md` | DRAFT | 0.1.0 | F8 | FREEZE-CONTROLLED |
| `ATTRIBUTION.md` | DRAFT | 0.1.0 | F8 | FREEZE-CONTROLLED |
| `COMMERCE-FRAUD.md` | DRAFT | 0.1.0 | F8 | FREEZE-CONTROLLED |
| `COMMISSIONS-PAYOUTS.md` | DRAFT | 0.1.0 | F8 | FREEZE-CONTROLLED |
| `OFFERS.md` | DRAFT | 0.1.0 | F8 | FREEZE-CONTROLLED |
| `PARTNER-PORTAL.md` | DRAFT | 0.1.0 | F8 | FREEZE-CONTROLLED |
| `PARTNER-STORES.md` | DRAFT | 0.1.0 | F8 | FREEZE-CONTROLLED |

### `docs/12-billing/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `BILLING-ARCHITECTURE.md` | DRAFT | 0.1.0 | F8 | FREEZE-CONTROLLED |
| `ENTITLEMENTS.md` | DRAFT | 0.1.0 | F8 | FREEZE-CONTROLLED |
| `FREE-PRO-MODEL.md` | DRAFT | 0.1.0 | F8 | FREEZE-CONTROLLED |

### `docs/13-intelligence/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `ENVIRONMENTAL-DATA.md` | DRAFT | 0.1.0 | F3/F8 | FREEZE-CONTROLLED |
| `FISHING-INTELLIGENCE.md` | DRAFT | 0.1.0 | F3/F8 | FREEZE-CONTROLLED |
| `PRIVACY-PRESERVING-AGGREGATION.md` | DRAFT | 0.1.0 | F3/F8 | FREEZE-CONTROLLED |

### `docs/14-operations/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `ASYNC-JOBS.md` | DRAFT | 0.1.0 | F9 | FREEZE-CONTROLLED |
| `ENVIRONMENTS.md` | DRAFT | 0.1.0 | F9 | FREEZE-CONTROLLED |
| `FEATURE-FLAGS.md` | DRAFT | 0.1.0 | F9 | FREEZE-CONTROLLED |
| `OBSERVABILITY.md` | DRAFT | 0.1.0 | F9 | FREEZE-CONTROLLED |
| `RUNBOOK-BASELINE.md` | DRAFT | 0.1.0 | F9 | FREEZE-CONTROLLED |

### `docs/15-quality/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `COMMERCE-TEST-MATRIX.md` | DRAFT | 0.1.0 | F9 | FREEZE-CONTROLLED |
| `OFFLINE-TEST-MATRIX.md` | DRAFT | 0.1.0 | F9 | FREEZE-CONTROLLED |
| `PRIVACY-TEST-MATRIX.md` | DRAFT | 0.1.0 | F9 | FREEZE-CONTROLLED |
| `QUALITY-GATES.md` | REVIEW | 0.2.0 | F9 | **LIVING** |
| `TEST-STRATEGY.md` | DRAFT | 0.1.0 | F9 | FREEZE-CONTROLLED |

### `docs/16-roadmap/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `DEPENDENCY-MAP.md` | DRAFT | 0.1.0 | F10 | FREEZE-CONTROLLED |
| `DOCUMENTATION-FREEZE-WAVES.md` | DRAFT | 0.1.0 | F10 | FREEZE-CONTROLLED |
| `IMPLEMENTATION-SLICE-ROADMAP.md` | DRAFT | 0.1.0 | F10 | FREEZE-CONTROLLED |

### `docs/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `README.md` | REVIEW | 0.2.0 | cross-cutting | **LIVING** |

### `docs/adr/`

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `ADR-0001-MOBILE-STACK.md` | PROPOSED | — | variável | FREEZE-CONTROLLED |
| `ADR-0002-WEB-STACK.md` | PROPOSED | — | variável | FREEZE-CONTROLLED |
| `ADR-0003-API-BOUNDARY.md` | ACCEPTED | — | variável | FREEZE-CONTROLLED |
| `ADR-0004-DATABASE-POSTGRES-POSTGIS.md` | PROPOSED | — | variável | FREEZE-CONTROLLED |
| `ADR-0005-BACKEND-HOSTING-VERCEL.md` | PROPOSED | — | variável | FREEZE-CONTROLLED |
| `ADR-0006-BACKEND-FRAMEWORK.md` | OPEN | — | variável | FREEZE-CONTROLLED |
| `ADR-0007-ORM-QUERY-LAYER.md` | OPEN | — | variável | FREEZE-CONTROLLED |
| `ADR-0008-AUTHENTICATION.md` | OPEN | — | variável | FREEZE-CONTROLLED |
| `ADR-0009-ONLINE-MAPS-GOOGLE.md` | PROPOSED | — | variável | FREEZE-CONTROLLED |
| `ADR-0010-OFFLINE-MAPS.md` | OPEN — BLOQUEANTE | — | variável | FREEZE-CONTROLLED |
| `ADR-0011-OFFLINE-SYNC.md` | PROPOSED | — | variável | FREEZE-CONTROLLED |
| `ADR-0012-GEO-PRIVACY.md` | ACCEPTED | — | variável | FREEZE-CONTROLLED |
| `ADR-0013-MEDIA-STORAGE.md` | PROPOSED | — | variável | FREEZE-CONTROLLED |
| `ADR-0014-BILLING.md` | OPEN | — | variável | FREEZE-CONTROLLED |
| `ADR-0015-ASYNC-JOBS.md` | OPEN | — | variável | FREEZE-CONTROLLED |
| `ADR-0016-OBSERVABILITY.md` | OPEN | — | variável | FREEZE-CONTROLLED |
| `ADR-0017-MONOREPO.md` | PROPOSED | — | variável | FREEZE-CONTROLLED |
| `ADR-0018-SOCIAL-GRAPH.md` | PROPOSED | — | variável | FREEZE-CONTROLLED |
| `ADR-0019-MESSAGING.md` | OPEN | — | variável | FREEZE-CONTROLLED |
| `ADR-0020-AFFILIATE-ATTRIBUTION.md` | PROPOSED | — | variável | FREEZE-CONTROLLED |
| `ADR-0021-PARTNER-PORTAL.md` | PROPOSED | — | variável | FREEZE-CONTROLLED |
| `README.md` | DRAFT | — | variável | FREEZE-CONTROLLED |

### raiz

| Documento | Status | Versão | Wave | Lifecycle |
|-----------|--------|--------|------|-----------|
| `CLAUDE.md` | REVIEW | 0.2.0 | cross-cutting | **LIVING** |
| `README.md` | DRAFT | — | cross-cutting | **LIVING** |

## 6. Regras

1. Documento novo entra nesta tabela no mesmo commit em que é criado.
2. Mudança de `Status` aqui e no cabeçalho do próprio documento são simultâneas.
3. `FROZEN` só por onda, conforme `FREEZE-POLICY.md`, e **nunca** em documento `LIVING`.
4. A composição das ondas vem de `FREEZE-POLICY.md` §7; esta tabela a reproduz.
5. Divergência entre esta tabela e o cabeçalho do documento é falha de `DOC-CONSISTENCY`.
6. Esta tabela é derivada: recalcule do SSOT antes de citá-la (`DECISION-POLICY.md` §8).
