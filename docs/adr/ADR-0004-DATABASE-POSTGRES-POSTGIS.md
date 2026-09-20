# ADR-0004 — Banco de Dados: PostgreSQL + PostGIS

- **Status:** PROPOSED
- **Date:** 2026-09-20
- **Onda:** F3

## Context
O produto é geoespacial por natureza: pontos, corpos d'água (linhas e polígonos), regiões,
consultas por viewport, proximidade e contenção. Além disso, precisa de transações
confiáveis, unicidade forte (idempotência, comissões) e portabilidade.

## Decision Drivers
- Consultas geoespaciais de primeira classe.
- Índices espaciais eficientes.
- Transações e restrições de unicidade.
- Portabilidade entre hospedagens.
- Maturidade e disponibilidade de profissionais.

## Options Considered
| Opção | Prós | Contras |
|-------|------|---------|
| **PostgreSQL + PostGIS** | Geo maduro, transacional, portátil, padrão de mercado | Exige provider com PostGIS habilitado |
| MySQL com funções espaciais | Difundido | Geo menos completo que PostGIS |
| MongoDB com índices geoespaciais | Flexível | Transações e integridade referencial mais fracas para este domínio |
| Banco relacional + serviço geo separado | Especialização | Dois sistemas para manter sincronizados; complexidade sem ganho nesta escala |

## Decision
Adotar **PostgreSQL com PostGIS**. PostGIS é **requisito de seleção** de qualquer provider
gerenciado: provider sem PostGIS está automaticamente fora.

## Consequences
- Geometrias em WGS84 (SRID 4326).
- Índices GiST para as entidades geográficas.
- A camada de acesso a dados (ADR-0007) precisa suportar PostGIS adequadamente.
- Testes de banco rodam contra PostGIS real, nunca substituto.

## Risks
- R-035: provider gerenciado sem PostGIS ou com versão limitada.
- Consultas geoespaciais mal escritas custam caro em escala.
- Migrações de geometria são delicadas.

## Security Impact
Menor privilégio para a aplicação; nenhuma credencial de banco em cliente.

## Privacy Impact
O banco guarda coordenadas verdadeiras (C4): cifragem em repouso, acesso auditado,
separação entre dado verdadeiro e projeção divulgável.

## Offline Impact
Indireto: o servidor é a autoridade; o dispositivo usa SQLite (ADR-0011).

## Portability Impact
Alto e positivo: PostgreSQL roda em praticamente qualquer provedor.
Regra: **nada específico do produto Supabase** no esquema ou nas consultas.

## Cost Impact
Custo de banco gerenciado + armazenamento. A verificar com fonte e data (A-009).

## Operational Impact
Backups, PITR, migrações, monitoramento de consultas lentas.

## Open Questions
- A-009: o provider gerenciado pretendido oferece PostGIS e PITR adequados?
- Uma região de banco basta para a latência no Brasil (A-015)?
- Estratégia de particionamento futuro para capturas/cliques?

## Evidence
Requisitos geoespaciais derivados de `GEO-DATA-MODEL.md`. Capacidades do provider
**não verificadas**.

## Supersedes / Superseded By
— / —
