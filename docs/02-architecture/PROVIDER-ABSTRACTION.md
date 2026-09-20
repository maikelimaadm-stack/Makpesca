---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0008, ADR-0013, ADR-0014, ADR-0015, ADR-0016
---

# Abstração de Providers

## 1. Catálogo de ports

| Port | Responsabilidade | Provider inicial |
|------|------------------|------------------|
| `AuthPort` | Autenticar, emitir/validar/revogar sessão, identidade federada | NEEDS-DECISION (ADR-0008) |
| `UserDirectoryPort` | Dados mínimos de identidade | Mesmo do AuthPort |
| `MediaStoragePort` | Autorizar upload, confirmar, ler, excluir, gerar derivativos | NEEDS-DECISION (ADR-0013) |
| `MapTilePort` (cliente) | Fornecer base cartográfica online | Google Maps Platform (proposto) |
| `OfflineMapPort` (cliente) | Fornecer base cartográfica offline | **ABERTO** (ADR-0010) |
| `GeocodingPort` | Endereço ↔ coordenada | NEEDS-DECISION |
| `BillingPort` | Assinaturas, recibos, webhooks | NEEDS-DECISION (ADR-0014) |
| `EnvironmentalDataPort` | Clima, vento, pressão, lua, nível de rio, maré | NEEDS-DECISION (Q-013) |
| `QueuePort` | Enfileirar e processar jobs | NEEDS-DECISION (ADR-0015) |
| `PushPort` | Notificações | FCM/APNs via adapter |
| `ObservabilityPort` | Log, métrica, trace, erro | NEEDS-DECISION (ADR-0016) |
| `FeatureFlagPort` | Flags de rollout e kill switch | Solução simples própria |
| `ClockPort` | Tempo (injeção, testabilidade, clock skew) | Interno |
| `IdPort` | Geração de identificadores | Interno (UUID) |

## 2. Forma das ports (conceitual)

Ports são descritas por **intenção de domínio**, não por capacidade do provider:

| Boa port | Port ruim |
|----------|-----------|
| `autorizarUploadDeMidia(tipo, tamanho, dono)` | `gerarUrlAssinadaS3(bucket, key)` |
| `concederEntitlements(assinatura)` | `processarWebhookRevenueCat(payload)` |
| `obterCondicoesAmbientais(regiao, instante)` | `chamarApiClimaX(lat, lon)` |
| `registrarEventoDeSaida(referral)` | `enviarPixelDoParceiro()` |

## 3. Regras de adapter

1. Adapter traduz erro do provider para erro de domínio conhecido — nunca vaza tipo do SDK.
2. Adapter aplica timeout e política de retry; o domínio não sabe disso.
3. Adapter **não** decide privacidade, autorização, preço ou elegibilidade.
4. Toda chamada externa é observável: duração, resultado, provider, correlação.
5. Falha de provider externo tem comportamento definido: degradar, enfileirar ou falhar
   explicitamente — nunca silenciar.

## 4. Degradação por indisponibilidade

| Provider fora | Comportamento esperado |
|---------------|------------------------|
| Mapa online | Mapa offline (se existir) ou estado vazio com aviso; app continua funcionando |
| Dados ambientais | Mostrar ausência, nunca dado inventado; marcar `qualidade: indisponível` |
| Storage | Registro é aceito; mídia fica na fila; nunca perder o registro |
| Billing | Manter entitlement vigente até expirar; nunca revogar por erro de rede |
| Push | Degradar silenciosamente; conteúdo continua no app |
| Observabilidade | Nunca derrubar requisição por falha de log |

## 5. Dados que nunca vão para provider externo

- Coordenada exata de ponto `PRIVATE` ou `SHARED` não autorizado.
- Conteúdo de mensagem privada (salvo provider de mensageria escolhido, com decisão explícita).
- E-mail/telefone para providers que não precisam deles.
- Qualquer secret em payload de cliente.

## 6. Como trocar um provider

1. Escrever novo adapter implementando a mesma port.
2. Migrar dados, se houver.
3. Rodar os dois em paralelo quando possível (flag).
4. Cortar via feature flag.
5. Remover o adapter antigo.
6. Registrar ADR de superseção.
