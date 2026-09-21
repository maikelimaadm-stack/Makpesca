---
name: mp-slice-plan
description: Planeja um slice de implementação (MP-XX) com escopo, dependências, gates, testes e critérios de aceite. Use ao preparar trabalho de implementação.
---

# mp-slice-plan

## SSOTs
- `docs/16-roadmap/IMPLEMENTATION-SLICE-ROADMAP.md`
- `docs/16-roadmap/DEPENDENCY-MAP.md`
- `docs/15-quality/QUALITY-GATES.md`

## Antes de tudo
Verificar o `IMPLEMENTATION-READY-GATE`. Se estiver **BLOCKED**, o resultado é um plano,
**não** uma autorização para implementar.

## Procedimento
1. Identificar o slice e sua posição no caminho crítico.
2. Listar dependências: slices anteriores, ADRs, perguntas abertas.
3. Verificar se algum ADR de que depende está `OPEN` → planejamento segue, execução não.
4. Delimitar escopo: o que entra e, explicitamente, **o que não entra**.
5. Listar SSOTs aplicáveis.
6. Listar gates aplicáveis.
7. Listar invariantes tocadas (`docs/03-domain/DOMAIN-INVARIANTS.md`).
8. Listar testes obrigatórios, incluindo cenários das matrizes.
9. Listar riscos endereçados (`RISK-REGISTER.md`).
10. Escrever critérios de aceite verificáveis.

## Modelo de saída
```
Slice: MP-XX — <nome>
Entrega:
Fora do escopo:
Depende de: (slices, ADRs, perguntas)
Bloqueios ativos:
SSOTs:
Gates:
Invariantes tocadas:
Testes obrigatórios:
Riscos endereçados:
Critérios de aceite:
```
