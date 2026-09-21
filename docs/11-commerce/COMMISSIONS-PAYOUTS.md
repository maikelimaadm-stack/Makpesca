---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0020
---

# Comissões e Pagamentos

## 1. Ciclo da comissão

```
conversão registrada → validação antifraude → comissão calculada (PENDING) →
janela de contestação → aprovada (APPROVED) → incluída em payout (PAID)
                     ↘ rejeitada (REJECTED) / estornada (REVERSED)
```

## 2. Estados

| Estado | Significado |
|--------|-------------|
| `PENDING` | Calculada, aguardando validação/janela |
| `APPROVED` | Validada, apta a pagamento |
| `PAID` | Incluída em payout liquidado |
| `REJECTED` | Conversão inválida ou fraudulenta |
| `REVERSED` | Estornada após aprovação (devolução, fraude tardia) |
| `DISPUTED` | Em contestação |

Transições são registradas com motivo, autor e data. Estado nunca é apagado.

## 3. Cálculo

Depende do modelo comercial (Q-019). Em qualquer modelo:

| Regra |
|-------|
| O cálculo é **determinístico e reproduzível** a partir dos dados da conversão |
| A regra vigente no momento da conversão é a aplicada (versionamento de regra) |
| Arredondamento definido e consistente |
| Moeda: BRL |
| Toda comissão referencia exatamente uma conversão (INV-C01) |

## 4. Payout

| Aspecto | Definição |
|---------|-----------|
| Periodicidade | A definir (proposta: mensal) |
| Valor mínimo | A definir |
| Janela de contestação | A definir (proposta: 30 dias após a conversão) |
| Forma de pagamento | **Pendente comercial/jurídico (Q-020)** |
| Documento fiscal | Pendente contábil |
| Conciliação | Obrigatória antes de liquidar |

## 5. Conciliação

Por que existe: a compra acontece fora da plataforma. Conciliação compara o que o parceiro
informou, o que nossos cliques indicam e o que foi efetivamente pago.

| Verificação |
|-------------|
| Conversões sem click correspondente na janela |
| Clicks com taxa de conversão anômala |
| Pedidos externos duplicados |
| Valores fora do padrão do parceiro |
| Conversões informadas fora do prazo |
| Comissões já pagas reaparecendo |

Divergência abre caso, não gera pagamento automático.

## 6. Disputas

O parceiro pode contestar dentro da janela. A disputa é decidida com base na trilha de
auditoria (`ATTRIBUTION.md` §7). A decisão é registrada e comunicada.

## 7. Riscos

| Risco | Mitigação |
|-------|-----------|
| Comissão duplicada (R-054) | Unicidade `(parceiro, pedido)` + idempotência + conciliação |
| Fraude de conversão (R-052) | Antifraude antes da aprovação |
| Pagamento antes da validação | Janela de contestação obrigatória |
| Erro de cálculo em massa | Regra versionada + reprocessamento auditável |
| Inconsistência contábil | Conciliação periódica e fechamento por período |

## 8. Separação de responsabilidades

| Sistema | Responsabilidade |
|---------|------------------|
| Makpesca | Registrar click, atribuir, calcular, conciliar, reportar |
| Parceiro | Informar conversões verdadeiras, honrar ofertas |
| Financeiro/contábil | Liquidar e documentar |

A Makpesca **não** processa pagamento do consumidor final nesta fase.

## 9. Fase

Pós-MVP, com poucos parceiros e conciliação manual no início. Automatizar só depois de
observar o comportamento real das conversões.
