---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0020
---

# Ofertas

## 1. Fluxo de uma oferta

```mermaid
flowchart LR
    P["Parceiro cria oferta<br/>(portal ou operação)"] --> V{"Validação:<br/>regras, validade, verificação"}
    V -- reprovada --> X["Rejeitada com motivo"]
    V -- aprovada --> PUB["Oferta publicada"]
    PUB --> D["Descoberta pelo usuário<br/>(mapa · busca · perfil da loja · contexto)"]
    D --> U["Usuário abre a oferta"]
    U --> A{"Ação escolhida"}
    A -- "site do parceiro" --> L["Link com referral"]
    A -- "WhatsApp" --> W["Contato com referral"]
    A -- "cupom" --> C["Código copiado (referral)"]
    L --> CL["Click registrado (idempotente)"]
    W --> CL
    C --> CL
    CL --> EXT["Compra acontece FORA da Makpesca"]
    EXT --> CONV["Conversão informada / conciliada"]
    CONV --> COM["Comissão (uma por conversão)"]
```

## 2. Estrutura de uma oferta

| Campo | Obrigatório |
|-------|-------------|
| Título | Sim |
| Descrição | Sim |
| Condições | Sim (o que vale, o que não vale) |
| Período de validade | **Sim** |
| Loja e unidades participantes | Sim |
| Categoria/marca | Recomendado |
| Imagem | Recomendado |
| Cupom | Opcional |
| Link de destino | Opcional |
| Limite de uso | Opcional |
| Público-alvo | Região; **nunca** localização exata |

## 3. Regras

| # | Regra |
|---|-------|
| 1 | Oferta sem validade não é publicada |
| 2 | Oferta vencida não é exibida (INV-C04) |
| 3 | Condições precisam ser compreensíveis antes do clique |
| 4 | Oferta é identificada como conteúdo de parceiro (INV-C05) |
| 5 | Preço anunciado é responsabilidade do parceiro; a Makpesca não vende |
| 6 | Oferta denunciada como enganosa é revisada e pode ser removida |
| 7 | Segmentação usa região, interesse e espécie — nunca ponto de pesca do usuário |

## 4. Exibição

| Local | Regra |
|-------|-------|
| Perfil da loja | Todas as ofertas vigentes |
| Mapa | Lojas próximas com indicação de oferta |
| Busca | Por categoria, marca, região |
| Feed | Limitado, rotulado, com frequência controlada |
| Contexto | Ex.: ao planejar uma pescaria na região |

Nunca interromper o fluxo de campo do usuário (marcar ponto, registrar captura) com
oferta.

## 5. Rastreamento

Toda ação de saída gera um `Referral` e um `Click`, com idempotência (um toque duplo não
conta dois cliques). O usuário é informado de que está saindo para o parceiro.

Detalhe em `ATTRIBUTION.md`.

## 6. Métricas

Impressões, cliques, taxa de clique, conversões conciliadas, denúncias.
Métricas do parceiro são agregadas e anônimas.

## 7. O que não fazemos

- Checkout dentro do app (fora de escopo inicial).
- Custódia de pagamento.
- Garantia de preço, estoque ou entrega.
- Segmentação por localização exata.
- Notificação push promocional sem consentimento específico.
