---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: —
---

# Política de Congelamento (Freeze)

## 1. Objetivo

Congelar significa: a partir deste ponto, implementação pode confiar no documento.
Um documento `FROZEN` é contrato.

## 2. Pré-condições para congelar uma onda

Uma onda (`F0`..`F10`, ver `../16-roadmap/DOCUMENTATION-FREEZE-WAVES.md`) só pode ser
congelada se **todas** as condições abaixo forem verdadeiras:

1. todos os documentos da onda estão em `REVIEW` ou melhor;
2. nenhum item `BLOCKING` aberto na onda;
3. todos os ADRs referenciados pela onda estão `ACCEPTED` ou `REJECTED` — nunca `OPEN`;
4. os gates aplicáveis da onda passaram (`../15-quality/QUALITY-GATES.md`);
5. riscos críticos da onda têm mitigação declarada no `RISK-REGISTER.md`;
6. perguntas abertas da onda foram respondidas ou reclassificadas para onda posterior
   com justificativa;
7. auditoria humana registrada.

**Se uma decisão crítica da onda continua aberta: `FREEZE = BLOCKED`.**

## 3. O que o freeze não faz

- Não torna o documento imutável para sempre.
- Não dispensa ADR de superseção.
- Não congela automaticamente documentos de ondas posteriores.

## 4. Como descongelar

1. abrir ADR novo que referencia o documento e o ADR original;
2. marcar o ADR original como `SUPERSEDED`;
3. marcar o documento como `SUPERSEDED` ou publicar nova versão com `Version` incrementada;
4. registrar em `DECISION-REGISTRY.md` com data e motivo;
5. reavaliar os gates impactados;
6. reavaliar slices já planejados que dependiam do documento.

## 5. Incremento de versão

| Mudança | Versão |
|---------|--------|
| Redação, links, exemplos | patch |
| Conteúdo novo sem contradizer o congelado | minor |
| Contradição com conteúdo congelado | major + ADR de superseção |

## 6. Estado atual

Nenhum documento está `FROZEN`. Nenhuma onda foi congelada.
A onda `F0` é a próxima candidata, após auditoria humana do MP-DOC-00 v2.
