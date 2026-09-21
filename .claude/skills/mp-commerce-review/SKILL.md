---
name: mp-commerce-review
description: Revisa lojas, ofertas, afiliados, atribuição, comissões e billing — com foco em fraude, duplicação e privacidade. Use ao alterar comércio ou assinatura.
---

# mp-commerce-review

## SSOTs
- `docs/11-commerce/*` (em especial `ATTRIBUTION.md`, `COMMERCE-FRAUD.md`)
- `docs/12-billing/*` (em especial `ENTITLEMENTS.md`)
- `docs/15-quality/COMMERCE-TEST-MATRIX.md`
- `.claude/rules/commerce-affiliates.md`

## Checklist — afiliados
1. Click e conversão são idempotentes?
2. Unicidade `(parceiro, pedido externo)` garantida?
3. Janela de atribuição explícita e auditável?
4. Antifraude antes de aprovar comissão?
5. Janela de contestação antes do payout?
6. Log de click imutável?
7. Estorno preserva histórico?
8. Parceiro isolado, sem acesso a dado de usuário?

## Checklist — billing
9. Entitlement derivado do estado, nunca incrementado?
10. Webhook duplicado não concede acesso duplicado?
11. Falha de rede não revoga acesso vigente?
12. Restore recupera os mesmos entitlements?
13. Downgrade não apaga dados?
14. Limite verificado também no servidor?

## Checklist — oferta
15. Validade e condições obrigatórias; oferta vencida não aparece?
16. Conteúdo patrocinado identificado?
17. Segmentação por região, nunca por localização exata?

## Saída
Achados + veredito de `COMMERCE-GATE` e `AFFILIATE-FRAUD-GATE`.
