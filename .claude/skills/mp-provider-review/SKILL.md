---
name: mp-provider-review
description: Avalia adoção ou troca de provider externo — licença, custo, portabilidade, privacidade e risco. Use antes de adicionar qualquer dependência de terceiro.
---

# mp-provider-review

## SSOTs
- `docs/02-architecture/PROVIDER-ABSTRACTION.md`
- `docs/02-architecture/PORTABILITY-STRATEGY.md`
- `docs/00-governance/DECISION-POLICY.md`
- `docs/06-maps-location/MAP-PROVIDER-MATRIX.md` (modelo de matriz)

## Checklist
1. Qual port isola este provider? Ela é descrita por **intenção de domínio**?
2. Licença e termos de uso — com **link e data de consulta**.
3. Custo inicial e em escala — com fonte e data.
4. O que sai da Makpesca para esse provider? Há dado C2/C3/C4 envolvido?
5. Impacto em LGPD: local de processamento, contrato, exclusão.
6. Comportamento quando o provider estiver fora do ar.
7. Custo e caminho de saída: o que quebraria se ele sumisse amanhã?
8. Há dado que passaria a existir só lá?
9. Maturidade, manutenção e risco de mudança de termos.
10. A adição está justificada, ou é overengineering?

## Regra dura
**Sem fonte verificada com data, o item é `NEEDS-DECISION`** e entra em
`docs/00-governance/OPEN-QUESTIONS.md`. Não preencher com estimativa apresentada como fato.

## Saída
Matriz preenchida (ou com `A VERIFICAR`), recomendação e rascunho de ADR.
