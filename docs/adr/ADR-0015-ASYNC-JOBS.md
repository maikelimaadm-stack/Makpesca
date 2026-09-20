# ADR-0015 — Jobs Assíncronos

- **Status:** **OPEN**
- **Date:** 2026-09-20
- **Onda:** F9

## Context
Processamento de mídia, notificações, webhooks de billing, agregações, limpeza, exportação
e exclusão de conta não podem acontecer dentro do request — tanto por experiência quanto
por limites da hospedagem serverless (R-034).

## Decision Drivers
- Simplicidade no início (volume baixo).
- Garantia de pelo menos uma entrega + idempotência.
- Retry com backoff e fila morta.
- Visibilidade operacional.
- Portabilidade: não depender do agendador proprietário da plataforma.
- Custo.

## Options Considered
| Opção | Prós | Contras |
|-------|------|---------|
| **Fila no próprio PostgreSQL** | Sem infraestrutura nova, transacional com os dados, simples de observar | Não escala indefinidamente; exige cuidado com concorrência |
| Fila gerenciada do provedor de nuvem | Escala, recursos prontos | Mais um provider; lock-in; custo |
| Redis + biblioteca de filas | Maduro, rápido | Mais infraestrutura para operar |
| Serviço de filas de terceiros | Pouca operação | Custo e dependência |

## Decision
**Em aberto.** Posição preliminar: **começar com fila no próprio PostgreSQL** atrás de
`QueuePort`, medir, e migrar para infraestrutura dedicada apenas quando o volume
justificar. Introduzir um sistema de filas antes de haver volume é overengineering (P10).

O que já está decidido:
1. `QueuePort` isola a implementação;
2. todo job é idempotente (entrega pelo menos uma vez);
3. jobs usam os mesmos casos de uso da API;
4. agendamento é declarado pela aplicação, não preso à plataforma;
5. fila morta com alerta.

## Consequences
MP-11 (Media Sync) depende de jobs funcionando.

## Risks
- Fila no banco competindo por recursos com as consultas do produto.
- Jobs travados sem visibilidade.
- Job não idempotente causando efeito duplicado.

## Security Impact
Jobs rodam com privilégio próprio, menor possível; não expõem endpoints públicos.

## Privacy Impact
Jobs manipulam dados sensíveis (mídia, exclusão de conta). Não podem registrar coordenadas
em log.

## Offline Impact
Indireto: o processamento de mídia influencia quando a foto fica pronta.

## Portability Impact
`QueuePort` + agendamento declarado pela aplicação.

## Cost Impact
Solução simples inicial tem custo quase zero; infraestrutura dedicada tem custo fixo.

## Operational Impact
Precisa de painel de estado: enfileirados, atraso, falhas, fila morta.

## Open Questions
- Qual o limiar de volume para migrar de solução?
- Onde roda o processo consumidor em um modelo serverless?
- Como agendar tarefas periódicas de forma portável?

## Evidence
Nenhuma medição. Decisão preliminar baseada em simplicidade.

## Supersedes / Superseded By
— / —
