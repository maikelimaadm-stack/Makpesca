---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: —
---

# Feature Flags

## 1. Para que servem aqui

| Uso | Exemplo |
|-----|---------|
| Rollout gradual | Liberar novo sync para 5% dos usuários |
| Beta | Recursos para testadores |
| **Kill switch** | Desligar imediatamente um endpoint que vaza dados |
| Operação | Reduzir carga desativando recurso caro |
| Segmentação técnica | Ativar por versão de app/plataforma |

O **kill switch é requisito de segurança**: a resposta a incidente depende de conseguir
desligar um caminho sem deploy (`../08-security-privacy/INCIDENT-RESPONSE.md` §4).

## 2. Solução

Começar simples: configuração no servidor, avaliada pela API e entregue ao cliente.
Nenhuma ferramenta externa até haver necessidade comprovada (`FeatureFlagPort` preserva a
troca futura).

## 3. Tipos

| Tipo | Vida | Regra |
|------|------|-------|
| Release | Curta | Removida após o rollout completo |
| Experimento | Média | Tem data de término |
| Operacional / kill switch | Longa | Documentada e testada |
| Entitlement | — | **Não é flag** — é Entitlement Service |

Não confundir flag com entitlement: flag decide se o recurso existe; entitlement decide
se aquele usuário pode usá-lo.

## 4. Regras

| # | Regra |
|---|-------|
| 1 | Toda flag tem dono, descrição e data de revisão |
| 2 | Flag de release é removida depois do rollout (dívida técnica) |
| 3 | O estado padrão é o **seguro** (desligado para o novo) |
| 4 | Flag nunca controla regra de privacidade de forma a poder "desligar" a proteção |
| 5 | Mudança de flag em produção é auditada |
| 6 | O cliente offline usa o último estado conhecido |
| 7 | Flags não se acumulam sem limite: excesso vira caos combinatório |

## 5. Avaliação no cliente

O app recebe as flags aplicáveis junto com a sessão/configuração, com TTL. Sem rede, usa
o último valor. Flag desconhecida = desligada.

## 6. Rollout seguro

```
interno → beta (voluntários) → 5% → 25% → 50% → 100%
```

Em cada etapa: observar métricas de erro, sync, desempenho e denúncias. Reversão é sempre
possível e testada antes do início.

## 7. Limpeza

Revisão periódica das flags. Flag sem dono, sem uso ou vencida é removida. Código morto
atrás de flag antiga é passivo, não segurança.
