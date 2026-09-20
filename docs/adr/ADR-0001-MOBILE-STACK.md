# ADR-0001 — Stack Mobile

- **Status:** PROPOSED
- **Date:** 2026-09-20
- **Onda:** F2

## Context
O aplicativo móvel é o produto principal. Precisa de: mapa, GPS, câmera, banco local
(SQLite), fila de upload resiliente, funcionamento offline confiável e presença em
Android e iOS. A equipe é pequena e o tempo até o MVP importa.

## Decision Drivers
- Um código para duas plataformas.
- Acesso confiável a GPS, câmera, armazenamento e SQLite.
- Upload em segundo plano e resiliente.
- Qualidade da integração com SDKs de mapa.
- Velocidade de desenvolvimento e tamanho da equipe.
- Facilidade de distribuição e atualização.

## Options Considered
| Opção | Prós | Contras |
|-------|------|---------|
| **React Native + Expo + TypeScript** | Um código, ecossistema grande, TypeScript compartilhado com API/Web, ciclo rápido | Dependência do ecossistema Expo; módulos nativos específicos podem exigir configuração adicional |
| React Native sem Expo | Mais controle nativo | Mais custo de manutenção de build |
| Flutter | Desempenho e consistência de UI | Linguagem diferente do resto da stack; não compartilha tipos com a API |
| Nativo (Kotlin + Swift) | Máximo controle e desempenho | Dobra o esforço; inviável para o tamanho da equipe |

## Decision
Adotar **React Native + Expo + TypeScript** como baseline, conforme o briefing.

## Consequences
- TypeScript de ponta a ponta: tipos de `packages/contracts` compartilhados.
- Ciclo de desenvolvimento rápido.
- Necessário validar, com prova de conceito, os pontos sensíveis: SQLite, mapa,
  upload em background e precisão de GPS.

## Risks
- Expo pode não cobrir algum requisito nativo (A-011): mitigação é usar módulos nativos
  ou ejetar, com custo.
- Desempenho de mapa com muitos marcadores.
- Consumo de bateria (R-047).

## Security Impact
Credenciais no keystore/keychain; atenção ao que bibliotecas de terceiros registram em log.

## Privacy Impact
O app lida com coordenadas exatas do próprio usuário. Nenhuma biblioteca de terceiros pode
receber esses dados. Crash reporting precisa de filtro (V4).

## Offline Impact
Decisivo: a escolha precisa suportar SQLite robusto, fila persistente e retomada de upload.
É o critério de aceitação mais importante da prova de conceito.

## Portability Impact
Trocar de framework mobile depois é caro. A mitigação é manter a lógica de domínio e os
contratos fora do código de UI, em pacotes compartilhados.

## Cost Impact
Custo de build/distribuição a verificar. Equipe menor reduz custo de desenvolvimento.

## Operational Impact
Atualizações passam pelas lojas; versões antigas convivem por muito tempo — a API precisa
tolerá-las (`API-VERSIONING`).

## Open Questions
- A-011: Expo cobre GPS, mapa, SQLite e upload em background necessários?
- Qual estratégia de atualização (build vs atualização over-the-air, se permitida)?

## Evidence
Nenhuma medição própria realizada. Decisão baseada no briefing e em experiência geral do
setor. **Prova de conceito obrigatória antes de `ACCEPTED`.**

## Supersedes / Superseded By
— / —
