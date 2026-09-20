---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0005
---

# Ambientes (operação)

Decisões arquiteturais em `../02-architecture/ENVIRONMENT-STRATEGY.md`.

## 1. Ambientes

| Ambiente | Quem usa | Dados | Estabilidade |
|----------|----------|-------|--------------|
| `local` | Desenvolvimento | Sintéticos | Sem garantia |
| `development` | Integração | Sintéticos | Baixa |
| `preview` | Revisão de PR | Sintéticos, efêmeros | Baixa |
| `staging` | Validação pré-produção | Sintéticos/anonimizados | Alta |
| `production` | Usuários reais | Reais | Máxima |

## 2. Isolamento

| Recurso | Regra |
|---------|-------|
| Banco | Instância/base separada por ambiente |
| Storage | Bucket separado por ambiente |
| Secrets | Conjunto separado, sem reuso |
| Push | Projeto separado |
| Billing | Sandbox fora de produção |
| Auth | Instância/tenant separado |
| Observabilidade | Separada, para não poluir alertas |

**Proibido:** apontar qualquer ambiente não-produtivo para o banco, storage ou billing
de produção.

## 3. Dados

| Ambiente | Origem dos dados |
|----------|------------------|
| local / development / preview | Seed sintético |
| staging | Seed sintético volumoso ou cópia **anonimizada** |
| production | Dados reais |

Cópia de produção sem anonimização para qualquer outro ambiente é violação de privacidade.

## 4. Seed sintético

Precisa cobrir: coordenadas em regiões brasileiras reais, as cinco precisões, pontos
compartilhados e revogados, capturas pendentes de sync, conflitos, mídia em fila,
assinaturas em todos os estados, denúncias abertas, parceiros e conversões.

Sem esse seed, não é possível testar os cenários obrigatórios.

## 5. Promoção

```
local → development → preview (por PR) → staging → production
```

Regras: mesma imagem/artefato promovido; mesmas migrações; staging sempre executa a
migração antes de produção; deploy em produção tem rollback testado.

## 6. Configuração

Toda configuração vem de variáveis de ambiente validadas na inicialização. Faltando algo
obrigatório, a aplicação **falha ao iniciar** — nunca assume padrão silencioso.

## 7. Domínios

| Ambiente | Domínios |
|----------|----------|
| production | `makpesca.com.br`, `api.makpesca.com.br`, `admin.`, `partners.` |
| staging | Subdomínios próprios, com robots bloqueados |
| preview | URLs efêmeras, protegidas por autenticação |

Ambiente não-produtivo nunca é indexado por buscadores.

## 8. Acesso

Produção: acesso mínimo, nominal, auditado, com 2FA. Demais ambientes: acesso da equipe
de desenvolvimento. Nenhum ambiente compartilha credenciais entre pessoas.
