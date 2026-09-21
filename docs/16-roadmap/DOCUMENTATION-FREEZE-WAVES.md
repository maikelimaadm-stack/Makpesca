---
Status: DRAFT
Version: 0.2.0
Last Updated: 2026-09-21
Owners: Maike Lima (autoridade humana final)
Related ADRs: todos
Wave: F10
Lifecycle: FREEZE-CONTROLLED
---

# Ondas de Congelamento da Documentação

Política em `../00-governance/FREEZE-POLICY.md`.
**Regra:** decisão crítica aberta na onda ⇒ `FREEZE = BLOCKED` para aquela onda.

## Como ler as listas de documentos

Cada onda tem um **Core Freeze Set** (a lista nominal que vira contrato) e pode
referenciar **Living Control Documents** (registros que nunca congelam).
Definição em `../00-governance/FREEZE-POLICY.md` §2, §3 e §7 — que é o SSOT da composição
de F0. Esta página reproduz aquela lista; divergência é falha de `DOC-CONSISTENCY`.

## Visão geral

| Onda | Tema | Estado | Bloqueio |
|------|------|--------|----------|
| **F0** | Constituição e visão | **READY_FOR_HUMAN_FREEZE** | nenhum item `BLOCKING`; falta `HUMAN APPROVAL` |
| F1 | MVP e domínios | PENDING | Q-002, Q-003, Q-015, Q-021; pesquisa de concorrência |
| F2 | Plataforma | PENDING | Q-024 |
| F3 | Dados e geo-privacy | PENDING | Q-007, Q-009, Q-016, Q-017, Q-023 |
| F4 | Offline e sync | PENDING | Depende de F3 |
| F5 | Mapas e GPS | **BLOCKED** | **Q-004, Q-005** (licença de tiles), Q-013 |
| F6 | API, Auth e Security | PENDING | Q-006, Q-008 |
| F7 | Social, comunidades, grupos, eventos | PENDING | Q-012, Q-018 |
| F8 | Lojas, afiliados e PRO | PENDING | Q-010, Q-011, Q-019, Q-020 |
| F9 | Operação e testes | PENDING | Q-022, Q-025 |
| F10 | Roadmap de implementação | PENDING | Depende de F0..F9 |

> `BLOCKED` é reservado para onda com item **`BLOCKING`** aberto. Hoje só **F5** está nessa
> situação (Q-004, Q-005). As demais têm pendências relevantes, mas não bloqueantes —
> ver `../00-governance/OPEN-QUESTIONS.md` §"Por onda".

---

## F0 — Constituição e visão

### Core Freeze Set (contrato da onda)
1. `docs/00-governance/PROJECT-CONSTITUTION.md`
2. `docs/00-governance/DECISION-POLICY.md`
3. `docs/00-governance/FREEZE-POLICY.md`
4. `docs/00-governance/GLOSSARY.md`
5. `docs/01-product/PRODUCT-VISION.md`
6. `docs/01-product/PRODUCT-PRINCIPLES.md`
7. `docs/01-product/NON-GOALS.md`

### Living Control Documents (nunca congelam)
8. `docs/00-governance/DOCUMENT-STATUS.md`
9. `docs/00-governance/DECISION-REGISTRY.md`
10. `docs/00-governance/OPEN-QUESTIONS.md`
11. `docs/00-governance/RISK-REGISTER.md`
12. `docs/00-governance/ASSUMPTIONS.md`
13. `docs/README.md`
14. `CLAUDE.md`

**Pré-condições:** autoridade humana definida (Maike Lima, Q-001 resolvida); princípios
revisados; glossário sem ambiguidade; Core Freeze Set sem promessa dependente de ADR `OPEN`.
**Bloqueio atual:** nenhum item `BLOCKING`.
**Falta:** `HUMAN APPROVAL` — ver `../00-governance/F0-FREEZE-CANDIDATE-REPORT.md`.

> F0 **não** congela provider nem base cartográfica offline: isso é matéria de F5
> (ADR-0010). A Constituição, Art. 4-A, registra explicitamente essa exclusão.

## F1 — MVP e domínios

**Documentos:** `PERSONAS`, `CORE-JOURNEYS`, `MVP-SCOPE`, `POST-MVP-SCOPE`,
`FUTURE-SCOPE`, `COMPETITOR-LANDSCAPE`, `MONETIZATION`, `PRODUCT-METRICS`,
`DOMAIN-MAP`, `BOUNDED-CONTEXTS`, `ENTITY-CATALOG`, `DOMAIN-INVARIANTS`.

**Pré-condições:** pesquisa de concorrência com fontes; recorte geográfico definido;
decisão sobre amizade mútua; origem do catálogo de espécies.
**Pendências (não `BLOCKING`):** Q-002, Q-003, Q-015, Q-021 e ausência de pesquisa verificada.

> `PRODUCT-VISION`, `PRODUCT-PRINCIPLES` e `NON-GOALS` pertencem a **F0**, não a F1.

## F2 — Plataforma

**Documentos:** `SYSTEM-CONTEXT`, `CONTAINER-ARCHITECTURE`, `COMPONENT-BOUNDARIES`,
`PORTABILITY-STRATEGY`, `PROVIDER-ABSTRACTION`, `REPOSITORY-STRATEGY`,
`ENVIRONMENT-STRATEGY`, `SCALABILITY-STRATEGY`, ADR-0001, ADR-0002, ADR-0003, ADR-0017.

**Pré-condições:** ferramenta de monorepo decidida; teste de portabilidade respondido.

## F3 — Dados e geo-privacy

**Documentos:** `CONCEPTUAL-DATA-MODEL`, `GEO-DATA-MODEL`, `DATA-CLASSIFICATION`,
`DATA-LIFECYCLE`, `BACKUP-RESTORE`, `GEO-PRIVACY`, `GEO-PRIVACY-THREAT-MODEL`,
`LOCATION-SHARING`, `PRIVACY-PRESERVING-AGGREGATION`, ADR-0004, ADR-0007, ADR-0012,
ADR-0013.

**Pré-condições:** ORM decidido; PostGIS validado no provider; retenção definida com
jurídico; política sobre menores; `k` mínimo definido.
**Bloqueio atual:** Q-007, Q-009, Q-016, Q-017, Q-023.

## F4 — Offline e sync

**Documentos:** `OFFLINE-FIRST-CONTRACT`, `LOCAL-DATABASE-STRATEGY`, `SYNC-PROTOCOL`,
`CONFLICT-RESOLUTION`, `MEDIA-SYNC`, `SYNC-FAILURE-MODES`, `OFFLINE-TEST-MATRIX`,
ADR-0011.

**Pré-condições:** F3 congelada; matriz de conflito revisada; janela de idempotência definida.

## F5 — Mapas e GPS

**Documentos:** `MAP-ARCHITECTURE`, `ONLINE-OFFLINE-MAP-STRATEGY`, `GPS-STRATEGY`,
`MAP-PROVIDER-MATRIX`, `ENVIRONMENTAL-DATA`, ADR-0009, ADR-0010.

**Pré-condições:** matriz de providers preenchida com fontes e datas; licença de uso
offline confirmada por escrito; custo estimado.
**Bloqueio atual: Q-004, Q-005 — este é o bloqueio mais importante do projeto.**

## F6 — API, Auth e Security

**Documentos:** todos de `07-api`, `SECURITY-BASELINE`, `THREAT-MODEL`, `AUTH-OPTIONS`,
`SECRETS-POLICY`, `PRIVACY-LGPD-CHECKLIST`, `INCIDENT-RESPONSE`, ADR-0005, ADR-0006,
ADR-0008.

**Pré-condições:** framework decidido; auth decidido; contrato de erro fechado;
checklist LGPD com revisão jurídica.
**Bloqueio atual:** Q-006, Q-008.

## F7 — Social, comunidades, grupos, eventos

**Documentos:** todos de `09-social`, ADR-0018, ADR-0019.

**Pré-condições:** F6 congelada; moderação com capacidade operacional definida;
decisão sobre criptografia de mensagens.

## F8 — Lojas, afiliados e PRO

**Documentos:** todos de `11-commerce`, todos de `12-billing`, `10-gamification`,
ADR-0014, ADR-0020, ADR-0021.

**Pré-condições:** modelo de comissão definido; forma de payout definida; provider de
billing decidido; preço testado; antifraude com controles implementáveis.
**Bloqueio atual:** Q-010, Q-011, Q-019, Q-020.

## F9 — Operação e testes

**Documentos:** todos de `14-operations`, todos de `15-quality`, ADR-0015, ADR-0016.

**Pré-condições:** runbooks escritos; observabilidade decidida; restore testado.
Autoridade humana já definida (Q-001 resolvida).

## F10 — Roadmap de implementação

**Documentos:** `IMPLEMENTATION-SLICE-ROADMAP`, `DEPENDENCY-MAP`, este documento.

**Pré-condições:** F0..F9 congeladas; slices com critérios de aceite;
`IMPLEMENTATION-READY-GATE` avaliado **por tranche** (ver `../15-quality/QUALITY-GATES.md` §14).

---

## Ordem recomendada de desbloqueio

1. ~~**Q-001 (owners)**~~ — **resolvida em 2026-09-21**: Maike Lima. F0 destravada.
2. **Q-004/Q-005 (licença de basemap offline)** — maior risco do projeto; investigar já.
   Bloqueia apenas F5 e MP-17, **não** o offline core nem o núcleo de implementação.
3. **Q-003, Q-021 (recorte e escopo)** — definem tamanho do MVP.
4. **Q-006, Q-007, Q-008 (stack)** — destravam F2, F3 e F6.
5. **Q-016, Q-017, Q-023 (LGPD e privacidade)** — destravam F3.
6. Demais.
