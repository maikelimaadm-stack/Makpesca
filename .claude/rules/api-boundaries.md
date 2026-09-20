# Regra — Fronteiras de API

## Aplicação
`apps/api`, `packages/domain`, `packages/contracts`, `packages/database` e qualquer
cliente que consuma dados.

## SSOTs
`docs/07-api/API-PRINCIPLES.md`, `docs/02-architecture/COMPONENT-BOUNDARIES.md`,
`docs/adr/ADR-0003-API-BOUNDARY.md`.

## Regras
1. Cliente **nunca** acessa PostgreSQL/Supabase diretamente para regra de negócio.
2. Fluxo obrigatório: `CLIENTES → api.makpesca.com.br → Application/Domain → Ports/Adapters → Infra`.
3. `packages/domain` não importa SDK, ORM, HTTP nem variável de ambiente.
4. DTO vive em `packages/contracts` e **não** é entidade de ORM.
5. Camada HTTP não contém regra de negócio nem decide precisão de coordenada.
6. Adapter não contém regra de negócio.
7. Job assíncrono usa os mesmos casos de uso da API.
8. Toda rota em `/v1`; quebra de contrato exige `/v2`.
9. Toda escrita sincronizável aceita `Idempotency-Key`.
10. Erro segue `docs/07-api/API-ERROR-CONTRACT.md`; `code` é estável.
11. Paginação por cursor; consultas geográficas com limite de área.
12. Nenhum recurso proprietário da hospedagem no contrato público.

## Proibido
- Endpoint que serialize entidade de banco diretamente.
- Regra de negócio em rota de Next.js.
- Concatenação de SQL.
- Filtro dinâmico livre vindo do cliente.
