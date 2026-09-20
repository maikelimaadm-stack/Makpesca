---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0003, ADR-0007, ADR-0017
---

# Fronteiras de Componentes

## 1. Regra de dependência

```
HTTP → Application → Domain
             ↓
           Ports ← Adapters → Infraestrutura
```

Dependência aponta sempre para dentro. O domínio é o centro e não conhece ninguém.

## 2. O que cada camada pode e não pode

### Domain
**Pode:** entidades, objetos de valor, invariantes, políticas de negócio (inclusive as
regras de geo-privacy e de conflito de sync), erros de domínio.
**Não pode:** HTTP, SQL, ORM, SDK, variável de ambiente, relógio global, aleatoriedade
não injetada, I/O.

### Application
**Pode:** casos de uso, orquestração, transação, autorização de alto nível, publicação de
eventos, chamadas a ports.
**Não pode:** conhecer framework HTTP, conhecer dialeto SQL, instanciar SDK.

### HTTP
**Pode:** rotear, validar entrada, autenticar, mapear erro para contrato, serializar DTO,
aplicar rate limit e idempotência.
**Não pode:** conter regra de negócio, acessar repositório diretamente, decidir precisão
de coordenada por conta própria.

### Ports
Interfaces declaradas em função da necessidade do domínio, nunca em função do provider.
Exemplo conceitual: uma port de storage expressa "autorizar upload de mídia" e
"confirmar mídia", não "gerar URL assinada do provedor X".

### Adapters
**Pode:** traduzir port ↔ provider, tratar erro do provider, aplicar retry/timeout.
**Não pode:** decidir regra, decidir privacidade, alterar semântica de domínio.

## 3. Pacotes previstos (monorepo)

| Pacote | Conteúdo | Depende de |
|--------|----------|-----------|
| `packages/domain` | entidades, invariantes, políticas | nada |
| `packages/contracts` | DTOs, esquemas de validação, tipos de erro, OpenAPI | domain (tipos) |
| `packages/database` | repositórios, migrações, mapeamentos | domain, contracts |
| `packages/config` | carga e validação de configuração | — |
| `packages/observability` | logging estruturado, redação de campos sensíveis | config |
| `packages/ui` | componentes compartilhados de web | — |
| `packages/testing` | utilitários e fixtures de teste | — |
| `packages/shared` | utilidades puras (datas, geo helpers sem provider) | — |

Regra: `domain` **não** depende de `database`. O inverso é permitido.

## 4. Fronteiras que não podem ser atravessadas

| Proibição | Motivo |
|-----------|--------|
| Cliente → banco | Constitucional Art. 2 |
| Domain → SDK | Portabilidade |
| DTO = entidade de ORM | Vazamento de esquema e de campos sensíveis |
| Adapter decidindo precisão geográfica | Geo-privacy tem de ser única e central |
| Job assíncrono com regra própria | Divergência de comportamento |
| Admin acessando banco direto | Auditoria e menor privilégio |

## 5. Componentes transversais

| Componente | Responsabilidade | Onde vive |
|------------|------------------|-----------|
| **Geo Privacy Service** | Decidir precisão efetiva e degradar coordenadas | Domain + Application |
| **Entitlement Service** | Responder o que o usuário pode fazer | Domain + Application |
| **Idempotency Registry** | Garantir exatamente-uma-vez lógico | Application + infraestrutura |
| **Sync Engine** | Cursor, versões, tombstones, conflitos | Application |
| **Media Pipeline** | Autorização, confirmação, derivativos, EXIF | Application + jobs |
| **Moderation Service** | Denúncia, fila, decisão, efeito | Application |
| **Attribution Service** | Click, referral, conversão, comissão | Application |

Cada um deles tem SSOT próprio; nenhum pode ser duplicado em outra camada.

## 6. Verificação

O `ARCH-CONSISTENCY` gate verifica, entre outras coisas: ausência de import de SDK no
domínio, ausência de acesso a banco fora de repositórios, e que toda serialização de
localização passa pelo Geo Privacy Service.
