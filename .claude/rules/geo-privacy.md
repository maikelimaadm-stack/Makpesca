# Regra — Geo-Privacidade

## Aplicação
Qualquer código que leia, escreva, transporte, exiba, registre ou agregue localização.

## SSOTs
`docs/06-maps-location/GEO-PRIVACY.md`,
`docs/08-security-privacy/GEO-PRIVACY-THREAT-MODEL.md`,
`docs/adr/ADR-0012-GEO-PRIVACY.md`.

## Regras
1. A degradação é **server-side**, antes da serialização. Esconder no cliente não vale.
2. Um **único** componente decide e aplica precisão (Geo Privacy Service).
3. Precisão efetiva = a mais restritiva entre dono, concessão, moderação e contexto.
4. Ponto nasce `PRIVATE`.
5. Publicar captura **não** publica o ponto.
6. Jitter é determinístico por (recurso, observador); nunca re-sorteado.
7. Quando a precisão é aproximada, o raio é informado e a interface não mente.
8. Cache de resposta com localização inclui o perfil do observador na chave.
9. Revogação tem efeito imediato e remove o dado nos dispositivos.
10. Concessão não pode ser repassada.
11. Mídia publicada não contém EXIF de GPS.
12. Endpoint novo com localização exige teste por perfil de observador.

## Proibido — sem exceção
- Coordenada em log, métrica, analytics ou crash report.
- Coordenada em URL, query string, deep link ou payload de push.
- Enviar pontos privados a serviço de terceiro.
- Ordenar ou filtrar por distância a recurso não autorizado.
- Responder 403 quando revelar a existência já é vazamento (usar 404).
- Publicar insight sem coorte mínima e verificação de reidentificação.

## Testes obrigatórios
`docs/15-quality/PRIVACY-TEST-MATRIX.md` — falha bloqueia (`PRIVACY-GATE`).
