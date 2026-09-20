# ADR-0008 — Autenticação

- **Status:** **OPEN**
- **Date:** 2026-09-20
- **Onda:** F6

## Context
Precisamos autenticar usuários em mobile e web, com sessões revogáveis, login social
(exigido pelas lojas quando há login federado) e conformidade com LGPD. Migrar identidade
depois é a migração mais cara que existe.

## Decision Drivers
Ver `../08-security-privacy/AUTH-OPTIONS.md` §3 — dez critérios, com destaque para:
segurança, custo em escala, **custo de saída**, LGPD e suporte a mobile.

## Options Considered
| Opção | Resumo |
|-------|--------|
| A. Supabase Auth encapsulado | Aproveita o provider já previsto; atrás de `AuthPort` |
| B. Clerk | Serviço especializado |
| C. Auth0 | Serviço maduro |
| D. Open-source auto-hospedado | Controle, mais operação |
| E. Solução própria | **Desaconselhada** — risco alto, sem diferencial de produto |

## Decision
**Em aberto.** Posição preliminar: escolher entre A, B e C, com `AuthPort` garantindo a
saída. A opção E é descartada por risco.

Requisitos inegociáveis para qualquer escolha:
1. identificador de usuário **próprio**; referência do provider é opaca;
2. sessões listáveis e revogáveis;
3. refresh rotativo com detecção de reutilização;
4. exclusão de conta propagada ao provider;
5. nenhuma autorização de produto delegada ao provider;
6. plano de migração documentado **antes** do lançamento.

## Consequences
Enquanto aberto, MP-03 (Auth) não pode começar.

## Risks
- R-011 (auth bypass), R-012 (conta comprometida).
- Lock-in de identidade: o mais caro do projeto.
- Requisitos das lojas para login social não verificados.

## Security Impact
Máximo. É a porta de entrada de tudo.

## Privacy Impact
Dados pessoais no provider. LGPD: local de processamento, contrato, exclusão.

## Offline Impact
Sessão precisa sobreviver a longos períodos sem rede; renovação exige conectividade, mas
a ausência dela **não pode impedir** a criação local de dados (OFF-3, OFF-9).

## Portability Impact
`AuthPort` é obrigatório. O identificador próprio é o que torna a migração possível.

## Cost Impact
A verificar por faixa de usuários ativos, com fonte e data.

## Operational Impact
Suporte a recuperação de conta, incidentes de credencial e revogação em massa.

## Open Questions
- Q-008: qual provider?
- Senha, magic link, passkeys ou combinação?
- Requisitos de Apple/Google para login social (verificar com fonte).
- Local de processamento e transferência internacional (LGPD).

## Evidence
Nenhuma verificada. Comparação qualitativa em `AUTH-OPTIONS.md`.

## Supersedes / Superseded By
— / —
