# Regra — Governança de Documentação

## Aplicação
Qualquer alteração em `docs/`, `CLAUDE.md`, `.claude/rules/` ou `.claude/skills/`.

## Regras
1. Antes de alterar, leia o SSOT do assunto em `docs/README.md`.
2. Um assunto tem **um** SSOT. Se precisar de outro, o primeiro passa a apontar para ele.
3. Documento relevante tem cabeçalho: `Status`, `Version`, `Last Updated`, `Owners`,
   `Related ADRs`.
4. `Status: FROZEN` **não muda silenciosamente**: exige ADR de superseção e registro em
   `docs/00-governance/DECISION-REGISTRY.md`.
5. Decisão relevante exige ADR (`docs/00-governance/DECISION-POLICY.md` §1).
6. Afirmação sobre terceiro (preço, licença, limite) exige fonte + data de consulta.
   Sem isso: marcar `NEEDS-DECISION` e registrar em `OPEN-QUESTIONS.md`.
7. **Não inventar pesquisa.** Estimativa apresentada como fato é falha grave.
8. Incremento de versão conforme `FREEZE-POLICY.md` §5.
9. Documento novo entra no índice `docs/README.md` e em `DOCUMENT-STATUS.md`.
10. Contradição entre documentos é falha do gate `DOC-CONSISTENCY`.

## Proibido
- Congelar documento com item `BLOCKING` aberto.
- Remover pergunta aberta sem respondê-la ou reclassificá-la com justificativa.
- Marcar PR como ready ou mergear sem pedido explícito.
