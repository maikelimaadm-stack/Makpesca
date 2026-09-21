---
Status: REVIEW
Version: 0.2.0
Last Updated: 2026-09-21
Owners: Maike Lima (autoridade humana final)
Related ADRs: todos
Wave: F0
Lifecycle: FREEZE-CONTROLLED
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

**Product Owner / Final Decision Authority: Maike Lima.**
Até delegação formal registrada, é também a autoridade humana final de arquitetura e
governança. O SSOT deste papel é `PROJECT-CONSTITUTION.md` Art. 15; esta seção é
derivada dele.

Agentes de IA **propõem, auditam e documentam**; nunca aceitam ADR, congelam onda,
liberam gate ou aprovam PR. Ver Constituição, Art. 15.

Documento fora do conjunto de congelamento de uma onda pode manter `Owners: (a definir)`
até ser incluído em uma onda. Documento cujo congelamento está em jogo, não.

Resolvido em 2026-09-21 (Q-001, ver `OPEN-QUESTIONS.md` §"Perguntas resolvidas").

## 8. Resumos e contagens derivados

Contagem, resumo ou tabela de estado que aparece fora do SSOT é **derivado**.

| Assunto | SSOT |
|---------|------|
| Estado de uma decisão / ADR | `DECISION-REGISTRY.md` + o campo `Status` do próprio ADR |
| Estado de um documento | `DOCUMENT-STATUS.md` + o cabeçalho do próprio documento |
| Perguntas abertas e `BLOCKING` | `OPEN-QUESTIONS.md` |
| Estado de gates | `../15-quality/QUALITY-GATES.md` |
| Composição de uma onda | `FREEZE-POLICY.md` §7 |

Regras:

1. **Recalcule do SSOT** antes de escrever qualquer contagem. Não copie um número de um
   resumo anterior, de um relatório ou de um corpo de PR.
2. **Relatório, corpo de PR, README e índice não são SSOT.** São instantâneos, e
   envelhecem.
3. Ao mudar um estado no SSOT, atualize os derivados conhecidos **no mesmo commit**.
4. Divergência entre derivado e SSOT é falha do gate `DOC-CONSISTENCY`.

Esta regra existe porque a rodada R1 encontrou exatamente esse defeito: contagens de ADR
copiadas de um resumo anterior em vez de recalculadas (`OPEN=7`/`PROPOSED=12`, quando os
arquivos diziam `OPEN=8`/`PROPOSED=11`).
