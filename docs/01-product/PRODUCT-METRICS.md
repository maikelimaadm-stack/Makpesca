---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0016
---

# Métricas de Produto

> Toda métrica descrita aqui deve respeitar `../08-security-privacy/PRIVACY-LGPD-CHECKLIST.md`.
> **Nenhuma métrica carrega coordenada exata.** Agregação geográfica mínima é região.

## 1. Métrica-chave da promessa

**Taxa de sincronização íntegra**: percentual de registros criados offline que chegam ao
servidor exatamente uma vez, sem perda e sem duplicação.

Meta de referência: `>= 99,9%`. Abaixo disso, o produto falhou na sua promessa central.

## 2. Métricas de confiança (qualidade não negociável)

| Métrica | Definição | Alvo |
|---------|-----------|------|
| Perda de registro offline | Registros criados no app que nunca chegaram ao servidor | 0 |
| Duplicação em sync | Registros duplicados após reenvio | 0 |
| Vazamento de precisão | Respostas de API com precisão acima da autorizada | 0 |
| Falha de revogação | Acesso mantido após revogar compartilhamento | 0 |
| Mídia órfã | Arquivos sem registro ou registros sem arquivo | tendendo a 0 |

## 3. Métricas de ativação

| Métrica | Definição |
|---------|-----------|
| Cadastro → primeiro ponto | % que cria um ponto em até 7 dias |
| Cadastro → primeira captura | % que registra captura em até 14 dias |
| Primeira sessão offline bem-sucedida | % que usa o app sem rede e sincroniza depois |
| Download de região offline | % que baixa ao menos uma região |

## 4. Métricas de engajamento

| Métrica | Observação |
|---------|-----------|
| Capturas registradas por usuário ativo/mês | Núcleo do valor |
| Pontos criados por usuário | Indicador de confiança na privacidade |
| Publicações por captura registrada | Mede disposição a compartilhar |
| Sessões com mapa aberto | Uso do recurso central |
| Participação em comunidade (pós-MVP) | Relevância local |

## 5. Métricas sociais e de segurança

| Métrica | Observação |
|---------|-----------|
| Denúncias por 1.000 publicações | Saúde da comunidade |
| Tempo até primeira ação de moderação | Capacidade operacional |
| Bloqueios por usuário ativo | Sinal de assédio |
| Taxa de conteúdo removido reincidente | Eficácia da moderação |

## 6. Métricas comerciais (pós-MVP)

| Métrica | Observação |
|---------|-----------|
| Cliques em oferta por usuário ativo | Interesse real |
| Conversões conciliadas / cliques | Qualidade da atribuição |
| Comissões contestadas | Saúde do antifraude |
| Conversão FREE → PRO | Monetização |
| Churn de PRO | Retenção |
| Falhas de entitlement (pagou sem acesso) | Deve ser 0 |

## 7. Métricas técnicas

| Métrica | Observação |
|---------|-----------|
| Latência p95 dos endpoints de mapa e sync | Experiência no campo |
| Taxa de erro 5xx por endpoint | Estabilidade |
| Retentativas de upload de mídia | Qualidade da fila |
| Custo de mapa por usuário ativo | `COST-GATE` |
| Custo de mídia por usuário ativo | `COST-GATE` |
| Consumo de bateria em sessão de mapa | R-047 |

## 8. Regras de instrumentação

1. Evento analítico **nunca** contém coordenada exata, token, e-mail ou telefone.
2. Identificador de usuário em analytics é pseudônimo, não o identificador do banco.
3. Localização em métrica é sempre agregada a região com coorte mínima.
4. Toda nova métrica passa pelo `PRIVACY-GATE`.
