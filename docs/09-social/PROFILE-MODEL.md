---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0018
---

# Modelo de Perfil

## 1. Conteúdo do perfil

| Campo | Visibilidade padrão | Observação |
|-------|---------------------|------------|
| Nome de exibição | Público | |
| `@handle` | Público | Único, imutável ou com limite de troca |
| Foto e capa | Público | |
| Bio | Público | Moderável |
| Cidade / região | **Configurável** | Padrão: região, nunca endereço |
| Espécies favoritas | Público | |
| Técnicas preferidas | Público | |
| Atividade recente | Configurável | Só conteúdo já público |
| Estatísticas | Configurável | Ver §3 |
| Conquistas | Configurável | Pós-MVP |
| Seguidores / seguindo | Configurável | Contagem e/ou lista |
| Comunidades | Configurável | |
| Selo PRO | Público (se o usuário quiser) | Nunca expõe dados de pagamento |

## 2. Níveis de visibilidade do perfil

| Nível | Quem vê |
|-------|---------|
| `PUBLIC` | Qualquer pessoa, inclusive não autenticada (web) |
| `AUTHENTICATED` | Somente usuários logados |
| `FOLLOWERS` | Somente seguidores |
| `PRIVATE` | Somente o próprio usuário |

## 3. Estatísticas — regra de privacidade

Estatísticas são derivadas **apenas de conteúdo já público** do usuário. Nunca:

- número de pontos privados;
- locais onde pesca;
- frequência em um corpo d'água específico se isso o localiza;
- mapa de calor da atividade.

Permitido: total de capturas públicas, espécies distintas públicas, tempo de uso,
conquistas, participação em comunidades.

## 4. Riscos de perfil

| Risco | Mitigação |
|-------|-----------|
| Perfil revela rotina e localização | Região ampla por padrão; sem mapa de calor |
| Assédio a partir do perfil | Bloqueio, denúncia, limitar quem pode comentar/mensagem |
| Identificação de menor | Idade mínima e restrições (Q-017) |
| Cópia de conteúdo | Marca d'água opcional (a avaliar) |

## 5. Edição e histórico

- O usuário pode alterar nome, bio, foto e visibilidade a qualquer momento.
- Troca de `@handle` é limitada para evitar confusão de identidade.
- Alteração de visibilidade tem efeito imediato, inclusive sobre conteúdo já publicado.

## 6. Perfil de outra pessoa

Ao ver um perfil, o observador recebe apenas o que a visibilidade e as relações permitem —
degradado no servidor, nunca filtrado no cliente. Bloqueio torna o perfil inacessível para
o bloqueado.

## 7. Exclusão

Ao excluir a conta, o perfil deixa de existir. Comentários e interações feitos por essa
pessoa em conteúdo alheio são anonimizados, não apagados (para não destruir conversas
de terceiros) — decisão a confirmar com jurídico.
