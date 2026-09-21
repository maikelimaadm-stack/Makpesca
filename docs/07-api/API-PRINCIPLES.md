---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0003, ADR-0006
---

# Princípios de API

## 1. A API é a fronteira

`api.makpesca.com.br` é o **único** caminho de regra de negócio. Mobile, Web, Admin e
Partners falam apenas com ela (constitucional, Art. 2).

## 2. Princípios

| # | Princípio |
|---|-----------|
| 1 | **API-first**: o contrato é definido antes do cliente e do banco |
| 2 | **Versionada**: `/v1/...` desde o início |
| 3 | **Previsível**: mesmos padrões de erro, paginação, filtro e ordenação em todos os recursos |
| 4 | **Explícita**: sem comportamento mágico dependente de cabeçalho não documentado |
| 5 | **Idempotente onde importa**: toda escrita sincronizável aceita `Idempotency-Key` |
| 6 | **Autorizada por objeto**: nunca confiar no identificador da rota |
| 7 | **Privada por construção**: nenhuma resposta serializa localização sem passar pelo Geo Privacy Service |
| 8 | **Portável**: nenhum recurso proprietário da hospedagem no contrato |
| 9 | **Observável**: toda requisição tem identificador de correlação |
| 10 | **Documentada**: OpenAPI gerado a partir do mesmo esquema que valida |

## 3. Estilo

- REST orientado a recursos, JSON.
- Substantivos no plural: `/v1/spots`, `/v1/catches`.
- Ações que não são CRUD ficam explícitas como subrecursos: `/v1/spots/{id}/grants`.
- Endpoints especializados quando o custo justifica (mapa, sync), documentados como tal.
- Sem GraphQL nesta fase: complexidade de autorização por campo e de cache não se paga
  no estágio atual (revisável por ADR).

## 4. DTOs

| Regra |
|-------|
| DTO é definido em `packages/contracts`, independente de ORM |
| Nunca serializar entidade de banco diretamente |
| Campo ausente ≠ campo nulo: a ausência é usada para `HIDDEN` |
| Datas em ISO 8601 com fuso |
| Identificadores são UUID em string |
| Unidades explícitas nos nomes (`weightGrams`, `lengthMm`, `radiusMeters`) |
| Enumerações em maiúsculas, estáveis, nunca renomeadas dentro de uma versão |

## 5. Validação

- Toda entrada é validada por esquema na borda.
- Validação sintática (formato) na camada HTTP; validação semântica (regra) no domínio.
- Erro de validação retorna todos os problemas encontrados, não apenas o primeiro.
- Campos desconhecidos são rejeitados em escrita (evita erro silencioso de cliente).

## 6. Paginação, filtros e ordenação

| Aspecto | Padrão |
|---------|--------|
| Paginação | Por cursor opaco (`cursor`, `limit`), com `nextCursor` na resposta |
| Limite | Padrão e máximo definidos por recurso |
| Filtros | Nomeados explicitamente por recurso; nenhum filtro dinâmico livre |
| Ordenação | Conjunto fechado de opções por recurso |
| Consultas geográficas | Sempre com limite de área e de resultados |

Offset/limit não é usado em listas grandes (custo e instabilidade de página).

## 7. Autorização

- Autenticação em toda rota, exceto as explicitamente públicas.
- Autorização por objeto em todo acesso (INV-A01).
- Escopos distintos por tipo de cliente: usuário, admin, parceiro, sistema (webhooks).
- Resposta para recurso não autorizado segue a política de `API-SECURITY.md`
  (não revelar existência quando isso for sensível).

## 8. Compatibilidade

Dentro de `/v1`, mudanças compatíveis são permitidas: adicionar campo opcional, adicionar
endpoint, adicionar valor de enumeração **desde que** clientes tolerem desconhecidos.
Quebras exigem `/v2` — ver `API-VERSIONING.md`.

## 9. Clientes móveis desatualizados

A API precisa conviver com aplicativos antigos por muito tempo (usuário não atualiza).
Consequências: nada de quebra silenciosa; suporte a versão mínima declarada; mecanismo de
aviso de atualização obrigatória quando a versão ficar insustentável.
