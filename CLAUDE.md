# CLAUDE.md — Regras Operacionais do MAKPESCA

Este arquivo vale para qualquer agente ou pessoa que altere este repositório.
Ele é curto de propósito. Os detalhes vivem nos SSOTs indicados.

## 0. Estado do projeto

Fase atual: **MP-DOC-00 — Fundação Documental**.
`IMPLEMENTATION-READY-GATE` = **BLOCKED**.
**Não implementar produto** (app, API executável, schema, migrations, deploy) até o gate ser liberado.

## 1. Antes de alterar arquitetura

- Leia os SSOTs relevantes em [docs/README.md](docs/README.md) antes de propor qualquer mudança estrutural.
- Mudança de arquitetura sem ADR correspondente não é aceita.
  Ver [docs/00-governance/DECISION-POLICY.md](docs/00-governance/DECISION-POLICY.md).

## 2. Documentos FROZEN

- Documento com `Status: FROZEN` **não muda silenciosamente**.
- Para alterar: abrir ADR de superseção + registrar em `DECISION-REGISTRY.md` + seguir
  [docs/00-governance/FREEZE-POLICY.md](docs/00-governance/FREEZE-POLICY.md).

## 3. Fronteira de arquitetura

- Mobile e Web **nunca** acessam PostgreSQL/Supabase diretamente para regra de negócio.
- Fluxo obrigatório: `CLIENTES → api.makpesca.com.br → Application/Domain → Ports/Adapters → Infra`.
- Domain **não** importa SDK de provider. DTO **não** é entidade de ORM.
  Ver [docs/02-architecture/PROVIDER-ABSTRACTION.md](docs/02-architecture/PROVIDER-ABSTRACTION.md).

## 4. Geo-privacy

- Degradação de precisão é **server-side**. O frontend nunca recebe coordenada verdadeira
  que deveria "apenas esconder".
- Ver [docs/06-maps-location/GEO-PRIVACY.md](docs/06-maps-location/GEO-PRIVACY.md) e
  [docs/08-security-privacy/GEO-PRIVACY-THREAT-MODEL.md](docs/08-security-privacy/GEO-PRIVACY-THREAT-MODEL.md).

## 5. Offline-first

- O mobile é offline-first: SQLite local é fonte de verdade da sessão do usuário até sincronizar.
- Ver [docs/05-offline-sync/OFFLINE-FIRST-CONTRACT.md](docs/05-offline-sync/OFFLINE-FIRST-CONTRACT.md).

## 6. Sync idempotente

- Toda operação de escrita sincronizável carrega id gerado no cliente + idempotency key.
- Reenvio nunca duplica. Ver [docs/05-offline-sync/SYNC-PROTOCOL.md](docs/05-offline-sync/SYNC-PROTOCOL.md).

## 7. Secrets

- Nenhum secret, token, chave ou credencial em código, doc, log ou commit.
  Ver [docs/08-security-privacy/SECRETS-POLICY.md](docs/08-security-privacy/SECRETS-POLICY.md).

## 8. Infraestrutura e dependências

- Nenhuma dependência, serviço ou infraestrutura nova sem justificativa registrada
  (ADR ou seção de decisão). Evitar overengineering.

## 9. Escopo por slice

- Trabalho é feito por slice (`MP-XX`). Um slice não invade escopo de outro.
  Ver [docs/16-roadmap/IMPLEMENTATION-SLICE-ROADMAP.md](docs/16-roadmap/IMPLEMENTATION-SLICE-ROADMAP.md).

## 10. Gates

- Gates são obrigatórios. **Falha de gate bloqueia** a entrega — não existe "passa mesmo assim".
  Ver [docs/15-quality/QUALITY-GATES.md](docs/15-quality/QUALITY-GATES.md).

## 11. Evidências

- Afirmação técnica relevante precisa de evidência: caminho de arquivo, saída de comando,
  link com data de consulta ou ADR.
- **Não inventar pesquisa.** Política, preço ou licença de terceiro exige fonte + data de consulta.
  Sem fonte verificada, marcar como `NEEDS-DECISION` / `NÃO VERIFICADO`.

## 12. Social e comércio

- Funcionalidade social nova exige tratamento de moderação, denúncia e abuso.
  Ver [docs/09-social/MODERATION.md](docs/09-social/MODERATION.md).
- Funcionalidade de afiliados exige antifraude e regra de atribuição explícita.
  Ver [docs/11-commerce/COMMERCE-FRAUD.md](docs/11-commerce/COMMERCE-FRAUD.md).

## 13. Git e PR

- Não marcar PR como ready, não mergear e não fazer force-push sem pedido explícito.
- Commits descritivos, uma branch por missão.

## 14. Relatório final

- Todo relatório final de missão é entregue em **um único bloco ```text```**, em pt-BR.

## 15. Skills disponíveis

Skills de revisão em `.claude/skills/`: `mp-doc-audit`, `mp-freeze-wave`, `mp-geo-privacy-review`,
`mp-offline-review`, `mp-api-review`, `mp-security-review`, `mp-architecture-check`,
`mp-social-review`, `mp-commerce-review`, `mp-provider-review`, `mp-slice-plan`, `mp-release-gate`.

Regras detalhadas por área em `.claude/rules/`.
