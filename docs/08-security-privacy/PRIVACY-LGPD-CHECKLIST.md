---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0012
---

# Checklist Técnico de LGPD

> Este é um checklist **técnico**, não parecer jurídico. Revisão jurídica é obrigatória
> antes do lançamento (Q-016, Q-017).

## 1. Localização

| # | Item | Estado |
|---|------|--------|
| 1.1 | Localização tratada como dado de sensibilidade elevada (C4) | Definido |
| 1.2 | Coleta apenas quando necessária para a finalidade | Definido |
| 1.3 | Usuário informado antes de conceder permissão | Definido |
| 1.4 | Sem coleta em background no MVP | Definido |
| 1.5 | Compartilhamento sempre por ato explícito, reversível | Definido |
| 1.6 | Precisão mínima necessária por padrão | Definido |
| 1.7 | Nenhuma coordenada exata a terceiros sem autorização | Definido |
| 1.8 | Terceiros (mapas, clima) recebem apenas o necessário e aproximado | Definido |

## 2. Finalidade e base legal

| # | Item | Estado |
|---|------|--------|
| 2.1 | Cada tratamento tem finalidade declarada | A completar por recurso |
| 2.2 | Base legal definida por finalidade (execução de contrato, consentimento, legítimo interesse) | **Pendente jurídico** |
| 2.3 | Consentimento separado para finalidades distintas (produto ≠ marketing ≠ insights) | Definido |
| 2.4 | Nenhum uso secundário sem nova base legal | Definido |

## 3. Consentimento

| # | Item | Estado |
|---|------|--------|
| 3.1 | Consentimento livre, informado e específico | Definido |
| 3.2 | Registro de quando e para quê foi concedido | Definido |
| 3.3 | Revogação tão fácil quanto a concessão | Definido |
| 3.4 | Revogação com efeito sobre tratamentos futuros e, quando possível, passados | Definido |
| 3.5 | Consentimento para insights agregados é opt-in explícito | Definido |

## 4. Transparência

| # | Item | Estado |
|---|------|--------|
| 4.1 | Política de privacidade em linguagem simples | Pendente |
| 4.2 | Lista de terceiros e finalidades | Pendente |
| 4.3 | Explicação de como funciona a precisão de localização | Pendente |
| 4.4 | Aviso de que dados já compartilhados podem ter sido anotados por terceiros | Definido |

## 5. Direitos dos titulares

| Direito | Como é atendido | Estado |
|---------|-----------------|--------|
| Acesso | Exportação de dados do titular | Definido |
| Correção | Edição de perfil e registros | Definido |
| Exclusão | Fluxo de exclusão de conta com propagação | Definido |
| Portabilidade | Export em formato legível por máquina | Definido |
| Informação sobre compartilhamento | Lista de terceiros + histórico de concessões | Definido |
| Revogação de consentimento | Nas configurações | Definido |
| Oposição | Canal de contato | Pendente |

Prazo de atendimento e canal oficial: **pendente jurídico**.

## 6. Retenção

| # | Item | Estado |
|---|------|--------|
| 6.1 | Prazo definido por categoria de dado | Parcial (`../04-data/DATA-LIFECYCLE.md`) |
| 6.2 | Purga automática ao fim do prazo | A implementar |
| 6.3 | Backups com prazo de expiração informado ao titular | Definido |
| 6.4 | Logs com retenção curta | Definido |

## 7. Dados derivados

| # | Item | Estado |
|---|------|--------|
| 7.1 | Insights só sobre dados com consentimento | Definido |
| 7.2 | Coorte mínima antes de publicar | Definido (valor em Q-023) |
| 7.3 | Verificação de reidentificação | Definido |
| 7.4 | Exclusão do dado de origem reflete nos derivados | Definido |

## 8. Analytics e terceiros

| # | Item | Estado |
|---|------|--------|
| 8.1 | Nenhum identificador direto em analytics | Definido |
| 8.2 | Nenhuma coordenada em analytics | Definido |
| 8.3 | Contrato/termos com cada operador | Pendente |
| 8.4 | Transferência internacional avaliada | **Pendente jurídico** |

## 9. Menores

| # | Item | Estado |
|---|------|--------|
| 9.1 | Idade mínima definida | **Pendente (Q-017)** |
| 9.2 | Fluxo de consentimento parental, se aplicável | Pendente |
| 9.3 | Restrições de recursos sociais para menores | Pendente |

## 10. Incidentes

| # | Item | Estado |
|---|------|--------|
| 10.1 | Processo de detecção e resposta | `INCIDENT-RESPONSE.md` |
| 10.2 | Critério de notificação à autoridade e aos titulares | Pendente jurídico |
| 10.3 | Registro de incidentes | Definido |

## 11. Comércio, afiliados e publicidade

| # | Item | Estado |
|---|------|--------|
| 11.1 | Parceiro não recebe dado pessoal sem base legal | Definido |
| 11.2 | Rastreamento de clique informado ao usuário | Definido |
| 11.3 | Conteúdo patrocinado identificado | Definido |
| 11.4 | Nenhuma segmentação por localização exata | Definido |

## 12. Governança

| # | Item | Estado |
|---|------|--------|
| 12.1 | Encarregado (DPO) designado | **Pendente** |
| 12.2 | Registro de operações de tratamento | Pendente |
| 12.3 | Avaliação de impacto para tratamento de localização | **Recomendada e pendente** |
| 12.4 | Revisão periódica | Pendente |
