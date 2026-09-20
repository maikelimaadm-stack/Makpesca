---
name: mp-architecture-check
description: Verifica fronteiras de arquitetura — cliente x API, domínio x provider, DTO x ORM, dependências entre pacotes. Use em mudanças estruturais.
---

# mp-architecture-check

## SSOTs
- `docs/02-architecture/CONTAINER-ARCHITECTURE.md`
- `docs/02-architecture/COMPONENT-BOUNDARIES.md`
- `docs/02-architecture/PROVIDER-ABSTRACTION.md`
- `docs/adr/ADR-0003-API-BOUNDARY.md`
- `.claude/rules/api-boundaries.md`

## Checklist
1. Nenhum cliente acessa PostgreSQL/Supabase diretamente para regra de negócio.
2. `packages/domain` não importa SDK, ORM, HTTP nem ambiente.
3. DTO não é entidade de ORM.
4. Adapter não contém regra de negócio.
5. Camada HTTP não decide privacidade nem regra.
6. Job assíncrono usa os mesmos casos de uso.
7. Dependências entre pacotes respeitam `REPOSITORY-STRATEGY.md` §4.
8. Provider novo entra por port, com justificativa registrada.
9. Nada proprietário da hospedagem no domínio ou no contrato.
10. Mudança estrutural tem ADR correspondente.

## Sinais de alerta
Import de SDK no domínio; acesso a banco fora de repositório; serialização de localização
fora do Geo Privacy Service; lógica de negócio em rota de Next.js; job com regra própria.

## Saída
Achados + veredito de `ARCH-CONSISTENCY`.
