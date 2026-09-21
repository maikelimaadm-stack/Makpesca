---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0003
---

# Contrato de Erros da API

## 1. Formato

Proposta: adotar **RFC 9457 (Problem Details for HTTP APIs)** como formato base, com
extensões próprias. Vantagens: padrão conhecido, extensível, bom para ferramentas.
Estado: `PROPOSED` — a confirmar no ADR-0006.

Forma conceitual da resposta de erro:

| Campo | Origem | Descrição |
|-------|--------|-----------|
| `type` | RFC 9457 | URI estável que identifica o tipo do problema |
| `title` | RFC 9457 | Resumo legível, estável |
| `status` | RFC 9457 | Código HTTP |
| `detail` | RFC 9457 | Detalhe do caso, **sem dado sensível** |
| `instance` | RFC 9457 | Referência da ocorrência |
| `code` | extensão | Código estável da aplicação (ex.: `SPOT_NOT_FOUND`) |
| `requestId` | extensão | Correlação para suporte |
| `errors[]` | extensão | Lista de problemas de validação por campo |
| `retryable` | extensão | Se faz sentido repetir |
| `retryAfterSeconds` | extensão | Quando repetir |

O cliente deve programar contra `code`, não contra a mensagem.

## 2. Mapeamento de status

| Status | Uso |
|--------|-----|
| 400 | Requisição malformada |
| 401 | Não autenticado ou credencial inválida/expirada |
| 403 | Autenticado, sem permissão |
| 404 | Recurso inexistente **ou** existência não revelável |
| 409 | Conflito (versão, unicidade, estado inválido) |
| 410 | Recurso removido definitivamente |
| 413 | Payload grande demais |
| 415 | Tipo de mídia não suportado |
| 422 | Semanticamente inválido (regra de negócio) |
| 423 | Recurso bloqueado (ex.: conta em moderação) |
| 429 | Limite de taxa |
| 500 | Erro inesperado |
| 502/503/504 | Dependência externa ou indisponibilidade |

## 3. 403 vs 404 — regra de privacidade

Quando revelar a existência do recurso já é vazamento (pontos privados, conteúdo de
terceiros, mensagens), a resposta é **404**, não 403.

`403` é usado quando a existência já é conhecida legitimamente pelo solicitante
(ex.: membro de grupo sem permissão administrativa).

Essa regra é obrigatória e testada (`PRIVACY-TEST-MATRIX`).

## 4. Erros de domínio

| `code` | Status | Quando |
|--------|--------|--------|
| `VALIDATION_FAILED` | 422 | Entrada inválida |
| `UNAUTHENTICATED` | 401 | Sem credencial válida |
| `FORBIDDEN` | 403 | Sem permissão, existência já conhecida |
| `NOT_FOUND` | 404 | Inexistente ou não revelável |
| `VERSION_CONFLICT` | 409 | `baseVersion` desatualizada no sync |
| `DUPLICATE_REQUEST` | 200/409 | Idempotência — ver `API-IDEMPOTENCY.md` |
| `RESOURCE_DELETED` | 410 | Tombstone |
| `RATE_LIMITED` | 429 | Excesso de requisições |
| `ENTITLEMENT_REQUIRED` | 403 | Recurso exige PRO |
| `QUOTA_EXCEEDED` | 403 | Limite do plano atingido |
| `MEDIA_UPLOAD_INVALID` | 422 | Hash/tipo/tamanho inválido |
| `GRANT_REVOKED` | 403 | Concessão revogada |
| `MODERATION_BLOCKED` | 423 | Conteúdo ou conta restrita |
| `PROVIDER_UNAVAILABLE` | 503 | Dependência externa fora |
| `INTERNAL_ERROR` | 500 | Inesperado |

## 5. O que uma mensagem de erro nunca contém

- coordenada de qualquer precisão;
- token, secret, credencial, chave;
- e-mail ou telefone de terceiro;
- consulta SQL, caminho de arquivo, stack trace;
- nome de tabela ou detalhe interno de esquema;
- informação que revele existência de recurso privado.

## 6. Erros de lote (sync)

Em operações de lote, o status HTTP reflete o transporte, não os itens. Cada item traz seu
próprio resultado e erro. Um item inválido **não** invalida o lote (INV-S08).

## 7. Erros no cliente

O app traduz `code` para mensagem em português, com ação clara. Erro desconhecido tem
mensagem genérica e `requestId` visível para suporte — nunca detalhe técnico cru.
