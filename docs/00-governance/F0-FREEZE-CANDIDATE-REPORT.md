---
Status: REVIEW
Version: 1.0.0
Last Updated: 2026-09-21
Owners: Maike Lima (autoridade humana final)
Related ADRs: ADR-0003, ADR-0012 (baselines constitucionais); ADR-0010 (excluído de F0)
Wave: F0
Lifecycle: LIVING
---

# Relatório de Candidatura ao Congelamento — Onda F0

> Este documento **não congela** F0. Ele apresenta a evidência para que a autoridade
> humana decida. Congelar é ato humano (`FREEZE-POLICY.md` §4).

## 1. Missão, branch e snapshot

| Item | Valor |
|------|-------|
| Missão | MP-DOC-00 v2 **R1** — remediação documental e preparação de F0 |
| Repositório | `maikelimaadm-stack/Makpesca` |
| Branch | `claude/mp-doc-00-foundation-wanppw` |
| Base | `main` @ `2c58f155663d98e69aeb19031b8fe7769e2a3089` |
| HEAD auditado (antes da R1) | `afd041fa58f37a2951ce12d94c1993d0187428dd` |
| Pull request | #1 — **OPEN, DRAFT**, não mergeada |
| Data do relatório | 2026-09-21 |
| Snapshot candidato | o commit da rodada R1 nesta branch (registrado no ato do freeze) |

O congelamento é **por snapshot**: se aprovado, o commit vigente passa a ser o snapshot
de F0 (`FREEZE-POLICY.md` §2).

## 2. F0 — Core Freeze Set

Estes 7 documentos viram **contrato** da onda. `Lifecycle: FREEZE-CONTROLLED`.

| # | Documento | Status | Owner |
|---|-----------|--------|-------|
| 1 | `docs/00-governance/PROJECT-CONSTITUTION.md` | REVIEW | Maike Lima |
| 2 | `docs/00-governance/DECISION-POLICY.md` | REVIEW | Maike Lima |
| 3 | `docs/00-governance/FREEZE-POLICY.md` | REVIEW | Maike Lima |
| 4 | `docs/00-governance/GLOSSARY.md` | REVIEW | Maike Lima |
| 5 | `docs/01-product/PRODUCT-VISION.md` | REVIEW | Maike Lima |
| 6 | `docs/01-product/PRODUCT-PRINCIPLES.md` | REVIEW | Maike Lima |
| 7 | `docs/01-product/NON-GOALS.md` | REVIEW | Maike Lima |

## 3. F0 — Living Control Documents e regra de evolução

Estes 7 **nunca** recebem `FROZEN`, em nenhuma onda. `Lifecycle: LIVING`.

| # | Documento | Por que é vivo |
|---|-----------|----------------|
| 8 | `docs/00-governance/DOCUMENT-STATUS.md` | Registra o estado de todos os documentos |
| 9 | `docs/00-governance/DECISION-REGISTRY.md` | Recebe cada decisão nova |
| 10 | `docs/00-governance/OPEN-QUESTIONS.md` | Perguntas abrem e fecham continuamente |
| 11 | `docs/00-governance/RISK-REGISTER.md` | Riscos surgem e mudam de estado |
| 12 | `docs/00-governance/ASSUMPTIONS.md` | Premissas são verificadas ao longo do tempo |
| 13 | `docs/README.md` | Índice cresce a cada documento novo |
| 14 | `CLAUDE.md` | Regras operacionais evoluem |

**Regra de evolução:** podem ser atualizados livremente durante `F1`..`F10`. A única
restrição é **não contradizer o Core congelado**. Havendo contradição, resolve-se com ADR
de superseção sobre o documento Core — não editando o living doc.

Acrescentar uma pergunta, um risco ou uma decisão é operação normal e **não** abre processo.

## 4. Ownership

| Papel | Responsável |
|-------|-------------|
| Product Owner / Final Decision Authority | **Maike Lima** |
| Autoridade humana final de arquitetura e governança | **Maike Lima**, até delegação formal |

Agentes de IA são **executores e revisores**: propõem, auditam e documentam. Nunca aceitam
ADR, congelam onda, liberam gate, aprovam PR ou mergeiam.

SSOT: `PROJECT-CONSTITUTION.md` Art. 15. Registro: `DECISION-REGISTRY.md` P-006/P-007.

## 5. Findings R1-01..R1-08

| ID | Finding | Status | Evidência |
|----|---------|--------|-----------|
| **R1-01** | Contagem de ADRs errada (`OPEN=7`, `PROPOSED=12`) | **CORRIGIDO** | `docs/adr/README.md` §5 e `QUALITY-GATES.md` §14 agora dizem `OPEN=8`, `PROPOSED=11`, `ACCEPTED=2`, total 21; tabela nominal por estado em `DECISION-REGISTRY.md` §1; varredura global sem ocorrências remanescentes |
| **R1-02** | Waves inconsistentes entre `DOCUMENTATION-FREEZE-WAVES` e `DOCUMENT-STATUS` | **CORRIGIDO** | Core/Living formalizados em `FREEZE-POLICY.md` §2, §3, §7 (SSOT) e reproduzidos em `DOCUMENT-STATUS.md` §4 e `DOCUMENTATION-FREEZE-WAVES.md`; coluna `Lifecycle` adicionada; `PRODUCT-VISION`, `PRODUCT-PRINCIPLES` e `NON-GOALS` movidos para **F0** |
| **R1-03** | Constituição congelava basemap offline não decidido | **CORRIGIDO** | `PROJECT-CONSTITUTION.md` Art. 4 (offline core, 11 garantias) e **Art. 4-A** (basemap = decisão separada); propagado para `PRODUCT-VISION`, `PRODUCT-PRINCIPLES`, `NON-GOALS` §10, `MVP-SCOPE`, `CORE-JOURNEYS` J1/J2, `OFFLINE-FIRST-CONTRACT` §0/§1/§3/§5, `README.md`, `CLAUDE.md` §5 |
| **R1-04** | `COST-GATE` global demais | **CORRIGIDO** | `QUALITY-GATES.md` §12 reescrito como scope-aware, com mapa de escopo por tranche; §14 torna `IMPLEMENTATION-READY` por tranche; Constituição Art. 10 registra o princípio |
| **R1-05** | Q-001 (owners) em aberto | **RESOLVIDO** | `PROJECT-CONSTITUTION.md` Art. 15; `DECISION-POLICY.md` §7; `OPEN-QUESTIONS.md` §"Perguntas resolvidas"; `DECISION-REGISTRY.md` P-006 |
| **R1-06** | Estado de gate `PASS (parcial)` | **CORRIGIDO** | `QUALITY-GATES.md` §0: vocabulário fechado `PASS｜FAIL｜BLOCKED｜PENDING｜NOT-APPLICABLE`; `DOC-CONSISTENCY` = `PENDING`; `HUMAN APPROVAL` registrado à parte |
| **R1-07** | Resumos derivados copiados sem recálculo | **CORRIGIDO** | `DECISION-POLICY.md` §8 (regra + tabela de SSOTs); `QUALITY-GATES.md` §15; `CLAUDE.md` §10-A |
| **R1-08** | Branch com sufixo | **MANTIDA** | `claude/mp-doc-00-foundation-wanppw`, ligada à PR #1. Não renomeada, não duplicada |

## 6. Gates aplicáveis a F0

F0 é uma onda **documental**: não produz código, não escolhe provider, não gera custo.

| Gate | Estado | Justificativa no escopo de F0 |
|------|--------|-------------------------------|
| `DOC-CONSISTENCY` | **PENDING** | Auditoria automatizada sem achados bloqueantes; vira `PASS` com a auditoria humana |
| `MAP-LICENSE-GATE` | `NOT-APPLICABLE` a F0 | F0 não congela basemap (Art. 4-A). Continua **BLOCKED** para F5 |
| `COST-GATE` | `NOT-APPLICABLE` a F0 | F0 não adota provider nem gera custo. Escopos `BLOCKED` permanecem em F5/F8 |
| `ARCH-CONSISTENCY`, `DOMAIN-CONSISTENCY`, `PRIVACY-GATE`, `OFFLINE-GATE`, `SECURITY-GATE`, `API-PORTABILITY-GATE`, `SOCIAL-SAFETY-GATE`, `COMMERCE-GATE`, `AFFILIATE-FRAUD-GATE`, `OPERABILITY-GATE` | `NOT-APPLICABLE` a F0 | Pressupõem código ou ondas posteriores |
| `IMPLEMENTATION-READY-GATE` | **BLOCKED** | Inalterado. F0 não o libera |

`HUMAN APPROVAL` (F0) = **PENDING** — autoridade: Maike Lima.

## 7. Perguntas abertas

**Nenhum item `BLOCKING` em F0.**

| Onda | `BLOCKING` aberto |
|------|-------------------|
| **F0** | **nenhum** |
| F5 | **Q-004, Q-005** (licença de basemap offline) |
| demais | nenhum `BLOCKING`; há pendências de criticidade ALTA por onda |

Q-001 foi resolvida em 2026-09-21 e está registrada em `OPEN-QUESTIONS.md` §"Perguntas
resolvidas", com resposta, data e origem.

As 25 perguntas restantes pertencem a F1..F10 e **não** bloqueiam F0 — F0 não decide
stack, provider, preço nem recurso de produto.

## 8. Baselines constitucionais

Dois ADRs estão `ACCEPTED` e sustentam artigos da Constituição:

| ADR | Artigo | Conteúdo |
|-----|--------|----------|
| **ADR-0003** — Fronteira de API | Art. 2 | `api.makpesca.com.br` é a única fronteira de regra de negócio; clientes nunca acessam o banco diretamente |
| **ADR-0012** — Geo-privacidade | Art. 3 | Visibilidade × precisão, degradação **server-side**, jitter determinístico por (recurso, observador) |

Nenhum outro ADR é pré-requisito de F0. Os 8 ADRs `OPEN` pertencem a F3, F5, F6, F7, F8 e F9.

## 9. Declaração explícita — o que F0 **não** congela

> **F0 não congela provider nem base cartográfica offline.**

Especificamente, F0 **não** decide e **não** promete:

- solução de basemap offline (ADR-0010, `OPEN`, bloqueante de F5);
- provider de mapa online (ADR-0009, `PROPOSED`);
- framework da API, ORM, autenticação, billing, jobs, observabilidade, mensageria;
- preço do PRO, modelo de comissão, fontes de dados ambientais;
- qualquer custo de provider.

O que F0 congela é **postura**: ordem de trabalho, fronteira de API, geo-privacidade
server-side, offline core, portabilidade, regras de decisão e de congelamento,
vocabulário, visão, princípios e não-objetivos.

A distinção **offline core × basemap offline** (Art. 4 e 4-A) é justamente o que torna F0
congelável sem depender de ADR-0010.

## 10. COST-GATE scope-aware

`COST-GATE` deixou de ser um bloqueio global. Avaliação por tranche
(`QUALITY-GATES.md` §12):

| Escopo | Estado | Bloqueia |
|--------|--------|----------|
| Núcleo (conta, ponto, captura, offline core, sync, mídia) | PENDING | MP-00..MP-12 |
| Mapa online | PENDING | MP-06 |
| **Basemap offline** | **BLOCKED** | MP-17 apenas |
| **Billing / PRO** | **BLOCKED** | MP-19 apenas |
| **Dados ambientais** | **BLOCKED** | MP-28, MP-29 apenas |
| Social / Afiliados | PENDING | as respectivas ondas |

Consequência: custo de billing ou de dados ambientais **não** bloqueia a marcação de um
ponto offline. Nenhum custo é ignorado — cada escopo `BLOCKED` segue registrado e bloqueia
a sua própria onda.

Para F0, o gate é `NOT-APPLICABLE`: a onda não adota provider algum.

## 11. Veredito de candidatura

```
F0 CANDIDATE VERDICT: READY_FOR_HUMAN_FREEZE
```

Verificação contra `FREEZE-POLICY.md` §4:

| # | Pré-condição | Resultado |
|---|--------------|-----------|
| 1 | Core Freeze Set em `REVIEW` ou melhor | **OK** — 7/7 em `REVIEW` |
| 2 | Nenhum item `BLOCKING` na onda | **OK** — F0 sem `BLOCKING` |
| 3 | ADRs do Core em `ACCEPTED`/`REJECTED` | **OK** — ADR-0003 e ADR-0012 `ACCEPTED`; nenhum ADR `OPEN` em F0 |
| 4 | Gates do escopo da onda | **OK** — nenhum gate aplicável a F0 está `FAIL` ou `BLOCKED` |
| 5 | Riscos críticos com mitigação | **OK** — `RISK-REGISTER.md` com 47 riscos e mitigação declarada |
| 6 | Perguntas respondidas ou reclassificadas | **OK** — Q-001 resolvida; demais pertencem a F1+ |
| 7 | Core sem promessa dependente de ADR `OPEN` | **OK** — corrigido em R1-03 |
| 8 | Owner definido para todo documento do Core | **OK** — Maike Lima em 7/7 |
| 9 | **Aprovação humana registrada** | **PENDENTE** — é exatamente o que falta |

**Conclusão:** as oito pré-condições técnicas estão satisfeitas. A nona é, por definição,
humana. F0 está pronta para a decisão; a decisão não foi tomada.

## 12. Pendências para a decisão humana

O que a autoridade precisa avaliar antes de congelar:

1. **Concordar com o recorte do Core Freeze Set** (7 documentos). Congelar significa que
   mudá-los exigirá ADR de superseção.
2. **Concordar com a separação offline core × basemap offline** (Art. 4 e 4-A). É a
   mudança conceitual mais relevante da R1: reduz a promessa pública do produto em troca
   de não congelar algo indecidível hoje.
3. **Confirmar o ownership** registrado (Art. 15), inclusive a regra de que agentes de IA
   nunca são owners finais.
4. **Concordar com o `COST-GATE` scope-aware.** É uma flexibilização deliberada: aceita-se
   avançar com custos de ondas futuras ainda desconhecidos.
5. **Revisar visão, princípios e não-objetivos** como texto de produto — são afirmações de
   posicionamento, não fatos verificáveis por ferramenta.
6. Registrar a decisão em `DECISION-REGISTRY.md` e mudar `HUMAN APPROVAL` para `GRANTED`,
   com data.

O que **não** está resolvido e permanece fora de F0: licença de basemap offline (Q-004,
Q-005), pesquisa de concorrência com fontes, custos verificados, e as decisões de stack
(ADR-0006, ADR-0007, ADR-0008).

## 13. Estado após este relatório

| Item | Estado |
|------|--------|
| F0 | `READY_FOR_HUMAN_FREEZE` — nada congelado |
| F5 | **BLOCKED** (Q-004, Q-005) |
| `IMPLEMENTATION-READY-GATE` | **BLOCKED** |
| `HUMAN APPROVAL` (F0) | **PENDING** |
| Código de produto no repositório | **nenhum** |
