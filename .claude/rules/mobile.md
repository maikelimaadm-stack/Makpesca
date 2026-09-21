# Regra — Mobile

## Aplicação
`apps/mobile`.

## SSOTs
`docs/05-offline-sync/*`, `docs/06-maps-location/GPS-STRATEGY.md`,
`docs/adr/ADR-0001-MOBILE-STACK.md`.

## Regras
1. O app é **offline-first**: a interface lê do SQLite local, não da rede.
2. Escrita local durável antes de confirmar na interface.
3. Estado de sincronização visível por item.
4. Credenciais no keystore/keychain — nunca no SQLite nem em storage comum.
5. GPS com amostragem adaptativa; **sem localização em background** no MVP.
6. Permissão solicitada no momento do uso, com explicação antes do diálogo do sistema.
7. Recusa de permissão não quebra o app (usar seleção no mapa).
8. Acurácia da leitura é exibida ao usuário ao marcar ponto.
9. Dado aproximado de terceiro é exibido **como aproximado**, com raio.
10. Nenhum log ou crash report com coordenada.
11. Migrações do banco local versionadas, com caminho de recuperação.
12. Avisar antes de qualquer ação que descarte dados pendentes.
13. Exibir espaço ocupado e permitir liberar sem perder pendências.

## Proibido
- Bloquear a interface esperando rede.
- Exibir erro que sugira perda de dado quando o dado está salvo localmente.
- Guardar coordenada de terceiro acima da precisão autorizada.
- Enviar lista de pontos privados a SDK de terceiro.
- Assumir cache de tiles sem licença (ver ADR-0010).
