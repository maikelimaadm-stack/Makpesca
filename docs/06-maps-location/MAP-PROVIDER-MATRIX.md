---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0009, ADR-0010
---

# Matriz de Providers de Mapa

## 0. Aviso metodológico

**Nenhuma célula desta matriz foi verificada em fonte primária nesta missão.**
Não há preços, limites ou termos de licença consultados com data. Por isso, todas as
células de avaliação estão marcadas como `A VERIFICAR`.

Esta matriz é a **estrutura da decisão**, não a decisão. Preenchê-la com estimativas
seria violar `CLAUDE.md` §11 (não inventar pesquisa).

## 1. Candidatos a avaliar

| Candidato | Natureza |
|-----------|----------|
| Google Maps Platform | Serviço proprietário de mapas (candidato online preferencial) |
| MapLibre (renderizador) | Renderizador open-source; precisa de fonte de dados/tiles |
| Dados compatíveis com OpenStreetMap | Fonte de dados aberta, com exigências de licença/atribuição |
| MapTiler | Serviço de tiles |
| PMTiles (formato) | Formato de pacote de tiles para distribuição/offline |
| Outros serviços de tiles | A levantar, com licença explícita para uso offline |

> Observação: "renderizador", "fonte de dados" e "serviço de tiles" são coisas diferentes.
> Uma solução completa normalmente combina os três. A matriz precisa registrar essa
> combinação, não tratar os nomes como alternativas equivalentes.

## 2. Critérios (colunas obrigatórias)

| # | Critério | Por que importa |
|---|----------|-----------------|
| 1 | Licença para uso **online** | Base legal |
| 2 | Licença para uso **offline** (armazenar e exibir sem rede) | **Decisivo** — R-030 |
| 3 | Custo inicial | Viabilidade |
| 4 | Custo em escala (por carregamento/sessão/região) | R-031 |
| 5 | Exigência de atribuição | Interface e conformidade |
| 6 | Download por região | Requisito de produto |
| 7 | Atualização de região baixada | Manutenção |
| 8 | Suporte iOS | Requisito |
| 9 | Suporte Android | Requisito |
| 10 | Suporte React Native (qualidade e manutenção) | Requisito |
| 11 | Vetor / raster | Tamanho e qualidade |
| 12 | Imagem de satélite | Valorizado por pescadores |
| 13 | Qualidade de hidrografia no Brasil | **Crítico para o domínio** |
| 14 | Geocoding | Busca por lugar |
| 15 | Navegação/rotas | Futuro |
| 16 | Lock-in e custo de saída | R-033 |
| 17 | Risco operacional (mudança de termos, descontinuação) | Sustentabilidade |
| 18 | Maturidade e manutenção | Risco técnico |

## 3. Matriz (a preencher)

| Critério | Google Maps | MapLibre + dados OSM | MapTiler | PMTiles | Outro |
|----------|-------------|----------------------|----------|---------|-------|
| 1. Licença online | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |
| 2. **Licença offline** | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |
| 3. Custo inicial | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |
| 4. Custo em escala | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |
| 5. Atribuição | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |
| 6. Download por região | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |
| 7. Atualização | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |
| 8. iOS | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |
| 9. Android | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |
| 10. React Native | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |
| 11. Vetor/raster | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |
| 12. Satélite | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |
| 13. Hidrografia BR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |
| 14. Geocoding | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |
| 15. Rotas | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |
| 16. Lock-in | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |
| 17. Risco operacional | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |
| 18. Maturidade | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR | A VERIFICAR |

## 4. Como preencher

Para cada célula: afirmação + link da fonte oficial + data de consulta. Exemplo de formato:

```
Permitido armazenar tiles offline: <sim/não/condicional>
Fonte: <URL oficial>
Consultado em: AAAA-MM-DD
Trecho relevante: "<citação literal>"
```

Célula sem fonte permanece `A VERIFICAR` e mantém `MAP-LICENSE-GATE` bloqueado.

## 5. Decisão

- Online: ADR-0009.
- Offline: ADR-0010 — **não pode ser decidido antes desta matriz estar preenchida**.
