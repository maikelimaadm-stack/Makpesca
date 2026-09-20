---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: —
---

# Runbook Baseline

> Runbook é procedimento para quem está sob pressão. Precisa ser direto e testado.
> Nesta fase ainda **não existe sistema em produção** — estes são os procedimentos que
> precisam existir antes do lançamento.

## 1. Procedimentos obrigatórios antes do lançamento

| # | Runbook | Estado |
|---|---------|--------|
| R-01 | Deploy e rollback da API | A escrever |
| R-02 | Migração de banco e reversão | A escrever |
| R-03 | Restauração de backup | A escrever |
| R-04 | Rotação de secrets | A escrever |
| R-05 | Resposta a vazamento de dados | Esqueleto em `INCIDENT-RESPONSE.md` |
| R-06 | Desligar recurso via kill switch | A escrever |
| R-07 | Reprocessar fila travada | A escrever |
| R-08 | Reconciliar billing divergente | A escrever |
| R-09 | Suspender parceiro / congelar payout | A escrever |
| R-10 | Atender pedido de exclusão de conta manualmente | A escrever |
| R-11 | Investigar duplicação de sync relatada | A escrever |
| R-12 | Tratar pico de denúncias | A escrever |

## 2. Estrutura de cada runbook

```
Título
Quando usar (sintoma observável)
Severidade
Pré-requisitos (acessos necessários)
Passos numerados
Verificação (como saber que funcionou)
Reversão (como desfazer)
Escalonamento (quando pedir ajuda)
Registro (o que anotar)
```

## 3. Esqueleto — R-03 Restauração de backup

**Quando usar:** perda ou corrupção de dados confirmada.
**Severidade:** SEV-1.

1. Declarar incidente e designar comandante.
2. **Parar as escritas afetadas** (kill switch do recurso).
3. Identificar o instante alvo da restauração (antes do evento).
4. Restaurar em ambiente isolado — **nunca sobre produção diretamente**.
5. Validar: contagens, integridade referencial, consultas geoespaciais, amostra de mídia.
6. Decidir: promover o restaurado ou aplicar correção cirúrgica.
7. Executar a promoção na janela combinada.
8. Reabrir as escritas.
9. Verificar reenvio de dispositivos (a idempotência protege contra duplicação).
10. Comunicar usuários se houve perda.
11. Post-mortem.

## 4. Esqueleto — R-06 Kill switch

**Quando usar:** vazamento suspeito, custo descontrolado, defeito grave em produção.

1. Identificar a flag correspondente ao recurso.
2. Desligar.
3. Confirmar por requisição de teste que o caminho está fechado.
4. Invalidar caches relacionados.
5. Registrar horário e motivo.
6. Avaliar o alcance do que ocorreu enquanto estava ligado.
7. Comunicar conforme severidade.

## 5. Esqueleto — R-11 Duplicação de sync relatada

1. Obter identificadores do usuário e dos registros (sem coordenadas no ticket).
2. Verificar se os registros têm o mesmo `entityId` ou `entityId` diferentes.
3. Se `entityId` diferentes: investigar se o cliente gerou dois identificadores
   (bug de cliente) — não é falha de idempotência.
4. Se `entityId` iguais: investigar o registro de idempotência.
5. Reproduzir o cenário em staging.
6. Corrigir a causa; só então tratar os dados afetados.
7. Nunca apagar dados do usuário sem confirmação explícita dele.

## 6. Acessos

Antes do lançamento, definir: quem tem acesso a produção, como se pede acesso temporário,
como é auditado e como é revogado. Sem isso, nenhum runbook é executável com segurança.

## 7. Exercícios

Antes do lançamento, executar ao menos: um restore completo, um rollback de deploy e uma
simulação de vazamento — com tempos medidos e registrados.
