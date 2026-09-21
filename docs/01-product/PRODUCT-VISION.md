---
Status: REVIEW
Version: 0.2.0
Last Updated: 2026-09-21
Owners: Maike Lima (autoridade humana final)
Related ADRs: ADR-0001, ADR-0002, ADR-0003, ADR-0010
Wave: F0
Lifecycle: FREEZE-CONTROLLED
---

# Visão de Produto

## 1. Frase-conceito

> **"Waze da pesca + comunidade especializada + ecossistema comercial da pesca."**

## 2. O que é o Makpesca

Uma plataforma de pesca onde o **mapa é a experiência central**. O pescador marca pontos,
registra capturas, consulta condições, funciona sem internet no meio do rio, e depois
compartilha com a comunidade o que quiser — e apenas o que quiser.

Ao redor disso existe um ecossistema: comunidades regionais e temáticas, grupos, eventos,
rankings, lojas parceiras, ofertas e um plano PRO com inteligência de pesca.

## 3. Os três pilares

### Pilar 1 — Mapa e campo (o que o pescador usa no rio)
Posição atual, pontos próprios e públicos, capturas, GPS, corpos d'água, condições
ambientais, rotas e planejamento — com o **offline core** garantido (abrir, consultar os
dados locais, obter GPS, marcar ponto, registrar captura, sincronizar depois).

> A **base cartográfica offline** (mapa exibível sem rede) é recurso **candidato**, não
> prometido: depende de ADR-0010 e do `MAP-LICENSE-GATE`, ambos em aberto.
> Ver Constituição, Art. 4-A.

### Pilar 2 — Comunidade (o que o pescador usa em casa)
Perfis, seguidores, feed de capturas, comunidades por rio/represa/estado/espécie/modalidade,
grupos, mensagens, eventos, rankings, conquistas e desafios.

### Pilar 3 — Ecossistema comercial (o que sustenta o produto)
Lojas parceiras com perfil e localização, ofertas, cupons, afiliados com atribuição
rastreável, portal de parceiros e Makpesca PRO.

## 4. O que torna o produto defensável

| Diferencial | Por quê |
|-------------|---------|
| **Offline real (core)** | No lugar onde a pesca acontece, normalmente não há sinal. Produto que exige rede não serve. Refere-se ao *offline core*: marcar, registrar e não perder nada sem rede — não à base cartográfica, que é decisão à parte |
| **Geo-privacidade levada a sério** | Ponto de pesca é patrimônio pessoal. Vazar ponto destrói confiança de forma irreversível |
| **Especialização** | Cada tela existe para pesca. Não é rede social genérica com tema de peixe |
| **Comunidade regional** | Pesca é local: rio, represa, espécie e temporada específicos |
| **Dados próprios acumulados** | Capturas, pontos e condições geram inteligência que só existe com base instalada |

## 5. Para quem

Ver `PERSONAS.md`. Em resumo: pescador amador brasileiro (esportivo ou recreativo), do
iniciante ao experiente, mais guias, organizadores de pescaria e lojas do setor.

## 6. Jornada central (resumo)

```
descobrir região → preparar o dispositivo → ir pescar sem sinal → marcar ponto →
registrar captura com foto → voltar → sincronizar → decidir o que publicar →
compartilhar com comunidade → descobrir pessoas, lojas e eventos
```

"Preparar o dispositivo" inclui baixar uma região **se e quando** houver solução de
basemap offline decidida (ADR-0010). Sem ela, a jornada permanece válida: o offline core
não depende do basemap.

Detalhe em `CORE-JOURNEYS.md`.

## 7. Postura de privacidade

A privacidade é posicionamento de produto, não só conformidade:

- ponto privado é privado **no servidor**, não na interface;
- compartilhar é ato explícito, reversível e granular;
- publicar captura **não** publica o ponto;
- precisão compartilhada é escolha do usuário.

## 8. O que o produto não é

Ver `NON-GOALS.md`. Resumidamente: não é rede social genérica, não é marketplace completo,
não é app de navegação náutica certificado, não é rastreador de pessoas em tempo real
e não é catálogo colaborativo de pontos alheios.

## 9. Horizonte

| Horizonte | Foco |
|-----------|------|
| MVP | Conta, mapa, ponto, captura, privacidade, offline, sync, social mínimo |
| Pós-MVP | Comunidades completas, PRO, lojas e afiliados; basemap offline **se** ADR-0010 resolver |
| Futuro | Inteligência de pesca, desafios patrocinados, portal de parceiros maduro, admin completo |

## 10. Como medimos sucesso

Ver `PRODUCT-METRICS.md`. A métrica-chave da promessa é: **captura registrada offline e
sincronizada sem perda nem duplicação**. Se isso falha, o produto perde a razão de existir.
