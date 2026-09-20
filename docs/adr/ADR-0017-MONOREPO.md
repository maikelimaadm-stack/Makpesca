# ADR-0017 — Monorepo

- **Status:** PROPOSED
- **Date:** 2026-09-20
- **Onda:** F2

## Context
O projeto terá cinco aplicações (mobile, web, admin, partners, api) e pacotes
compartilhados (domínio, contratos, banco, observabilidade, UI). O contrato entre API e
clientes precisa ser compartilhado com segurança de tipos.

## Decision Drivers
- Contrato único compartilhado entre API e quatro clientes.
- Refatoração atômica de domínio e contratos.
- Padronização de lint, tipos e testes.
- Equipe pequena.
- Suporte a Expo no mesmo repositório.

## Options Considered
| Opção | Prós | Contras |
|-------|------|---------|
| **Monorepo com pnpm workspace + Turborepo** | Contrato compartilhado, build incremental, um repositório | Configuração inicial; build pode ficar lento sem cache |
| Monorepo com workspaces puros (sem orquestrador) | Mais simples | Sem cache/build por afetados |
| Nx | Recursos completos | Mais opinativo e pesado |
| Múltiplos repositórios | Isolamento | Versionar e publicar contratos entre repositórios é atrito constante |

## Decision
Adotar **monorepo**, com **pnpm workspace + Turborepo** como candidato preferencial
(Q-024, criticidade baixa). A estrutura está em `REPOSITORY-STRATEGY.md`.

**Nenhum app é criado nesta fase.**

## Consequences
- Regras de dependência entre pacotes verificadas em CI.
- `packages/domain` não depende de nada.
- Pipeline por pacote afetado.
- Mobile tem pipeline próprio de build.

## Risks
- Acoplamento acidental entre pacotes — mitigado por verificação de dependências.
- Build lento com o crescimento — mitigado por cache e execução por afetados.
- Complexidade de configuração inicial.

## Security Impact
Um único lugar para auditar dependências e varrer segredos.

## Privacy Impact
Nenhum direto.

## Offline Impact
Nenhum direto.

## Portability Impact
Positivo: pacotes compartilhados isolam domínio e contratos das aplicações.

## Cost Impact
Baixo. Evitar cache pago obrigatório é critério de escolha do orquestrador.

## Operational Impact
Um repositório, um fluxo de PR, um conjunto de verificações.

## Open Questions
- Q-024: Turborepo ou alternativa?
- Como versionar o contrato para clientes móveis antigos?
- Pipeline de build do Expo dentro do monorepo funciona bem?

## Evidence
Baseado na estrutura proposta no briefing. Sem medição.

## Supersedes / Superseded By
— / —
