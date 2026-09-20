# MAKPESCA

Plataforma de pesca: mapa, pontos, capturas, offline real, rede social especializada
e ecossistema comercial (lojas parceiras, ofertas, afiliados).

> **Conceito:** "Waze da pesca + comunidade especializada + ecossistema comercial da pesca."

## Estado atual do repositório

**Fase: MP-DOC-00 — Fundação Documental.**

Este repositório contém **somente documentação**. Não existe código de produto,
não existe app, não existe API executável, não existe schema de banco.

| Gate | Estado |
|------|--------|
| `IMPLEMENTATION-READY-GATE` | **BLOCKED** |

Nenhuma implementação de produto pode começar antes que o
`IMPLEMENTATION-READY-GATE` seja liberado conforme
[docs/15-quality/QUALITY-GATES.md](docs/15-quality/QUALITY-GATES.md).

## Ordem de trabalho obrigatória

```
DOCUMENTAR → AUDITAR → CORRIGIR → CONGELAR POR ONDAS → DEFINIR SLICES
          → IMPLEMENTAR → TESTAR → CERTIFICAR → LANÇAR
```

## Por onde começar

1. [docs/README.md](docs/README.md) — índice oficial e mapa de SSOTs.
2. [docs/00-governance/PROJECT-CONSTITUTION.md](docs/00-governance/PROJECT-CONSTITUTION.md) — regras inegociáveis.
3. [docs/01-product/PRODUCT-VISION.md](docs/01-product/PRODUCT-VISION.md) — visão do produto.
4. [docs/01-product/MVP-SCOPE.md](docs/01-product/MVP-SCOPE.md) — o que entra no MVP.
5. [docs/16-roadmap/DOCUMENTATION-FREEZE-WAVES.md](docs/16-roadmap/DOCUMENTATION-FREEZE-WAVES.md) — ondas de congelamento.
6. [CLAUDE.md](CLAUDE.md) — regras operacionais para agentes.

## Baseline técnico (proposto, não congelado)

| Camada | Baseline |
|--------|----------|
| Mobile | React Native + Expo + TypeScript |
| Web | Next.js + TypeScript |
| API | API própria em TypeScript, `api.makpesca.com.br` |
| Banco | PostgreSQL + PostGIS (Supabase como infraestrutura inicial) |
| Local mobile | SQLite |
| Mapa online | Google Maps Platform (candidato) |
| Mapa offline | **decisão aberta** — ver [ADR-0010](docs/adr/ADR-0010-OFFLINE-MAPS.md) |
| Arquivos | Object Storage via adapter |

Regra estrutural: **clientes nunca acessam PostgreSQL/Supabase diretamente para regra de negócio.**

```
CLIENTES → api.makpesca.com.br → Application/Domain → Ports/Adapters → Infraestrutura
```

## Domínios planejados

| Domínio | Uso |
|---------|-----|
| `makpesca.com.br` | Web pública / produto web |
| `api.makpesca.com.br` | API própria (único caminho de regra de negócio) |
| `admin.makpesca.com.br` | Painel administrativo interno |
| `partners.makpesca.com.br` | Portal de parceiros |

## Licença e status

Projeto privado em fase de fundação documental. Todos os documentos estão em `DRAFT`.
Nada está `FROZEN`.
