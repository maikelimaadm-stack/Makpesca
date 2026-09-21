---
Status: REVIEW
Version: 0.2.0
Last Updated: 2026-09-21
Owners: Maike Lima (autoridade humana final)
Related ADRs: —
Wave: F0
Lifecycle: FREEZE-CONTROLLED
---

# Política de Congelamento (Freeze)

## 1. Objetivo

Congelar significa: a partir deste ponto, implementação pode confiar no documento.
Um documento `FROZEN` é contrato.

## 2. O que é congelado: snapshot, não pasta

Uma onda é congelada **por snapshot**, identificado por um commit.

| Conceito | Definição |
|----------|-----------|
| **Snapshot da onda** | O commit exato em que a onda foi congelada |
| **Core Freeze Set** | O conjunto nominal de documentos que vira **contrato** da onda |
| **Living Control Documents** | Documentos de controle que **continuam evoluindo** depois do freeze |

Congelar a onda `Fn` significa: os documentos do **Core Freeze Set de `Fn`**, no
snapshot registrado, são contrato. Nada fora desse conjunto é congelado por tabela.

## 3. Core Freeze Set × Living Control Documents

### Core Freeze Set
- É a lista **nominal** de documentos da onda (não "tudo que está na pasta").
- Ao congelar, cada um recebe `Status: FROZEN` e `Lifecycle: FREEZE-CONTROLLED`.
- Mudança exige ADR de superseção (§5).

### Living Control Documents
- Registros de controle que existem justamente para **acompanhar** o projeto:
  status de documentos, decisões, perguntas abertas, riscos, premissas, índice e
  regras operacionais.
- São `Lifecycle: LIVING`. **Nunca** recebem `FROZEN`.
- Continuam sendo atualizados livremente ao longo de `F1`..`F10` — acrescentar uma
  pergunta, um risco ou uma decisão é operação normal, não alteração de contrato.

### A única regra que os prende

> **Um Living Control Document não pode contradizer o Core congelado.**

Se surgir contradição, ela **não** é resolvida editando o living doc: exige
ADR de superseção sobre o documento Core correspondente (§5). O living doc então
registra a mudança.

Isso é deliberadamente leve: atualizar um registro vivo não abre processo; apenas
contradizer um contrato abre.

## 4. Pré-condições para congelar uma onda

Uma onda (`F0`..`F10`, ver `../16-roadmap/DOCUMENTATION-FREEZE-WAVES.md`) só pode ser
congelada se **todas** as condições abaixo forem verdadeiras:

1. todos os documentos do **Core Freeze Set** da onda estão em `REVIEW` ou melhor;
2. nenhum item `BLOCKING` aberto na onda;
3. todos os ADRs referenciados **pelo Core Freeze Set** estão `ACCEPTED` ou `REJECTED`
   — nunca `OPEN`;
4. os gates aplicáveis **ao escopo da onda** passaram (`../15-quality/QUALITY-GATES.md`);
   gate bloqueado por escopo alheio à onda não a bloqueia;
5. riscos críticos da onda têm mitigação declarada no `RISK-REGISTER.md`;
6. perguntas abertas da onda foram respondidas ou reclassificadas para onda posterior
   com justificativa;
7. o Core Freeze Set não promete recurso que depende de decisão ainda `OPEN`;
8. todo documento do Core Freeze Set tem **owner** definido (Art. 15 da Constituição);
9. **aprovação humana registrada** (`HUMAN APPROVAL = GRANTED`, com data e autoridade).

**Se uma decisão crítica da onda continua aberta: `FREEZE = BLOCKED`.**

O congelamento é **ato humano**. Nenhum agente congela uma onda: um agente pode declarar
a onda `READY_FOR_HUMAN_FREEZE` e apresentar a evidência.

## 4-A. O que o freeze não faz

- Não torna o documento imutável para sempre.
- Não dispensa ADR de superseção.
- Não congela automaticamente documentos de ondas posteriores.

## 5. Como descongelar

1. abrir ADR novo que referencia o documento e o ADR original;
2. marcar o ADR original como `SUPERSEDED`;
3. marcar o documento como `SUPERSEDED` ou publicar nova versão com `Version` incrementada;
4. registrar em `DECISION-REGISTRY.md` com data e motivo;
5. reavaliar os gates impactados;
6. reavaliar slices já planejados que dependiam do documento.

## 6. Incremento de versão

| Mudança | Versão |
|---------|--------|
| Redação, links, exemplos | patch |
| Conteúdo novo sem contradizer o congelado | minor |
| Contradição com conteúdo congelado | major + ADR de superseção |

## 7. Core Freeze Set e Living Control Documents da onda F0

Esta lista é a definição canônica de F0. `DOCUMENT-STATUS.md` e
`../16-roadmap/DOCUMENTATION-FREEZE-WAVES.md` devem reproduzi-la exatamente.

### F0 — Core Freeze Set (7 documentos, `FREEZE-CONTROLLED`)

| # | Documento |
|---|-----------|
| 1 | `docs/00-governance/PROJECT-CONSTITUTION.md` |
| 2 | `docs/00-governance/DECISION-POLICY.md` |
| 3 | `docs/00-governance/FREEZE-POLICY.md` |
| 4 | `docs/00-governance/GLOSSARY.md` |
| 5 | `docs/01-product/PRODUCT-VISION.md` |
| 6 | `docs/01-product/PRODUCT-PRINCIPLES.md` |
| 7 | `docs/01-product/NON-GOALS.md` |

### F0 — Living Control Documents (7 documentos, `LIVING`)

| # | Documento | Por que é vivo |
|---|-----------|----------------|
| 8 | `docs/00-governance/DOCUMENT-STATUS.md` | Registra o estado de todos os documentos, sempre |
| 9 | `docs/00-governance/DECISION-REGISTRY.md` | Recebe cada decisão nova do projeto |
| 10 | `docs/00-governance/OPEN-QUESTIONS.md` | Perguntas abrem e fecham continuamente |
| 11 | `docs/00-governance/RISK-REGISTER.md` | Riscos surgem e mudam de estado |
| 12 | `docs/00-governance/ASSUMPTIONS.md` | Premissas são verificadas ao longo do tempo |
| 13 | `docs/README.md` | Índice cresce a cada documento novo |
| 14 | `CLAUDE.md` | Regras operacionais evoluem com o projeto |

Os documentos 8 a 14 **nunca** recebem `FROZEN`, em nenhuma onda. Eles são
transversais: pertencem ao controle do projeto, não ao contrato de uma onda.

## 8. Estado atual

Nenhum documento está `FROZEN`. Nenhuma onda foi congelada.
A onda `F0` é a candidata corrente — ver `F0-FREEZE-CANDIDATE-REPORT.md`.
`HUMAN APPROVAL` = **PENDING** (autoridade: Maike Lima).
