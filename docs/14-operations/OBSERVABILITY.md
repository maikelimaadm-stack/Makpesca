---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0016
---

# Observabilidade

## 1. Pilares

| Pilar | Uso | Fase |
|-------|-----|------|
| Logs estruturados | Investigação | MVP |
| Métricas | Saúde e tendência | MVP (básico) |
| Traces | Latência entre componentes | Pós-MVP |
| Error tracking | Defeitos em produção | MVP |
| Performance (RUM/mobile) | Experiência real | Pós-MVP |

## 2. Logs

Formato JSON estruturado, com campos padronizados:

| Campo | Descrição |
|-------|-----------|
| `timestamp` | UTC |
| `level` | `debug`/`info`/`warn`/`error` |
| `message` | Estável, sem interpolar dado sensível |
| `requestId` | Correlação por requisição |
| `correlationId` | Correlação entre serviços/jobs |
| `userRef` | Pseudônimo, nunca e-mail |
| `route`, `method`, `status`, `durationMs` | Contexto HTTP |
| `deviceId` | Quando relevante |
| `appVersion`, `platform` | Diagnóstico |
| `error` | Tipo e código; stack apenas em ambiente interno |

## 3. Proibições absolutas nos logs

| Nunca registrar |
|-----------------|
| **Coordenada de qualquer precisão** |
| Token, senha, secret, chave |
| E-mail, telefone, documento |
| Conteúdo de mensagem privada |
| Corpo de requisição de rotas sensíveis |
| Consulta SQL com parâmetros reais |

A redação é automática por nome de campo (`../04-data/DATA-CLASSIFICATION.md` §4).
Exceção exige justificativa revisada — na prática, para coordenadas **não existe exceção**.

## 4. Métricas mínimas

### API
Requisições por rota, taxa de erro por rota, latência p50/p95/p99, 429 por rota, tamanho
de resposta, consumo de dependências externas.

### Sync
Itens pendentes, idade do item mais antigo, taxa de `duplicate`, taxa de `conflict`,
tempo até convergência, falhas permanentes.

### Mídia
Uploads iniciados/concluídos/falhos, tempo médio, tentativas por upload, órfãos detectados.

### Jobs
Fila por tipo, atraso, tempo de execução, falhas, reprocessamentos.

### Billing
Webhooks recebidos/duplicados/falhos, divergências de reconciliação, falhas de entitlement.

### Comércio
Cliques, conversões, comissões por estado, sinais de fraude.

### Negócio
Usuários ativos, capturas registradas, pontos criados, publicações, denúncias.

### Custo
Custo de mapa, mídia e banco por usuário ativo (`COST-GATE`).

## 5. Alertas

| Alerta | Severidade |
|--------|-----------|
| Taxa de erro 5xx acima do limiar | Alta |
| Latência p95 de sync/mapa acima do alvo | Alta |
| Fila de jobs com atraso crescente | Média |
| Falha de webhook de billing | Alta |
| Divergência de reconciliação | Alta |
| Pico de denúncias | Média |
| Pico de 401/403 (possível ataque) | Alta |
| Detecção de campo sensível em log | **Crítica** |
| Backup falhou | **Crítica** |

## 6. Correlação

`requestId` é gerado na borda (ou aceito do cliente, se confiável e validado), propagado
por toda a cadeia, incluindo jobs assíncronos, e devolvido em respostas de erro para
suporte.

## 7. Mobile

Crash reporting com filtro de dados sensíveis, métricas de desempenho de tela, tamanho do
banco local, estado da fila de sync, consumo de bateria em sessão de mapa.

**Nenhum relatório de erro do app pode conter coordenadas** (GP-R4, V4).

## 8. Retenção

Logs: retenção curta (proposta: 30 dias). Métricas: agregadas por mais tempo.
Erros: conforme necessidade de investigação. Auditoria administrativa: retenção longa.

## 9. Provider

Decisão aberta (ADR-0016, Q-025). Requisito: formato de log é nosso, o destino é
substituível. Nenhum provider recebe dado que os logs não deveriam conter.
