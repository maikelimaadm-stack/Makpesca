# Regra — Social

## Aplicação
Feed, posts, comentários, comunidades, grupos, eventos, mensagens.

## SSOTs
`docs/09-social/*`, `docs/adr/ADR-0018-SOCIAL-GRAPH.md`.

## Regras
1. Todo recurso social responde à pergunta: "como isso serve a quem pesca?"
2. **Recurso social não é lançado sem denúncia, bloqueio e caminho de moderação.**
3. Nenhuma relação social concede localização por si só — exige `LocationGrant`.
4. Publicar captura nunca publica o ponto.
5. Bloqueio encerra follow nos dois sentidos e as concessões entre as partes.
6. Conteúdo removido por moderação some para todos.
7. Contadores públicos não revelam conteúdo oculto.
8. Limites anti-spam em publicação, comentário, convite e mensagem.
9. Descoberta por região usa região declarada + consentimento, nunca coordenada.
10. Conteúdo patrocinado é rotulado e limitado em frequência.
11. Comunidades recebem, no máximo, precisões baixas (`REGION`, `WATER_BODY_ONLY`).
12. Ranking só considera conteúdo elegível (ver antifraude).

## Proibido
- Feed que ordene por proximidade exata.
- Sugerir pessoas com base em localização precisa.
- Recurso de localização em tempo real sem decisão própria registrada.
- Notificação contendo coordenada.
