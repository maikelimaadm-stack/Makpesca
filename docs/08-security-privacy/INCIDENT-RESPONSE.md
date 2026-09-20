---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: —
---

# Resposta a Incidentes

## 1. Severidades

| Nível | Definição | Exemplos |
|-------|-----------|----------|
| **SEV-1** | Vazamento de dado C4 ou indisponibilidade total | Coordenadas privadas expostas; secrets vazados; API fora |
| **SEV-2** | Vazamento de dado C2/C3, fraude em escala, perda de dados | Dados pessoais expostos; duplicação massiva; comissões indevidas |
| **SEV-3** | Degradação relevante sem vazamento | Sync lento, uploads falhando, região indisponível |
| **SEV-4** | Defeito contido, sem impacto sistêmico | Bug em recurso isolado |

**Vazamento de coordenada de ponto privado é sempre SEV-1**, mesmo que afete um único usuário.

## 2. Fluxo

```
detectar → classificar → conter → erradicar → recuperar → comunicar → aprender
```

| Etapa | O que fazer |
|-------|-------------|
| **Detectar** | Alerta automático, relato de usuário, relato externo de vulnerabilidade |
| **Classificar** | Definir severidade em minutos; na dúvida, classificar para cima |
| **Conter** | Desligar o caminho afetado (feature flag/kill switch), revogar credenciais, bloquear origem |
| **Erradicar** | Corrigir a causa, não só o sintoma |
| **Recuperar** | Restaurar serviço, validar integridade, reprocessar o que falhou |
| **Comunicar** | Usuários afetados, autoridade quando aplicável, parceiros quando aplicável |
| **Aprender** | Post-mortem sem culpabilização, com ações datadas |

## 3. Papéis

Nesta fase não há pessoas designadas (Q-001). Antes do lançamento, definir:
comandante do incidente, pessoa técnica responsável, pessoa de comunicação, encarregado
de dados (LGPD). Sem nomes, o processo não funciona.

## 4. Contenção por tipo

| Incidente | Contenção imediata |
|-----------|--------------------|
| Vazamento de coordenadas por endpoint | Desligar o endpoint via flag; revogar cache; avaliar alcance por logs de acesso |
| Secret vazado | Rotacionar e revogar; auditar uso |
| Conta administrativa comprometida | Revogar sessões, trocar credenciais, auditar ações |
| Fraude de afiliado em escala | Suspender payouts, congelar conversões suspeitas |
| Billing inconsistente | Congelar concessão automática; conciliar manualmente; nunca revogar acesso pago |
| Perda de dados | Parar escrita afetada; avaliar restore; preservar evidência |
| Abuso/assédio coordenado | Sanções, restrição de recurso, suporte às vítimas |

## 5. Preservação de evidência

Antes de corrigir, preservar: logs relevantes, identificadores de requisição, versão
implantada, configuração vigente. Correção que apaga a evidência impede entender a causa.

## 6. Comunicação

| Público | Quando | Conteúdo |
|---------|--------|----------|
| Usuários afetados | O quanto antes, com informação confirmada | O que aconteceu, o que foi exposto, o que fizemos, o que a pessoa pode fazer |
| Todos os usuários | Se houver impacto amplo | Status e prazo |
| Autoridade (ANPD) | Conforme critério legal | Pendente jurídico |
| Parceiros | Se dados comerciais afetados | Escopo e medidas |

Comunicação nunca minimiza o ocorrido nem promete o que não foi verificado.

## 7. Post-mortem

Obrigatório para SEV-1 e SEV-2, em até 5 dias úteis. Conteúdo: linha do tempo, impacto
medido, causa raiz, o que detectou (ou por que não detectou), ações corretivas com
responsável e prazo, e o controle que será adicionado para impedir a repetição.

## 8. Exercício

Antes do lançamento: simular ao menos um SEV-1 de vazamento de coordenada e um restore
de backup, medindo tempo real de resposta.
