---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0004, ADR-0012
---

# Modelo de Dados Geoespaciais

## 1. Princípios

1. Toda geometria usa **WGS84 (SRID 4326)** como referência de armazenamento.
2. Cálculo de distância usa tipo geográfico ou projeção adequada — nunca comparação
   ingênua de graus.
3. PostGIS é requisito de seleção do banco (ver ADR-0004).
4. Coordenada verdadeira e coordenada divulgável nunca ocupam o mesmo campo.

## 2. Tipos de geometria por entidade

| Entidade | Geometria | Observação |
|----------|-----------|------------|
| `Spot` | Ponto | coordenada verdadeira |
| `Catch` | Ponto (opcional) | pode divergir do ponto |
| `WaterBody` | Linha ou polígono | rio como linha; represa/lago como polígono |
| `Region` | Polígono / multipolígono | hierarquia país → estado → município → bacia |
| `StoreLocation` | Ponto | endereço comercial, público |
| `Event.meetingPoint` | Ponto | precisão própria |
| `OfflineRegion` | Polígono ou caixa | área baixada pelo usuário |
| Célula de agregação | Grade | usada por Intelligence |

## 3. Precisões e suas representações

| Precisão | O que é retornado | Observação |
|----------|-------------------|------------|
| `EXACT` | coordenada verdadeira | só para autorizados |
| `APPROXIMATE` | coordenada com jitter estável dentro de um raio declarado | raio parametrizado e informado ao cliente |
| `REGION` | centroide/identificador da região | sem ponto real |
| `WATER_BODY_ONLY` | identificador do corpo d'água | sem coordenada |
| `HIDDEN` | nada | ausência explícita do campo |

Regras:
- o raio de `APPROXIMATE` é **declarado** na resposta (o cliente precisa saber que é aproximado);
- o jitter é determinístico por (recurso, observador) — ver INV-G06;
- nunca retornar `APPROXIMATE` derivado de uma leitura diferente a cada chamada.

## 4. Consultas previstas

| Consulta | Uso | Consideração |
|----------|-----|--------------|
| Pontos dentro do viewport | Mapa | Limite de área e de resultados; degradação por observador |
| Pontos próximos a mim | Descoberta | Raio máximo; nunca revelar precisão superior à autorizada |
| Capturas públicas por corpo d'água | Exploração | Agregação |
| Lojas próximas | Comércio | Dado público, sem restrição especial |
| Região offline: o que baixar | Offline | Recorte por polígono |
| Agregações por célula | Intelligence | Coorte mínima antes de publicar |

## 5. Índices (conceitual)

Serão necessários índices espaciais (GiST) em: `Spot.location`, `Catch.location`,
`StoreLocation.location`, `WaterBody.geometry`, `Region.geometry`.
A definição concreta ocorre na fase de implementação, não aqui.

## 6. Derivação de região e corpo d'água

Ao registrar ponto ou captura, o servidor deriva `regionId` e, quando possível,
`waterBodyId` por contenção/proximidade. Essa derivação:

- acontece no servidor (o cliente offline pode estimar e o servidor corrige);
- é armazenada para permitir agregação sem reprocessar geometria;
- **não** substitui a coordenada verdadeira.

## 7. Qualidade de localização

| Campo | Significado |
|-------|-------------|
| `locationSource` | `GPS`, `MAP_PICK`, `IMPORT`, `MANUAL` |
| `locationAccuracyMeters` | precisão informada pelo sensor |
| `locationCapturedAt` | quando a leitura foi obtida |
| `locationTrustSignals` | indícios de falsificação (mock location, salto improvável) |

Localização com sinal de falsificação não é descartada silenciosamente: é marcada e
torna o registro inelegível para ranking (ver R-044).

## 8. Offline

A região baixada pelo usuário guarda: polígono, data do download, versão dos dados,
tamanho em disco e origem (provider). O conteúdo cartográfico obedece à licença do
provider escolhido em ADR-0010 — **decisão aberta e bloqueante**.

## 9. Proibições

- Nunca colocar coordenada em índice de busca textual.
- Nunca expor coordenada verdadeira em resposta de listagem pública, nem "para filtrar
  depois no cliente".
- Nunca enviar conjunto de pontos privados para serviço de terceiros (geocoding, mapa,
  analytics).
- Nunca registrar coordenada exata em log.
