# Regra — Offline e Sincronização

## Aplicação
`apps/mobile`, endpoints de sync, fila de mídia.

## SSOTs
`docs/05-offline-sync/OFFLINE-FIRST-CONTRACT.md`, `SYNC-PROTOCOL.md`,
`CONFLICT-RESOLUTION.md`, `MEDIA-SYNC.md`, `docs/adr/ADR-0011-OFFLINE-SYNC.md`.

## Regras
1. Escrita local é durável **antes** de a interface confirmar.
2. Identificador de entidade é UUID gerado no cliente.
3. Toda mutação carrega `idempotencyKey` estável; reenvio usa **a mesma** chave.
4. Push antes de pull; cursor opaco; resultado por item.
5. `version` da entidade é do servidor e só cresce.
6. Exclusão gera tombstone; entidade excluída não ressuscita.
7. Conflito segue a matriz; **em privacidade, vence o mais restritivo**.
8. O estado de sync de cada item é visível ao usuário.
9. Falha tem motivo compreensível e caminho de recuperação.
10. Mídia nunca bloqueia a criação do registro.
11. Upload é retomável e verificado por hash.
12. Tempo do servidor é autoridade de ordenação.

## Proibido
- Confirmar na interface antes de persistir localmente.
- Gerar nova `idempotencyKey` a cada tentativa.
- Sincronizar por timestamp do dispositivo.
- Descartar item da fila sem avisar o usuário.
- Receber coordenada de terceiro acima da precisão autorizada "para filtrar depois".

## Testes obrigatórios
`docs/15-quality/OFFLINE-TEST-MATRIX.md` — falha bloqueia (`OFFLINE-GATE`).
