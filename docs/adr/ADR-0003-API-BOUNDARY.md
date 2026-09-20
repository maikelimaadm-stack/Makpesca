# ADR-0003 — Fronteira de API

- **Status:** **ACCEPTED**
- **Date:** 2026-09-20
- **Onda:** F2

## Context
Um produto com dados sensíveis de localização, offline-first e múltiplos clientes precisa
de um ponto único onde as regras existam. A alternativa comum — clientes acessando o banco
gerenciado diretamente por SDK — dispersaria autorização, privacidade e validação por
quatro aplicações e tornaria a degradação de coordenadas impossível de garantir.

## Decision Drivers
- Geo-privacidade precisa ser aplicada em um único lugar.
- Autorização por objeto não pode depender do cliente.
- Clientes móveis antigos convivem por muito tempo.
- Portabilidade de infraestrutura.
- Auditabilidade.

## Options Considered
| Opção | Prós | Contras |
|-------|------|---------|
| **API própria como única fronteira** | Controle total, privacidade garantida, portável | Mais código para escrever |
| Clientes acessando o banco via SDK do provider | Rápido de começar | Regras dispersas; impossível garantir degradação; lock-in profundo; risco crítico de vazamento |
| Híbrido (leituras pelo SDK, escritas pela API) | Menos código | Leitura é exatamente onde o vazamento acontece; pior dos dois mundos |

## Decision
**Toda regra de negócio passa por `api.makpesca.com.br`.** Mobile, Web, Admin e Partners
nunca acessam PostgreSQL/Supabase diretamente para leitura ou escrita de domínio.

```
CLIENTES → api.makpesca.com.br → Application/Domain → Ports/Adapters → Infraestrutura
```

Esta decisão é **constitucional** (Art. 2) e não pode ser flexibilizada por conveniência.

## Consequences
- Todo acesso a dados exige endpoint.
- Degradação de coordenadas acontece em um único componente.
- O provider de banco pode ser trocado sem afetar clientes.
- Mais trabalho inicial, muito menos risco.

## Risks
- Tentação de "atalho" em prazo apertado. Mitigação: gate `ARCH-CONSISTENCY`.
- API vira gargalo de desenvolvimento. Mitigação: contratos definidos cedo.

## Security Impact
Positivo e decisivo: autorização por objeto centralizada e auditável.

## Privacy Impact
**Pré-requisito** da geo-privacidade server-side. Sem esta decisão, ADR-0012 é inexequível.

## Offline Impact
O cliente sincroniza com a API, não com o banco. Protocolo explícito e versionável.

## Portability Impact
Alto e positivo: o banco e a hospedagem ficam atrás da API.

## Cost Impact
Mais desenvolvimento inicial; menos custo de incidente e de migração.

## Operational Impact
Um ponto para observar, limitar, versionar e proteger.

## Open Questions
Nenhuma. Decisão aceita.

## Evidence
Derivada dos requisitos de privacidade do produto (`GEO-PRIVACY.md`) e do modelo de
ameaças (`GEO-PRIVACY-THREAT-MODEL.md`).

## Supersedes / Superseded By
— / —
