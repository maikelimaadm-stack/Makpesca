---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0012, ADR-0016
---

# Classificação de Dados

## 1. Níveis

| Nível | Definição | Exemplos |
|-------|-----------|----------|
| **C0 — Público** | Publicável sem restrição | Catálogo de espécies, conteúdo público de loja |
| **C1 — Interno** | Operacional, não sensível | Métricas agregadas, catálogos internos |
| **C2 — Pessoal** | Identifica uma pessoa | Nome, e-mail, telefone, foto de perfil |
| **C3 — Sensível do produto** | Vaza valor ou expõe a pessoa | Capturas privadas, conteúdo de mensagens, histórico |
| **C4 — Crítico** | Vazamento causa dano direto e irreversível | **Coordenada exata de ponto privado**, credenciais, tokens, secrets |

## 2. Classificação por dado

| Dado | Nível | Regras especiais |
|------|-------|------------------|
| Coordenada verdadeira de `Spot`/`Catch` | **C4** | Nunca em log, analytics, URL, push, cache compartilhado, export de terceiro |
| Coordenada degradada (`APPROXIMATE`+) | C1/C2 | Conforme concessão |
| E-mail, telefone | C2 | Nunca em resposta pública |
| Token de sessão / refresh | C4 | Nunca persistido em texto claro fora do keystore do dispositivo |
| Secrets de provider | C4 | Somente em cofre de secrets |
| Foto de captura | C3 | EXIF removido antes de publicar |
| Mensagem privada | C3 | Retenção mínima necessária; acesso só para apuração registrada |
| Denúncia e caso de moderação | C3 | Acesso restrito à operação |
| Dados de assinatura | C2 | Sem dados de cartão no nosso lado |
| Comissões e conversões | C1/C2 | Dados de parceiro isolados |
| Logs de aplicação | C1 | Com redação obrigatória de C2/C3/C4 |
| Métricas agregadas | C0/C1 | Só após coorte mínima |

## 3. Regras por nível

| Nível | Em log | Em analytics | Em cache CDN | Em export | Em backup |
|-------|--------|--------------|--------------|-----------|-----------|
| C0 | sim | sim | sim | sim | sim |
| C1 | sim | sim (agregado) | condicional | sim | sim |
| C2 | **apenas id pseudônimo** | pseudônimo | não | ao titular | cifrado |
| C3 | **nunca conteúdo** | nunca | não | ao titular | cifrado |
| C4 | **nunca** | **nunca** | **nunca** | ao titular, sob controle | cifrado + acesso auditado |

## 4. Redação obrigatória

O logger estruturado (`packages/observability`) mantém lista de campos proibidos e faz
redação automática. Campos reconhecidos por nome (`location`, `lat`, `lng`, `coordinates`,
`token`, `password`, `secret`, `email`, `phone`) são redigidos por padrão — opt-out exige
justificativa explícita revisada.

## 5. Acesso administrativo

Acesso a dados C3/C4 pela operação exige: motivo registrado, escopo mínimo, prazo e
registro de auditoria. Acesso a coordenada exata de ponto privado por administrador é
evento auditado e deve ser raro e justificado.

## 6. Transferência a terceiros

| Terceiro | Pode receber | Nunca recebe |
|----------|-------------|--------------|
| Provider de mapa | viewport do usuário | lista de pontos privados |
| Provider de dados ambientais | coordenada aproximada | coordenada exata de ponto privado |
| Analytics | eventos pseudônimos agregados | C2 identificável, C3, C4 |
| Parceiro comercial | métricas agregadas de suas ofertas | dados pessoais de usuários |
| Provider de push | token de dispositivo e payload mínimo | conteúdo sensível, coordenadas |
