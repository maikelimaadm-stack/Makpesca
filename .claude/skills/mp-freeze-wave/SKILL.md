---
name: mp-freeze-wave
description: Avalia se uma onda de documentação (F0..F10) pode ser congelada. Use quando pedirem para congelar, revisar ou liberar uma onda.
---

# mp-freeze-wave

## SSOTs
- `docs/16-roadmap/DOCUMENTATION-FREEZE-WAVES.md`
- `docs/00-governance/FREEZE-POLICY.md`
- `docs/00-governance/OPEN-QUESTIONS.md`
- `docs/15-quality/QUALITY-GATES.md`

## Procedimento
1. Identificar os documentos e ADRs da onda.
2. Verificar `Status` de cada documento (precisa estar em `REVIEW` ou melhor).
3. Verificar se há item `BLOCKING` aberto na onda → se houver, **`FREEZE = BLOCKED`**.
4. Verificar se todos os ADRs da onda estão `ACCEPTED` ou `REJECTED` (nunca `OPEN`).
5. Verificar os gates aplicáveis à onda.
6. Verificar riscos críticos da onda com mitigação declarada.
7. Verificar se a auditoria humana foi registrada.

## Regra dura
Decisão crítica aberta ⇒ **FREEZE = BLOCKED**. Não existe congelamento parcial "com ressalva".

## Saída
Para cada condição: ATENDE / NÃO ATENDE + evidência (arquivo + trecho).
Veredito final: `FREEZE PERMITIDO` ou `FREEZE BLOCKED` com a lista do que falta.
