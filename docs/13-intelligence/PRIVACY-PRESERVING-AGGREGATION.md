---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0012
---

# Agregação com Preservação de Privacidade

## 1. Problema

Agregar dados de localização parece seguro e não é. Um "insight regional" pode revelar o
ponto de uma pessoa quando poucos contribuem. O risco é de **reidentificação por dedução**,
não de vazamento direto.

## 2. Pipeline obrigatório

| Etapa | Controle | Falha ⇒ |
|-------|----------|---------|
| 1. Filtro de consentimento | Só dados com opt-in | Excluir o dado |
| 2. Filtro de elegibilidade | Só público, moderado, sem fraude | Excluir o dado |
| 3. Generalização espacial | Célula/região com tamanho mínimo | Aumentar a célula |
| 4. Generalização temporal | Janela mínima | Aumentar a janela |
| 5. Coorte mínima | ≥ k usuários distintos e ≥ n registros | **Suprimir** |
| 6. Supressão de outliers | Registro único que domina a célula | Suprimir |
| 7. Verificação de reidentificação | Simulação de atacante | Suprimir ou generalizar mais |
| 8. Publicação | Com metadados de base e limitações | — |

## 3. Parâmetros (a definir — Q-023)

| Parâmetro | Proposta inicial | Estado |
|-----------|------------------|--------|
| `k` (usuários distintos por célula) | ≥ 5 | NEEDS-DECISION |
| `n` (registros por célula) | ≥ 20 | NEEDS-DECISION |
| Tamanho mínimo de célula | A definir por contexto | NEEDS-DECISION |
| Janela temporal mínima | Faixa de horário + semana | NEEDS-DECISION |
| Participação máxima de um usuário em uma célula | ≤ 30% dos registros | NEEDS-DECISION |

Esses valores precisam ser validados com dados reais antes do lançamento do recurso.

## 4. Ataques a considerar

| Ataque | Defesa |
|--------|--------|
| **Diferencial**: comparar o insight antes e depois de um registro novo | Não recalcular em tempo real; publicar em lotes com atraso |
| **Interseção**: cruzar vários insights para isolar | Consistência de células; limitar granularidade combinada |
| **Singling out**: célula com um contribuinte dominante | Limite de participação por usuário |
| **Conhecimento externo**: atacante sabe que fulano pesca naquela represa | Coorte mínima + generalização |
| **Séries temporais**: acompanhar a célula ao longo do tempo | Janelas amplas, sem publicar variação fina |

## 5. O que nunca é publicado

- Mapa de calor de alta resolução.
- Contagem de capturas em célula pequena.
- "Melhor horário" para uma célula com poucos contribuintes.
- Qualquer estatística sobre pontos privados.
- Ranking de locais por produtividade em granularidade fina.

O último item merece destaque: seria um recurso atraente e é exatamente o que transformaria
o produto em uma máquina de expor pontos.

## 6. Direito de saída

O usuário pode desativar a participação nos insights a qualquer momento. Efeito: os dados
dele saem do próximo recálculo. Insight já publicado é recalculado no ciclo seguinte.

## 7. Auditoria

Cada insight publicado registra: parâmetros usados, tamanho da coorte, período, versão do
pipeline. Isso permite reconstituir e revisar decisões — e provar conformidade.

## 8. Revisão

Alterar qualquer parâmetro deste pipeline exige revisão de privacidade (`PRIVACY-GATE`) e
registro em `../00-governance/DECISION-REGISTRY.md`.
