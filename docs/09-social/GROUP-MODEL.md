---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0018, ADR-0019
---

# Modelo de Grupos

## 1. Diferença entre grupo e comunidade

| Aspecto | Comunidade | Grupo |
|---------|-----------|-------|
| Tamanho | Grande, aberto | Pequeno, fechado |
| Propósito | Pertencimento temático/regional | Organização prática |
| Entrada | Aberta ou por solicitação | Por convite |
| Conteúdo | Público dentro da comunidade | Restrito aos membros |
| Localização | Precisões baixas | Pode receber concessão explícita |

## 2. Estrutura

| Elemento | Descrição |
|----------|-----------|
| Privacidade | `PUBLIC` (visível, entrada controlada) ou `PRIVATE` (invisível) |
| Papéis | `OWNER`, `ADMIN`, `MEMBER` |
| Convites | Link ou convite direto, com validade e limite |
| Limite de membros | Definido pelo produto |
| Avisos | Mensagem fixada pelos administradores |
| Conversa | Ver `MESSAGING-MODEL.md` |
| Fotos e capturas | Compartilhadas entre membros |
| Pontos compartilhados | **Somente por concessão explícita do dono** |
| Pescarias | Eventos do grupo |
| Votação | Enquete simples para decidir data/local |
| Calendário | Eventos do grupo |

## 3. Regra crítica de localização

> **Entrar em um grupo não dá acesso a ponto nenhum.**
> O dono de cada ponto concede individualmente, com precisão e prazo.

Quando alguém sai do grupo (ou é removido), o acesso derivado cessa imediatamente.

## 4. Convites

| Regra |
|-------|
| Convite tem validade e pode ser revogado |
| Limite de convites por usuário por janela (anti-spam) |
| Usuário bloqueado não pode ser convidado pelo bloqueador, nem o contrário |
| Entrada por link exige aprovação em grupos privados |

## 5. Moderação

Administradores moderam dentro do grupo. Denúncia à plataforma está disponível **dentro**
do grupo — conteúdo privado não é terra sem lei. A plataforma só acessa conteúdo de grupo
privado mediante denúncia ou obrigação legal, com registro de auditoria.

## 6. Ciclo de vida

Criado → ativo → inativo → arquivado ou excluído.
Ao excluir: conteúdo removido conforme política de retenção; concessões encerradas;
membros notificados.

## 7. Riscos

| Risco | Mitigação |
|-------|-----------|
| Grupo usado para coletar pontos | Concessão individual, revogável, sem repasse |
| Abuso dentro de grupo fechado | Denúncia disponível internamente |
| Convites em massa | Limites e detecção |
| Administrador removendo todos | Papel de dono protegido; histórico de ações |
