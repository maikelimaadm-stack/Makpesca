---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0001, ADR-0002, ADR-0003, ADR-0004, ADR-0005, ADR-0006, ADR-0017
---

# Arquitetura de Containers

## 1. Diagrama

```mermaid
flowchart TB
    subgraph Clients["Clientes"]
      MOB["Mobile<br/>React Native + Expo + TS"]
      WEB["Web<br/>Next.js + TS"]
      ADM["Admin<br/>Next.js + TS"]
      PRT["Partners<br/>Next.js + TS"]
    end

    subgraph APIC["api.makpesca.com.br"]
      HTTP["HTTP Layer<br/>rotas, validação, authn/authz, erros, idempotência"]
      APP["Application Layer<br/>casos de uso, orquestração, transações"]
      DOM["Domain Layer<br/>entidades, invariantes, regras<br/>SEM SDK de provider"]
      PORTS["Ports<br/>interfaces do domínio"]
    end

    subgraph Adapters["Adapters"]
      REPO["Repositórios<br/>PostgreSQL + PostGIS"]
      STOA["Storage Adapter"]
      AUTHA["Auth Adapter"]
      BILLA["Billing Adapter"]
      ENVA["Environmental Data Adapter"]
      QUEA["Queue Adapter"]
      OBSA["Observability Adapter"]
      PUSHA["Push Adapter"]
    end

    subgraph Infra["Infraestrutura"]
      PG[("PostgreSQL + PostGIS")]
      OBJ[("Object Storage")]
      IDP["Identity Provider"]
      BILLX["Lojas / Billing"]
      ENVX["APIs ambientais"]
      QUEX["Fila / Jobs"]
      OBSX["Logs / Métricas / Traces"]
      PUSHX["FCM / APNs"]
    end

    MOB --> HTTP
    WEB --> HTTP
    ADM --> HTTP
    PRT --> HTTP

    HTTP --> APP --> DOM
    APP --> PORTS
    PORTS --> REPO --> PG
    PORTS --> STOA --> OBJ
    PORTS --> AUTHA --> IDP
    PORTS --> BILLA --> BILLX
    PORTS --> ENVA --> ENVX
    PORTS --> QUEA --> QUEX
    PORTS --> OBSA --> OBSX
    PORTS --> PUSHA --> PUSHX

    MOB --- SQLITE[("SQLite local<br/>outbox + cache + mídia")]
```

## 2. Containers

| Container | Tecnologia baseline | Responsabilidade |
|-----------|--------------------|------------------|
| App Mobile | React Native + Expo + TypeScript | Experiência de campo, offline-first, GPS, mapa, captura, fila de sync |
| Web | Next.js + TypeScript | Landing, conteúdo público, perfis, exploração |
| Admin | Next.js + TypeScript | Moderação, catálogos, auditoria, conciliação |
| Partners | Next.js + TypeScript | Perfil de loja, ofertas, relatórios |
| API | TypeScript (framework em ADR-0006) | Única fronteira de regra de negócio |
| Banco | PostgreSQL + PostGIS | Persistência, geometria, índices geoespaciais |
| Object Storage | via adapter | Mídia |
| Fila/Jobs | via adapter | Processamento assíncrono |
| SQLite local | expo-sqlite ou equivalente | Fonte de verdade local do dispositivo |

## 3. Camadas internas da API

| Camada | Pode depender de | Nunca depende de |
|--------|------------------|------------------|
| HTTP | Application, DTOs | Domínio interno, ORM |
| Application | Domain, Ports | Adapters concretos, SDK de provider |
| Domain | Nada externo | Framework HTTP, ORM, SDKs, ambiente |
| Ports | Tipos do domínio | Implementações |
| Adapters | Ports, SDK do provider | Regras de negócio |

Detalhe em `COMPONENT-BOUNDARIES.md`.

## 4. Restrições estruturais

1. Cliente não fala com banco. Sempre API.
2. Domínio não importa SDK.
3. DTO não é entidade de ORM.
4. Adapter não contém regra de negócio.
5. Job assíncrono usa os mesmos casos de uso, não caminhos paralelos.
6. Toda escrita sincronizável passa pelo mecanismo de idempotência.
7. Toda leitura de localização passa pela degradação de geo-privacy antes de serializar.

## 5. Dados que ficam no dispositivo

| Dado | Motivo |
|------|--------|
| Pontos e capturas do usuário | Offline-first |
| Outbox de mutações | Sincronização |
| Fila de mídia + arquivos locais | Upload retomável |
| Cursor de sync e versões | Convergência |
| Região de mapa baixada | Mapa offline (depende de ADR-0010) |
| Catálogos (espécies, iscas, técnicas) | Uso offline |

Dados de terceiros ficam no dispositivo **apenas** na precisão autorizada.
