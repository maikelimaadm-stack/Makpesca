---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: —
---

# Conquistas

## 1. Propósito

Reconhecer progresso individual sem criar competição direta. Conquista é sobre a jornada
do próprio pescador — por isso tem risco de fraude menor que o ranking.

## 2. Categorias

| Categoria | Exemplos |
|-----------|----------|
| Primeiros passos | Primeira captura registrada, primeiro ponto, primeira publicação |
| Volume | 10, 100, 1.000 capturas |
| Diversidade | 5, 10, 25 espécies distintas |
| Exploração | Pescou em N corpos d'água; N regiões; primeira região offline |
| Social | Entrou em comunidade, participou de evento, ajudou com resposta útil |
| Contribuição | Contribuiu com catálogo, reportou conteúdo corretamente |
| Conservação | Registros de soltura (pesque e solte) |
| Constância | Registrou em N meses seguidos |

## 3. Regras

| # | Regra |
|---|-------|
| 1 | Conquista considera capturas privadas do próprio usuário (é dele, sobre ele) |
| 2 | Exibir a conquista no perfil é opcional |
| 3 | A conquista **não** revela onde nem quando o usuário pescou |
| 4 | Conquista concedida não é removida sem registro de motivo (INV-R03) |
| 5 | Conquista de exploração usa região, nunca coordenada |
| 6 | Conquista não é vendida nem incluída em plano pago |

## 4. Privacidade

Ponto sensível: uma conquista do tipo "pescou no Rio X" **publica indiretamente** onde a
pessoa esteve. Por isso:

- conquistas geográficas usam recorte amplo (estado, bacia), não corpo d'água específico,
  a menos que o usuário autorize;
- exibição no perfil é opt-in;
- nenhuma conquista é anunciada automaticamente no feed sem escolha do usuário.

## 5. Cálculo

Avaliação assíncrona após eventos relevantes (nova captura, nova publicação). Idempotente:
reprocessar não concede duas vezes. Conquista concedida guarda a evidência (referência ao
que a gerou), sem expor essa evidência a terceiros.

## 6. Antifraude

Menor risco, mas não zero: conquistas de volume podem ser infladas com registros falsos.
Mitigação: limites de registro por janela, detecção de padrão e conquistas que dependem de
diversidade real em vez de repetição.

## 7. Fase

Pós-MVP.
