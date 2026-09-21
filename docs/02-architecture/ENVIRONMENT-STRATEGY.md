---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0005
---

# Estratégia de Ambientes (arquitetura)

Detalhe operacional em `../14-operations/ENVIRONMENTS.md`. Aqui ficam as
**consequências arquiteturais**.

## 1. Ambientes

| Ambiente | Propósito | Dados |
|----------|-----------|-------|
| `local` | Desenvolvimento na máquina | Sintéticos |
| `development` | Integração contínua compartilhada | Sintéticos |
| `preview` | Um por branch/PR | Sintéticos, efêmeros |
| `staging` | Espelho de produção para validação | Sintéticos/anonimizados |
| `production` | Usuários reais | Reais |

## 2. Isolamento obrigatório

1. Banco separado por ambiente. **Nunca** apontar preview/staging para o banco de produção.
2. Storage separado por ambiente.
3. Credenciais separadas por ambiente, sem reuso.
4. Provider de push, billing e auth em modo sandbox fora de produção.
5. Ambiente não-produtivo **não** recebe cópia de dado pessoal real sem anonimização.

## 3. Consequências arquiteturais

- Toda configuração entra por `packages/config`, validada na inicialização. Falta de
  configuração obrigatória = falha imediata, nunca comportamento silencioso.
- Nada de `if (ambiente === 'production')` espalhado no domínio. Comportamento variável
  é configuração, não condicional de código de negócio.
- Chave de provider é injetada, nunca embutida em cliente.
- Cliente mobile aponta para a API por configuração de build, e sabe distinguir ambientes.

## 4. Dados de teste

Geração sintética precisa cobrir: coordenadas em regiões reais brasileiras, pontos com as
cinco precisões, capturas offline pendentes, conflitos de sync, mídia em fila, assinaturas
em todos os estados e cenários de denúncia.

## 5. Promoção

```
local → development → preview (PR) → staging → production
```

Nenhum artefato vai para produção sem ter passado por staging com as mesmas migrações.
