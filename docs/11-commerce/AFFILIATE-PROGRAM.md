---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0020
---

# Programa de Afiliados

## 1. Modelo

```
usuário → Makpesca → oferta → link/cupom → loja parceira →
compra externa → conversão → comissão
```

A compra acontece **fora** da Makpesca. Não somos marketplace no início
(`../01-product/NON-GOALS.md` §5).

## 2. Entidades

| Entidade | Papel |
|----------|-------|
| `Referral` | Encaminhamento rastreável (usuário → parceiro, por um canal) |
| `ReferralSession` | Sessão de navegação associada ao referral |
| `Click` | Evento de saída registrado |
| `Attribution` | Ligação entre conversão e referral |
| `Conversion` | Compra/ação confirmada no parceiro |
| `Commission` | Valor devido pela conversão |
| `Payout` | Pagamento consolidado ao/do parceiro |
| `Campaign` | Agrupamento comercial |
| `Coupon` | Cupom rastreável |
| `AffiliateLink` | Link com parâmetros de rastreio |
| `FraudSignal` | Indício de fraude associado a click/conversão |

## 3. Canais de conversão (fase inicial)

| Canal | Como rastrear | Confiabilidade |
|-------|---------------|----------------|
| Site do parceiro | Link com parâmetros + retorno do parceiro | Média-alta |
| WhatsApp | Cupom/código mencionado | Baixa-média |
| Cupom em loja física | Código informado no caixa | Média |
| Link de programa de afiliados de terceiro | Integração do programa | Alta (quando existir) |

**Realidade a assumir:** conversão por WhatsApp e loja física depende de informação do
parceiro. Por isso a conciliação é parte do processo, não uma exceção.

## 4. Fluxo operacional

| Etapa | Responsável |
|-------|-------------|
| Publicar oferta | Parceiro / operação |
| Registrar click | Makpesca (idempotente) |
| Realizar venda | Parceiro |
| Informar conversão | Parceiro (portal/integração) ou conciliação periódica |
| Validar conversão | Makpesca (antifraude) |
| Calcular comissão | Makpesca |
| Aprovar | Makpesca, após janela de contestação |
| Pagar | Conforme contrato |

## 5. Regras

| # | Regra |
|---|-------|
| 1 | Uma conversão externa gera no máximo uma comissão por parceiro (INV-C01) |
| 2 | Click sem referral válido não gera atribuição (INV-C03) |
| 3 | Comissão só é paga após conciliação e antifraude (INV-C02) |
| 4 | Existe janela de contestação antes do pagamento |
| 5 | Devolução/cancelamento da compra estorna a comissão |
| 6 | Usuário sabe que está saindo para um parceiro |
| 7 | Comissão nunca altera a ordenação apresentada como "melhor" (P9) |

## 6. Modelo de comissão

**Decisão aberta (Q-019):** percentual sobre a venda, valor fixo por conversão, valor por
lead qualificado, ou plano de assinatura do parceiro. Cada modelo tem risco e esforço de
conciliação diferentes.

Antes da decisão, o programa não pode ser lançado comercialmente.

## 7. Privacidade

| Regra |
|-------|
| O parceiro não recebe identidade do usuário |
| O referral usa identificador próprio, não o identificador do usuário |
| Nenhum dado de pesca é compartilhado |
| O usuário pode desativar personalização de ofertas |
| Rastreamento é informado na política de privacidade |

## 8. Riscos

Ver `COMMERCE-FRAUD.md` (R-052, R-053, R-054) e `COMMISSIONS-PAYOUTS.md`.

## 9. Fase

Pós-MVP. Começar com **poucos parceiros piloto**, conciliação manual e volume pequeno,
para validar o modelo antes de automatizar.
