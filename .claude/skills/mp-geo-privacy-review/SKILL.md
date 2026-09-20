---
name: mp-geo-privacy-review
description: Revisa qualquer mudança que toque localização — precisão, visibilidade, concessões, degradação, logs e vazamentos. Use sempre que houver coordenada envolvida.
---

# mp-geo-privacy-review

## SSOTs
- `docs/06-maps-location/GEO-PRIVACY.md`
- `docs/08-security-privacy/GEO-PRIVACY-THREAT-MODEL.md`
- `docs/15-quality/PRIVACY-TEST-MATRIX.md`
- `.claude/rules/geo-privacy.md`

## Checklist
1. A degradação acontece **server-side**, por um **único** componente?
2. Precisão efetiva = a mais restritiva entre dono, concessão, moderação e contexto?
3. Publicar captura deixa o ponto intacto?
4. Jitter é determinístico por (recurso, observador)?
5. O raio de `APPROXIMATE` é informado ao cliente?
6. Cache inclui o perfil do observador na chave?
7. Revogação tem efeito imediato, inclusive no dispositivo?
8. Existe teste por perfil de observador (P1..P12) para cada endpoint com localização?
9. Nenhuma coordenada em log, analytics, crash, URL, deep link ou push?
10. EXIF removido antes de publicar?
11. 404 em vez de 403 quando revelar a existência é vazamento?
12. Nenhum ponto privado enviado a terceiros?
13. Insight passa por coorte mínima e verificação de reidentificação?

## Ataques a considerar
Averaging, jitter repetido, triangulação por metadados, interseção de publicações,
diferença entre caminhos, coorte pequena, rastro temporal.

## Saída
Achados com severidade e correção. Veredito do `PRIVACY-GATE`.
**Qualquer item falho bloqueia.**
