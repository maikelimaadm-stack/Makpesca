# ADR-0020 — Atribuição de Afiliados

- **Status:** PROPOSED
- **Date:** 2026-09-20
- **Onda:** F8

## Context
A compra acontece **fora** da Makpesca (site do parceiro, WhatsApp, loja física). Precisamos
ligar uma conversão a um encaminhamento nosso de forma auditável, sem gerar comissão
duplicada e sem expor dados do usuário ao parceiro.

## Decision Drivers
- Auditabilidade (o parceiro precisa entender por que atribuímos ou não).
- Impossibilidade de comissão duplicada.
- Privacidade do usuário.
- Viabilidade com conversão fora da plataforma.
- Resistência a fraude.

## Options Considered
| Opção | Prós | Contras |
|-------|------|---------|
| **Last-click com janela + cupom com precedência** | Simples, previsível, padrão de mercado, auditável | Ignora contribuição de toques anteriores |
| First-click | Valoriza a descoberta | Menos alinhado ao momento da compra |
| Multi-touch com pesos | Mais "justo" | Complexo, difícil de auditar e de explicar ao parceiro |
| Somente cupom | Muito simples e confiável | Perde conversões por link; depende do usuário lembrar |

## Decision
Adotar **last-click dentro de uma janela**, com **cupom tendo precedência** sobre click
quando ambos existirem.

Mecanismos obrigatórios:
1. `Idempotency-Key` no registro de click e de conversão;
2. unicidade `(partnerStoreId, externalOrderRef)` — impede comissão duplicada;
3. janela de atribuição explícita e documentada (proposta: 7 dias, `NEEDS-DECISION`);
4. log de cliques **imutável**;
5. antifraude antes de aprovar comissão;
6. janela de contestação antes do payout;
7. conciliação obrigatória.

## Consequences
- A regra precisa ser comunicada ao parceiro no contrato.
- Toda conversão é reconstituível: click → referral → conversão → comissão → payout.
- Conversões por WhatsApp e loja física dependem de informação do parceiro — a conciliação
  é parte do processo, não exceção.

## Risks
- R-052 fraude de afiliado, R-053 fraude de atribuição, R-054 comissão duplicada.
- Parceiro subnotificando conversões (CF8).
- Disputas sobre janela de atribuição.

## Security Impact
Endpoint de conversão exige autenticação de parceiro/sistema e verificação de assinatura
quando via webhook.

## Privacy Impact
O parceiro **nunca** recebe identidade, contato, localização ou dados de pesca do usuário.
O referral usa identificador próprio.

## Offline Impact
Cliques podem ocorrer sem rede? Não: abrir uma oferta exige conectividade. Ainda assim, o
registro é idempotente para tolerar reenvio.

## Portability Impact
Modelo próprio; integrações com programas de terceiros entram por adapter.

## Cost Impact
Armazenamento de cliques em volume; agregação periódica reduz custo.

## Operational Impact
Conciliação periódica, tratamento de disputas, suspensão de parceiros.

## Open Questions
- Q-019: modelo de comissão (percentual, fixo, por lead).
- Q-020: forma de payout.
- Janela de atribuição definitiva.
- Como tratar conversão sem nenhum click (só cupom divulgado fora)?

## Evidence
Derivado de `ATTRIBUTION.md`. Sem dados reais de conversão.

## Supersedes / Superseded By
— / —
