---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0012
---

# Rankings

## 1. Princípio

Ranking é motivação, não verdade absoluta. Como cria incentivo para fraude, **antifraude
e elegibilidade vêm antes do recurso** (ver `ANTI-FRAUD.md`).

## 2. Dimensões

| Dimensão | Exemplos |
|----------|----------|
| Métrica | Quantidade de capturas, espécies distintas, maior exemplar (peso/comprimento), constância |
| Escopo | Global, região, estado, corpo d'água, comunidade |
| Recorte temático | Espécie, modalidade |
| Período | Dia, semana, mês, temporada, ano, desafio |

## 3. Regras de elegibilidade

Uma captura só entra em ranking se:

| # | Condição |
|---|----------|
| 1 | Está publicada (não privada) |
| 2 | Tem espécie identificada do catálogo |
| 3 | Tem mídia (quando a métrica for de tamanho/peso) |
| 4 | Passou pela verificação de moderação |
| 5 | Não tem sinal de localização falsificada |
| 6 | Está dentro do período e do escopo |
| 7 | O autor não está sob sanção |
| 8 | A mídia não é duplicata de outra já usada (hash) |

Capturas privadas **nunca** entram em ranking (INV-R01).

## 4. Privacidade

| Regra |
|-------|
| Ranking nunca revela localização acima da precisão autorizada (INV-R02) |
| Ranking por corpo d'água usa apenas capturas que autorizaram esse nível |
| Participação em ranking é opt-in configurável |
| Um ranking regional com poucos participantes pode identificar pessoas: aplicar coorte mínima |

## 5. Cálculo

| Aspecto | Regra |
|---------|-------|
| Atualização | Periódica (não em tempo real), para reduzir custo e manipulação |
| Empate | Critério determinístico e publicado (ex.: quem registrou antes) |
| Recalcular | Quando captura é removida, despublicada ou invalidada |
| Histórico | Rankings encerrados são congelados com a data |

## 6. Apresentação

- Exibir sempre o período e o escopo.
- Exibir o critério da métrica em linguagem clara.
- Não exibir dado que permita inferir local.
- Permitir ao usuário sair do ranking.

## 7. Riscos

| Risco | Mitigação |
|-------|-----------|
| Fraude por foto reciclada | Hash de mídia e verificação |
| Fraude por medida inflada | Revisão do topo; exigência de foto com referência |
| Localização falsa | Inelegibilidade |
| Pressão para publicar ponto | Ranking nunca exige precisão alta |
| Incentivo a más práticas de pesca | Métricas que não premiem quantidade excessiva; destaque para soltura |

## 8. Fase

Pós-MVP. Nenhum ranking é lançado antes de `ANTI-FRAUD.md` ter controles implementáveis.
