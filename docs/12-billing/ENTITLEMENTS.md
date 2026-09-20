---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0014
---

# Entitlements

## 1. Definição

Entitlement é **o que o usuário pode fazer**, expresso de forma independente de como ele
obteve esse direito. O app pergunta "posso?" e recebe a resposta — nunca calcula sozinho.

## 2. Formato conceitual

| Campo | Descrição |
|-------|-----------|
| `key` | Identificador estável do direito |
| `value` | Booleano ou numérico (limite) |
| `source` | Assinatura, promoção, concessão manual, plano gratuito |
| `expiresAt` | Validade |
| `cacheTtl` | Quanto tempo o cliente pode confiar no valor offline |

## 3. Catálogo proposto

| Chave | Tipo | FREE | PRO |
|-------|------|------|-----|
| `offline_regions.max` | número | baixo | alto |
| `offline_region.area_max_km2` | número | menor | maior |
| `spots.max` | número | limite generoso | ilimitado |
| `catch.photos_max` | número | menor | maior |
| `map.advanced_layers` | booleano | não | sim |
| `history.advanced_stats` | booleano | não | sim |
| `filters.advanced` | booleano | não | sim |
| `environment.detailed` | booleano | não | sim |
| `intelligence.insights` | booleano | não | sim |
| `planning.trip` | booleano | não | sim |
| `profile.pro_badge` | booleano | não | sim |

Valores numéricos **não estão definidos**: dependem do custo real medido (`COST-GATE`).

## 4. Regras

| # | Regra |
|---|-------|
| 1 | O Entitlement Service é a **fonte única**; nenhum outro código decide acesso |
| 2 | O cliente consulta e respeita; nunca infere pelo plano |
| 3 | Entitlement é derivado do estado, não somado por evento (INV-B01) |
| 4 | Toda verificação de limite acontece **também** no servidor |
| 5 | Ultrapassar limite retorna erro específico (`QUOTA_EXCEEDED`), com orientação |
| 6 | Downgrade não apaga dados; excede vira somente leitura |
| 7 | Entitlement pode vir de origem não paga (promoção, beta, suporte) |
| 8 | Toda concessão manual é auditada |

## 5. Verificação em duas camadas

| Camada | Papel |
|--------|-------|
| Cliente | Experiência: mostrar limites, evitar ações inúteis, funcionar offline |
| Servidor | **Autoridade**: rejeitar o que exceder, independentemente do cliente |

Confiar apenas no cliente é falha de segurança; confiar apenas no servidor é experiência
ruim offline. Precisa das duas.

## 6. Offline

- Entitlements têm `cacheTtl`.
- Sem rede e dentro da validade: valem.
- Sem rede e fora da validade: manter o último estado e revalidar depois — nunca degradar
  o usuário no campo (OFF-9).
- Ao reconectar: sincronizar e, se houver excedente criado offline, tratar com tolerância
  (aceitar o que foi criado, avisar o usuário) em vez de descartar dados.

## 7. Evolução

Adicionar entitlement novo não pode quebrar clientes antigos: chave desconhecida é tratada
como "não concedido" de forma segura, e o app antigo continua funcionando com o que conhece.
