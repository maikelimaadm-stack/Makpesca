# ADR-0021 — Portal de Parceiros

- **Status:** PROPOSED
- **Date:** 2026-09-20
- **Onda:** F8

## Context
Parceiros precisam manter perfil, unidades, ofertas e acompanhar resultados. Enquanto o
número de parceiros for pequeno, a operação manual pela equipe Makpesca é viável e mais
barata que construir um portal.

## Decision Drivers
- Autonomia do parceiro reduz custo operacional.
- Isolamento estrito entre parceiros.
- Nenhum dado de usuário exposto.
- Custo de construir e manter mais uma aplicação.
- Momento certo: portal cedo demais é desperdício.

## Options Considered
| Opção | Prós | Contras |
|-------|------|---------|
| **Aplicação web separada (`apps/partners`) no mesmo monorepo, usando a mesma API** | Isolamento de interface, contrato único, sem regra paralela | Mais uma aplicação para manter |
| Área dentro da web pública | Menos aplicações | Mistura públicos e riscos de autorização |
| Painel administrativo compartilhado com a operação | Rápido | Confunde papéis; risco de exposição de dados internos |
| Sem portal (operação manual) | Custo zero inicial | Não escala com o número de parceiros |

## Decision
Adotar **aplicação web separada no mesmo monorepo**, consumindo a mesma API com escopo de
parceiro — **construída apenas quando o número de parceiros justificar**.

Até lá, a operação do parceiro é manual, feita pela equipe. Essa é a decisão econômica
correta enquanto o modelo comercial ainda está sendo validado.

## Consequences
- Escopo de autorização de parceiro definido na API desde o início.
- Isolamento por `partnerStoreId` verificado (INV-A05).
- Métricas do parceiro são agregadas e suprimidas em volume baixo.

## Risks
- R-055 parceiro malicioso.
- Vazamento entre parceiros por falha de autorização.
- Construir o portal antes de validar o modelo comercial.

## Security Impact
Conta separada da conta de usuário final; papéis internos; 2FA para dados financeiros;
auditoria de ações.

## Privacy Impact
**Nenhum dado pessoal de usuário** no portal. Métricas agregadas, com supressão quando o
volume permitir dedução.

## Offline Impact
Nenhum.

## Portability Impact
Mesma stack web dos demais; sem dependência adicional.

## Cost Impact
Uma aplicação a mais para hospedar e manter — daí o adiamento até haver demanda.

## Operational Impact
Suporte a parceiros, verificação, suspensão, disputas de comissão.

## Open Questions
- A partir de quantos parceiros o portal se justifica?
- Quais permissões internas o parceiro precisa?
- O portal permite editar oferta sem nova aprovação, ou tudo passa por revisão?

## Evidence
Derivado de `PARTNER-PORTAL.md`. Sem dados de demanda real.

## Supersedes / Superseded By
— / —
