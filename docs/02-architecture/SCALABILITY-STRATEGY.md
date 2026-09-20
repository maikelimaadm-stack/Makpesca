---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0004, ADR-0018
---

# Estratégia de Escalabilidade

## 1. Postura

Escalar depois de medir. Nesta fase não existe base instalada; otimizar agora é
overengineering (P10). O que fazemos agora é **não fechar portas**.

## 2. Pontos de pressão previstos

| Área | Pressão | Sintoma esperado | Caminho de evolução |
|------|---------|------------------|---------------------|
| Consultas geoespaciais por viewport | Muitos pontos em região popular | Latência de mapa | Índice GiST, limite de bbox, clustering server-side, tiles de dados |
| Feed | Fan-out de seguidores | Latência e custo de leitura | Começar fan-out on read → materializar por usuário se necessário |
| Sync | Muitos dispositivos e mutações | Fila longa, lock | Cursor por usuário, lotes, paginação, backpressure |
| Mídia | Upload e egress | Custo e tempo | Derivativos, CDN, compressão no cliente |
| Jobs | Thumbnails, agregações, webhooks | Atraso | Fila por tipo, prioridade, concorrência controlada |
| Rankings | Agregações por período/região | Custo de cálculo | Pré-agregação incremental |
| Insights | Agregações amplas | Custo e risco de privacidade | Batch, coorte mínima, cache |

## 3. Decisões que preservam evolução

1. Identificadores opacos e estáveis, gerados no cliente — permitem particionamento futuro.
2. Escritas sincronizáveis idempotentes — permitem reprocessamento e replay.
3. Leituras paginadas por cursor — evitam offset caro.
4. Separação entre "dado verdadeiro" e "dado divulgável" — permite cache de leitura pública
   sem risco de vazar precisão.
5. Jobs fora do request — permite trocar hospedagem sem reescrever fluxo.
6. Eventos de domínio nomeados — permitem consumidores futuros.

## 4. Limites de plataforma a respeitar

A hospedagem serverless inicial impõe limites de tempo, payload e execução em background
(R-034). Consequências:

- operação longa **nunca** no request: vai para job;
- upload de mídia vai direto para o storage, não passa pelo corpo da API;
- exportação de dados é assíncrona, com entrega posterior;
- relatórios de parceiro são pré-calculados.

## 5. Cache

| Camada | O que pode ser cacheado | Nunca |
|--------|------------------------|-------|
| Cliente | Catálogos, região baixada, dados próprios | Coordenada de terceiro acima da precisão autorizada |
| CDN | Mídia pública, conteúdo público de SEO | Qualquer resposta autenticada |
| API | Catálogos, agregações públicas | Respostas que dependem do observador, sem chave por observador |

Regra crítica: **a chave de cache de qualquer resposta com localização inclui o perfil de
autorização do solicitante.** Caso contrário, cache vira vazamento (ver R-001).

## 6. Quando revisitar

Gatilhos para reavaliar esta estratégia: p95 de mapa acima do alvo, feed acima do alvo,
custo por usuário ativo acima do previsto, fila de jobs com atraso persistente.
