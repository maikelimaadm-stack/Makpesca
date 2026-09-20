---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: todos
---

# Architecture Decision Records (ADRs)

## 1. O que é um ADR aqui

Registro de uma decisão relevante, com contexto, alternativas, consequências e riscos.
**Decisão não registrada não existe** (Constituição, Art. 8).

## 2. Estados

| Estado | Significado |
|--------|-------------|
| `OPEN` | Problema reconhecido, sem decisão |
| `PROPOSED` | Opção preferida, sem validação completa |
| `ACCEPTED` | Decidido; vale para implementação |
| `FROZEN` | Decidido e congelado por onda |
| `SUPERSEDED` | Substituído por outro ADR |
| `REJECTED` | Avaliado e recusado |

## 3. Estrutura obrigatória

Todo ADR contém: Title, Status, Date, Context, Decision Drivers, Options Considered,
Decision, Consequences, Risks, Security Impact, Privacy Impact, Offline Impact,
Portability Impact, Cost Impact, Operational Impact, Open Questions, Evidence, Supersedes,
Superseded By.

## 4. Índice

| ADR | Título | Status | Onda | Bloqueia |
|-----|--------|--------|------|----------|
| [0001](ADR-0001-MOBILE-STACK.md) | Stack mobile | PROPOSED | F2 | MP-04 |
| [0002](ADR-0002-WEB-STACK.md) | Stack web | PROPOSED | F2 | MP-15 |
| [0003](ADR-0003-API-BOUNDARY.md) | Fronteira de API | **ACCEPTED** | F2 | — |
| [0004](ADR-0004-DATABASE-POSTGRES-POSTGIS.md) | PostgreSQL + PostGIS | PROPOSED | F3 | MP-02 |
| [0005](ADR-0005-BACKEND-HOSTING-VERCEL.md) | Hospedagem inicial | PROPOSED | F6 | MP-01 |
| [0006](ADR-0006-BACKEND-FRAMEWORK.md) | Framework da API | **OPEN** | F6 | MP-01 |
| [0007](ADR-0007-ORM-QUERY-LAYER.md) | ORM / query layer | **OPEN** | F3 | MP-02 |
| [0008](ADR-0008-AUTHENTICATION.md) | Autenticação | **OPEN** | F6 | MP-03 |
| [0009](ADR-0009-ONLINE-MAPS-GOOGLE.md) | Mapa online | PROPOSED | F5 | MP-06 |
| [0010](ADR-0010-OFFLINE-MAPS.md) | **Mapa offline** | **OPEN — BLOQUEANTE** | F5 | MP-17 |
| [0011](ADR-0011-OFFLINE-SYNC.md) | Sincronização offline | PROPOSED | F4 | MP-10 |
| [0012](ADR-0012-GEO-PRIVACY.md) | Geo-privacidade | **ACCEPTED** | F3 | MP-07 |
| [0013](ADR-0013-MEDIA-STORAGE.md) | Armazenamento de mídia | PROPOSED | F3 | MP-11 |
| [0014](ADR-0014-BILLING.md) | Billing | **OPEN** | F8 | MP-19 |
| [0015](ADR-0015-ASYNC-JOBS.md) | Jobs assíncronos | **OPEN** | F9 | MP-11 |
| [0016](ADR-0016-OBSERVABILITY.md) | Observabilidade | **OPEN** | F9 | MP-01 |
| [0017](ADR-0017-MONOREPO.md) | Monorepo | PROPOSED | F2 | MP-00 |
| [0018](ADR-0018-SOCIAL-GRAPH.md) | Grafo social | PROPOSED | F7 | MP-13 |
| [0019](ADR-0019-MESSAGING.md) | Mensageria | **OPEN** | F7 | MP-23 |
| [0020](ADR-0020-AFFILIATE-ATTRIBUTION.md) | Atribuição de afiliados | PROPOSED | F8 | MP-21 |
| [0021](ADR-0021-PARTNER-PORTAL.md) | Portal de parceiros | PROPOSED | F8 | MP-27 |

## 5. Resumo do estado

| Estado | Quantidade |
|--------|-----------|
| ACCEPTED | 2 |
| PROPOSED | 12 |
| **OPEN** | **7** |
| FROZEN | 0 |

**7 ADRs abertos** impedem o congelamento de suas ondas.
ADR-0010 é o bloqueio mais grave do projeto.

## 6. Como criar um ADR

1. copiar a estrutura da seção 3;
2. numerar em sequência;
3. registrar em `../00-governance/DECISION-REGISTRY.md`;
4. referenciar nos documentos afetados;
5. nunca editar um ADR `ACCEPTED`/`FROZEN` — criar um novo que o substitua.
