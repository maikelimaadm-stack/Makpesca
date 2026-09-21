---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0014
---

# Modelo FREE / PRO

## 1. Princípio

O plano FREE precisa ser **genuinamente útil**. A base gratuita é o que cria a comunidade,
os dados e o valor do produto. PRO amplia; não destrava o básico.

## 2. Preço

Referência: **~R$ 19,90/mês — NÃO congelado** (Q-011).
Faixas anual e promocional a definir. Taxas das lojas afetam a receita líquida.

## 3. Divisão proposta (nenhuma linha congelada)

| Recurso | FREE | PRO |
|---------|------|-----|
| Conta, perfil, feed, comunidades | Sim | Sim |
| Pontos privados | Limite generoso | Ilimitado |
| Capturas | Ilimitadas | Ilimitadas |
| Fotos por captura | Limite menor | Limite maior |
| Mapa online | Sim | Sim |
| Regiões offline | Poucas (limite baixo) | Muitas / maiores |
| Camadas avançadas de mapa | Não | Sim |
| Histórico e estatísticas | Básico | Avançado |
| Filtros avançados | Não | Sim |
| Condições ambientais detalhadas | Básico | Detalhado + previsão |
| Melhores horários / insights | Não | Sim |
| Planejamento de pescaria | Não | Sim |
| Exportação dos próprios dados | **Sim (LGPD)** | Sim |
| Denúncia, bloqueio, moderação | **Sim** | Sim |
| Selo PRO no perfil | Não | Opcional |

## 4. O que **nunca** é pago

| Item | Motivo |
|------|--------|
| Privacidade e controle de precisão | Privacidade não é produto premium |
| Exportação e exclusão de dados | Direito legal |
| Denúncia, bloqueio, segurança | Segurança não se vende |
| Registro de captura e ponto básico | É o núcleo do produto |
| Funcionamento offline básico | É a promessa central |

Cobrar por qualquer um desses seria trair os princípios do produto.

## 5. Transição entre planos

| Situação | Comportamento |
|----------|---------------|
| FREE → PRO | Entitlements concedidos assim que a assinatura é validada |
| PRO → FREE (cancelamento) | Acesso mantido até o fim do período pago (INV-B05) |
| Excedente após downgrade | **Nunca apagar dados do usuário**; o excedente fica somente leitura até o usuário ajustar |
| Falha de pagamento | Grace period antes de reduzir |
| Reassinatura | Restaura o acesso, dados preservados |

A regra "nunca apagar dados por downgrade" é inegociável: o usuário confiou o acervo dele
ao produto.

## 6. Limites e comunicação

Limites do FREE são exibidos **antes** de o usuário esbarrar neles, com clareza.
Nada de descobrir o limite no meio da pescaria, sem rede.

## 7. Riscos

| Risco | Mitigação |
|-------|-----------|
| FREE inútil afasta a base | Revisar limites com dados de uso |
| PRO sem valor percebido | Entitlements que resolvem dor real (offline e inteligência) |
| Preço inadequado | Teste de preço antes de congelar |
| Custo por usuário PRO acima da receita | `COST-GATE` — mapas offline e mídia são os vetores |

## 8. Fase

Pós-MVP. O MVP roda sem cobrança, para aprender o custo real por usuário antes de precificar.
