---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0008, ADR-0012
---

# Baseline de Segurança

Mínimo obrigatório. Nenhum slice é aceito abaixo desta linha.

## 1. Identidade e sessão

| Controle | Obrigatório |
|----------|-------------|
| Senha forte ou autenticação sem senha (magic link/passkey/provedor federado) | Sim |
| Token de acesso curto + refresh revogável e rotativo | Sim |
| Detecção de reutilização de refresh | Sim |
| Listagem e revogação de sessões pelo usuário | Sim |
| 2FA para admin | Sim |
| Bloqueio progressivo após tentativas falhas | Sim |
| Notificação de novo dispositivo | Recomendado |

## 2. Autorização

| Controle | Obrigatório |
|----------|-------------|
| Verificação por objeto em toda operação | Sim (INV-A01) |
| Testes negativos de autorização por endpoint | Sim |
| Separação de escopos (usuário/admin/parceiro/sistema) | Sim |
| Menor privilégio para operação interna | Sim |
| Auditoria de ação administrativa | Sim |

## 3. Dados

| Controle | Obrigatório |
|----------|-------------|
| TLS em todo tráfego | Sim |
| Cifragem em repouso no banco e no storage | Sim |
| Classificação de dados aplicada (`../04-data/DATA-CLASSIFICATION.md`) | Sim |
| Redação automática de campos sensíveis em log | Sim |
| Remoção de EXIF antes de publicar mídia | Sim |
| Backups cifrados com acesso auditado | Sim |

## 4. Aplicação

| Controle | Obrigatório |
|----------|-------------|
| Validação de esquema em toda entrada | Sim |
| Consultas parametrizadas | Sim |
| Rate limiting | Sim |
| Tratamento de erro sem vazamento de detalhe interno | Sim |
| Dependências com lockfile e auditoria periódica | Sim |
| Revisão de segurança antes de liberar slice sensível | Sim |

## 5. Mobile

| Controle | Obrigatório |
|----------|-------------|
| Credenciais no keystore/keychain | Sim |
| Sem log de dados sensíveis no dispositivo | Sim |
| Sem coordenada exata em crash report | Sim |
| Permissões solicitadas no momento do uso, com explicação | Sim |
| Proteção contra captura de tela em telas sensíveis | A avaliar |
| Detecção de ambiente comprometido | A avaliar |

## 6. Infraestrutura

| Controle | Obrigatório |
|----------|-------------|
| Secrets em cofre, nunca no repositório | Sim |
| Credenciais separadas por ambiente | Sim |
| Acesso a produção restrito e auditado | Sim |
| Isolamento entre ambientes | Sim |
| Rotação de credenciais com procedimento definido | Sim |

## 7. Operação

| Controle | Obrigatório |
|----------|-------------|
| Plano de resposta a incidentes | Sim (`INCIDENT-RESPONSE.md`) |
| Alertas de segurança definidos | Sim |
| Teste de restore periódico | Sim |
| Canal para relato de vulnerabilidade | Sim |

## 8. Cobertura OWASP

| Risco | Tratamento |
|-------|-----------|
| Broken Object Level Authorization (BOLA/IDOR) | Autorização por objeto + testes negativos |
| Broken Authentication | Sessões curtas, rotação, revogação, bloqueio progressivo |
| Broken Object Property Level Authorization | DTO explícito; nunca serializar entidade crua |
| Unrestricted Resource Consumption | Rate limit, limites de área e de payload |
| Broken Function Level Authorization | Escopos separados e verificados |
| Unrestricted Access to Sensitive Business Flows | Limites em fluxos sensíveis (convites, denúncias, referrals) |
| Server Side Request Forgery | Nenhuma URL fornecida por usuário é buscada pelo servidor sem lista permitida |
| Security Misconfiguration | Configuração validada na inicialização |
| Improper Inventory Management | OpenAPI e matriz de endpoints mantidas |
| Unsafe Consumption of APIs | Adapters com timeout, validação e tratamento de erro |

## 9. Mobile (OWASP MASVS, resumo)

Armazenamento seguro de credenciais, comunicação com TLS, ausência de segredo embutido
relevante, proteção contra engenharia reversa proporcional ao risco, tratamento de
permissões e ausência de dados sensíveis em backup automático do sistema operacional.
