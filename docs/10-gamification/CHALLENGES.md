---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: —
---

# Desafios

## 1. O que é

Competição com período, regra e, eventualmente, patrocinador e prêmio. É o recurso com
**maior incentivo à fraude** do produto — e o único que pode envolver dinheiro de terceiros.

## 2. Estrutura

| Campo | Descrição |
|-------|-----------|
| Nome e descrição | |
| Período | Início e fim, com fuso |
| Escopo | Espécie, região, corpo d'água, comunidade, modalidade |
| Regras | Critério objetivo de pontuação |
| Elegibilidade | Quem pode participar |
| Requisitos de comprovação | Foto, medida, testemunha, referência de escala |
| Patrocinador | Parceiro, quando houver |
| Prêmio | Descrição e regulamento |
| Regulamento | Documento formal quando houver prêmio |
| Estado | Rascunho, aberto, encerrado, apurado, cancelado |

## 3. Elegibilidade

Além das regras de ranking (`RANKINGS.md` §3):

| # | Condição adicional |
|---|--------------------|
| 1 | Inscrição explícita no desafio |
| 2 | Aceite do regulamento |
| 3 | Captura registrada **durante** o período (não importada depois) |
| 4 | Registro do tipo `LIVE` quando o desafio exigir |
| 5 | Mídia original, com hash único |
| 6 | Sem sinais de localização falsificada |
| 7 | Conta sem sanção ativa |

## 4. Antifraude específico

| Vetor | Controle |
|-------|----------|
| Foto reutilizada | Hash + comparação com o acervo do usuário e global |
| Foto de terceiro | Verificação de metadados de captura e de coerência temporal |
| Medida inflada | Exigência de referência de escala; revisão manual do topo |
| Localização falsa | Sinais de GPS + coerência com a região do desafio |
| Múltiplas contas | Detecção de dispositivo e padrão |
| Registro fora do período | Tempo do servidor é autoridade |
| Conluio | Revisão humana antes da premiação |

**Todo desafio com prêmio tem revisão humana obrigatória antes da apuração final.**

## 5. Patrocínio

| Regra |
|-------|
| Patrocinador é identificado claramente |
| Patrocinador **não** tem acesso a dados pessoais dos participantes |
| Patrocinador não influencia a apuração |
| Prêmio e responsabilidade do prêmio constam no regulamento |
| Desafio patrocinado não vira apuração enviesada por interesse comercial |

## 6. Aspectos legais

Desafio com premiação pode ter implicações legais (regras de promoção comercial,
sorteio, tributação). **Exige validação jurídica** antes do primeiro desafio premiado.
Sem essa validação, desafios são apenas simbólicos, sem prêmio material.

Nunca operar como aposta (`NON-GOALS` §7).

## 7. Privacidade

Participação pode ser pública (faz parte do jogo), mas a **localização** continua sob as
mesmas regras: participar de um desafio regional não obriga a revelar o ponto.

## 8. Fase

Futuro. Depende de rankings estáveis, antifraude funcionando e validação jurídica.
