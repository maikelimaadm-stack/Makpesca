# ADR-0005 — Hospedagem Inicial do Backend

- **Status:** PROPOSED
- **Date:** 2026-09-20
- **Onda:** F6

## Context
A API precisa de um lugar para rodar desde o início, com baixo custo operacional e pouca
administração de infraestrutura. O briefing indica a Vercel como hospedagem inicial.

## Decision Drivers
- Baixo esforço operacional no início.
- Ambientes de preview por PR.
- Custo inicial baixo.
- **Capacidade de sair depois sem reescrever** (requisito constitucional, Art. 7).

## Options Considered
| Opção | Prós | Contras |
|-------|------|---------|
| **Vercel (inicial)** | Deploy simples, previews, integrado ao Next.js | Limites de execução, risco de custo em escala, modelo serverless para trabalhos longos |
| Container em provedor de nuvem | Controle, sem limite de execução | Mais trabalho operacional desde o dia 1 |
| Plataforma como serviço com containers | Meio-termo | Um provider a mais para avaliar |
| Servidor próprio | Controle total | Inviável para a equipe atual |

## Decision
Usar **Vercel como hospedagem inicial**, com a API escrita de forma **portável**:
processo HTTP padrão, empacotável em container, sem dependência de recursos proprietários
de runtime, com jobs fora do request.

## Consequences
- `API-PORTABILITY-GATE` passa a ser obrigatório.
- Trabalhos longos vão para fila desde o início (ADR-0015).
- Upload de mídia nunca passa pelo corpo da API.
- Configuração por variáveis de ambiente validadas.

## Risks
- R-034: limites de tempo, payload e execução.
- Custo crescendo com o uso.
- Tentação de usar recursos proprietários por conveniência.

## Security Impact
Superfície reduzida (sem servidor para administrar), mas menos controle de rede.
Secrets ficam na plataforma — ver `SECRETS-POLICY`.

## Privacy Impact
Dados transitam pela plataforma. Avaliar local de processamento para LGPD.

## Offline Impact
Nenhum direto. Mas indisponibilidade da API não pode impedir o uso offline do app.

## Portability Impact
**É o ponto central desta decisão.** A hospedagem é assumida como temporária por
princípio, não por desconfiança.

## Cost Impact
A verificar com fonte e data (A-010). Projeção por usuário ativo é requisito do `COST-GATE`.

## Operational Impact
Deploy e previews simples; observabilidade e jobs precisam de solução complementar.

## Open Questions
- A-010: os limites da plataforma comportam a API pretendida?
- Onde rodam os jobs agendados?
- Qual o custo em cenários de 10 mil e 100 mil usuários ativos?

## Evidence
Baseado no briefing. Limites e preços **não verificados**.

## Supersedes / Superseded By
— / —
