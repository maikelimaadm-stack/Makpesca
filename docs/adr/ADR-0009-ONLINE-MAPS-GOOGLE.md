# ADR-0009 — Mapa Online

- **Status:** PROPOSED
- **Date:** 2026-09-20
- **Onda:** F5

## Context
O mapa é a experiência central do produto quando há conectividade. Precisa de boa base
cartográfica no Brasil, imagem de satélite (valorizada por pescadores) e SDK maduro para
React Native e web.

## Decision Drivers
- Qualidade da base no Brasil, especialmente hidrografia.
- Imagem de satélite.
- Maturidade de SDK em iOS, Android e web.
- Custo por uso.
- Restrições de licença.

## Options Considered
| Opção | Prós esperados | Contras esperados |
|-------|----------------|-------------------|
| **Google Maps Platform** | Base e satélite de alta qualidade, SDKs maduros, boa cobertura no Brasil | Custo por uso; restrições de cache; lock-in |
| Renderizador open-source + tiles de terceiro | Custo potencialmente menor, mais controle | Qualidade e satélite a verificar; mais integração |
| Apple Maps (iOS) + outro (Android) | Nativo em iOS | Dois comportamentos diferentes; complexidade |

## Decision
Adotar **Google Maps Platform como candidato preferencial para o mapa online**, conforme o
briefing — com duas condições explícitas:

1. a camada de mapa fica **isolada** nos clientes, para permitir troca;
2. **esta decisão não se estende ao mapa offline** (ADR-0010), que é decisão separada.

## Consequences
- Dados do produto nunca são enviados ao provider (apenas viewport).
- Chave de cliente tratada como pública, restrita por aplicativo e monitorada.
- Atribuição conforme exigido pela licença.
- Custo monitorado com teto e alerta.

## Risks
- R-031: custo cresce com o uso.
- R-033: lock-in.
- R-030: **assumir que o uso online autoriza o uso offline** — o erro mais caro possível.

## Security Impact
Chave no cliente é extraível: restringir por pacote/origem e por API habilitada.

## Privacy Impact
O provider recebe a área visualizada. **Nunca** recebe a lista de pontos privados do
usuário. Isso precisa ser verificado na implementação, não assumido.

## Offline Impact
**Nenhum.** O offline é tratado no ADR-0010. Esta decisão não resolve offline.

## Portability Impact
Médio: a camada de mapa isolada permite troca com custo de reescrita da camada de
apresentação, sem afetar dados.

## Cost Impact
A verificar com a tabela oficial de preços, com data. Requisito do `COST-GATE`.

## Operational Impact
Monitorar consumo, definir teto, alerta de custo anômalo.

## Open Questions
- Q-005: o que a licença permite em termos de cache, inclusive temporário?
- Qual o custo por carregamento/sessão no plano pretendido?
- A qualidade da hidrografia brasileira atende ao domínio?

## Evidence
Nenhuma verificada nesta missão. **Não pode ir para `ACCEPTED` sem citação de termos e
preços com data.**

## Supersedes / Superseded By
— / —
