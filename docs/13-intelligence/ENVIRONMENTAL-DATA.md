---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: —
---

# Dados Ambientais

## 1. Dados desejados

| Dado | Uso | Criticidade |
|------|-----|-------------|
| Temperatura do ar | Contexto da captura | Média |
| Chuva / precipitação | Planejamento | Alta |
| Vento (velocidade e direção) | Segurança e produtividade | Alta |
| Pressão atmosférica | Correlação com atividade dos peixes | Alta |
| Fase da lua | Tradicionalmente relevante na pesca | Alta |
| Nascer e pôr do sol | Planejamento | Média |
| Temperatura da água | Correlação | Média (fonte difícil) |
| Nível do rio | **Decisivo em rios** | Alta (fonte difícil) |
| Vazão | Complementar | Média |
| Maré | Pesca costeira | Alta para litoral |

## 2. Modelo de dado

Cada valor carrega, obrigatoriamente:

| Campo | Motivo |
|-------|--------|
| `provider` | Rastreabilidade e licença |
| `observedAt` / `forecastFor` | Observação ≠ previsão |
| `quality` | Confiabilidade declarada |
| `origin` | Estação, modelo, sensor |
| `unit` | Unidade explícita |
| `ttl` | Validade do cache |
| `isForecast` | Distinguir claramente do observado |

Nunca exibir previsão como se fosse medição.

## 3. Arquitetura

`EnvironmentalDataPort` com adapters por provider. O domínio pede "condições para esta
região neste instante" — não conhece o provider.

Cache com TTL por tipo de dado (pressão muda rápido; fase da lua é determinística).
Snapshot é vinculado à captura para preservar o contexto histórico mesmo que o provider
mude.

## 4. Privacidade

| Regra |
|-------|
| A consulta ao provider usa coordenada **aproximada/região**, nunca a exata do ponto privado |
| Nenhum identificador de usuário vai ao provider |
| O snapshot armazenado fica vinculado à captura, sob as mesmas regras de privacidade |

## 5. Fontes

**Decisão aberta (Q-013).** Nenhuma fonte foi verificada nesta missão. Para cada candidata,
levantar com link e data:

1. cobertura geográfica no Brasil (inclusive interior);
2. dados disponíveis e granularidade;
3. licença e permissão de uso comercial;
4. custo por chamada / limite de requisições;
5. exigência de atribuição;
6. confiabilidade e disponibilidade histórica;
7. formato e facilidade de integração.

Nível de rio e vazão costumam depender de fontes oficiais específicas; maré idem.
São os dados mais difíceis — e dos mais valiosos.

## 6. Indisponibilidade

Provider fora do ar: mostrar ausência do dado, **nunca** valor inventado ou antigo
apresentado como atual. Dado expirado é rotulado como desatualizado.

## 7. Custo

Consultas ambientais podem ser cobradas por chamada. Mitigação: cache agressivo por
região + TTL, consultas em lote, e restringir dados detalhados ao PRO.

## 8. Fase

Pós-MVP para dados básicos (lua, sol, clima). Nível de rio e maré dependem de fonte
disponível.
