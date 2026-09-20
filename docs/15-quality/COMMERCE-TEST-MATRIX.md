---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0014, ADR-0020
---

# Matriz de Testes de Comércio e Billing

## 1. Afiliados — clique e atribuição

| # | Caso | Esperado |
|---|------|----------|
| C-01 | Clique em oferta | Um `Click` e um `Referral` |
| C-02 | Toque duplo rápido | **Um único** click (idempotência) |
| C-03 | Reenvio do mesmo registro de click | Um único click |
| C-04 | Clique em ofertas de parceiros diferentes | Referrals independentes |
| C-05 | Conversão dentro da janela | Atribuída ao último click válido |
| C-06 | Conversão fora da janela | **Não** atribuída |
| C-07 | Conversão sem referral | Sem comissão |
| C-08 | Cupom usado com click de outro parceiro | Cupom tem precedência |

## 2. Afiliados — conversão e comissão

| # | Caso | Esperado |
|---|------|----------|
| C-10 | Mesma conversão informada duas vezes | **Uma única comissão** |
| C-11 | Mesmo `externalOrderRef` em parceiros diferentes | Tratado como conversões distintas |
| C-12 | Conversão estornada após comissão aprovada | Comissão `REVERSED`, histórico preservado |
| C-13 | Conversão rejeitada por antifraude | Sem comissão; caso registrado |
| C-14 | Payout executado sem conciliação | **Bloqueado** |
| C-15 | Comissão já paga reaparecendo | Detectada e bloqueada |
| C-16 | Recalcular comissões de um período | Resultado idêntico (determinismo) |

## 3. Afiliados — fraude

| # | Caso | Esperado |
|---|------|----------|
| C-20 | Muitos cliques do mesmo usuário na mesma oferta | Limitado; sinais registrados |
| C-21 | Conversão instantânea após o clique (tempo irreal) | Sinal de fraude |
| C-22 | Parceiro informando conversões em massa fora do padrão | Sinal + revisão |
| C-23 | Contas múltiplas com o mesmo padrão de dispositivo | Sinal |
| C-24 | Conversão com valor fora do padrão do parceiro | Sinal |

## 4. Ofertas

| # | Caso | Esperado |
|---|------|----------|
| C-30 | Oferta sem validade | Não publicada |
| C-31 | Oferta vencida | Não exibida |
| C-32 | Oferta de parceiro suspenso | Não exibida |
| C-33 | Oferta denunciada como enganosa | Entra em revisão |
| C-34 | Segmentação de oferta | Usa região; **nunca** localização exata |

## 5. Isolamento entre parceiros

| # | Caso | Esperado |
|---|------|----------|
| C-40 | Parceiro A consulta dados do parceiro B | Negado |
| C-41 | Relatório de parceiro | Somente dados próprios, agregados |
| C-42 | Parceiro tenta obter identidade de usuários | Impossível pela API |
| C-43 | Métrica com volume muito baixo | Suprimida (evita dedução) |

## 6. Billing — entitlements

| # | Caso | Esperado |
|---|------|----------|
| C-50 | Assinatura criada | Entitlements PRO concedidos |
| C-51 | **Webhook duplicado** | Entitlement único, sem soma |
| C-52 | Webhooks fora de ordem | Vale o estado final correto |
| C-53 | Cancelamento | Acesso mantido até o fim do período |
| C-54 | Expiração | Volta a FREE; **dados preservados** |
| C-55 | Restore em novo dispositivo | Mesmos entitlements |
| C-56 | Falha de comunicação com o provider | Acesso vigente **não** é revogado |
| C-57 | Reembolso | Entitlement encerrado conforme política |
| C-58 | Compra em iOS e uso em Android | Entitlement segue a conta Makpesca |
| C-59 | Divergência na reconciliação | Alerta e caso aberto |

## 7. Limites e cotas

| # | Caso | Esperado |
|---|------|----------|
| C-60 | FREE excede limite de regiões offline | `QUOTA_EXCEEDED` com orientação |
| C-61 | Downgrade com excedente | Dados preservados, excedente somente leitura |
| C-62 | Limite verificado apenas no cliente | **Servidor também rejeita** |
| C-63 | Criação offline que excede a cota | Aceita com aviso; tratada na sincronização |

## 8. Automação

Casos C-02, C-10, C-51 e C-56 são os **mais críticos** e rodam em CI a cada alteração em
comércio ou billing. Falha bloqueia o merge (`COMMERCE-GATE`, `AFFILIATE-FRAUD-GATE`).
