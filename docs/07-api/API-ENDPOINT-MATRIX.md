---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0003
---

# Matriz de Endpoints (conceitual)

> **Superfície pretendida, não especificação implementável.** Não há payloads nem
> implementação. Serve para dimensionar escopo e verificar consistência entre domínios.

Colunas: `Fase` (MVP / PÓS / FUT), `Auth` (público, usuário, admin, parceiro, sistema),
`Idem` (aceita `Idempotency-Key`), `Geo` (passa pelo Geo Privacy Service).

## 1. Identidade e conta

| Método | Caminho | Fase | Auth | Idem | Geo |
|--------|---------|------|------|------|-----|
| POST | `/v1/auth/session` | MVP | público | não | não |
| DELETE | `/v1/auth/session` | MVP | usuário | não | não |
| POST | `/v1/auth/refresh` | MVP | usuário | não | não |
| GET | `/v1/me` | MVP | usuário | não | não |
| PATCH | `/v1/me` | MVP | usuário | sim | não |
| GET | `/v1/me/sessions` | MVP | usuário | não | não |
| DELETE | `/v1/me/sessions/{id}` | MVP | usuário | não | não |
| POST | `/v1/me/export` | MVP | usuário | sim | sim |
| POST | `/v1/me/deletion` | MVP | usuário | sim | não |

## 2. Pontos

| Método | Caminho | Fase | Auth | Idem | Geo |
|--------|---------|------|------|------|-----|
| GET | `/v1/spots` | MVP | usuário | não | **sim** |
| POST | `/v1/spots` | MVP | usuário | **sim** | sim |
| GET | `/v1/spots/{id}` | MVP | usuário | não | **sim** |
| PATCH | `/v1/spots/{id}` | MVP | usuário | **sim** | sim |
| DELETE | `/v1/spots/{id}` | MVP | usuário | **sim** | não |
| GET | `/v1/spots/{id}/grants` | MVP | usuário | não | não |
| POST | `/v1/spots/{id}/grants` | MVP | usuário | **sim** | sim |
| DELETE | `/v1/spots/{id}/grants/{grantId}` | MVP | usuário | sim | não |

## 3. Capturas

| Método | Caminho | Fase | Auth | Idem | Geo |
|--------|---------|------|------|------|-----|
| GET | `/v1/catches` | MVP | usuário | não | **sim** |
| POST | `/v1/catches` | MVP | usuário | **sim** | sim |
| GET | `/v1/catches/{id}` | MVP | usuário | não | **sim** |
| PATCH | `/v1/catches/{id}` | MVP | usuário | **sim** | sim |
| DELETE | `/v1/catches/{id}` | MVP | usuário | **sim** | não |
| POST | `/v1/catches/{id}/publication` | MVP | usuário | sim | **sim** |

## 4. Mapa

| Método | Caminho | Fase | Auth | Idem | Geo |
|--------|---------|------|------|------|-----|
| GET | `/v1/map/features` | MVP | usuário | não | **sim** |
| GET | `/v1/map/clusters` | MVP | usuário | não | **sim** |
| GET | `/v1/water-bodies` | PÓS | usuário | não | não |
| GET | `/v1/regions` | MVP | usuário | não | não |
| GET | `/v1/map/offline-regions` | PÓS | usuário | não | não |
| POST | `/v1/map/offline-regions` | PÓS | usuário | sim | não |

## 5. Sincronização

| Método | Caminho | Fase | Auth | Idem | Geo |
|--------|---------|------|------|------|-----|
| POST | `/v1/sync/push` | MVP | usuário | **sim (por item)** | sim |
| GET | `/v1/sync/pull` | MVP | usuário | não | **sim** |
| GET | `/v1/sync/status` | MVP | usuário | não | não |

## 6. Mídia

| Método | Caminho | Fase | Auth | Idem | Geo |
|--------|---------|------|------|------|-----|
| POST | `/v1/media/tickets` | MVP | usuário | **sim** | não |
| POST | `/v1/media/{id}/confirm` | MVP | usuário | **sim** | não |
| GET | `/v1/media/{id}` | MVP | usuário | não | não |
| DELETE | `/v1/media/{id}` | MVP | usuário | sim | não |

## 7. Catálogos

| Método | Caminho | Fase | Auth | Idem | Geo |
|--------|---------|------|------|------|-----|
| GET | `/v1/catalog/species` | MVP | usuário | não | não |
| GET | `/v1/catalog/baits` | MVP | usuário | não | não |
| GET | `/v1/catalog/techniques` | MVP | usuário | não | não |
| GET | `/v1/catalog/versions` | MVP | usuário | não | não |

## 8. Social

| Método | Caminho | Fase | Auth | Idem | Geo |
|--------|---------|------|------|------|-----|
| GET | `/v1/feed` | MVP | usuário | não | **sim** |
| POST | `/v1/posts` | MVP | usuário | sim | sim |
| GET | `/v1/posts/{id}` | MVP | usuário | não | **sim** |
| DELETE | `/v1/posts/{id}` | MVP | usuário | sim | não |
| POST | `/v1/posts/{id}/comments` | MVP | usuário | sim | não |
| POST | `/v1/posts/{id}/reactions` | MVP | usuário | sim | não |
| POST | `/v1/users/{id}/follow` | MVP | usuário | sim | não |
| DELETE | `/v1/users/{id}/follow` | MVP | usuário | sim | não |
| GET | `/v1/users/{id}/profile` | MVP | usuário | não | **sim** |
| POST | `/v1/reports` | MVP | usuário | sim | não |
| POST | `/v1/users/{id}/block` | MVP | usuário | sim | não |

## 9. Comunidades, grupos, mensagens, eventos

| Método | Caminho | Fase | Auth | Idem | Geo |
|--------|---------|------|------|------|-----|
| GET/POST | `/v1/communities` | PÓS | usuário | sim | sim |
| POST | `/v1/communities/{id}/membership` | PÓS | usuário | sim | não |
| GET/POST | `/v1/groups` | PÓS | usuário | sim | não |
| POST | `/v1/groups/{id}/invites` | PÓS | usuário | sim | não |
| GET/POST | `/v1/conversations` | PÓS | usuário | sim | não |
| GET/POST | `/v1/conversations/{id}/messages` | PÓS | usuário | **sim** | **sim** |
| GET/POST | `/v1/events` | PÓS | usuário | sim | **sim** |
| POST | `/v1/events/{id}/participation` | PÓS | usuário | sim | não |

## 10. Gamificação

| Método | Caminho | Fase | Auth | Idem | Geo |
|--------|---------|------|------|------|-----|
| GET | `/v1/rankings` | PÓS | usuário | não | **sim** |
| GET | `/v1/achievements` | PÓS | usuário | não | não |
| GET | `/v1/challenges` | FUT | usuário | não | sim |
| POST | `/v1/challenges/{id}/entries` | FUT | usuário | sim | sim |

## 11. Comércio e afiliados

| Método | Caminho | Fase | Auth | Idem | Geo |
|--------|---------|------|------|------|-----|
| GET | `/v1/partners/stores` | PÓS | usuário | não | não |
| GET | `/v1/partners/stores/{id}` | PÓS | usuário | não | não |
| GET | `/v1/offers` | PÓS | usuário | não | não |
| POST | `/v1/offers/{id}/referrals` | PÓS | usuário | **sim** | não |
| POST | `/v1/affiliate/conversions` | PÓS | sistema/parceiro | **sim** | não |
| GET | `/v1/partner/dashboard` | PÓS | parceiro | não | não |
| GET | `/v1/partner/offers` | PÓS | parceiro | não | não |
| GET | `/v1/partner/reports` | PÓS | parceiro | não | não |

## 12. Billing

| Método | Caminho | Fase | Auth | Idem | Geo |
|--------|---------|------|------|------|-----|
| GET | `/v1/billing/entitlements` | PÓS | usuário | não | não |
| POST | `/v1/billing/receipts` | PÓS | usuário | **sim** | não |
| POST | `/v1/billing/restore` | PÓS | usuário | **sim** | não |
| POST | `/v1/webhooks/billing` | PÓS | sistema | **sim** | não |

## 13. Ambiental e inteligência

| Método | Caminho | Fase | Auth | Idem | Geo |
|--------|---------|------|------|------|-----|
| GET | `/v1/environment/conditions` | PÓS | usuário | não | **sim** |
| GET | `/v1/intelligence/insights` | FUT | usuário (PRO) | não | **sim** |

## 14. Admin

| Método | Caminho | Fase | Auth | Idem | Geo |
|--------|---------|------|------|------|-----|
| GET | `/v1/admin/reports` | PÓS | admin | não | não |
| POST | `/v1/admin/moderation/{caseId}/decision` | PÓS | admin | sim | não |
| GET | `/v1/admin/users/{id}` | PÓS | admin | não | **sim** |
| GET | `/v1/admin/audit` | PÓS | admin | não | não |

## 15. Observações

1. Toda linha marcada com `Geo = sim` **precisa** passar pelo Geo Privacy Service.
2. Toda linha com `Idem = sim` precisa de teste de duplicação.
3. Esta matriz é revisada a cada slice; divergência entre ela e a implementação futura é
   falha do gate `DOC-CONSISTENCY`.
