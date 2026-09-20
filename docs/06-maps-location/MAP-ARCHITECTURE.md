---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0009, ADR-0010, ADR-0012
---

# Arquitetura de Mapa

## 1. Separação fundamental

O mapa tem **duas camadas independentes**:

| Camada | O que é | De onde vem |
|--------|---------|-------------|
| **Base cartográfica** | Ruas, relevo, satélite, hidrografia | Provider de mapa (online) ou pacote offline |
| **Dados Makpesca** | Pontos, capturas, lojas, eventos, comunidades, regiões | **Sempre** da nossa API / SQLite local |

Consequência: trocar o provider de base cartográfica **não** afeta os dados do produto.
Os dados do produto nunca são enviados ao provider de mapa.

## 2. Camadas de conteúdo (a documentar como recurso)

| Camada | Origem | Offline | Fase |
|--------|--------|---------|------|
| Posição atual | GPS do dispositivo | Sim | MVP |
| Pontos próprios | Local + API | Sim | MVP |
| Pontos compartilhados comigo | API (precisão autorizada) | Sim, se baixado | MVP |
| Pontos públicos | API | Parcial | MVP |
| Clusters | Calculado (cliente e/ou servidor) | Sim | MVP |
| Capturas recentes | API | Parcial | Pós-MVP |
| Favoritos | Local + API | Sim | Pós-MVP |
| Corpos d'água | Catálogo | Sim | Pós-MVP |
| Regiões offline baixadas | Local | Sim | Pós-MVP |
| Lojas parceiras | API | Parcial | Pós-MVP |
| Eventos | API | Não | Pós-MVP |
| Comunidades por região | API | Não | Pós-MVP |
| Pescadores próximos (com consentimento) | API | Não | Pós-MVP |
| Clima, vento, pressão, lua | Adapter ambiental | Cache com TTL | Pós-MVP |
| Nível do rio / vazão | Adapter ambiental | Cache com TTL | Pós-MVP |
| Rotas e planejamento | Cliente + provider | Parcial | Futuro |
| Batimetria | Fonte licenciada | Depende | Futuro (Q-014) |

## 3. Filtros previstos

Espécie, isca, técnica, período, tipo de corpo d'água, tipo de ponto, capturas recentes,
apenas meus pontos, apenas compartilhados comigo, favoritos, distância máxima.

Regra: **filtro nunca vaza informação**. Um filtro que retorna "nenhum resultado" não pode
revelar, por eliminação, a existência ou posição de um ponto privado de terceiro.

## 4. Desempenho

| Requisito | Regra |
|-----------|-------|
| Limite de área | Consulta por viewport com área máxima |
| Limite de resultados | Paginação e/ou clustering server-side |
| Clustering | Cliente para volumes pequenos; servidor quando necessário |
| Bateria | Amostragem de GPS adaptativa; sem localização em background no MVP (R-047, R-048) |
| Renderização | Evitar redesenhar marcadores a cada frame; agrupar atualizações |

## 5. Interação com geo-privacy

Toda camada que exibe localização de terceiro recebe **apenas** a precisão autorizada.
O cliente não tem, em momento algum, a coordenada verdadeira que deveria esconder.
Quando a precisão é `APPROXIMATE`, a interface **mostra explicitamente** que a posição é
aproximada (e o raio), para não induzir o usuário ao erro.

## 6. Mapa na Web

A Web usa a mesma separação de camadas. Pode usar SDK diferente do mobile, desde que os
dados venham da mesma API com a mesma degradação de precisão.

## 7. Dependências abertas

- Provider online: ADR-0009 (proposto: Google Maps Platform).
- Provider offline: **ADR-0010, decisão aberta e bloqueante** (Q-004, Q-005).
- Nunca assumir que o provider online pode servir ao offline.
