---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0012, ADR-0018, ADR-0020
---

# Catálogo de Entidades

> Modelo **conceitual**. Não é schema, não é DDL, não é ORM. Nenhum tipo de banco aqui.

Convenções: `id` é UUID gerado no cliente quando a entidade é criável offline.
Toda entidade sincronizável tem `createdAt`, `updatedAt`, `deletedAt?`, `version`,
`clientId`, `lastSyncedAt?`.

## 1. Identity

### User
`id`, `handle`, `email` (privado), `phone?` (privado), `status`, `createdAt`,
`authProviderRef` (opaco), `locale`, `termsAcceptedAt`, `deletedAt?`

### Profile
`userId`, `displayName`, `bio?`, `avatarMediaId?`, `coverMediaId?`, `city?`, `regionId?`,
`favoriteSpeciesIds[]`, `visibility`, `statsSnapshot?`, `updatedAt`

### Session
`id`, `userId`, `deviceId`, `deviceLabel`, `createdAt`, `lastSeenAt`, `revokedAt?`,
`ipCountry?` (sem IP completo em log)

## 2. Fishing Core

### Spot (ponto)
| Campo | Observação |
|-------|-----------|
| `id` | UUID do cliente |
| `ownerId` | dono |
| `name` | rótulo do usuário |
| `description?` | |
| `location` | **coordenada verdadeira**, nunca serializada sem política |
| `locationSource` | `GPS` / `MAP_PICK` / `IMPORT` / `MANUAL` |
| `locationAccuracyMeters?` | precisão do sensor |
| `waterBodyId?` | corpo d'água |
| `regionId?` | região derivada |
| `spotType?` | estrutura, laje, poço, barranco etc. |
| `visibility` | `PRIVATE` \| `SHARED` \| `PUBLIC` |
| `sharedPrecision` | `EXACT` \| `APPROXIMATE` \| `REGION` \| `WATER_BODY_ONLY` \| `HIDDEN` |
| `tags[]` | |
| `isFavorite` | |
| `createdAt/updatedAt/deletedAt/version` | sync |

### Catch (captura)
| Campo | Observação |
|-------|-----------|
| `id` | UUID do cliente |
| `userId` | |
| `mediaIds[]` | fotos |
| `speciesId?` | catálogo |
| `speciesFreeText?` | quando não identificada |
| `weightGrams?` | |
| `lengthMm?` | |
| `quantity` | default 1 |
| `baitId?` / `baitFreeText?` | |
| `techniqueId?` | |
| `gearNotes?` | |
| `caughtAt` | data/hora informada |
| `caughtAtDeviceTz` | fuso do dispositivo |
| `location?` | coordenada verdadeira |
| `locationSource` | origem da localização |
| `spotId?` | ponto associado |
| `waterBodyId?` | |
| `notes?` | |
| `environmentSnapshotId?` | condições no momento |
| `recordSource` | `LIVE` (no local) \| `MANUAL_LATER` \| `IMPORT` |
| `visibility` | independente do ponto |
| `sharedPrecision` | independente do ponto |
| `publicationStatus` | `DRAFT` \| `PUBLISHED` \| `UNPUBLISHED` \| `REMOVED` |
| `moderationStatus` | `NONE` \| `PENDING` \| `APPROVED` \| `REJECTED` |
| `released` | soltou o peixe? |
| `createdAt/updatedAt/deletedAt/version` | sync |

### Trip (pescaria)
`id`, `userId`, `title?`, `startedAt`, `endedAt?`, `waterBodyId?`, `regionId?`,
`eventId?`, `participantIds[]?`, `notes?`, campos de sync

## 3. Catalog

### Species
`id`, `commonName`, `alternateNames[]`, `scientificName?`, `family?`, `regionsIds[]`,
`waterType` (`FRESH`/`SALT`/`BOTH`), `imageMediaId?`, `status`, `source`

### Bait / Technique / Gear
`id`, `name`, `type`, `description?`, `status`

### WaterBody (corpo d'água)
`id`, `name`, `type` (`RIO`/`REPRESA`/`LAGO`/`LAGOA`/`ACUDE`/`COSTA`/`MAR`),
`geometry` (linha/polígono), `regionIds[]`, `source`, `license`

### Region
`id`, `name`, `level` (`PAIS`/`ESTADO`/`MUNICIPIO`/`BACIA`/`CUSTOM`), `geometry`,
`parentRegionId?`

## 4. Geo & Privacy

### LocationPolicy (valor, não tabela)
`visibility`, `precision`, derivada por objeto e observador.

### LocationGrant (concessão)
`id`, `resourceType` (`SPOT`/`CATCH`/`LIVE_LOCATION`), `resourceId`, `grantorId`,
`granteeType` (`USER`/`GROUP`/`EVENT`/`COMMUNITY`), `granteeId`, `precision`,
`expiresAt?`, `revokedAt?`, `createdAt`

## 5. Sync

### OutboxItem (local)
`id`, `entityType`, `entityId`, `operation`, `payload`, `idempotencyKey`, `attempts`,
`nextAttemptAt`, `lastError?`, `createdAt`

### SyncCursor
`userId`, `deviceId`, `cursor`, `updatedAt`

### Tombstone
`entityType`, `entityId`, `deletedAt`, `retainUntil`

## 6. Media

### MediaAsset
`id`, `ownerId`, `kind` (`IMAGE`/`VIDEO`), `status` (`LOCAL_ONLY`/`UPLOADING`/`UPLOADED`/
`PROCESSED`/`FAILED`/`DELETED`), `localPath?` (só no dispositivo), `remoteRef?`,
`contentHash`, `bytes`, `width?`, `height?`, `capturedAt?`, `exifStripped`,
`derivatives[]`, `createdAt/updatedAt`

## 7. Social

### Post
`id`, `authorId`, `type` (`CATCH`/`TEXT`/`PHOTO`/`EVENT`/`SPOT_SHARE`), `refId?`, `body?`,
`mediaIds[]`, `communityId?`, `visibility`, `publicationStatus`, `moderationStatus`,
`counters`, `createdAt/updatedAt/deletedAt`

### Comment / Reaction / Follow / SavedItem
`Comment`: `id`, `postId`, `authorId`, `body`, `parentCommentId?`, `moderationStatus`
`Reaction`: `id`, `targetType`, `targetId`, `userId`, `kind`
`Follow`: `followerId`, `followeeId`, `createdAt`, `status`
`SavedItem`: `userId`, `targetType`, `targetId`, `createdAt`

## 8. Community / Group / Messaging / Events

### Community
`id`, `name`, `slug`, `type` (`REGIONAL`/`WATER_BODY`/`SPECIES`/`MODALITY`/`INTEREST`),
`description`, `rules[]`, `regionId?`, `waterBodyId?`, `visibility`, `joinPolicy`,
`memberCount`, `status`

### Membership
`communityId`, `userId`, `role` (`MEMBER`/`MODERATOR`/`ADMIN`), `status`, `joinedAt`

### Group
`id`, `name`, `privacy` (`PUBLIC`/`PRIVATE`), `ownerId`, `memberLimit?`, `createdAt`

### Conversation / Message
`Conversation`: `id`, `type` (`DIRECT`/`GROUP`), `participantIds[]`, `createdAt`
`Message`: `id`, `conversationId`, `senderId`, `type` (`TEXT`/`MEDIA`/`CATCH`/`SPOT`/
`LOCATION`/`EVENT_INVITE`), `body?`, `refId?`, `sentAt`, `deliveredAt?`, `readAt?`,
`deletedAt?`, `moderationStatus`

### Event
`id`, `organizerId`, `communityId?`, `groupId?`, `name`, `description`, `startsAt`,
`endsAt?`, `meetingPointLocation?`, `meetingPointPrecision`, `waterBodyId?`, `privacy`,
`participantLimit?`, `status`, `agenda?`, `sharedSpotIds[]`

## 9. Gamification

`Ranking`: `id`, `scope` (`GLOBAL`/`REGION`/`COMMUNITY`/`SPECIES`), `scopeRefId?`,
`metric`, `period`, `entries[]`, `computedAt`
`Achievement`: `id`, `code`, `name`, `criteria`, `tier`
`UserAchievement`: `userId`, `achievementId`, `grantedAt`, `evidenceRef?`
`Challenge`: `id`, `name`, `period`, `speciesId?`, `regionId?`, `rules`, `eligibility`,
`sponsorPartnerId?`, `prizeDescription?`, `status`

## 10. Commerce & Affiliates

`PartnerStore`: `id`, `legalName`, `displayName`, `status`, `verification`, `brands[]`,
`categories[]`, `contact`, `logoMediaId?`, `coverMediaId?`
`StoreLocation`: `id`, `partnerStoreId`, `address`, `location`, `openingHours`, `phone?`,
`whatsapp?`
`Offer`: `id`, `partnerStoreId`, `title`, `description`, `conditions`, `startsAt`,
`endsAt`, `couponId?`, `targetUrl?`, `status`
`Coupon`: `id`, `code`, `discountDescription`, `usageLimit?`, `validity`
`Referral`: `id`, `userId?`, `offerId?`, `partnerStoreId`, `createdAt`, `channel`
`Click`: `id`, `referralId`, `occurredAt`, `deviceFingerprintHash?`, `fraudSignals[]`
`Conversion`: `id`, `referralId?`, `partnerStoreId`, `externalOrderRef`, `amount?`,
`occurredAt`, `status`, `source`
`Commission`: `id`, `conversionId`, `amount`, `status`, `payoutId?`
`Payout`: `id`, `partnerStoreId?`, `period`, `total`, `status`

## 11. Billing

`Subscription`: `id`, `userId`, `plan` (`FREE`/`PRO`), `store` (`APPLE`/`GOOGLE`/`WEB`),
`externalRef`, `status`, `currentPeriodEnd`, `graceUntil?`, `trialEnd?`
`Entitlement`: `userId`, `key`, `value`, `sourceSubscriptionId?`, `expiresAt?`

## 12. Trust & Safety / Admin

`Report`: `id`, `reporterId`, `targetType`, `targetId`, `reason`, `details?`, `status`
`Block`: `blockerId`, `blockedId`, `createdAt`
`ModerationCase`: `id`, `reportIds[]`, `assignee?`, `decision?`, `decidedAt?`
`Sanction`: `id`, `userId`, `type`, `scope`, `expiresAt?`, `reason`
`AuditLog`: `id`, `actorType`, `actorId`, `action`, `targetType`, `targetId`, `at`,
`metadata` (sem dado sensível)

## 13. Environmental

`EnvironmentSnapshot`: `id`, `regionOrPointRef`, `observedAt`, `provider`, `quality`,
`ttl`, `airTempC?`, `waterTempC?`, `windKph?`, `windDir?`, `pressureHpa?`,
`precipitationMm?`, `moonPhase?`, `sunrise?`, `sunset?`, `riverLevelM?`, `riverFlow?`,
`tide?`
