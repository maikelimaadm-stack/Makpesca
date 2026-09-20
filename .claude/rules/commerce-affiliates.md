# Regra — Comércio e Afiliados

## Aplicação
Lojas parceiras, ofertas, cupons, referrals, conversões, comissões, payouts, billing.

## SSOTs
`docs/11-commerce/*`, `docs/12-billing/*`, `docs/adr/ADR-0020-AFFILIATE-ATTRIBUTION.md`,
`ADR-0014-BILLING.md`.

## Regras
1. Comissão **nunca** altera o que é apresentado como "melhor" ao usuário.
2. Conteúdo patrocinado é sempre identificável.
3. Oferta sem validade não é publicada; oferta vencida não é exibida.
4. Click e conversão são **idempotentes**.
5. Unicidade `(parceiro, pedido externo)` — uma conversão gera no máximo uma comissão.
6. Nenhum payout sem antifraude e conciliação.
7. Janela de contestação antes de pagar.
8. Log de cliques e conversões é imutável; correção cria novo registro.
9. Parceiro só acessa dados do próprio parceiro; métricas agregadas e suprimidas em
   volume baixo.
10. Parceiro **nunca** recebe identidade, contato, localização ou dados de pesca do usuário.
11. Segmentação de oferta usa região, nunca localização exata.
12. Entitlement é derivado do estado da assinatura, nunca incrementado por evento.
13. Webhook de billing duplicado não concede acesso duplicado.
14. Falha de comunicação com o provider nunca revoga acesso vigente.
15. Downgrade nunca apaga dados do usuário.

## Proibido
- Vender dados de usuários.
- Expor pontos de pesca a parceiros.
- Destaque pago sem rotulagem.
- Push promocional sem consentimento específico.
- Pagar comissão sem conciliação.
