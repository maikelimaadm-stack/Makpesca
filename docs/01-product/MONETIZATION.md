---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0014, ADR-0020, ADR-0021
---

# Monetização

## 1. Fontes de receita previstas

| # | Fonte | Horizonte | Estado |
|---|-------|-----------|--------|
| 1 | Assinatura Makpesca PRO | Pós-MVP | PROPOSED |
| 2 | Comissão de afiliados (lojas parceiras) | Pós-MVP | PROPOSED |
| 3 | Planos de destaque para parceiros | Futuro | HYPOTHESIS |
| 4 | Desafios/campanhas patrocinadas | Futuro | HYPOTHESIS |
| 5 | Marketplace com checkout interno | Fora de escopo inicial | NON-GOAL no início |

## 2. Makpesca PRO

- Modelo: FREE + PRO.
- Preço de **referência**: ~R$ 19,90/mês. **NÃO congelado** — ver `OPEN-QUESTIONS.md` (Q-011).
- Cobrança inicial pelas lojas (App Store / Google Play); assinatura web como possibilidade futura.
- Entitlements concedidos por serviço próprio, nunca pelo cliente — ver `../12-billing/ENTITLEMENTS.md`.

### Candidatos a entitlement PRO
Mapas offline avançados, mais regiões, pontos privados ilimitados, histórico e estatísticas
avançadas, inteligência de pesca, filtros avançados, condições ambientais detalhadas,
melhores horários, insights e planejamento.

> Nenhum entitlement está congelado. A régua FREE/PRO precisa manter o FREE útil:
> um FREE inútil mata a base que gera o valor da comunidade e dos dados.

## 3. Afiliados

Fluxo:

```
usuário → Makpesca → oferta → link/cupom → loja parceira → compra externa
       → conversão → comissão
```

Princípios:

- comissão **nunca** altera o que é apresentado como "melhor" ao usuário;
- conteúdo patrocinado é rotulado;
- conversão precisa de conciliação — comissão duplicada é defeito grave (R-054);
- antifraude obrigatório antes de qualquer payout.

Detalhe em `../11-commerce/AFFILIATE-PROGRAM.md`, `../11-commerce/ATTRIBUTION.md`
e `../11-commerce/COMMISSIONS-PAYOUTS.md`.

## 4. Custos que a monetização precisa cobrir

| Custo | Natureza | Risco |
|-------|----------|-------|
| Mapa online (por carregamento/sessão) | Variável com uso | R-031 |
| Mapa offline (licença/serviço) | A definir | R-030 |
| Armazenamento e egress de mídia | Variável com base instalada | R-032 |
| Banco gerenciado | Fixo + variável | — |
| Hospedagem de API | Variável | R-034 |
| Dados ambientais (APIs) | Possivelmente por chamada | Q-013 |
| Moderação e suporte | Humano | R-046 |
| Taxas das lojas de aplicativo | Percentual da assinatura | — |

**Regra:** recurso sem custo unitário compreendido não é aprovado para implementação
(ver `PRODUCT-PRINCIPLES.md` P12 e o `COST-GATE`).

## 5. O que não fazemos por dinheiro

- Não vendemos dados de localização.
- Não expomos pontos privados a parceiros.
- Não transformamos ranking em espaço pago disfarçado.
- Não usamos dark pattern para forçar upgrade.
