---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0015
---

# Jobs Assíncronos

## 1. Por que existem

A hospedagem serverless limita tempo e recursos por requisição (R-034). Além disso,
muitas tarefas não devem bloquear o usuário. Tudo que é longo, repetível ou tolerante a
atraso vira job.

## 2. Catálogo de jobs

| Job | Gatilho | Prioridade |
|-----|---------|-----------|
| Processar mídia (EXIF, derivativos) | Upload confirmado | Alta |
| Notificações (push/e-mail) | Evento de domínio | Alta |
| Processar webhook de billing | Webhook recebido | **Alta** |
| Reconciliação de billing | Agendado | Alta |
| Agregações (contadores, estatísticas) | Agendado/evento | Média |
| Rankings | Agendado | Média |
| Conquistas | Evento | Média |
| Insights | Agendado | Baixa |
| Limpeza de órfãos (mídia, tickets) | Agendado | Baixa |
| Purga por retenção | Agendado | Média |
| Exportação de dados do usuário | Solicitação | Média |
| Exclusão de conta | Solicitação | **Alta** |
| Triagem de moderação | Evento | Alta |
| Conciliação de afiliados | Agendado | Média |
| Reprocessamento manual | Operação | Variável |

## 3. Garantias

| Garantia | Regra |
|----------|-------|
| Entrega | Pelo menos uma vez — portanto **todo job é idempotente** |
| Ordem | Não garantida; jobs não dependem de ordem entre si |
| Retry | Backoff exponencial com teto |
| Dead letter | Após N tentativas, fila morta com alerta |
| Visibilidade | Estado consultável pela operação |
| Timeout | Definido por tipo |

## 4. Regras

| # | Regra |
|---|-------|
| 1 | Job usa os mesmos casos de uso da API — nunca regra paralela |
| 2 | Job é idempotente por construção |
| 3 | Job carrega `correlationId` |
| 4 | Job não loga dado sensível |
| 5 | Falha de job nunca corrompe estado parcialmente |
| 6 | Job longo é divisível em lotes |
| 7 | Job que afeta dados do usuário é auditado |

## 5. Abstração

`QueuePort` isola o provider (ADR-0015 em aberto). Candidatos vão de fila gerenciada a
tabela de jobs no próprio Postgres.

**Posição preliminar:** começar com a solução mais simples que atenda (possivelmente fila
no próprio banco), medir, e só então adotar infraestrutura dedicada. Introduzir um sistema
de filas antes de haver volume é overengineering (P10).

## 6. Agendamento

Jobs periódicos são declarados pela aplicação, não presos ao agendador da plataforma
(portabilidade). Cada agendamento tem: frequência, janela aceitável, tempo máximo e
comportamento se a execução anterior ainda estiver rodando.

## 7. Observabilidade

Por tipo de job: enfileirados, em execução, concluídos, falhos, tempo médio, atraso,
itens em dead letter. Alerta quando o atraso cresce de forma sustentada.
