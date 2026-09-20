---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: —
---

# Estratégia de Testes

> Nenhum teste é escrito nesta fase. Este documento define **o que será exigido** quando a
> implementação for liberada.

## 1. Níveis

| Nível | Escopo | Velocidade | Quantidade |
|-------|--------|-----------|-----------|
| Unit | Funções e regras puras | Muito rápida | Muitos |
| Domain | Invariantes e políticas | Rápida | Muitos |
| Integration | Casos de uso com adapters reais/falsos | Média | Vários |
| Database | Consultas, migrações, PostGIS | Média | Vários |
| API contract | Contrato HTTP por perfil de observador | Média | Vários |
| Sync | Protocolo, idempotência, conflitos | Média | **Prioritário** |
| Offline | Comportamento sem rede no dispositivo | Lenta | **Prioritário** |
| Geo-privacy | Precisão efetiva por observador | Média | **Prioritário** |
| Security | Autorização negativa, abuso | Média | Prioritário |
| Mobile E2E | Fluxos principais no app | Lenta | Poucos e essenciais |
| Web E2E | Fluxos principais na web | Lenta | Poucos |
| Admin E2E | Moderação | Lenta | Poucos |
| Partners E2E | Ofertas e relatórios | Lenta | Poucos |
| Load | Mapa, sync, feed | Sob demanda | Poucos |
| Migrations | Aplicar e reverter | Média | Todos |
| Backup/restore | Procedimento real | Manual periódico | Todos |

## 2. Prioridade

A pirâmide clássica não descreve este produto. Aqui, os testes mais valiosos são os de
**sync, offline e geo-privacy** — é onde os defeitos são caros e invisíveis.

## 3. Cenários obrigatórios

Nenhum slice relacionado é aceito sem estes cenários passando:

| # | Cenário |
|---|---------|
| 1 | **Offline sem duplicar**: criar registros offline, reconectar, sincronizar várias vezes → exatamente um de cada |
| 2 | **Privacidade de coordenadas**: para cada perfil de observador, verificar a precisão recebida em todos os endpoints com localização |
| 3 | **Sharing e revogação**: conceder, verificar acesso, revogar, verificar bloqueio imediato |
| 4 | **Sync idempotente**: repetir a mesma chave, verificar efeito único |
| 5 | **Delete convergence**: excluir em um dispositivo, verificar que não ressuscita no outro |
| 6 | **Media retry**: interromper upload, retomar, verificar integridade e ausência de duplicata |
| 7 | **Conversão afiliada sem comissão duplicada**: mesma conversão informada duas vezes → uma comissão |
| 8 | **Webhook de billing duplicado**: mesmo evento duas vezes → entitlement único |

## 4. Testes por invariante

Cada invariante de `../03-domain/DOMAIN-INVARIANTS.md` precisa de ao menos um teste.
Invariante sem teste é invariante em risco.

## 5. Dados de teste

Seed determinístico, cobrindo coordenadas reais brasileiras, todas as precisões, todos os
estados de sync, mídia em todos os estados e assinaturas em todos os estados.
**Nenhum dado real de usuário em teste.**

## 6. Ambiente de teste

Testes de banco usam PostgreSQL com PostGIS real (não substituto), porque a geometria é o
ponto crítico. Testes de API rodam contra a aplicação real com adapters de teste.

## 7. Critérios de aceite por slice

| Critério |
|----------|
| Testes dos níveis aplicáveis passando |
| Cenários obrigatórios relacionados passando |
| Invariantes tocadas com teste |
| Sem redução de cobertura em áreas críticas |
| Testes de autorização negativa para todo endpoint novo |
| Teste de privacidade para todo endpoint com localização |

## 8. O que não fazemos

- Perseguir percentual de cobertura como meta isolada.
- Testes frágeis que dependem de tempo real ou de ordem de execução.
- Mock de PostGIS.
- Teste que valida a implementação em vez do comportamento.
