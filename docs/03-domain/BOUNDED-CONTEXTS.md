---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0012, ADR-0018, ADR-0020
---

# Contextos Delimitados

## 1. Contextos e linguagem

| Contexto | Agregados principais | Linguagem própria |
|----------|---------------------|-------------------|
| **Identity** | `User`, `Session`, `Profile` | conta, sessão, perfil |
| **Fishing** | `Spot`, `Catch`, `Trip` | ponto, captura, pescaria |
| **Catalog** | `Species`, `Bait`, `Technique`, `Gear`, `WaterBody` | espécie, isca, técnica, equipamento |
| **GeoPrivacy** | `LocationPolicy`, `LocationGrant` | visibilidade, precisão, concessão |
| **Sync** | `OutboxItem`, `SyncCursor`, `Tombstone` | mutação, cursor, lápide |
| **Media** | `MediaAsset`, `UploadTicket` | mídia, ticket |
| **Social** | `Post`, `Comment`, `Reaction`, `Follow` | publicação, comentário, reação |
| **Community** | `Community`, `Membership`, `CommunityRule` | comunidade, membro, regra |
| **Group** | `Group`, `GroupMembership`, `Invite` | grupo, convite |
| **Messaging** | `Conversation`, `Message` | conversa, mensagem |
| **Events** | `Event`, `Participation` | evento, participação |
| **Gamification** | `Ranking`, `Achievement`, `Challenge` | ranking, conquista, desafio |
| **Commerce** | `PartnerStore`, `StoreLocation`, `Offer`, `Coupon` | parceiro, unidade, oferta |
| **Affiliates** | `Referral`, `Click`, `Conversion`, `Commission`, `Payout` | referral, conversão, comissão |
| **Billing** | `Subscription`, `Entitlement` | assinatura, direito |
| **Intelligence** | `Insight`, `AggregationJob` | insight, agregação |
| **TrustSafety** | `Report`, `Block`, `ModerationCase`, `Sanction` | denúncia, bloqueio, caso |

## 2. Tradução entre contextos

O mesmo termo muda de significado conforme o contexto. Tradução explícita é obrigatória:

| Termo | Em Fishing | Em Social | Em Intelligence |
|-------|-----------|-----------|-----------------|
| **Captura** | Registro completo com coordenada verdadeira | Publicação com precisão degradada | Linha anônima dentro de uma coorte |
| **Localização** | Coordenada exata | Precisão efetiva para o observador | Célula de agregação |
| **Usuário** | Dono dos dados | Perfil público | Contribuinte anônimo |

Esta tabela é a razão pela qual **Social nunca lê a tabela de pontos diretamente**.

## 3. Relações entre contextos

| De → Para | Tipo | Observação |
|-----------|------|------------|
| Fishing → GeoPrivacy | Conformista | Fishing obedece à política de precisão |
| Social → Fishing | Anticorrupção | Social recebe projeção segura, nunca a entidade crua |
| Sync → todos | Genérico | Sync opera sobre entidades sincronizáveis por contrato |
| Gamification → Fishing | Consulta com elegibilidade | Só capturas elegíveis entram em ranking |
| Intelligence → Fishing | Agregação com coorte mínima | Nunca linha individual |
| Affiliates → Commerce | Parceria | Referral depende de oferta/parceiro |
| Billing → todos | Fornecedor de entitlement | Todos perguntam, ninguém decide sozinho |
| TrustSafety → Social/Community/Messaging | Autoridade | Decisão de moderação sobrepõe visibilidade |

## 4. Entidades sincronizáveis

Apenas estas atravessam o protocolo de sync offline:

`Spot`, `Catch`, `Trip`, `MediaAsset` (metadados), preferências do usuário e catálogos
(somente leitura, pull).

Social, comércio, billing e moderação **não** são sincronizáveis offline no MVP.

## 5. Consistência

| Fronteira | Consistência |
|-----------|--------------|
| Dentro de um agregado | Forte, transacional |
| Entre agregados do mesmo contexto | Forte quando barata, eventual quando não |
| Entre contextos | **Eventual**, por evento |
| Dispositivo ↔ servidor | Eventual, convergente |
