---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0011, ADR-0012, ADR-0014, ADR-0020
---

# Invariantes de Domínio

Invariante é regra que **nunca** pode ser violada, em nenhum caminho de código,
em nenhum job, em nenhuma migração.

## 1. Privacidade e localização

| ID | Invariante |
|----|-----------|
| INV-G01 | Coordenada verdadeira nunca é serializada para um observador sem `EXACT` efetivo |
| INV-G02 | Precisão efetiva = menor entre a precisão declarada pelo dono e a autorizada ao observador |
| INV-G03 | Ponto criado nasce `PRIVATE` com precisão `EXACT` apenas para o dono |
| INV-G04 | Publicar uma captura nunca altera a visibilidade do ponto associado |
| INV-G05 | Revogação de concessão tem efeito imediato em toda leitura subsequente |
| INV-G06 | Jitter aplicado a um objeto é determinístico por (objeto, observador) e não é re-sorteado |
| INV-G07 | Nenhuma resposta cacheada com localização pode ser servida a observador com perfil de autorização diferente |
| INV-G08 | Mídia publicada não contém metadados de GPS |
| INV-G09 | Insight publicado respeita coorte mínima e agregação espacial/temporal |

## 2. Propriedade e autorização

| ID | Invariante |
|----|-----------|
| INV-A01 | Toda leitura e escrita de recurso verifica propriedade ou concessão explícita |
| INV-A02 | Identificador de recurso em rota nunca implica autorização |
| INV-A03 | Usuário bloqueado não acessa conteúdo nem contata quem o bloqueou |
| INV-A04 | Ação administrativa gera registro de auditoria imutável |
| INV-A05 | Parceiro só lê dados do próprio parceiro |

## 3. Sincronização

| ID | Invariante |
|----|-----------|
| INV-S01 | Mesma `idempotencyKey` nunca produz dois efeitos |
| INV-S02 | Identificador de entidade é gerado no cliente e preservado pelo servidor |
| INV-S03 | Reenvio de mutação já aplicada retorna o mesmo resultado |
| INV-S04 | `version` de entidade só cresce |
| INV-S05 | Delete gera tombstone com retenção maior que a janela máxima de sync |
| INV-S06 | Entidade excluída não é recriada por sync de dispositivo desatualizado |
| INV-S07 | Registro criado offline é durável localmente antes de a interface confirmar |
| INV-S08 | Falha parcial de lote não aplica efeitos incoerentes; cada item é independente |
| INV-S09 | Tempo do servidor é autoridade de ordenação; tempo do dispositivo é informativo |

## 4. Mídia

| ID | Invariante |
|----|-----------|
| INV-M01 | Mídia só é vinculada após confirmação de upload íntegro (hash confere) |
| INV-M02 | Registro (captura/post) existe mesmo que a mídia ainda esteja na fila |
| INV-M03 | Arquivo sem registro por período definido é órfão e é removido por job |
| INV-M04 | Exclusão de registro agenda a exclusão da mídia correspondente |
| INV-M05 | Upload é sempre autorizado pela API; cliente nunca escreve direto sem ticket |

## 5. Fishing Core

| ID | Invariante |
|----|-----------|
| INV-F01 | Captura pertence a exatamente um usuário |
| INV-F02 | Captura pode existir sem ponto, mas não pode apontar para ponto de outro usuário sem concessão |
| INV-F03 | Medidas (peso, comprimento, quantidade) são não negativas |
| INV-F04 | `caughtAt` não pode ser futuro além da tolerância de clock skew |
| INV-F05 | Espécie livre (`speciesFreeText`) não vira catálogo automaticamente |

## 6. Social e moderação

| ID | Invariante |
|----|-----------|
| INV-T01 | Conteúdo removido por moderação não é servido a ninguém exceto auditoria |
| INV-T02 | Denúncia sempre gera caso rastreável |
| INV-T03 | Sanção ativa restringe efetivamente as ações previstas no seu escopo |
| INV-T04 | Ao bloquear, a relação de follow entre as partes é encerrada |
| INV-T05 | Contadores públicos (curtidas, comentários) não revelam conteúdo oculto |

## 7. Gamificação

| ID | Invariante |
|----|-----------|
| INV-R01 | Só captura elegível entra em ranking |
| INV-R02 | Ranking nunca expõe localização acima da precisão autorizada |
| INV-R03 | Conquista concedida não é revogada sem registro de motivo |
| INV-R04 | Empate em ranking tem critério determinístico |

## 8. Comércio e afiliados

| ID | Invariante |
|----|-----------|
| INV-C01 | Uma conversão externa gera no máximo uma comissão por parceiro |
| INV-C02 | Comissão só é paga após conciliação e verificação antifraude |
| INV-C03 | Click sem referral válido não gera atribuição |
| INV-C04 | Oferta exibida tem validade vigente |
| INV-C05 | Conteúdo patrocinado é identificável pelo usuário |

## 9. Billing

| ID | Invariante |
|----|-----------|
| INV-B01 | Entitlement é derivado do estado da assinatura, nunca incrementado por evento |
| INV-B02 | Webhook duplicado não concede acesso duplicado |
| INV-B03 | Falha de comunicação com o provider nunca revoga entitlement vigente |
| INV-B04 | Restore em novo dispositivo recupera os mesmos entitlements |
| INV-B05 | Cancelamento mantém acesso até o fim do período pago |

## 10. Verificação

Cada invariante deve ter, quando a implementação começar, pelo menos um teste automatizado
correspondente. Invariante sem teste é invariante em risco.
Ver `../15-quality/TEST-STRATEGY.md`.
