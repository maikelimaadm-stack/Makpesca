---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: todos
---

# Roadmap de Slices de Implementação

> **Nada aqui é executado enquanto `IMPLEMENTATION-READY-GATE` estiver BLOCKED.**
> Este é o plano, não a execução.

## 1. Princípios do fatiamento

| Princípio |
|-----------|
| Cada slice entrega valor verificável ponta a ponta |
| Um slice não invade escopo de outro |
| Slice tem critério de aceite objetivo |
| Slice que toca localização carrega o `PRIVACY-GATE` |
| Slice que toca sync carrega o `OFFLINE-GATE` |
| Fundamentos antes de recursos: identidade, dados e privacidade primeiro |

## 2. Sequência revisada

A sequência abaixo ajusta a ordem proposta originalmente, com base nas dependências reais
(ver `DEPENDENCY-MAP.md`). As mudanças relevantes estão marcadas.

| Slice | Nome | Entrega | Onda mínima | Observação |
|-------|------|---------|-------------|------------|
| MP-00 | Foundation | Monorepo, padrões, CI, configuração | F0-F2 | — |
| MP-01 | API Foundation | Esqueleto da API, erros, validação, OpenAPI, logs | F2, F6 | **Movido para antes do Mobile Shell** |
| MP-02 | Data Foundation | Banco, PostGIS, migrações, repositórios | F3 | **Movido para antes de Auth** |
| MP-03 | Auth | Autenticação, sessões, revogação | F6 | Depende de API + dados |
| MP-04 | Mobile Shell | App navegável, configuração, sessão | F2 | Depois que há API real |
| MP-05 | Local SQLite | Banco local, migrações locais | F4 | **Antes do mapa**: o mapa depende de dados locais |
| MP-06 | Online Map | Mapa com posição atual e pins | F5 | — |
| MP-07 | Geo Privacy Core | Visibilidade, precisão, degradação server-side | F3 | **Antecipado**: precisa existir antes de criar pontos |
| MP-08 | Offline Spot | Criar/editar ponto offline | F4 | Já nasce com privacidade |
| MP-09 | Offline Catch | Registrar captura offline | F4 | — |
| MP-10 | Sync Core | Outbox, push/pull, idempotência, conflitos | F4 | Slice mais crítico |
| MP-11 | Media Sync | Upload retomável, EXIF, derivativos | F4 | — |
| MP-12 | Sharing | Concessões, revogação, prazos | F3 | — |
| MP-13 | Basic Social / Profile | Perfil, follow, denúncia, bloqueio | F7 | Moderação junto, não depois |
| MP-14 | Feed | Feed simples com precisão correta | F7 | — |
| MP-15 | Web Foundation | Landing, login, perfis públicos | F2 | — |
| MP-16 | Admin Mínimo | Moderação básica e auditoria | F9 | **Antecipado**: social sem moderação não vai a público |
| MP-17 | Offline Maps | Regiões offline | F5 | **Depende de ADR-0010** |
| MP-18 | Communities | Comunidades e feed local | F7 | — |
| MP-19 | Billing / Entitlements | FREE/PRO, entitlements, restore | F8 | — |
| MP-20 | Partner Stores | Lojas, perfis, verificação | F8 | — |
| MP-21 | Offers + Affiliate Tracking | Ofertas, cliques, atribuição | F8 | — |
| MP-22 | Events / Groups | Grupos e eventos | F7 | — |
| MP-23 | Messaging | Conversas | F7 | — |
| MP-24 | Rankings / Achievements | Com antifraude | F8 | Antifraude é pré-requisito |
| MP-25 | Challenges | Desafios | F8 | Exige validação jurídica |
| MP-26 | Admin Completo | Operação completa | F9 | — |
| MP-27 | Partner Portal | Portal de parceiros | F8 | — |
| MP-28 | Environmental Data | Dados ambientais | F5 | — |
| MP-29 | Fishing Intelligence | Insights agregados | F3+F8 | Exige coorte mínima validada |
| MP-30 | Hardening | Segurança, desempenho, custo | F9 | — |
| MP-31 | Beta | Beta fechado com usuários reais | F9 | — |
| MP-32 | Production | Lançamento | F10 | — |

## 3. Mudanças em relação à sequência original (e por quê)

| Mudança | Justificativa |
|---------|---------------|
| API Foundation antes de Mobile Shell | Um app sem API real vira mock que depois é jogado fora |
| Data Foundation antes de Auth | Auth precisa persistir usuário e sessão |
| SQLite local antes do mapa | O mapa exibe dados locais; sem eles, o mapa é decorativo |
| **Geo Privacy antes de criar pontos** | Criar pontos sem a regra de privacidade gera dados legados inseguros e retrabalho |
| Admin mínimo antes de abrir o social | Recurso social sem moderação não é lançável (P11) |
| Ranking depois do antifraude | Ranking sem antifraude cria incentivo impossível de policiar depois |

## 4. Marcos

| Marco | Slices | Significado |
|-------|--------|-------------|
| **M1 — Ciclo de campo** | MP-00..MP-12 | Marcar, registrar, offline, sincronizar, compartilhar |
| **M2 — Comunidade mínima** | MP-13..MP-18 | Social utilizável e moderado |
| **M3 — Sustentabilidade** | MP-19..MP-21 | PRO e comércio |
| **M4 — Ecossistema** | MP-22..MP-29 | Recursos avançados |
| **M5 — Produção** | MP-30..MP-32 | Endurecimento e lançamento |

M1 é o que prova o produto. Se M1 não ficar sólido, nada adiante importa.

## 5. Critérios de aceite por slice (modelo)

```
Slice: MP-XX
Entrega:
Fora do escopo:
Documentos SSOT aplicáveis:
Gates aplicáveis:
Testes obrigatórios:
Invariantes tocadas:
Critério de aceite verificável:
Riscos endereçados:
```

## 6. Estado

Nenhum slice foi iniciado. Nenhum será iniciado antes da liberação do
`IMPLEMENTATION-READY-GATE`.
