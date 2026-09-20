---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0001..ADR-0021
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

## 2. Decisões de processo

| # | Decisão | Estado | Origem |
|---|---------|--------|--------|
| P-001 | Documentação antes de implementação | ACCEPTED | PROJECT-CONSTITUTION Art. 1 |
| P-002 | Congelamento por ondas F0..F10 | ACCEPTED | FREEZE-POLICY |
| P-003 | Gates bloqueantes | ACCEPTED | QUALITY-GATES |
| P-004 | `IMPLEMENTATION-READY-GATE` = BLOCKED | ACCEPTED | MP-DOC-00 |
| P-005 | Documentação principal em pt-BR | ACCEPTED | MP-DOC-00 |

## 3. Histórico de alterações

| Data | Decisão | De → Para | Motivo | Autor |
|------|---------|-----------|--------|-------|
| 2026-09-20 | — | — | Criação do registro na missão MP-DOC-00 v2 | (a definir) |

## 4. Regra

Decisão que não está nesta tabela **não existe** para efeito de implementação.
