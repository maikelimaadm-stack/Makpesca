---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: —
---

# Panorama Competitivo

## 0. Aviso metodológico — leia antes de usar este documento

**Nesta missão (MP-DOC-00 v2) não foi realizada verificação em fonte primária.**
Nenhum preço, recurso, termo de uso ou número de usuários foi consultado na documentação
oficial ou no site dos concorrentes com data registrada.

Portanto, este documento contém **estrutura de análise e hipóteses declaradas**, não fatos.
Toda linha está classificada. Nada aqui pode sustentar decisão congelada.

### Classificação obrigatória

| Marca | Significado |
|-------|-------------|
| `FACT` | Verificado em fonte primária, com link e data de consulta |
| `OBSERVATION` | Observado diretamente no produto, com data e versão |
| `USER REPORT` | Relato de usuário/terceiro, com origem identificada |
| `HYPOTHESIS` | Suposição da equipe, não verificada |
| `OPPORTUNITY` | Oportunidade derivada, dependente da validação acima |

**Neste momento não existe nenhuma linha `FACT` ou `OBSERVATION` neste documento.**

## 1. Concorrentes a investigar

| Nome | Tipo | Relevância esperada | Status da pesquisa |
|------|------|---------------------|--------------------|
| Fishbrain | App internacional de pesca com rede social e mapa | ALTA | NÃO PESQUISADO |
| Fishing Points | App de mapa/pontos de pesca com uso offline | ALTA | NÃO PESQUISADO |
| Sua Pesca | App brasileiro do setor | ALTA | NÃO PESQUISADO |
| TucunaPro | App brasileiro do setor | MÉDIA | NÃO PESQUISADO |
| Navionics / cartas náuticas | Cartografia náutica e batimetria | MÉDIA | NÃO PESQUISADO |
| Windy / apps de clima | Condições ambientais | MÉDIA | NÃO PESQUISADO |
| Grupos de WhatsApp/Facebook regionais | Concorrente informal real | ALTA | NÃO PESQUISADO |

> A menção acima reflete os nomes indicados no briefing. **Não afirma** que esses produtos
> existem hoje com esses recursos, preços ou disponibilidade no Brasil.

## 2. Roteiro de pesquisa obrigatório (por concorrente)

Para cada concorrente, coletar com link e data:

1. plataformas suportadas (iOS, Android, Web);
2. existência e qualidade de mapa offline; se há download de região;
3. modelo de privacidade de pontos (existe ponto privado? precisão configurável?);
4. modelo social (feed, seguidores, comunidades, mensagens);
5. registro de capturas (campos disponíveis, fotos, espécies);
6. dados ambientais oferecidos e fontes citadas;
7. modelo de monetização e preço com moeda e data;
8. presença e localização em português do Brasil;
9. catálogo de espécies brasileiras;
10. parcerias comerciais/lojas;
11. reclamações recorrentes em lojas de aplicativos (classificar como `USER REPORT`);
12. termos de uso relevantes (uso de dados, propriedade de conteúdo).

## 3. Hipóteses de posicionamento (a validar)

| ID | Hipótese | Classificação |
|----|----------|---------------|
| H-01 | Nenhum concorrente trata geo-privacidade como recurso central de produto, com precisão granular e revogação | `HYPOTHESIS` |
| H-02 | O offline dos concorrentes é parcial e falha em locais sem sinal prolongado | `HYPOTHESIS` |
| H-03 | Apps internacionais têm catálogo de espécies e comunidade fracos para o Brasil | `HYPOTHESIS` |
| H-04 | A comunidade de pesca brasileira hoje se organiza majoritariamente em WhatsApp/Facebook | `HYPOTHESIS` |
| H-05 | Lojas de pesca locais não têm canal digital eficiente de divulgação segmentada | `HYPOTHESIS` |

## 4. Oportunidades derivadas (dependentes de validação)

| ID | Oportunidade | Depende de |
|----|--------------|-----------|
| O-01 | Privacidade granular de pontos como diferencial declarado de marca | H-01 |
| O-02 | Offline verdadeiramente confiável, testado como requisito e não como recurso | H-02 |
| O-03 | Comunidades regionais brasileiras por rio/represa/estado | H-03, H-04 |
| O-04 | Ecossistema comercial local com atribuição honesta | H-05 |
| O-05 | Catálogo de espécies e iscas brasileiro de qualidade | H-03 |

## 5. Regra de uso

Este documento **não pode** ser congelado enquanto todas as linhas relevantes forem
`HYPOTHESIS`. A pesquisa com fonte primária é pré-condição para o freeze da onda `F1`.
Ver `../00-governance/OPEN-QUESTIONS.md`.
