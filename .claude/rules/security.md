# Regra — Segurança

## Aplicação
Todo o repositório.

## SSOTs
`docs/08-security-privacy/SECURITY-BASELINE.md`, `THREAT-MODEL.md`, `SECRETS-POLICY.md`,
`docs/07-api/API-SECURITY.md`.

## Regras
1. Autorização **por objeto** em toda operação. Id na rota não implica permissão.
2. Todo endpoint novo tem teste de autorização negativa.
3. Autenticação em toda rota, exceto lista explícita de públicas.
4. Refresh rotativo com detecção de reutilização; sessões revogáveis.
5. Entrada validada por esquema; campos desconhecidos rejeitados.
6. Consultas parametrizadas sempre.
7. Rate limiting em autenticação, criação de conteúdo, listagens e sync.
8. Upload só por ticket autorizado, com validação de tipo real e limite de tamanho.
9. Webhook: assinatura verificada, idempotente por evento, replay rejeitado.
10. Erro não vaza stack, SQL, caminho de arquivo nem existência de recurso privado.
11. Nenhum secret no repositório, em log ou em documento.
12. Ação administrativa é auditada.
13. Recurso novo exige análise de ameaça (`SECURITY-GATE`).

## Proibido
- Confiar em validação feita apenas no cliente.
- Chave com permissão de escrita embutida em app.
- Endpoint administrativo sem escopo próprio.
- Desativar verificação de certificado.
- Buscar URL fornecida pelo usuário sem lista permitida.
