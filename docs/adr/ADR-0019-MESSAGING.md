# ADR-0019 — Mensageria

- **Status:** **OPEN**
- **Date:** 2026-09-20
- **Onda:** F7

## Context
Mensagens individuais e de grupo servem para organizar pescarias e trocar informações.
É também o recurso com maior risco de assédio, golpe e coleta de pontos por engenharia
social — e o que mais tensiona a relação entre privacidade e moderação.

## Decision Drivers
- Custo operacional (mensageria em tempo real é cara de manter).
- Capacidade de moderar mediante denúncia.
- Privacidade do conteúdo.
- Comportamento com conectividade ruim.
- Multi-dispositivo.
- Prevenção de abuso.

## Options Considered
| Opção | Prós | Contras |
|-------|------|---------|
| Implementação própria sobre a API + push | Controle total, sem provider novo, moderação possível | Trabalho de implementação; tempo real exige solução adicional |
| Provider de chat de terceiro | Rápido, recursos prontos | Custo, dados de conversa em terceiro, lock-in, LGPD |
| Delegar ao WhatsApp (sem chat próprio) | Custo zero, usuários já usam | Sem moderação, sem rastro, expõe telefone dos usuários — **inaceitável** |

Observação: a terceira opção parece econômica e é a pior em privacidade, porque obriga o
usuário a revelar o telefone para conversar.

## Decision
**Em aberto (Q-012).** Posição preliminar: **implementação própria simples** (sem tempo
real sofisticado no início: entrega por push + sincronização ao abrir), atrás de um
domínio isolado.

Decisões já tomadas, independentemente da escolha:
1. compartilhar ponto por mensagem é uma **concessão** com todas as regras de ADR-0012;
2. denúncia e bloqueio disponíveis dentro da conversa;
3. limites de envio e de solicitações para contas novas;
4. nenhum telefone de usuário é exposto a outro usuário.

## Consequences
MP-23 depende desta decisão. Mensageria **não** entra no protocolo de sync offline do MVP.

## Risks
- R-042 assédio, R-043 abuso de chat.
- Coleta de pontos por engenharia social.
- Custo de tempo real subestimado.

## Security Impact
Autorização por conversa; nenhum acesso cruzado; auditoria de acesso administrativo.

## Privacy Impact
Conteúdo é C3. Criptografia fim-a-fim é **decisão aberta (Q-018)** com trade-off explícito:
E2E impede moderação e complica denúncia, que são compromissos do produto (P11).

## Offline Impact
Mensagens criadas offline ficam pendentes, com idempotência para não duplicar.
Leitura offline limitada ao já sincronizado.

## Portability Impact
Implementação própria evita lock-in; provider de terceiro concentra dados sensíveis fora.

## Cost Impact
Tempo real e armazenamento de histórico são os custos principais.

## Operational Impact
Fila de denúncias de chat; retenção para apuração; suporte a vítimas.

## Open Questions
- Q-012: própria ou provider?
- Q-018: criptografia fim-a-fim?
- Retenção de mensagens (Q-016).
- Tempo real desde o início ou apenas push + sincronização?

## Evidence
Requisitos em `MESSAGING-MODEL.md`. Providers não avaliados.

## Supersedes / Superseded By
— / —
