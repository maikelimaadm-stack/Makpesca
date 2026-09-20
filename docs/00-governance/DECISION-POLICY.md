---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: todos
---

# Política de Decisão

## 1. O que exige ADR

Exige ADR qualquer decisão que:

- escolha ou troque um provider (mapa, auth, storage, billing, banco, hospedagem);
- altere a fronteira entre cliente, API, domínio e infraestrutura;
- defina protocolo de sincronização, formato de erro, versionamento ou idempotência;
- defina regra estrutural de privacidade ou segurança;
- defina modelo de dados estrutural (identidade, geometria, propriedade, visibilidade);
- crie dependência recorrente de custo;
- crie lock-in relevante.

Não exige ADR: redação, exemplo, reorganização de texto, correção de link.

## 2. Estados de decisão

| Estado | Significado |
|--------|-------------|
| `OPEN` | Problema reconhecido, sem opção escolhida |
| `PROPOSED` | Opção preferida existe, sem validação |
| `ACCEPTED` | Decidido, vale para implementação |
| `FROZEN` | Decidido e congelado por onda |
| `SUPERSEDED` | Substituído por outro ADR |
| `REJECTED` | Avaliado e recusado |

## 3. Níveis de confiança do baseline

| Nível | Uso |
|-------|-----|
| `BASELINE` | Ponto de partida assumido, revisável sem trauma |
| `NEEDS-DECISION` | Exige investigação antes de congelar |
| `BLOCKING` | Impede o congelamento da onda enquanto aberto |

## 4. Critérios obrigatórios de avaliação

Toda opção comparada é avaliada por, no mínimo:

1. adequação funcional;
2. custo inicial e custo em escala;
3. risco de lock-in e custo de saída;
4. impacto em offline;
5. impacto em privacidade e segurança;
6. impacto em LGPD;
7. suporte a iOS, Android e Web quando aplicável;
8. maturidade, manutenção e comunidade;
9. observabilidade e operabilidade;
10. licença e termos de uso.

## 5. Evidência

Afirmação sobre terceiro (preço, limite, licença, capacidade) exige:

- fonte primária (documentação oficial, termos de uso, tabela de preços);
- data de consulta;
- citação literal do ponto relevante quando decisivo.

Sem isso o item vira `NEEDS-DECISION` e entra em `OPEN-QUESTIONS.md`.
**Não é permitido preencher com estimativa apresentada como fato.**

## 6. Reversão

Toda decisão `ACCEPTED` documenta o caminho de reversão: o que precisaria acontecer
para voltar atrás e qual o custo estimado. Decisão sem caminho de reversão é risco e
entra no `RISK-REGISTER.md`.

## 7. Quem decide

Nesta fase o projeto não tem papéis nomeados. `Owners: (a definir)` é intencional e
deve ser resolvido antes da onda F0 ser congelada — ver `OPEN-QUESTIONS.md` (Q-001).
