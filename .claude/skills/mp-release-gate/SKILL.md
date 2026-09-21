---
name: mp-release-gate
description: Avalia todos os gates de qualidade antes de liberar algo — incluindo o IMPLEMENTATION-READY-GATE. Use antes de qualquer liberação, congelamento final ou lançamento.
---

# mp-release-gate

## SSOT
`docs/15-quality/QUALITY-GATES.md` — este skill **não** define gates, apenas os avalia.

## Gates a avaliar
`DOC-CONSISTENCY`, `ARCH-CONSISTENCY`, `DOMAIN-CONSISTENCY`, `PRIVACY-GATE`,
`OFFLINE-GATE`, `MAP-LICENSE-GATE`, `API-PORTABILITY-GATE`, `SECURITY-GATE`,
`SOCIAL-SAFETY-GATE`, `COMMERCE-GATE`, `AFFILIATE-FRAUD-GATE`, `COST-GATE`,
`OPERABILITY-GATE`, `IMPLEMENTATION-READY-GATE`.

## Procedimento
1. Para cada gate aplicável ao escopo, coletar **evidência** (arquivo, teste, comando, ADR).
2. Marcar: `PASS` / `PENDING` / `BLOCKED` — nunca "provavelmente".
3. Um gate `BLOCKED` **bloqueia a liberação**. Não existe exceção informal.
4. Verificar o `IMPLEMENTATION-READY-GATE` contra as oito condições listadas no SSOT.
5. Se algo faltar, listar exatamente o que falta e quem/ o que resolve.

## Regra dura
Liberar um gate exige decisão registrada em
`docs/00-governance/DECISION-REGISTRY.md`. Skill nenhum libera gate sozinho.

## Saída
Tabela `gate → estado → evidência → o que falta`, seguida do veredito de liberação.
