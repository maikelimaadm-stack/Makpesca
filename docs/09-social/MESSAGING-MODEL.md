---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0019
---

# Modelo de Mensagens

## 1. Escopo

| Tipo | Fase |
|------|------|
| Conversa individual | Pós-MVP |
| Conversa de grupo | Pós-MVP |
| Mensagem com parceiro comercial | Futuro (provavelmente via WhatsApp do parceiro) |

## 2. Tipos de mensagem

| Tipo | Conteúdo | Observação de privacidade |
|------|----------|---------------------------|
| `TEXT` | Texto | Moderável mediante denúncia |
| `MEDIA` | Foto | Passa pelo pipeline de mídia |
| `CATCH` | Referência a uma captura | Precisão conforme autorização |
| `SPOT` | Referência a ponto **autorizado** | Exige `LocationGrant`; nunca envia coordenada crua |
| `LOCATION` | Localização pontual autorizada | Precisão escolhida, com prazo |
| `EVENT_INVITE` | Convite para evento | — |
| `REACTION` | Reação a uma mensagem | — |

**Compartilhar um ponto por mensagem é uma concessão**, com todas as regras de
`../06-maps-location/LOCATION-SHARING.md` — inclusive revogação.

## 3. Quem pode iniciar conversa

| Regra proposta |
|----------------|
| Usuário que eu sigo pode me enviar mensagem |
| Desconhecido cai em "solicitação de mensagem" |
| Bloqueado não pode enviar nada |
| Limite de solicitações por janela |
| Conta nova tem limites mais rígidos |

## 4. Entrega e estado

Estados: enviada → entregue → lida. Mensagens criadas sem rede ficam pendentes e usam
idempotência para não duplicar no reenvio.

Mensageria **não** faz parte do protocolo de sync offline no MVP: é um domínio próprio,
com fila própria.

## 5. Criptografia

**Decisão aberta (Q-018).** Trade-off honesto:

| Opção | Ganho | Custo |
|-------|-------|-------|
| Sem E2E, cifrado em trânsito e repouso | Permite moderação por denúncia; mais simples | Plataforma tem acesso técnico ao conteúdo |
| Com E2E | Privacidade máxima | Impede moderação, dificulta denúncia, complica multi-dispositivo e backup |

Como o produto tem compromisso com moderação e combate a abuso (P11), a opção sem E2E com
acesso restrito e auditado é a hipótese de trabalho. Decisão exige registro explícito.

## 6. Moderação e abuso

| Mecanismo |
|-----------|
| Denúncia dentro da conversa |
| Bloqueio com efeito imediato |
| Limites de envio por janela |
| Retenção de mensagens denunciadas para apuração |
| Acesso da operação ao conteúdo só mediante caso aberto, com auditoria |
| Sanções: restrição de envio, suspensão |

## 7. Retenção e exclusão

| Item | Política |
|------|----------|
| Mensagem excluída pelo remetente | Some para todos, com marca de "mensagem removida" |
| Conversa excluída pelo usuário | Some para ele; permanece para o outro |
| Exclusão de conta | Mensagens anonimizadas; conteúdo tratado conforme política |
| Retenção geral | **Pendente (Q-016)** |

## 8. Riscos

| Risco | Mitigação |
|-------|-----------|
| Assédio privado | Bloqueio, denúncia, limites |
| Golpe/fraude comercial | Aviso sobre transações fora da plataforma, denúncia |
| Coleta de pontos por engenharia social | Interface deixa claro o que está sendo concedido e permite revogar |
| Spam em massa | Limites, reputação, detecção de padrão |
| Conteúdo ilegal | Denúncia, retenção para apuração, cooperação legal |
