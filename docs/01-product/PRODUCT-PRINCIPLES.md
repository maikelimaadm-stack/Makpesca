---
Status: REVIEW
Version: 0.2.0
Last Updated: 2026-09-21
Owners: Maike Lima (autoridade humana final)
Related ADRs: ADR-0010, ADR-0011, ADR-0012
Wave: F0
Lifecycle: FREEZE-CONTROLLED
---

# Princípios de Produto

## P1 — O campo vem antes da vitrine
Se uma decisão melhora a experiência de quem está no rio sem sinal e piora a vitrine social,
ela ganha. O produto existe primeiro para o momento da pesca.

## P2 — Privacidade por padrão
Ponto novo nasce `PRIVATE`. Compartilhar é ação explícita. Nunca o contrário.

## P3 — Publicar captura ≠ publicar ponto
São decisões separadas, em momentos diferentes da interface. O usuário nunca deve
descobrir depois que revelou o local.

## P4 — Offline não é modo degradado
Sem rede, o app continua útil e confiável: abre, mostra os dados locais, obtém GPS, permite
marcar ponto, registrar captura e anexar mídia; sincroniza depois, sem duplicar.
A sincronização é invisível quando funciona.

Este princípio cobre o **offline core**. A base cartográfica offline é decisão separada e
ainda aberta (Constituição, Art. 4-A); o core não depende dela.

## P5 — Nada se perde
Registro criado offline é durável antes mesmo de chegar à tela de sucesso. Perda de dado
é o pior defeito possível do produto.

## P6 — Reversibilidade
Compartilhamento pode ser revogado. Publicação pode ser despublicada. Conta pode ser
exportada e excluída.

## P7 — Especialização, não generalidade
Cada recurso social precisa responder: "como isso serve a quem pesca?" Se não responde,
não entra.

## P8 — Local importa
Rio, represa, espécie e temporada são o eixo de relevância — não "quem tem mais seguidores".

## P9 — Honestidade comercial
Oferta tem validade, condição e parceiro identificados. Conteúdo patrocinado é rotulado.
Comissão não altera o que o usuário vê como "melhor".

## P10 — Simplicidade antes de sofisticação
O MVP entrega o ciclo completo simples. Inteligência, gamificação e comércio vêm depois,
sobre base sólida.

## P11 — Confiança é operacional
Denúncia, bloqueio e moderação existem desde o primeiro recurso social. Recurso social
sem ferramenta de abuso não é lançado.

## P12 — Custo é requisito
Mapa e mídia são os maiores custos previstos. Recurso que não tem custo compreendido não
é aprovado para implementação.
