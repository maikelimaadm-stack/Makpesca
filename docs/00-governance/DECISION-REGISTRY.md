---
Status: REVIEW
Version: 0.2.0
Last Updated: 2026-09-21
Owners: Maike Lima (autoridade humana final)
Related ADRs: ADR-0001..ADR-0021
Wave: cross-cutting (controle vivo; registrada em F0)
Lifecycle: LIVING
---

# Registro de Decisões

Índice único de todas as decisões do projeto. Detalhe em `../adr/`.

## 1. Decisões baseline (assumidas nesta fase)

| # | Decisão | Estado | ADR | Observação |
|---|---------|--------|-----|------------|
| D-001 | Mobile em React Native + Expo + TypeScript | PROPOSED | ADR-0001 | Baseline do briefing |
| D-002 | Web em Next.js + TypeScript | PROPOSED | ADR-0002 | Baseline do briefing |
| D-003 | API própria como única fronteira de negócio | ACCEPTED | ADR-0003 | Constitucional (Art. 2) |
| D-004 | PostgreSQL + PostGIS | PROPOSED | ADR-0004 | PostGIS é requisito |
| D-005 | Hospedagem inicial da API na Vercel | PROPOSED | ADR-0005 | Atrás de boundary; saída obrigatória |
| D-006 | Framework HTTP da API | OPEN | ADR-0006 | Hono vs Fastify vs outro |
| D-007 | ORM / camada de query | OPEN | ADR-0007 | Drizzle vs Prisma vs Kysely |
| D-008 | Autenticação | OPEN | ADR-0008 | Supabase Auth encapsulado vs Clerk vs Auth0 vs outro |
| D-009 | Mapa online: Google Maps Platform | PROPOSED | ADR-0009 | Preferência inicial |
| D-010 | Mapa offline | OPEN | ADR-0010 | **BLOCKING** — licença de tiles |
| D-011 | Protocolo de sincronização offline | PROPOSED | ADR-0011 | Outbox + cursor + idempotência |
| D-012 | Geo-privacy server-side com visibilidade × precisão | ACCEPTED | ADR-0012 | Constitucional (Art. 3) |
| D-013 | Armazenamento de mídia em object storage via adapter | PROPOSED | ADR-0013 | Provider específico em aberto |
| D-014 | Billing de assinatura | OPEN | ADR-0014 | Lojas + agregador |
| D-015 | Jobs assíncronos | OPEN | ADR-0015 | Abstração de fila primeiro |
| D-016 | Observabilidade | OPEN | ADR-0016 | Logs estruturados obrigatórios |
| D-017 | Monorepo | PROPOSED | ADR-0017 | pnpm workspace + Turborepo (a validar) |
| D-018 | Grafo social: follow assimétrico | PROPOSED | ADR-0018 | Amizade mútua opcional |
| D-019 | Mensageria | OPEN | ADR-0019 | Build vs provider |
| D-020 | Atribuição de afiliados | PROPOSED | ADR-0020 | Click + cupom, last-click com janela |
| D-021 | Portal de parceiros | PROPOSED | ADR-0021 | App separado no mesmo monorepo |

### Contagem de ADRs (recalculada dos arquivos em 2026-09-21)

| Estado | Quantidade | ADRs |
|--------|-----------|------|
| ACCEPTED | **2** | ADR-0003, ADR-0012 |
| PROPOSED | **11** | ADR-0001, 0002, 0004, 0005, 0009, 0011, 0013, 0017, 0018, 0020, 0021 |
| OPEN | **8** | ADR-0006, 0007, 0008, 0010, 0014, 0015, 0016, 0019 |
| FROZEN / SUPERSEDED / REJECTED | 0 | — |
| **Total** | **21** | — |

Nenhum ADR `OPEN` pertence à onda **F0**.

## 2. Decisões de processo

| # | Decisão | Estado | Origem |
|---|---------|--------|--------|
| P-001 | Documentação antes de implementação | ACCEPTED | PROJECT-CONSTITUTION Art. 1 |
| P-002 | Congelamento por ondas F0..F10 | ACCEPTED | FREEZE-POLICY |
| P-003 | Gates bloqueantes | ACCEPTED | QUALITY-GATES |
| P-004 | `IMPLEMENTATION-READY-GATE` = BLOCKED | ACCEPTED | MP-DOC-00 |
| P-005 | Documentação principal em pt-BR | ACCEPTED | MP-DOC-00 |
| P-006 | **Product Owner / autoridade humana final: Maike Lima** | ACCEPTED | PROJECT-CONSTITUTION Art. 15 (R1-05) |
| P-007 | Agentes de IA são executores/revisores, nunca owners finais | ACCEPTED | PROJECT-CONSTITUTION Art. 15 |
| P-008 | Onda congelada por snapshot; Core Freeze Set × Living Control Documents | ACCEPTED | FREEZE-POLICY §2, §3, §7 (R1-02) |
| P-009 | Offline App Core é constitucional; basemap offline é decisão separada | ACCEPTED | PROJECT-CONSTITUTION Art. 4 e 4-A (R1-03) |
| P-010 | Gates são avaliados por escopo (`COST-GATE` scope-aware) | ACCEPTED | QUALITY-GATES §0, §12 (R1-04) |
| P-011 | Vocabulário fechado de estado de gate; aprovação humana registrada à parte | ACCEPTED | QUALITY-GATES §0 (R1-06) |
| P-012 | Contagens e resumos derivados são recalculados do SSOT | ACCEPTED | DECISION-POLICY §8 (R1-07) |

## 3. Histórico de alterações

| Data | Decisão | De → Para | Motivo | Autor |
|------|---------|-----------|--------|-------|
| 2026-09-20 | — | — | Criação do registro na missão MP-DOC-00 v2 | (a definir) |
| 2026-09-21 | P-006 | — → ACCEPTED | Q-001 resolvida: Maike Lima como Product Owner e autoridade humana final | Maike Lima |
| 2026-09-21 | P-007..P-012 | — → ACCEPTED | Remediação MP-DOC-00 v2 R1 (findings R1-02..R1-07) | Maike Lima |
| 2026-09-21 | Contagem de ADRs | OPEN=7 / PROPOSED=12 → **OPEN=8 / PROPOSED=11** | Correção de contagem derivada divergente do SSOT (R1-01) | MP-DOC-00 v2 R1 |

## 4. Regra

Decisão que não está nesta tabela **não existe** para efeito de implementação.
