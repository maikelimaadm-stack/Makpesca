---
name: mp-offline-review
description: Revisa offline-first, sincronização, idempotência, conflitos e fila de mídia. Use ao alterar sync, banco local ou upload.
---

# mp-offline-review

## SSOTs
- `docs/05-offline-sync/OFFLINE-FIRST-CONTRACT.md`
- `docs/05-offline-sync/SYNC-PROTOCOL.md`
- `docs/05-offline-sync/CONFLICT-RESOLUTION.md`
- `docs/05-offline-sync/MEDIA-SYNC.md`
- `docs/15-quality/OFFLINE-TEST-MATRIX.md`
- `.claude/rules/offline-sync.md`

## Checklist
1. Escrita local é durável antes de a interface confirmar?
2. Identificador é UUID gerado no cliente?
3. `idempotencyKey` é estável entre tentativas da mesma intenção?
4. Push antes de pull; cursor opaco; resultado por item?
5. Reenvio retorna `duplicate` sem novo efeito?
6. Exclusão gera tombstone e não ressuscita?
7. Conflito segue a matriz, com **privacidade no mais restritivo**?
8. Estado de sync visível por item, com motivo em caso de falha?
9. Mídia não bloqueia a criação do registro; upload retomável e verificado por hash?
10. Backoff com jitter; 429 respeitado; 4xx não entra em loop?
11. Tempo do servidor decide ordenação?
12. Cenário de referência completo coberto por teste?

## Cenários que não podem faltar
O-06 (app morto na escrita), O-12 (queda no push), O-13 (resposta perdida),
O-22 (editar vs excluir), O-31 (app morto no upload), O-44 (revogação enquanto offline).

## Saída
Achados + veredito do `OFFLINE-GATE`.
