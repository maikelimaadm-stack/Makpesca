---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0011, ADR-0013
---

# Ciclo de Vida dos Dados

> Prazos marcados como `NEEDS-DECISION` dependem de decisão jurídica/produto (Q-016).

## 1. Estados de um registro

```
criado local (offline) → pendente de sync → aceito pelo servidor →
ativo → [arquivado] → excluído logicamente (tombstone) → purga física
```

## 2. Retenção proposta

| Dado | Retenção ativa | Após exclusão | Estado |
|------|---------------|---------------|--------|
| Ponto / captura | Enquanto a conta existir | Purga após janela de tombstone | NEEDS-DECISION (janela) |
| Mídia | Enquanto o registro existir | Exclusão assíncrona + limpeza de derivativos | PROPOSED |
| Tombstone | Maior que a janela máxima de sync (proposta: 180 dias) | Purga | NEEDS-DECISION |
| Mensagem privada | NEEDS-DECISION | Exclusão para ambos os lados conforme política | NEEDS-DECISION |
| Denúncia / caso de moderação | Prazo de apuração + histórico de reincidência | Anonimização | NEEDS-DECISION |
| Log de aplicação | Curto (proposta: 30 dias) | Purga automática | PROPOSED |
| Log de auditoria administrativa | Longo (proposta: 2 anos) | Preservado | NEEDS-DECISION |
| Click / referral | Janela de atribuição + conciliação | Agregação | PROPOSED |
| Conversão / comissão | Obrigação fiscal/contratual | Preservado conforme lei | NEEDS-DECISION |
| Dados de assinatura | Enquanto ativa + período legal | Preservado conforme lei | NEEDS-DECISION |
| Backups | Ver `BACKUP-RESTORE.md` | Expiram com o backup | PROPOSED |

## 3. Exclusão de conta

Ao solicitar exclusão:

1. a conta entra em estado `PENDING_DELETION` com janela de arrependimento (proposta: 7 dias);
2. sessões são revogadas;
3. conteúdo público é despublicado;
4. dados pessoais são removidos ou anonimizados;
5. pontos e capturas privados são removidos;
6. tombstones são propagados aos dispositivos do usuário;
7. mídia é agendada para exclusão;
8. dados com obrigação legal (fiscal, fraude) são retidos em forma mínima e segregada;
9. conteúdo de terceiros que mencione o usuário é tratado por anonimização, não por
   exclusão do conteúdo alheio.

**Exclusão precisa convergir para os dispositivos** — um aparelho offline que volta depois
não pode ressuscitar dados excluídos (INV-S06).

## 4. Exportação

- O titular exporta os próprios dados: perfil, pontos (com coordenada verdadeira),
  capturas, mídia, publicações, comunidades, mensagens conforme política.
- A exportação é assíncrona, entregue por link autenticado e expirável.
- A exportação **não** inclui dados de terceiros acima da precisão autorizada.

## 5. Anonimização

Anonimizar significa remover a ligação com a pessoa de forma irreversível:
identificador substituído, campos livres removidos, localização reduzida a célula de
agregação com coorte mínima. Pseudonimização (identificador trocado, mas reversível)
**não** conta como anonimização para fins de publicação de insight.

## 6. Dados derivados

Contadores, rankings, conquistas, insights e agregações derivadas precisam ser
reprocessados ou invalidados quando o dado de origem é excluído. Insight publicado que
dependia de dado excluído é recalculado no próximo ciclo.

## 7. Ciclo de vida no dispositivo

| Dado local | Política |
|------------|----------|
| Registros do usuário | Persistem até exclusão ou logout com limpeza |
| Mídia pendente | Persiste até upload confirmado; depois pode ser liberada |
| Cache de terceiros | TTL curto; nunca acima da precisão autorizada |
| Região offline | Até o usuário remover ou o plano exigir |
| Logout | Limpa dados locais sensíveis; preserva o que não é do usuário (catálogos) |
