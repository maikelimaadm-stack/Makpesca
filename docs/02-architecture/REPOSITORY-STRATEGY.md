---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0017
---

# Estratégia de Repositório

> **Nenhum app é criado nesta fase.** Esta é a estrutura proposta, não executada.

## 1. Estrutura proposta

```
makpesca/
  apps/
    mobile/        # React Native + Expo
    web/           # Next.js (makpesca.com.br)
    admin/         # Next.js (admin.makpesca.com.br)
    partners/      # Next.js (partners.makpesca.com.br)
    api/           # API própria (api.makpesca.com.br)
  packages/
    domain/        # entidades, invariantes, políticas
    contracts/     # DTOs, schemas, erros, OpenAPI
    database/      # repositórios e migrações
    config/        # configuração validada
    observability/ # logging estruturado e redação
    ui/            # componentes web compartilhados
    testing/       # utilitários e fixtures
    shared/        # utilidades puras
  docs/
  .claude/
    rules/
    skills/
  CLAUDE.md
  README.md
```

## 2. Monorepo: por quê

| Vantagem | Relevância aqui |
|----------|-----------------|
| Contrato único entre API e clientes | Alta — `contracts` é compartilhado por 5 apps |
| Refatoração atômica de domínio | Alta |
| Padronização de lint, tipos e testes | Alta |
| Menos repositórios para governar | Alta em equipe pequena |

| Desvantagem | Mitigação |
|-------------|-----------|
| Build mais lento | Cache e build por afetados |
| Acoplamento acidental | Regras de dependência entre pacotes verificadas em CI |
| Mobile com ferramenta própria (Expo) | Tratar `apps/mobile` com pipeline separado |

## 3. Ferramenta

Candidato: **pnpm workspace + Turborepo**. Alternativas a considerar: npm/yarn workspaces
puros, Nx, Moon. Decisão em ADR-0017 (Q-024, criticidade baixa).

Critérios: velocidade de build incremental, suporte a Expo, simplicidade, manutenção ativa,
ausência de lock-in em serviço pago para cache.

## 4. Regras de dependência entre pacotes

| De | Pode depender de |
|----|------------------|
| `apps/*` | `packages/*` |
| `packages/database` | `domain`, `contracts`, `config` |
| `packages/contracts` | `domain` (apenas tipos) |
| `packages/domain` | **nada** |
| `packages/observability` | `config` |
| `packages/ui` | `contracts` (tipos), nada de domínio |

Violação de dependência é falha de CI (`ARCH-CONSISTENCY`).

## 5. Convenções

- Branches: `claude/<slice>-<descrição>` para trabalho automatizado; `feat/…`, `fix/…` para humano.
- Um slice por PR sempre que possível.
- Documentação alterada no mesmo PR que altera comportamento.
- PR só é marcado como ready mediante pedido explícito.

## 6. O que não fica no repositório

Secrets, arquivos de ambiente reais, dumps de banco, mídia de usuário, chaves de provider,
relatórios com dado pessoal.
