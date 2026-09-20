# ADR-0014 — Billing

- **Status:** **OPEN**
- **Date:** 2026-09-20
- **Onda:** F8

## Context
O Makpesca PRO precisa ser cobrado. Em aplicativos móveis, a venda de conteúdo digital
normalmente passa pelas lojas, com suas regras e taxas. O produto precisa de entitlements
consistentes: nunca "pagou e não liberou", nunca "liberou sem pagar".

## Decision Drivers
- Consistência de entitlements acima de tudo.
- Custo total (taxa da loja + eventual agregador).
- Esforço de integração e casos de borda (reembolso, restore, grace period, família).
- Conciliação e auditoria.
- Portabilidade para assinatura web no futuro.

## Options Considered
| Opção | Prós | Contras |
|-------|------|---------|
| Integração direta com App Store e Google Play | Sem intermediário nem taxa extra | Duas integrações, validação de recibo própria, muitos casos de borda |
| Agregador (ex.: RevenueCat ou equivalente) | Uma integração, casos de borda resolvidos, relatórios | Custo adicional, dependência, dados em terceiro |
| Assinatura web própria | Melhor margem | Regras das lojas restringem venda externa; verificar |
| Híbrido (lojas agora, web depois) | Pragmático | Dois caminhos para manter |

**Preços, taxas e políticas não foram verificados nesta missão.**

## Decision
**Em aberto (Q-010).** O que **já está decidido**, independentemente do provider:

1. o **Entitlement Service é a fonte única** de acesso;
2. entitlement é **derivado do estado**, nunca incrementado por evento;
3. webhook duplicado não concede acesso duplicado;
4. falha de comunicação **nunca** revoga acesso vigente;
5. nenhum dado de cartão passa pela Makpesca;
6. o cliente nunca decide entitlement;
7. reconciliação periódica é obrigatória.

## Consequences
Enquanto aberto, MP-19 não começa. As regras acima já podem ser documentadas e testadas.

## Risks
- R-050 inconsistência, R-051 webhook duplicado.
- Mudança de regras das lojas.
- Taxas comprometendo a margem do preço pretendido (Q-011).

## Security Impact
Webhooks assinados e verificados; replay rejeitado; idempotência por evento.

## Privacy Impact
Dados de assinatura são C2. Nenhuma localização vai ao provider de billing.

## Offline Impact
Entitlements em cache com validade; sem rede, mantém o último estado — nunca bloquear o
usuário no campo (OFF-9).

## Portability Impact
`BillingPort` + entitlements próprios permitem trocar o provider mantendo os direitos.

## Cost Impact
Taxa da loja + eventual taxa do agregador. Precisa entrar no cálculo do preço do PRO.

## Operational Impact
Conciliação, suporte a "paguei e não liberou", reembolsos.

## Open Questions
- Q-010: agregador ou integração direta?
- Q-011: preço do PRO.
- Quais as taxas reais das lojas para o caso do produto (verificar com fonte e data)?
- Assinatura web é permitida e viável?

## Evidence
Nenhuma verificada. Requisitos derivados de `BILLING-ARCHITECTURE.md`.

## Supersedes / Superseded By
— / —
