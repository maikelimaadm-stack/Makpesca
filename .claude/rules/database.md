# Regra — Banco de Dados

## Aplicação
`packages/database`, migrações, consultas geoespaciais.

## SSOTs
`docs/04-data/CONCEPTUAL-DATA-MODEL.md`, `GEO-DATA-MODEL.md`, `DATA-CLASSIFICATION.md`,
`DATA-LIFECYCLE.md`, `docs/adr/ADR-0004-DATABASE-POSTGRES-POSTGIS.md`, `ADR-0007`.

## Regras
1. PostgreSQL + PostGIS. Provider sem PostGIS está fora.
2. Geometrias em WGS84 (SRID 4326); distância por tipo geográfico ou projeção adequada.
3. Identificadores são UUID; entidades criáveis offline recebem o UUID do cliente.
4. Identificador de provider externo fica em coluna separada e opaca — nunca chave primária.
5. Entidade sincronizável tem `createdAt`, `updatedAt`, `deletedAt`, `version`, `serverSeq`.
6. Migrações versionadas, reversíveis, executáveis fora da plataforma.
7. Restrições de unicidade para o que não pode duplicar (idempotência, comissões).
8. Consultas geográficas com limite de área e índice espacial.
9. Coordenada verdadeira nunca é lida fora do caminho que passa pelo Geo Privacy Service.
10. Nenhum arquivo de mídia no banco.
11. Nenhum recurso proprietário da hospedagem no esquema ou nas consultas.
12. Testes de banco rodam contra PostGIS real.

## Proibido
- Regras de acesso do banco gerenciado substituindo autorização da API.
- Migração destrutiva sem caminho de preservação.
- Consulta sem limite em tabela que cresce.
- `SELECT *` em caminho que serializa resposta.
