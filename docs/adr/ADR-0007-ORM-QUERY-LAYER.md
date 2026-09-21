# ADR-0007 — ORM / Camada de Query

- **Status:** **OPEN**
- **Date:** 2026-09-20
- **Onda:** F3

## Context
A camada de acesso a dados precisa lidar com PostGIS, migrações versionadas, consultas
geoespaciais eficientes e mapeamento para entidades de domínio — **sem** que DTOs virem
entidades de ORM.

## Decision Drivers
- **Suporte real a PostGIS** (tipos geográficos, funções espaciais, índices).
- Migrações versionadas e reversíveis.
- Controle sobre a consulta gerada (desempenho geoespacial).
- Tipagem forte sem acoplar o domínio.
- Facilidade de escrever SQL puro quando necessário.
- Maturidade e manutenção.

## Options Considered
| Opção | Prós esperados | Contras esperados |
|-------|----------------|-------------------|
| **Drizzle** | Próximo do SQL, tipado, migrações | Ecossistema mais novo; suporte a PostGIS a verificar |
| **Prisma** | Ergonomia, ferramentas maduras | Abstração maior; suporte a PostGIS historicamente limitado — **a verificar** |
| **Kysely** | Construtor de consultas tipado, muito próximo do SQL | Sem ORM completo; mais código manual |
| SQL puro + mapeamento manual | Controle total | Muito código repetitivo; risco de erro |

**Nada acima foi verificado nesta missão.** O suporte a PostGIS é o critério eliminatório
e precisa de teste prático, não de leitura de documentação apenas.

## Decision
**Em aberto.** Provável formato da decisão: um construtor de consultas tipado para o
grosso do trabalho **+ SQL explícito** para consultas geoespaciais críticas.

Método:
1. escrever as cinco consultas geoespaciais mais importantes (viewport, proximidade,
   contenção em polígono, agregação por célula, junção com corpos d'água) em cada candidato;
2. verificar tipos, plano de execução e legibilidade;
3. testar migrações com colunas de geometria e índices GiST;
4. registrar evidências com data.

## Consequences
Enquanto aberto, MP-02 (Data Foundation) não pode começar.

## Risks
- Escolher uma camada que não suporte PostGIS bem e descobrir tarde.
- Abstração que esconda consultas caras.
- Acoplamento do domínio às entidades da ferramenta.

## Security Impact
Consultas parametrizadas são obrigatórias. Qualquer caminho que permita concatenação de
SQL é eliminado.

## Privacy Impact
A camada acessa coordenadas verdadeiras. Regra: repositórios retornam entidades de
domínio; **a serialização para fora passa obrigatoriamente pelo Geo Privacy Service**.

## Offline Impact
Nenhum direto (o SQLite local tem estratégia própria).

## Portability Impact
Deve permanecer em SQL padrão + PostGIS, sem recursos proprietários de hospedagem.

## Cost Impact
Consultas ineficientes aumentam custo de banco diretamente.

## Operational Impact
Migrações precisam ser reversíveis e executáveis fora da plataforma.

## Open Questions
- Q-007: qual camada suporta PostGIS adequadamente na prática?
- Como garantir que DTO nunca seja a entidade da ferramenta?
- Estratégia de migração: ferramenta própria da biblioteca ou independente?

## Evidence
Nenhuma. **Verificação prática obrigatória antes de `ACCEPTED`.**

## Supersedes / Superseded By
— / —
