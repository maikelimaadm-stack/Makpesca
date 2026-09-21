---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0020
---

# Fraude no Comércio e Afiliados

## 1. Quem frauda e por quê

| Ator | Motivação |
|------|-----------|
| Usuário | Vantagem em cupom, prêmio, ou ganho se houver programa de indicação |
| Parceiro | Comissão indevida ou inflar métricas; ou o oposto: subnotificar conversões |
| Terceiro automatizado | Explorar o programa em escala |
| Conluio usuário-parceiro | Conversões inventadas |

## 2. Vetores

| # | Vetor | Descrição | Detecção |
|---|-------|-----------|----------|
| CF1 | Auto-clique | Usuário clica repetidamente na própria oferta | Idempotência + limite por usuário/janela |
| CF2 | Click stuffing | Cliques gerados sem intenção real | Taxa de conversão anômala, padrão temporal |
| CF3 | Conversões inventadas | Parceiro informa pedidos que não existiram | Conciliação, amostragem, verificação de valores |
| CF4 | Pedido duplicado | Mesmo pedido informado duas vezes | Unicidade `(parceiro, pedido)` |
| CF5 | Atribuição roubada | Parceiro reivindica conversão de outro | Regra de atribuição auditável, log imutável |
| CF6 | Contas falsas | Criar contas para gerar cliques | Sinais de dispositivo, verificação, limites |
| CF7 | Cupom vazado/compartilhado em massa | Uso fora do público pretendido | Limite de uso, monitoramento |
| CF8 | Subnotificação | Parceiro esconde conversões para não pagar | Amostragem, comparação com cliques, contrato |
| CF9 | Estorno abusivo | Cancelar compras após comissão | Estorno automático + histórico de reincidência |
| CF10 | Oferta falsa para atrair cliques | Oferta que não existe na loja | Denúncia, verificação, suspensão |

## 3. Sinais de fraude (`FraudSignal`)

Volume de cliques por usuário/janela, taxa de conversão fora do padrão do parceiro,
intervalo curtíssimo entre click e conversão, valores repetidos, pedidos sequenciais,
mesma origem de dispositivo em muitas contas, conversões concentradas em horário atípico,
discrepância entre cliques e conversões informadas.

## 4. Controles obrigatórios

| # | Controle |
|---|----------|
| 1 | Idempotência em click e conversão |
| 2 | Unicidade `(parceiro, pedido externo)` |
| 3 | Janela de atribuição explícita |
| 4 | Janela de contestação antes do payout |
| 5 | Antifraude executado antes de aprovar comissão |
| 6 | Revisão humana acima de um limiar de valor |
| 7 | Log imutável de cliques e conversões |
| 8 | Conciliação periódica obrigatória |
| 9 | Contrato com o parceiro prevendo auditoria e estorno |
| 10 | Suspensão de parceiro reincidente |

**Nenhum payout é executado sem 5, 6 (quando aplicável) e 8.**

## 5. Resposta

| Gravidade | Ação |
|-----------|------|
| Sinal isolado | Marcar e observar |
| Padrão | Segurar comissões daquele período, abrir caso |
| Fraude confirmada (usuário) | Sanção na conta, perda de benefícios |
| Fraude confirmada (parceiro) | Suspensão, estorno, encerramento de contrato |
| Fraude em escala | Suspender o programa e revisar controles |

## 6. Proteção do usuário

O usuário não pode ser prejudicado por fraude de parceiro: se uma oferta não é honrada,
a resposta é contra o parceiro. A Makpesca **não** repassa o prejuízo ao usuário nem
expõe seus dados na apuração.

## 7. Métricas de saúde

Taxa de cliques por usuário ativo, taxa de conversão por parceiro (com desvio),
comissões contestadas, comissões estornadas, casos de fraude abertos e confirmados,
tempo médio de conciliação.
