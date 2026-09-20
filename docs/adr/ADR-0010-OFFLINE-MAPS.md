# ADR-0010 — Mapa Offline

- **Status:** **OPEN — BLOQUEANTE**
- **Date:** 2026-09-20
- **Onda:** F5

## Context
Offline real é a promessa central do produto: no lugar onde a pesca acontece, geralmente
não há sinal. Isso exige base cartográfica disponível **sem rede**.

Existe um risco jurídico e de produto de primeira grandeza: **armazenar e exibir tiles de
um provider proprietário fora do que a licença permite**. Se o produto for construído
assumindo que "cacheamos o mapa do provider online", ele pode se tornar inviável ou ilegal
depois de pronto (R-030).

Por isso, esta decisão é **separada** de ADR-0009 e bloqueia a onda F5.

## Decision Drivers
1. **Licença explícita para uso offline** — critério eliminatório.
2. Download por região com tamanho controlado.
3. Qualidade da base no Brasil, sobretudo hidrografia.
4. Suporte a React Native em Android e iOS.
5. Custo por região/usuário/atualização.
6. Atualização de região já baixada.
7. Atribuição exigida.
8. Manutenção ativa e risco operacional.
9. Necessidade (ou não) de satélite offline.

## Options Considered

> **Nenhuma opção foi verificada.** A matriz completa está em
> `../06-maps-location/MAP-PROVIDER-MATRIX.md`, com todas as células em `A VERIFICAR`.

| Família de solução | Observação |
|--------------------|------------|
| Renderizador open-source + dados abertos compatíveis com OSM | Precisa verificar licença de redistribuição e de armazenamento no app, além da atribuição obrigatória |
| Serviço comercial de tiles com licença de uso offline | Precisa verificar se a licença cobre armazenamento no dispositivo e por quanto tempo |
| Formato de pacote de tiles (ex.: PMTiles) + fonte licenciada | O formato resolve distribuição, **não** resolve licença: a fonte dos dados é que decide |
| Base própria construída a partir de dados abertos | Maior controle, maior esforço e responsabilidade |
| Não oferecer mapa offline (apenas dados do produto sem base) | Reduz a promessa; ainda permite GPS, pontos e capturas sem rede |

Observação importante: renderizador, fonte de dados e serviço de tiles são coisas
distintas. A decisão é sobre a **combinação**, não sobre um nome isolado.

## Decision
**Em aberto.** Nenhuma solução é adotada nesta missão.

Método obrigatório para decidir:
1. preencher a matriz de providers com fonte e data para cada célula;
2. obter, por escrito, a resposta sobre armazenamento offline de cada candidato;
3. medir tamanho em disco de uma região típica de pesca;
4. avaliar a qualidade da hidrografia brasileira na base;
5. estimar custo por região e por atualização;
6. validar suporte real em React Native nas duas plataformas;
7. registrar a decisão aqui e atualizar o `MAP-LICENSE-GATE`.

## Consequences
- MP-17 (Offline Maps) não pode começar.
- `MAP-LICENSE-GATE` = **BLOCKED**, logo F5 não congela.
- O produto **não pode anunciar** "mapas offline" antes desta decisão.
- Plano de contingência: se nenhuma solução for viável, o offline do MVP entrega GPS,
  pontos, capturas e dados do produto **sem base cartográfica detalhada** — degradação
  aceitável, mas que precisa ser decidida conscientemente, não descoberta tarde.

## Risks
- **R-030 (crítico):** violação de licença.
- Custo inesperado por região.
- Qualidade insuficiente da base no Brasil.
- Biblioteca sem manutenção em React Native.
- Construir o recurso e ter de removê-lo.

## Security Impact
Pacotes baixados devem ter integridade verificada. Nenhum dado do usuário vai junto.

## Privacy Impact
**Positivo:** mapa offline reduz o envio de viewport a terceiros, ou seja, revela menos
sobre onde o usuário está olhando.

## Offline Impact
**Máximo.** É a decisão que define a qualidade da promessa central do produto.

## Portability Impact
`OfflineMapPort` isola a solução no cliente. Ainda assim, a troca implica rebaixar ou
reconstruir pacotes já distribuídos.

## Cost Impact
Desconhecido. Faz parte do `COST-GATE`.

## Operational Impact
Atualização de regiões, versionamento de pacotes, espaço em disco do usuário.

## Open Questions
- **Q-004:** qual solução é legalmente compatível e viável?
- **Q-005:** o provider online permite cache persistente no plano pretendido?
- Satélite offline é viável sob alguma licença?
- Qual o tamanho aceitável de uma região para o usuário?

## Evidence
**Nenhuma.** Este ADR existe para registrar que a decisão está aberta e é bloqueante.
Preenchê-lo com suposições seria exatamente o erro que ele existe para evitar.

## Supersedes / Superseded By
— / —
