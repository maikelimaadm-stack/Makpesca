---
name: mp-api-review
description: Revisa contrato, versionamento, erros, idempotência, paginação e portabilidade da API. Use ao criar ou alterar endpoints.
---

# mp-api-review

## SSOTs
- `docs/07-api/API-PRINCIPLES.md`, `API-VERSIONING.md`, `API-ERROR-CONTRACT.md`,
  `API-IDEMPOTENCY.md`, `API-ENDPOINT-MATRIX.md`, `API-PORTABILITY.md`
- `.claude/rules/api-boundaries.md`

## Checklist
1. Rota em `/v1`; mudança é compatível ou exige `/v2`?
2. DTO em `packages/contracts`, sem vazar entidade de ORM?
3. Entrada validada por esquema; campos desconhecidos rejeitados?
4. Erro segue o contrato, com `code` estável e sem dado sensível?
5. 404 em vez de 403 quando a existência é sensível?
6. Escrita sincronizável aceita `Idempotency-Key`?
7. Paginação por cursor; consulta geográfica com limite de área?
8. Autorização **por objeto**, com teste negativo?
9. Endpoint com localização passa pelo Geo Privacy Service?
10. OpenAPI gerado do mesmo esquema da validação?
11. Nenhum recurso proprietário da hospedagem no contrato?
12. `API-ENDPOINT-MATRIX.md` atualizada?

## Saída
Achados + veredito de `API-PORTABILITY-GATE` e `DOC-CONSISTENCY` (matriz atualizada).
