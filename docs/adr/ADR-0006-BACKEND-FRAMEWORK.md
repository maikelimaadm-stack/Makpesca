# ADR-0006 — Framework da API

- **Status:** **OPEN**
- **Date:** 2026-09-20
- **Onda:** F6

## Context
A API em TypeScript precisa de um framework HTTP. A escolha afeta portabilidade,
validação, geração de OpenAPI, velocidade dos testes e desempenho.

## Decision Drivers
- Rodar tanto em ambiente serverless quanto em container.
- Validação integrada com geração de OpenAPI a partir do mesmo esquema.
- Testes rápidos sem emulador de plataforma.
- Desempenho adequado.
- Manutenção ativa e comunidade.
- Simplicidade — não queremos um framework que imponha arquitetura.

## Options Considered
| Opção | Prós esperados | Contras esperados |
|-------|----------------|-------------------|
| **Hono** | Leve, portátil entre runtimes, bom para serverless | Ecossistema menor que o de frameworks veteranos |
| **Fastify** | Maduro, rápido, ecossistema grande, validação por esquema | Orientado a Node tradicional; adaptação a serverless a verificar |
| Express | Onipresente | Antigo; validação e tipagem fracas |
| NestJS | Estrutura pronta | Impõe arquitetura e peso desnecessários aqui |
| Sem framework (Node HTTP) | Controle total | Reinventar roteamento, validação e erros |

**Nenhuma dessas linhas foi medida.** São expectativas a confirmar.

## Decision
**Em aberto.** Nenhuma escolha é feita nesta missão.

Método para decidir:
1. implementar a mesma prova de conceito nos dois principais candidatos: três endpoints
   (um com geo, um com idempotência, um com upload ticket), validação, OpenAPI e testes;
2. medir: tempo de cold start, latência, tempo de suíte de testes, linhas de código,
   facilidade de portar para container;
3. registrar evidências com data;
4. decidir e atualizar este ADR.

## Consequences
Enquanto aberto, MP-01 (API Foundation) não pode começar.

## Risks
- Trocar de framework depois de muitos endpoints é caro.
- Escolher por moda em vez de por medição.
- Framework que amarre a um runtime específico quebraria ADR-0005.

## Security Impact
Qualidade do tratamento de erros, parsing e limites de payload depende do framework.

## Privacy Impact
Indireto: o que o framework registra em log por padrão precisa ser auditado (V2).

## Offline Impact
Indireto, via desempenho do endpoint de sync.

## Portability Impact
**Critério decisivo.** Framework preso a uma plataforma é eliminado.

## Cost Impact
Desempenho afeta custo de execução em modelo serverless.

## Operational Impact
Afeta observabilidade, middlewares e ergonomia de manutenção.

## Open Questions
- Q-006: qual framework?
- Como gerar OpenAPI a partir do mesmo esquema da validação?
- Qual biblioteca de validação (decisão acoplada)?

## Evidence
Nenhuma. **Este ADR não pode sair de `OPEN` sem medição própria registrada.**

## Supersedes / Superseded By
— / —
