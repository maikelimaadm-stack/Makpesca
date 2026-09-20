---
name: mp-doc-audit
description: Audita a documentação do MAKPESCA — SSOTs, links, cabeçalhos de status, contradições, pendências e ausência de código de produto. Use antes de congelar uma onda ou ao revisar alterações em docs/.
---

# mp-doc-audit

## SSOTs
- `docs/README.md` (índice e mapa de SSOTs)
- `docs/00-governance/DOCUMENT-STATUS.md`
- `docs/00-governance/OPEN-QUESTIONS.md`
- `.claude/rules/documentation-governance.md`

## O que verificar
1. Todo documento tem cabeçalho com `Status`, `Version`, `Last Updated`, `Owners`, `Related ADRs`.
2. Todo documento existe no índice `docs/README.md` e em `DOCUMENT-STATUS.md`.
3. Nenhum link quebrado (caminhos relativos válidos).
4. Um SSOT por assunto; sem duplicação de autoridade.
5. Sem contradição entre documentos (especialmente escopo MVP, precisão de localização e gates).
6. Termos conforme `docs/00-governance/GLOSSARY.md`.
7. Afirmação sobre terceiro tem fonte + data, ou está marcada `A VERIFICAR`/`NEEDS-DECISION`.
8. Nenhum arquivo vazio.
9. **Nenhum código de produto no repositório** enquanto `IMPLEMENTATION-READY-GATE` estiver BLOCKED.
10. ADRs `OPEN` refletidos em `OPEN-QUESTIONS.md` e no índice `docs/adr/README.md`.

## Saída
Lista de achados com: arquivo, linha quando aplicável, severidade (BLOQUEIA / CORRIGIR / OBSERVAR) e correção proposta.
Terminar com o veredito do gate `DOC-CONSISTENCY`.
