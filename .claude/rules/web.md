# Regra — Web

## Aplicação
`apps/web`, `apps/admin`, `apps/partners`.

## SSOTs
`docs/01-product/MVP-SCOPE.md` (§Web), `docs/adr/ADR-0002-WEB-STACK.md`,
`docs/11-commerce/PARTNER-PORTAL.md`.

## Regras
1. A web consome a **mesma API**; nenhuma regra de negócio no servidor do framework web.
2. Conteúdo público exibe apenas dados já degradados pelo servidor.
3. CORS restrito às origens dos nossos apps; sem `*` em produção.
4. Cabeçalhos de segurança padrão; proteção contra XSS e CSRF.
5. Ambientes não-produtivos não são indexados por buscadores.
6. Admin exige 2FA e registra auditoria de toda ação.
7. Partners isola dados por parceiro e nunca exibe dados pessoais de usuários.
8. Componentes compartilhados em `packages/ui`; nada de domínio ali.
9. Nenhuma chave de servidor exposta no cliente.
10. Páginas públicas não expõem contadores ou listas que revelem conteúdo oculto.

## Proibido
- Usar rota do framework web como backend paralelo.
- Renderizar coordenada acima da precisão autorizada, mesmo que oculta por CSS.
- Página pública que liste usuários sem consentimento de visibilidade.
