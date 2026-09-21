---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0011
---

# Modos de Falha da Sincronização

Cada falha aqui precisa de comportamento definido. "Não sei o que acontece" é defeito.

## 1. Rede

| Falha | Comportamento esperado |
|-------|------------------------|
| Sem conectividade | Não tenta; aguarda evento de rede; UI mostra "pendente" sem alarme |
| Conexão cai no meio do push | Reenvia com **a mesma** `idempotencyKey`; servidor responde `duplicate` se já aplicou |
| Conexão cai no meio do upload | Retoma do ponto suportado; se não suportar, reinicia o mesmo objeto (mesmo hash) |
| Rede muito lenta | Timeout com backoff; não bloqueia a interface |
| Captive portal (rede que responde HTML) | Detecta resposta inválida e trata como falha de rede |

## 2. Servidor

| Falha | Comportamento |
|-------|---------------|
| 5xx transitório | Backoff exponencial com jitter |
| 429 | Respeita `Retry-After` |
| 503 em manutenção | Pausa o ciclo; informa estado no app |
| Resposta parcial de lote | Aplica os itens bem-sucedidos; mantém os demais pendentes |
| Servidor aplicou mas o cliente não recebeu a resposta | Reenvio com a mesma chave devolve `duplicate` — **sem duplicar** |

## 3. Dados

| Falha | Comportamento |
|-------|---------------|
| Validação rejeitada (4xx) | Marca `ERROR` com motivo; não reenvia automaticamente |
| Conflito de versão | Aplica matriz de conflito |
| Entidade referenciada inexistente (ex.: ponto excluído) | Reavalia o vínculo; captura permanece, referência é limpa |
| Tombstone para entidade já ausente | Sem efeito, sem erro |
| Cursor expirado | Ressincronização completa do escopo |
| Payload corrompido localmente | Item vai para quarentena local, com relato; nunca trava a fila inteira |

## 4. Dispositivo

| Falha | Comportamento |
|-------|---------------|
| App morto durante escrita local | Escrita transacional; ou aplicou tudo, ou nada |
| App morto durante upload | Fila persistente retoma na próxima abertura |
| Disco cheio | Aviso antes de capturar mídia/baixar região; nunca corromper o banco local |
| Relógio muito errado | Servidor decide ordem; app avisa se a divergência for grande |
| Troca de fuso horário | `caughtAt` preserva o fuso original de registro |
| Logout com pendências | Avisa e oferece sincronizar antes |
| Desinstalação com pendências | Dados pendentes são perdidos — o app deve avisar quando houver pendência antiga |

## 5. Multi-dispositivo

| Falha | Comportamento |
|-------|---------------|
| Dois dispositivos editam a mesma entidade | Matriz de conflito |
| Dispositivo antigo volta após meses | Cursor expirado → ressincronização; tombstones impedem ressurreição |
| Dispositivo com credencial revogada | Sincronização bloqueada; dados locais preservados até decisão do usuário |

## 6. Mídia

| Falha | Comportamento |
|-------|---------------|
| Hash não confere | Reenvio; após N tentativas, `FAILED` com motivo |
| Ticket expirado | Solicita novo ticket |
| Storage indisponível | Backoff; registro permanece íntegro |
| Processamento falha | Original preservado; alerta operacional |
| Arquivo local apagado pelo sistema | Marca `FAILED` e informa que a foto não pode mais ser enviada |

## 7. Falhas silenciosas (as piores)

Estas precisam de detecção ativa, porque não geram erro:

| Falha | Detecção |
|-------|----------|
| Item preso na outbox indefinidamente | Métrica de idade do item mais antigo + alerta no app |
| Cursor que não avança | Métrica de progresso de pull |
| Duplicação lógica sem violar chave | Verificação por `idempotencyKey` e auditoria periódica |
| Mídia órfã acumulando | Job de reconciliação com relatório |
| Precisão degradada errada em cache | Testes de contrato por perfil de observador |

## 8. Regra geral

Toda falha precisa de: estado visível, motivo compreensível, caminho de recuperação e
métrica. Falha que só aparece como "carregando" eterno é defeito grave.
