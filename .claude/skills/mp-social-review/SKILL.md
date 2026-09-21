---
name: mp-social-review
description: Revisa recursos sociais — feed, comunidades, grupos, eventos, mensagens — quanto a privacidade, moderação e abuso. Use ao criar ou alterar recurso social.
---

# mp-social-review

## SSOTs
- `docs/09-social/SOCIAL-MODEL.md`, `FEED-MODEL.md`, `COMMUNITY-MODEL.md`,
  `GROUP-MODEL.md`, `MESSAGING-MODEL.md`, `EVENTS-MODEL.md`, `MODERATION.md`, `REPORT-BLOCK.md`
- `.claude/rules/social.md`

## Checklist
1. O recurso serve especificamente a quem pesca?
2. **Existe denúncia, bloqueio e caminho de moderação?** (sem isso, não lança)
3. Nenhuma relação social concede localização por si só?
4. Publicar captura deixa o ponto intacto?
5. Bloqueio encerra follow e concessões entre as partes?
6. Conteúdo removido some para todos; contadores não revelam o oculto?
7. Limites anti-spam definidos (publicação, comentário, convite, mensagem)?
8. Descoberta usa região + consentimento, nunca coordenada?
9. Conteúdo patrocinado é rotulado e limitado?
10. A capacidade de moderação comporta o alcance do recurso?
11. Notificações sem dado sensível?
12. Menores têm restrições, quando aplicável?

## Saída
Achados + veredito do `SOCIAL-SAFETY-GATE`.
