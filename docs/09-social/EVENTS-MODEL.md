---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0012
---

# Modelo de Eventos

## 1. O que é um evento

Uma pescaria organizada: data, local de encontro, participantes e combinados. É o recurso
social com maior risco de vazamento de localização — por isso tem regras próprias.

## 2. Estrutura

| Campo | Observação |
|-------|------------|
| Organizador | Responsável |
| Comunidade / grupo | Contexto (opcional) |
| Nome e descrição | |
| Data e horário | Com fuso |
| Local | Ponto de encontro, com precisão própria |
| Privacidade | `PUBLIC`, `COMMUNITY`, `GROUP`, `INVITE_ONLY` |
| Limite de participantes | Opcional |
| Participantes | Com estado de confirmação |
| Confirmação | `GOING`, `MAYBE`, `NOT_GOING` |
| Cancelamento | Com motivo e notificação |
| Roteiro | Programação |
| Pontos compartilhados | Concessões explícitas aos participantes |
| Discussão | Conversa do evento |
| Fotos | Mídia vinculada |
| Equipamentos | Lista sugerida / o que cada um leva |
| Ponto de encontro | Local + horário + instruções |

## 3. Localização no evento

| Elemento | Regra |
|----------|-------|
| Ponto de encontro | Precisão definida pelo organizador; `EXACT` apenas para confirmados |
| Pontos de pesca | Cada dono concede individualmente; participar não concede nada |
| Evento público | Ponto de encontro em precisão baixa até a confirmação |
| Após o evento | Concessões temporárias expiram |
| Cancelamento | Concessões encerradas |

## 4. Ciclo de vida

```
rascunho → publicado → confirmações → em andamento → concluído
                    ↘ cancelado
```

Evento concluído mantém fotos, capturas e discussão, respeitando as privacidades
individuais de cada captura.

## 5. Notificações

Convite, confirmação, alteração de data/local, lembrete e cancelamento.
**Nenhuma notificação carrega coordenada** — apenas referência ao evento (GP-R4).

## 6. Riscos

| Risco | Mitigação |
|-------|-----------|
| Evento público revela ponto de pesca | Precisão baixa até confirmação; ponto de encontro ≠ ponto de pesca |
| Participante indesejado | Organizador aprova/remove participantes |
| Evento falso para atrair pessoas | Denúncia, verificação de organizador reincidente |
| Sobrelotação | Limite de participantes |
| Segurança física dos participantes | Aviso de que a plataforma não organiza nem responde pelo evento |

## 7. Relação com capturas

Capturas registradas durante o evento podem ser vinculadas a ele. Vincular **não** altera
a privacidade da captura: cada participante continua decidindo o que publica e com qual
precisão.
