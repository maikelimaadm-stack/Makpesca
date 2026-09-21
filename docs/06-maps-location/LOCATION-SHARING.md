---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0012
---

# Compartilhamento de Localização

## 1. O que pode ser compartilhado

| Objeto | Compartilhável | Observação |
|--------|----------------|------------|
| Ponto (`Spot`) | Sim | Com precisão escolhida |
| Captura (`Catch`) | Sim | Independente do ponto |
| Ponto de encontro de evento | Sim | Com participantes |
| Localização atual do usuário | **Não no MVP** | Alto risco; exige decisão própria (Q-026) |
| Região/corpo d'água | Sim | Baixo risco |

## 2. Destinatários

| Tipo | Regra |
|------|-------|
| Usuário específico | Concessão direta |
| Grupo | Todos os membros atuais; sair do grupo encerra o acesso |
| Participantes de evento | Enquanto participarem e até o fim do evento + margem |
| Comunidade | Apenas precisões baixas (`REGION`, `WATER_BODY_ONLY`) — nunca `EXACT` |
| Público | Somente com escolha explícita do dono |

## 3. Ciclo de vida da concessão

```
criada → ativa → [expirada por prazo] → [revogada pelo dono] → encerrada
```

| Evento | Efeito |
|--------|--------|
| Revogação | Imediata; leitura seguinte já não recebe |
| Expiração | Automática, sem ação do dono |
| Saída do grupo/evento | Encerra o acesso derivado |
| Bloqueio entre as partes | Encerra todas as concessões entre elas |
| Exclusão do recurso | Encerra as concessões |
| Exclusão da conta do dono | Encerra as concessões |

## 4. Efeito da revogação em dados já baixados

Realidade técnica: o que já foi entregue ao dispositivo de alguém não pode ser "apagado"
com garantia absoluta. Por isso:

1. a revogação bloqueia toda leitura futura, incluindo sync;
2. o pull entrega uma instrução de remoção para os dispositivos que tinham acesso;
3. o app cliente **deve** remover o dado local ao receber a revogação;
4. a interface informa o dono, com honestidade, que quem já viu pode ter anotado;
5. por isso, o produto orienta compartilhar com a **menor precisão suficiente**.

Prometer ao usuário que a revogação apaga a memória de terceiros seria mentira.

## 5. Interface

Ao compartilhar, o usuário decide explicitamente:

1. **com quem** (pessoa, grupo, evento);
2. **o quê** (o ponto, a captura, ou só a região);
3. **com qual precisão** (as cinco opções, explicadas em linguagem simples);
4. **por quanto tempo** (indeterminado ou com prazo).

Depois, ele vê uma lista de "quem tem acesso ao quê" e pode revogar com um toque.

## 6. Proibições

| Proibição | Motivo |
|-----------|--------|
| Repasse de concessão (quem recebe compartilhar adiante) | O dono perderia o controle |
| Concessão implícita por participar de comunidade | Consentimento precisa ser ativo |
| Aumentar precisão sem ação do dono | Nunca |
| Compartilhar localização de terceiro | Só o dono compartilha o que é dele |
| Link público com coordenada | Link vaza por encaminhamento, histórico e índice de busca |

## 7. Auditoria

Registra-se: quem concedeu, para quem, qual recurso, qual precisão, quando, prazo e quando
foi revogada. O dono pode consultar esse histórico dos seus próprios recursos.
