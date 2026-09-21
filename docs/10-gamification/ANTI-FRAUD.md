---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: —
---

# Antifraude (Gamificação)

> Antifraude comercial/afiliados está em `../11-commerce/COMMERCE-FRAUD.md`.

## 1. O que se tenta fraudar

| Alvo | Ganho para o fraudador |
|------|------------------------|
| Ranking | Prestígio |
| Desafio | Prêmio material |
| Conquista | Aparência de experiência |
| Reputação | Credibilidade para vender/guiar |

## 2. Vetores

| # | Vetor | Detecção |
|---|-------|----------|
| F1 | Foto de internet ou de terceiro | Hash global, análise de metadados, coerência com o histórico |
| F2 | Foto própria reutilizada | Hash do acervo do usuário |
| F3 | Medida/peso inflados | Distribuição estatística por espécie; outliers para revisão |
| F4 | Localização falsificada | Sinal de mock location, salto impossível, incoerência com a região |
| F5 | Registro retroativo apresentado como ao vivo | `recordSource` + tempo do servidor |
| F6 | Múltiplas contas | Sinais de dispositivo, padrão de uso, mesma mídia |
| F7 | Conluio entre usuários | Grafo de interações e coincidências |
| F8 | Registro em massa automatizado | Rate limit, padrão temporal |
| F9 | Espécie declarada incorretamente | Verificação por comunidade e revisão |

## 3. Princípios de resposta

| Princípio |
|-----------|
| **Nunca apagar o registro do usuário por suspeita** — marcar como inelegível |
| Suspeita não é condenação: sinais somam, não decidem sozinhos |
| Revisão humana antes de qualquer consequência relevante |
| Explicar ao usuário a razão da inelegibilidade e permitir contestar |
| Não revelar os detalhes da detecção (senão ensina a burlar) |

## 4. Estados de um registro para gamificação

| Estado | Significado |
|--------|-------------|
| `ELIGIBLE` | Conta normalmente |
| `UNDER_REVIEW` | Fora do ranking até a decisão |
| `INELIGIBLE` | Fora do ranking, com motivo |
| `CONFIRMED_FRAUD` | Sanção ao autor, registro marcado |

O registro continua existindo para o usuário em todos os casos.

## 5. Sinais coletados

Hash de mídia, `locationSource`, indicadores de localização simulada, coerência temporal,
velocidade implícita entre registros, padrão de horário, similaridade com registros de
outras contas, reincidência.

**Nenhum sinal é armazenado com coordenada exata em sistema de análise** — usa-se célula
de agregação.

## 6. Sanções

| Gravidade | Ação |
|-----------|------|
| Suspeita isolada | Inelegibilidade daquele registro |
| Padrão recorrente | Exclusão de rankings por período |
| Fraude confirmada em desafio | Desclassificação + perda de prêmio + sanção na conta |
| Reincidência | Suspensão ou banimento |

## 7. Pré-requisito

**Nenhum ranking ou desafio é lançado sem, no mínimo:** hash de mídia, sinais de
localização, limites de registro e caminho de revisão humana. Sem isso, o recurso cria
incentivo que não conseguimos policiar.
