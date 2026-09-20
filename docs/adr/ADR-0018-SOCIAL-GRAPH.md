# ADR-0018 — Grafo Social

- **Status:** PROPOSED
- **Date:** 2026-09-20
- **Onda:** F7

## Context
O produto precisa de relações entre usuários para alimentar feed, descoberta e
comunidades. A escolha entre follow assimétrico e amizade mútua afeta modelo de
autorização, interface e complexidade.

## Decision Drivers
- Simplicidade do modelo de autorização.
- Adequação ao domínio (pesca é sobre conteúdo e região, não sobre círculo de amigos).
- Descoberta de conteúdo relevante.
- Prevenção de assédio.
- **Nenhuma relação social pode conceder localização por si só.**

## Options Considered
| Opção | Prós | Contras |
|-------|------|---------|
| **Follow assimétrico** | Simples, bom para descoberta de conteúdo, uma única relação | Não oferece camada natural de "confiança" |
| Amizade mútua | Camada de confiança natural; útil para compartilhar pontos | Mais atrito; mais complexidade |
| Ambos | Flexível | **Dobra a complexidade de autorização** e confunde o usuário |

## Decision
Adotar **follow assimétrico** como grafo principal. A adoção adicional de amizade mútua
fica **em aberto (Q-002)** e só se justifica se houver uso essencial — por exemplo, servir
de camada padrão para mensagens ou compartilhamento.

Regra permanente: **nenhuma relação social concede acesso a localização.**
Localização exige `LocationGrant` explícito (ADR-0012).

## Consequences
- Feed baseado em quem se segue + comunidades + região.
- Perfil com visibilidade configurável, inclusive "somente seguidores".
- Bloqueio encerra follow nos dois sentidos e concessões entre as partes.

## Risks
- R-042 assédio: mitigado por bloqueio, denúncia e limites de mensagem.
- Coleta de conteúdo por contas que seguem muita gente: mitigada por limites e rate limit.
- Se adotarmos amizade depois, migrar o modelo tem custo.

## Security Impact
Autorização baseada em relação precisa ser verificada por objeto, nunca inferida.

## Privacy Impact
Relação social **não** é autorização de localização. Essa separação é o ponto central.

## Offline Impact
Nenhum: grafo social não é sincronizado offline no MVP.

## Portability Impact
Modelo próprio, sem dependência de provider.

## Cost Impact
Fan-out do feed é o custo relevante (R-040) — tratado em `FEED-MODEL.md`.

## Operational Impact
Moderação precisa agir sobre relações (bloqueio forçado, restrição).

## Open Questions
- Q-002: adotar amizade mútua? Com qual propósito essencial?
- Limites de follow por janela.
- Visibilidade padrão das listas de seguidores.

## Evidence
Derivado de `SOCIAL-MODEL.md` e `FOLLOW-FRIEND-MODEL.md`. Sem validação com usuários.

## Supersedes / Superseded By
— / —
