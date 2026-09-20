---
name: mp-security-review
description: Revisão de segurança — autenticação, autorização por objeto, IDOR/BOLA, uploads, webhooks, secrets e abuso. Use em qualquer mudança sensível.
---

# mp-security-review

## SSOTs
- `docs/08-security-privacy/SECURITY-BASELINE.md`
- `docs/08-security-privacy/THREAT-MODEL.md`
- `docs/08-security-privacy/SECRETS-POLICY.md`
- `docs/07-api/API-SECURITY.md`
- `.claude/rules/security.md`

## Checklist
1. Autorização por objeto em toda operação, com teste negativo (IDOR/BOLA)?
2. Autenticação obrigatória, com exceções explícitas e justificadas?
3. Refresh rotativo, detecção de reutilização, sessões revogáveis?
4. Entrada validada; consultas parametrizadas?
5. Rate limiting nos caminhos sensíveis?
6. Upload por ticket, com validação de tipo real e limite?
7. Webhook com assinatura verificada, idempotente e com proteção contra replay?
8. Erro sem stack, SQL, caminho ou existência de recurso privado?
9. Nenhum secret no código, log, documento ou histórico?
10. Ação administrativa auditada, com menor privilégio?
11. Recurso novo tem análise de ameaça registrada?
12. Dependências novas justificadas e auditadas?

## Priorizar
C1/C2 do `THREAT-MODEL.md`: vazamento de coordenadas por endpoint e por log.

## Saída
Achados com severidade (CRÍTICO / ALTO / MÉDIO / BAIXO) e veredito do `SECURITY-GATE`.
