---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0001, ADR-0011
---

# Estratégia de Banco Local (SQLite)

## 1. Papel

O SQLite é a **fonte de verdade da sessão do usuário no dispositivo**. A interface lê do
SQLite, não da rede. A rede alimenta o SQLite.

```
UI → SQLite local → (outbox) → API → PostgreSQL
UI ← SQLite local ← (pull)  ← API ← PostgreSQL
```

## 2. Grupos de tabelas locais (conceitual)

| Grupo | Conteúdo |
|-------|----------|
| Dados do usuário | pontos, capturas, pescarias, preferências |
| Metadados de mídia | referência local, hash, estado de upload |
| Outbox | mutações pendentes com idempotency key |
| Estado de sync | cursor, versões conhecidas, tombstones recebidos |
| Catálogos | espécies, iscas, técnicas, regiões, corpos d'água |
| Dados de terceiros autorizados | pontos concedidos, na precisão autorizada |
| Regiões offline | metadados do pacote baixado |
| Entitlements em cache | com validade |

## 3. Regras

1. Escrita do usuário é **durável antes** de confirmar na interface (OFF-2).
2. Toda entidade local carrega: `id` (UUID do cliente), `version`, `updatedAt`,
   `syncState` (`LOCAL_ONLY`, `PENDING`, `SYNCED`, `CONFLICT`, `ERROR`), `deletedAt?`.
3. Nenhuma coordenada de terceiro é guardada acima da precisão autorizada (OFF-8).
4. Dados locais sensíveis (sessão, credenciais) ficam no armazenamento seguro do sistema
   operacional, **não** no SQLite.
5. Consultas de lista sempre paginadas — o dispositivo pode ter milhares de registros.

## 4. Migrações locais

- Versionadas e sequenciais, aplicadas na abertura do app.
- **Nunca destrutivas** sem caminho de preservação: migração que perderia dado precisa
  copiar, transformar e só então remover.
- Antes de migração de risco: cópia de segurança local do arquivo.
- Falha de migração não pode deixar o app inutilizável — precisa de caminho de recuperação
  e de relato de erro (R-026).
- Testes de upgrade de versão N → N+1 são obrigatórios.

## 5. Tamanho e limpeza

| Item | Política |
|------|----------|
| Mídia já enviada e confirmada | Pode liberar o arquivo original conforme preferência |
| Cache de terceiros | TTL; limpeza por LRU |
| Região offline | Removível pelo usuário; tamanho exibido |
| Tombstones locais | Purga após a janela de sync |
| Logs locais | Rotativos, sem dado sensível |

O app deve informar o espaço ocupado e permitir liberar espaço sem perder dados pendentes.

## 6. Segurança local

- Dispositivo perdido é cenário real: dados locais devem depender do desbloqueio do
  aparelho; credenciais no keystore/keychain.
- Logout limpa dados do usuário; mas **nunca** descarta silenciosamente mutações pendentes:
  avisar antes.
- Considerar cifrar o banco local (decisão aberta; custo de desempenho a medir).

## 7. Multi-conta e multi-dispositivo

- Um banco por usuário logado no dispositivo; troca de conta não mistura dados.
- O mesmo usuário em vários dispositivos gera convergência via servidor, não entre
  dispositivos diretamente.
