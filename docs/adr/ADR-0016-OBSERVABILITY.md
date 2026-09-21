# ADR-0016 — Observabilidade

- **Status:** **OPEN**
- **Date:** 2026-09-20
- **Onda:** F9

## Context
Um produto com sincronização offline e privacidade crítica precisa de observabilidade
desde o primeiro dia — mas uma observabilidade que **não pode** registrar justamente os
dados mais interessantes para depurar (coordenadas).

## Decision Drivers
- Logs estruturados com correlação.
- **Redação automática de dados sensíveis** — requisito eliminatório.
- Custo previsível.
- Rastreamento de erros em API e mobile.
- Portabilidade do formato.

## Options Considered
| Opção | Prós | Contras |
|-------|------|---------|
| Logs em saída padrão + coletor da plataforma | Simples, barato | Consulta limitada |
| Serviço gerenciado de observabilidade | Recursos completos | Custo; dados em terceiro |
| Stack open-source auto-hospedada | Controle | Operação pesada para a equipe |
| Híbrido (erros em serviço, logs na plataforma) | Equilíbrio | Dois lugares para olhar |

## Decision
**Em aberto (Q-025).** O que já está decidido:

1. o **formato do log é nosso** (JSON estruturado, campos padronizados) — o destino é
   substituível;
2. a **redação de campos sensíveis é feita por nós**, antes de sair da aplicação, nunca
   delegada ao provider;
3. `requestId`/`correlationId` propagados por toda a cadeia, inclusive jobs;
4. crash reporting mobile com filtro obrigatório de dados sensíveis;
5. nenhuma ferramenta que capture respostas da API inteiras.

## Consequences
- `packages/observability` existe desde MP-00.
- Todo log passa por uma camada única, que aplica a redação.
- Falha de observabilidade nunca derruba uma requisição.

## Risks
- **R-061:** logs com dado sensível. É o risco central desta decisão.
- Custo de ingestão crescendo com o volume.
- Observabilidade insuficiente impedindo diagnosticar problemas de sync.

## Security Impact
Logs são fonte de detecção de ataque; ao mesmo tempo, logs demais viram passivo.

## Privacy Impact
**Crítico.** Coordenada em log é vazamento (V2). A redação por nome de campo é obrigatória
e deve ter teste automatizado que busque padrões de coordenada nos logs de um fluxo
completo (PR-30).

## Offline Impact
Métricas de sync são o principal instrumento para saber se o offline está funcionando na
vida real.

## Portability Impact
Formato próprio garante que trocar o destino seja barato.

## Cost Impact
A verificar por volume. Retenção curta reduz custo e risco.

## Operational Impact
Define a capacidade de responder a incidentes.

## Open Questions
- Q-025: qual stack e qual custo?
- Qual retenção por tipo de log?
- Traces desde o início ou depois?
- Como testar automaticamente a ausência de dados sensíveis nos logs?

## Evidence
Requisitos derivados de `OBSERVABILITY.md`. Providers **não avaliados**.

## Supersedes / Superseded By
— / —
