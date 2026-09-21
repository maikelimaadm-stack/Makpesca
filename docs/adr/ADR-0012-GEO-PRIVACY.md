# ADR-0012 — Geo-Privacidade

- **Status:** **ACCEPTED**
- **Date:** 2026-09-20
- **Onda:** F3

## Context
Ponto de pesca é patrimônio pessoal. Vazar a coordenada de um ponto privado é dano
irreversível e destrói a confiança que sustenta o produto. Ao mesmo tempo, o produto
precisa de compartilhamento social — logo, precisa de um modelo que permita revelar
**parcialmente**.

## Decision Drivers
- Vazamento é irreversível.
- O usuário precisa de controle granular e compreensível.
- O frontend não pode ser responsável por esconder nada.
- Ataques de inferência (média, triangulação) são reais.
- O modelo precisa ser simples o bastante para ser implementado corretamente.

## Options Considered
| Opção | Prós | Contras |
|-------|------|---------|
| **Dois eixos: visibilidade × precisão, aplicados no servidor** | Expressivo, granular, verificável | Exige disciplina em toda serialização |
| Apenas visibilidade (público/privado) | Simples | Não permite "mostrar a captura, esconder o ponto" — mata o social |
| Esconder no cliente | Trivial | **Não é privacidade**; o dado já saiu |
| Arredondar coordenadas | Simples | Preserva vizinhança; vulnerável a média e triangulação |

## Decision
Adotar **visibilidade × precisão, com degradação server-side**:

- Visibilidade: `PRIVATE` | `SHARED` | `PUBLIC`
- Precisão: `EXACT` | `APPROXIMATE` | `REGION` | `WATER_BODY_ONLY` | `HIDDEN`
- **Precisão efetiva = a mais restritiva** entre o declarado pelo dono, o concedido ao
  observador, e o que moderação/bloqueio permitem.
- Um **único componente** (Geo Privacy Service) decide e aplica.
- Jitter de `APPROXIMATE` é **determinístico** por (recurso, observador), com semente
  secreta do servidor, e nunca é re-sorteado.
- Publicar captura **nunca** altera a visibilidade do ponto.
- Concessões são revogáveis, com prazo opcional, sem encadeamento.

Esta decisão é **constitucional** (Art. 3).

## Consequences
- Todo endpoint que retorna localização passa pelo mesmo componente.
- Cache de resposta com localização inclui o perfil do observador na chave.
- Testes de contrato por perfil são obrigatórios e bloqueantes.
- A interface precisa explicar as cinco precisões em linguagem simples.

## Risks
- R-001 a R-007: vazamento por API, EXIF, média, triangulação, log, URL, backup.
- Complexidade de interface: o usuário precisa entender sem estudar.
- Esquecer a degradação em um endpoint novo — mitigado por teste obrigatório.
- Vazamento da semente do jitter permitiria recuperar coordenadas: tratada como segredo
  crítico.

## Security Impact
Depende de autorização por objeto correta (ADR-0003 + `API-SECURITY`).

## Privacy Impact
É a decisão de privacidade central do produto.

## Offline Impact
O dispositivo só recebe dados de terceiros já degradados. Revogação precisa viajar pelo
sync e remover o dado local.

## Portability Impact
Lógica própria, independente de provider.

## Cost Impact
Custo de cache por observador e de processamento na serialização.

## Operational Impact
Acesso administrativo a coordenada exata é auditado e deve ser raro.

## Open Questions
- Q-023: coorte mínima para agregações.
- Raio padrão de `APPROXIMATE` por contexto.
- Procedimento de rotação da semente do jitter.

## Evidence
Derivado de `GEO-PRIVACY.md` e `GEO-PRIVACY-THREAT-MODEL.md`.

## Supersedes / Superseded By
— / —
