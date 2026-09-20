---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0011
---

# Matriz de Testes Offline

Todos os casos abaixo são **obrigatórios** antes de considerar o offline pronto.

## 1. Criação offline

| # | Caso | Resultado esperado |
|---|------|--------------------|
| O-01 | Criar ponto sem rede | Salvo local, `PENDING`, visível imediatamente |
| O-02 | Criar captura com foto sem rede | Salvo local, mídia `LOCAL_ONLY` |
| O-03 | Editar registro pendente antes de sincronizar | Uma única versão enviada |
| O-04 | Excluir registro pendente nunca enviado | Removido local, nada enviado |
| O-05 | Fechar o app logo após criar | Dado presente ao reabrir |
| O-06 | Matar o app durante a escrita | Ou salvou tudo, ou nada — sem estado corrompido |
| O-07 | Reiniciar o aparelho com pendências | Fila preservada |

## 2. Sincronização

| # | Caso | Resultado esperado |
|---|------|--------------------|
| O-10 | Reconectar com 1 item pendente | Sincroniza, vira `SYNCED` |
| O-11 | Reconectar com 100 itens | Sincroniza em lotes, sem travar a interface |
| O-12 | Perder conexão no meio do push | Reenvia com a mesma chave; **sem duplicar** |
| O-13 | Servidor responde após o cliente desistir | Reenvio retorna `duplicate` |
| O-14 | Sincronizar duas vezes seguidas | Nenhum efeito adicional |
| O-15 | 429 do servidor | Respeita o tempo indicado |
| O-16 | 5xx transitório | Backoff, sucesso depois |
| O-17 | 4xx de validação | Item marcado com erro, sem loop de reenvio |
| O-18 | Credencial expirada durante o sync | Renova e continua; se não conseguir, mantém pendente |

## 3. Conflitos

| # | Caso | Resultado esperado |
|---|------|--------------------|
| O-20 | Editar o mesmo ponto em dois dispositivos | Matriz de conflito aplicada |
| O-21 | Conflito de visibilidade (um abre, outro fecha) | **Vence o mais restritivo** |
| O-22 | Editar em A, excluir em B | Exclusão vence |
| O-23 | Conflito de fotos | União, nenhuma foto perdida |
| O-24 | Dispositivo offline por mais tempo que a retenção | Ressincronização completa |
| O-25 | Tentar recriar entidade excluída | Rejeitado, não ressuscita |

## 4. Mídia

| # | Caso | Resultado esperado |
|---|------|--------------------|
| O-30 | Upload interrompido por perda de rede | Retoma, sem duplicar |
| O-31 | App morto durante upload | Retoma na próxima abertura |
| O-32 | Trocar Wi-Fi por dados móveis | Respeita a preferência; retoma quando permitido |
| O-33 | Mesma foto enviada duas vezes | Uma única mídia (mesmo hash) |
| O-34 | Arquivo local apagado pelo sistema | `FAILED` com motivo claro |
| O-35 | Disco cheio ao capturar | Aviso antes, sem corromper o banco local |
| O-36 | Foto com GPS no EXIF publicada | Publicada **sem** EXIF |

## 5. Leitura offline

| # | Caso | Resultado esperado |
|---|------|--------------------|
| O-40 | Abrir mapa de região baixada sem rede | Renderiza |
| O-41 | Abrir região não baixada sem rede | Estado vazio claro; dados do produto ainda visíveis |
| O-42 | Consultar catálogo sem rede | Funciona |
| O-43 | Ver ponto concedido por terceiro sem rede | Na precisão autorizada, nunca acima |
| O-44 | Concessão revogada enquanto offline | Ao sincronizar, dado local é removido |

## 6. Ciclo completo

| # | Caso | Resultado esperado |
|---|------|--------------------|
| O-50 | **Cenário de referência completo** (`../05-offline-sync/OFFLINE-FIRST-CONTRACT.md` §1) | Convergência sem perda e sem duplicação |
| O-51 | Repetir o ciclo 10 vezes seguidas | Estado estável |
| O-52 | Dois dispositivos executando o ciclo em paralelo | Convergência |

## 7. Limites e degradação

| # | Caso | Resultado esperado |
|---|------|--------------------|
| O-60 | Exceder limite do plano offline | Erro claro, sem perder dado criado |
| O-61 | Entitlement expirado sem rede | Acesso mantido; revalida depois (OFF-9) |
| O-62 | Logout com pendências | Aviso antes de descartar |
| O-63 | Banco local com milhares de registros | Listas paginadas, desempenho aceitável |
| O-64 | Migração do banco local | Nenhum dado perdido; recuperável se falhar |

## 8. Como medir

Automação onde possível (simulação de rede, kill do processo, injeção de falha) e um
roteiro manual em dispositivos reais antes de cada lançamento relevante.
