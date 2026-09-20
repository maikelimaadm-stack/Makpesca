---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0018
---

# Modelo de Seguidores e Amizade

## 1. Decisão de base

O grafo principal é **follow assimétrico** (ADR-0018, `PROPOSED`).
A existência de "amizade" mútua é **decisão aberta** (Q-002).

## 2. Follow

| Propriedade | Regra |
|-------------|-------|
| Direção | Assimétrica: A segue B sem reciprocidade |
| Aprovação | Automática para perfil público; por solicitação para perfil restrito |
| Efeito | Conteúdo de B aparece no feed de A conforme visibilidade |
| Não dá acesso a | Pontos privados, localização exata, mensagens |
| Desfazer | A qualquer momento, sem notificar |
| Remover seguidor | O dono pode remover quem o segue |

## 3. Amizade (se adotada)

Se a decisão for adotar amizade mútua, ela precisa de propósito claro — caso contrário é
complexidade sem valor.

| Uso possível | Justificativa |
|--------------|---------------|
| Camada de confiança para compartilhar pontos | Facilita J5 |
| Permissão padrão para mensagens diretas | Reduz assédio |
| Visibilidade intermediária (`FRIENDS`) | Entre público e privado |

**Se nenhum desses usos for essencial, não adotar.** Duas relações paralelas confundem o
usuário e dobram a complexidade de autorização.

## 4. Implicações de autorização

| Relação | Dá acesso a |
|---------|-------------|
| Seguidor | Conteúdo `PUBLIC` e o marcado para seguidores |
| Amigo (se existir) | Acima + conteúdo `FRIENDS` |
| Nenhuma | Apenas `PUBLIC` |
| Bloqueado | Nada |

**Nenhuma relação social concede, por si só, acesso a localização exata.**
Localização exige concessão explícita (`LocationGrant`).

## 5. Bloqueio

| Efeito |
|--------|
| Encerra follow nos dois sentidos (INV-T04) |
| Encerra concessões de localização entre as partes |
| Remove o conteúdo de cada um da visão do outro |
| Impede mensagens, menções, comentários e convites |
| Não notifica o bloqueado |
| É reversível pelo bloqueador |

## 6. Limites

| Limite | Motivo |
|--------|--------|
| Máximo de follows por janela | Anti-spam e anti-coleta |
| Máximo de solicitações pendentes | Anti-assédio |
| Restrição para contas novas | Anti-abuso |

## 7. Privacidade das listas

Seguidores e seguindo têm visibilidade configurável. Contagens podem ser públicas com as
listas privadas. Quem bloqueou nunca aparece nas listas do bloqueado.
