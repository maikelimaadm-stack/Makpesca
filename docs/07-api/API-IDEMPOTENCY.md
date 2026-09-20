---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0011
---

# Idempotência

## 1. Por que é obrigatória

O cliente principal opera offline, com rede instável. Reenvio é normal, não excepcional.
Sem idempotência, o produto duplica dados do usuário — defeito inaceitável (R-020).

## 2. Onde se aplica

| Operação | Idempotência |
|----------|--------------|
| Criação de ponto, captura, pescaria | **Obrigatória** |
| Atualização sincronizável | **Obrigatória** |
| Exclusão sincronizável | **Obrigatória** |
| Lote de sync | **Obrigatória** (por item) |
| Confirmação de upload de mídia | **Obrigatória** |
| Webhook de billing recebido | **Obrigatória** (por event id) |
| Registro de click de afiliado | **Obrigatória** |
| Publicação de post/comentário | Recomendada |
| Leitura | Naturalmente idempotente |

## 3. Mecanismo

1. O cliente gera uma `idempotencyKey` (UUID) **antes** de tentar enviar.
2. A chave é persistida na outbox junto com a mutação.
3. Toda tentativa da **mesma intenção** usa a mesma chave.
4. O servidor guarda `(chave, escopo, hash do payload, resultado)` por uma janela definida.
5. Repetição com a mesma chave devolve o **mesmo resultado**, sem reexecutar efeitos.

Escopo da chave: usuário + tipo de operação. Chaves de usuários diferentes nunca colidem.

## 4. Casos

| Caso | Resposta |
|------|----------|
| Primeira vez | Executa e guarda o resultado |
| Repetição idêntica | Devolve o resultado guardado (`duplicate`), sem novo efeito |
| Mesma chave, payload diferente | **Erro** — indica bug de cliente; não executa |
| Chave fora da janela de retenção | Trata como nova; a unicidade de domínio (id do cliente) ainda protege |
| Execução em andamento (concorrência) | Segunda chamada aguarda ou recebe "em processamento", nunca duplica |

## 5. Defesa em profundidade

Idempotência por chave **não é a única** proteção. Também:

- identificador de entidade gerado no cliente é chave natural: recriar a mesma entidade é
  um `UPDATE`, não um `INSERT`;
- restrições de unicidade no banco para relações críticas (ex.: uma comissão por conversão
  por parceiro);
- verificação de estado desejado em vez de incremento (entitlements, contadores críticos).

Essas três camadas juntas tornam a duplicação improvável mesmo com falha de uma delas.

## 6. Nunca fazer

| Antipadrão | Por quê |
|------------|---------|
| Gerar a chave no servidor | Não protege o reenvio do cliente |
| Gerar nova chave a cada tentativa | Anula o mecanismo |
| Usar timestamp como chave | Colide e não é estável |
| Incrementar contador em webhook | Duplicação concede benefício duplicado (R-051) |
| Confiar só no `try/catch` do cliente | Falha de rede pode ocorrer após o efeito |

## 7. Janela de retenção

Proposta: reter resultados por período maior que a janela realista de reenvio offline
(sugestão inicial: 30 dias). Valor exato é `NEEDS-DECISION`, dependente do custo de
armazenamento e do comportamento observado.

## 8. Teste obrigatório

Para cada operação idempotente: enviar duas vezes a mesma chave e verificar um único
efeito; enviar a mesma chave com payload diferente e verificar rejeição; simular crash
entre efeito e resposta e verificar que o reenvio não duplica.
