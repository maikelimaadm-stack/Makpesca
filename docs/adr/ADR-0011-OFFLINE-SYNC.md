# ADR-0011 — Sincronização Offline

- **Status:** PROPOSED
- **Date:** 2026-09-20
- **Onda:** F4

## Context
O app é offline-first. Registros são criados sem rede e sincronizados depois, em condições
ruins de conectividade, possivelmente a partir de vários dispositivos. Duplicação e perda
de dados são os piores defeitos possíveis do produto.

## Decision Drivers
- Zero perda, zero duplicação.
- Reenvio é normal, não excepcional.
- Convergência entre dispositivos.
- Exclusões precisam convergir.
- Simplicidade suficiente para ser implementável e testável.

## Options Considered
| Opção | Prós | Contras |
|-------|------|---------|
| **Outbox + cursor + idempotência + versões + tombstones** | Explícito, testável, sob nosso controle, adequado ao modelo de propriedade dos dados | Precisamos implementar e testar tudo |
| CRDTs | Convergência automática | Complexidade alta; ganho pequeno num modelo onde cada registro tem um dono |
| Biblioteca/serviço de sync pronto | Menos código | Lock-in; geo-privacidade precisa entrar no meio do caminho; controle insuficiente sobre autorização |
| Sync ingênuo por timestamp | Simples | Falha com clock skew, empates e exclusões; duplica |

## Decision
Adotar **outbox no cliente + push/pull por cursor + idempotência por chave + versão de
entidade + tombstones**, conforme `../05-offline-sync/SYNC-PROTOCOL.md`.

Elementos:
1. identificadores de entidade gerados no cliente (UUID);
2. `idempotencyKey` estável por intenção;
3. push antes de pull;
4. resultado por item (`applied`/`duplicate`/`conflict`/`rejected`/`deferred`);
5. cursor opaco para pull;
6. versão da entidade definida pelo servidor;
7. tombstones com retenção maior que a janela de sync;
8. matriz de conflito por campo, com **privacidade sempre no mais restritivo**.

## Consequences
- A API precisa de endpoints de sync dedicados.
- O servidor guarda resultados de idempotência por uma janela.
- O cliente mantém estado de sync visível ao usuário.
- Testes de sync são prioritários (`OFFLINE-TEST-MATRIX`).

## Risks
- R-020 duplicação, R-021 perda, R-022 conflito, R-023 ressurreição, R-025 clock skew.
- Complexidade concentrada em MP-10 — o slice mais arriscado.

## Security Impact
Endpoints de sync exigem autorização por objeto como qualquer outro. Lote não é exceção.

## Privacy Impact
**Crítico:** o pull entrega dados de terceiros já degradados. O dispositivo nunca recebe
coordenada verdadeira que deveria esconder. Revogação viaja pelo pull como instrução de
remoção.

## Offline Impact
É a decisão que materializa o contrato offline.

## Portability Impact
Protocolo próprio e documentado: não depende de provider.

## Cost Impact
Armazenamento de registros de idempotência e tombstones; tráfego de sync.

## Operational Impact
Métricas de sync são sinal de saúde do produto: pendências, duplicatas, conflitos,
convergência.

## Open Questions
- Janela de retenção de idempotência (proposta: 30 dias).
- Retenção de tombstones (proposta: 180 dias).
- Tamanho ideal de lote.
- Como tratar dispositivos muito desatualizados além da ressincronização completa.

## Evidence
Derivado dos requisitos de `OFFLINE-FIRST-CONTRACT.md`. Sem medição — os parâmetros
precisam ser validados em teste.

## Supersedes / Superseded By
— / —
