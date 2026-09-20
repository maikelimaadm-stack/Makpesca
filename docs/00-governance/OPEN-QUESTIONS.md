---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0006, ADR-0007, ADR-0008, ADR-0010, ADR-0013, ADR-0014, ADR-0019
---

# Perguntas Abertas

Toda pergunta aqui tem onda-alvo. Pergunta `BLOCKING` impede o congelamento da sua onda.

| ID | Pergunta | Onda | Criticidade | Impacto se errar | Como resolver |
|----|----------|------|-------------|------------------|---------------|
| Q-001 | Quem são os owners nominais por área? | F0 | BLOCKING | Nada tem dono; decisões travam | Definição do responsável do produto |
| Q-002 | O produto adota "amizade" mútua além de follow? | F1 | ALTA | Muda modelo social e permissões | Decisão de produto + ADR-0018 |
| Q-003 | Qual o recorte geográfico inicial (Brasil todo? região piloto?) | F1 | ALTA | Muda custo, moderação e catálogo de espécies | Decisão de produto |
| Q-004 | Qual solução de mapa offline é legalmente compatível e viável? | F5 | **BLOCKING** | Recurso central do produto pode ser inviável ou ilegal | Pesquisa com fonte + data; ADR-0010 |
| Q-005 | Google Maps permite, no plano pretendido, cache persistente de tiles? | F5 | **BLOCKING** | Risco de violação de termos | Ler Terms of Service oficiais e registrar citação + data |
| Q-006 | Qual framework HTTP TypeScript? | F6 | ALTA | Custo de troca depois de muitos endpoints | Prova de conceito comparativa; ADR-0006 |
| Q-007 | Qual ORM/query layer com suporte adequado a PostGIS? | F3 | ALTA | Reescrita de camada de dados | Avaliação com consultas geo reais; ADR-0007 |
| Q-008 | Qual provedor de autenticação? | F6 | ALTA | Migração de identidade é cara e arriscada | Comparação em AUTH-OPTIONS; ADR-0008 |
| Q-009 | Qual object storage para mídia? | F3 | MÉDIA | Custo de egress e migração de arquivos | Comparação de custo com fonte; ADR-0013 |
| Q-010 | Billing: lojas + agregador (ex. RevenueCat) ou integração direta? | F8 | ALTA | Retrabalho de entitlements | Comparação com fonte de preço; ADR-0014 |
| Q-011 | Preço do PRO (~R$ 19,90/mês é referência, não decisão) | F8 | MÉDIA | Monetização inviável ou subprecificada | Pesquisa de mercado + teste |
| Q-012 | Mensageria própria ou provider? | F7 | MÉDIA | Custo operacional e privacidade | ADR-0019 |
| Q-013 | Quais fontes de dados ambientais (clima, nível de rio, maré) com licença adequada? | F5 | ALTA | Recurso PRO pode não existir | Levantamento de APIs com termos + data |
| Q-014 | Existe fonte de batimetria licenciável para as regiões alvo? | F5 | BAIXA | Recurso opcional | Levantamento; pode ficar FUTURE |
| Q-015 | Catálogo de espécies: fonte própria, pública ou colaborativa? | F1 | MÉDIA | Qualidade de dados e moderação | Decisão de produto + fonte |
| Q-016 | Política de retenção de dados (capturas, mídia, mensagens, logs) | F3 | ALTA | LGPD e custo | Definir em DATA-LIFECYCLE + jurídico |
| Q-017 | Menores de idade: o app permite? Com quais limites? | F3 | ALTA | LGPD Art. 14; risco jurídico | Jurídico + produto |
| Q-018 | Mensagens serão cifradas fim-a-fim? | F7 | MÉDIA | Conflito com moderação e denúncia | Decisão explícita com trade-off |
| Q-019 | Modelo de comissão dos afiliados (percentual, fixo, por lead?) | F8 | MÉDIA | Contrato comercial e cálculo | Comercial + ADR-0020 |
| Q-020 | Quem paga e como se paga o parceiro (payout)? | F8 | MÉDIA | Operação financeira | Comercial + jurídico |
| Q-021 | O MVP inclui web pública ou só landing? | F1 | MÉDIA | Escopo e prazo | Decisão de produto |
| Q-022 | Admin no MVP é painel ou operação manual via banco/ferramenta interna? | F9 | MÉDIA | Capacidade de moderar desde o dia 1 | Decisão de produto |
| Q-023 | Qual a região mínima de coorte para publicar insight sem reidentificação? | F3 | ALTA | Vazamento de ponto por agregação | Definir k mínimo e validar |
| Q-024 | Monorepo: Turborepo ou alternativa? | F2 | BAIXA | Ergonomia de build | ADR-0017 |
| Q-025 | Observabilidade: qual stack e qual custo? | F9 | MÉDIA | Operação cega | ADR-0016 |
| Q-026 | O app terá modo "pescaria ao vivo" com localização em tempo real? | FUTURE | ALTA | Risco de privacidade elevado | Só após F3 congelada |

## Itens BLOCKING atualmente abertos

- **Q-004** e **Q-005** — mapa offline e licença de tiles. Bloqueiam `F5`.
- **Q-001** — owners. Bloqueia `F0`.

Enquanto houver item `BLOCKING` na onda, `FREEZE = BLOCKED` para aquela onda.
