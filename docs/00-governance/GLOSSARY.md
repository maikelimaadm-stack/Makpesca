---
Status: REVIEW
Version: 0.2.0
Last Updated: 2026-09-21
Owners: Maike Lima (autoridade humana final)
Related ADRs: —
Wave: F0
Lifecycle: FREEZE-CONTROLLED
---

# Glossário MAKPESCA

Vocabulário único do projeto. Termo usado fora deste glossário é ambiguidade.

## Domínio de pesca

| Termo | Definição |
|-------|-----------|
| **Spot / Ponto** | Local geográfico marcado por um usuário, com visibilidade e precisão próprias |
| **Catch / Captura** | Registro de um peixe capturado, com espécie, medidas, mídia e contexto ambiental |
| **Species / Espécie** | Item do catálogo de espécies, com nome comum, nome científico e região |
| **Bait / Isca** | Isca usada, natural ou artificial, do catálogo |
| **Technique / Técnica** | Modalidade ou técnica empregada |
| **WaterBody / Corpo d'água** | Rio, represa, lago, lagoa, açude, costa ou mar; entidade geográfica de referência |
| **Region / Região** | Recorte geográfico usado para agregação, offline e privacidade |
| **Trip / Pescaria** | Sessão de pesca, potencialmente agrupando capturas e participantes |

## Geo-privacidade

| Termo | Definição |
|-------|-----------|
| **Visibility** | Quem pode ver o objeto: `PRIVATE`, `SHARED`, `PUBLIC` |
| **Precision** | Quanto da localização é revelado: `EXACT`, `APPROXIMATE`, `REGION`, `WATER_BODY_ONLY`, `HIDDEN` |
| **Effective precision** | Precisão resultante após aplicar autorização do solicitante |
| **Degradation** | Transformação server-side da coordenada verdadeira em coordenada divulgável |
| **Jitter** | Deslocamento aleatório aplicado a uma coordenada |
| **Stable jitter** | Jitter determinístico por (objeto, observador) para impedir ataque de média |
| **Averaging attack** | Coletar várias leituras ruidosas do mesmo ponto e tirar a média para recuperar o real |
| **Reidentification** | Reconstruir identidade ou localização real a partir de dados agregados |

## Offline e sincronização

| Termo | Definição |
|-------|-----------|
| **Offline-first** | O app funciona sem rede; a rede é melhoria, não requisito |
| **Outbox** | Fila local de mutações pendentes de envio |
| **Inbox / Pull** | Recebimento de mudanças do servidor desde um cursor |
| **Client-generated id** | Identificador (UUID) criado no dispositivo antes de existir servidor |
| **Idempotency key** | Chave que garante que reenviar uma operação não a aplica duas vezes |
| **Sync cursor** | Marcador de posição do último estado sincronizado |
| **Entity version** | Versão da entidade usada para detectar conflito |
| **Tombstone** | Marca de exclusão propagável, para que delete convirja |
| **Media queue** | Fila local de uploads de mídia com retomada |
| **Clock skew** | Diferença entre relógio do dispositivo e do servidor |
| **Convergence** | Estado final igual entre dispositivos e servidor após sincronizar |

## Arquitetura

| Termo | Definição |
|-------|-----------|
| **SSOT** | Single Source of Truth: documento que manda sobre um assunto |
| **Port** | Interface definida pelo domínio |
| **Adapter** | Implementação de uma port usando um provider concreto |
| **DTO** | Objeto de transporte da API, independente de ORM e de banco |
| **Boundary** | Fronteira que um provider não atravessa |
| **Slice** | Fatia vertical de implementação (`MP-XX`) |
| **Gate** | Verificação obrigatória que bloqueia avanço |
| **Wave / Onda** | Grupo de documentos congelados juntos (`F0`..`F10`) |

## Social

| Termo | Definição |
|-------|-----------|
| **Follow** | Relação assimétrica de acompanhamento |
| **Friend** | Relação mútua confirmada (se adotada) |
| **Community** | Coletivo aberto, regional ou temático, com moderação própria |
| **Group** | Coletivo fechado ou por convite, orientado a organização |
| **Feed** | Linha de publicações relevante para um usuário |
| **Post** | Publicação de usuário; pode referenciar captura, ponto autorizado ou evento |
| **Report** | Denúncia de conteúdo ou pessoa |
| **Block** | Bloqueio interpessoal |

## Comércio

| Termo | Definição |
|-------|-----------|
| **PartnerStore** | Loja parceira |
| **StoreLocation** | Unidade física de uma loja |
| **Offer** | Oferta divulgada por um parceiro |
| **Coupon** | Cupom associado a oferta ou campanha |
| **Referral** | Encaminhamento rastreável de usuário para um parceiro |
| **Click** | Evento de saída rastreado |
| **Attribution** | Ligação entre uma conversão e um referral |
| **Conversion** | Compra ou ação confirmada no parceiro |
| **Commission** | Valor devido pela conversão |
| **Payout** | Pagamento consolidado de comissões |

## Billing

| Termo | Definição |
|-------|-----------|
| **FREE** | Plano gratuito |
| **PRO** | Makpesca PRO, plano pago |
| **Entitlement** | Direito de uso concedido por um plano |
| **Restore** | Recuperação de assinatura existente em novo dispositivo |
| **Grace period** | Janela em que o acesso continua apesar de falha de cobrança |
