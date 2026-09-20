---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0012
---

# Matriz de Testes de Privacidade

Estes testes protegem o ativo mais valioso do produto. São **bloqueantes**.

## 1. Perfis de observador

Todo endpoint que retorna localização é testado com **todos** estes perfis:

| Perfil | Descrição |
|--------|-----------|
| P1 | Dono do recurso |
| P2 | Usuário com concessão `EXACT` |
| P3 | Usuário com concessão `APPROXIMATE` |
| P4 | Usuário com concessão `REGION` |
| P5 | Usuário com concessão `WATER_BODY_ONLY` |
| P6 | Usuário autenticado sem concessão |
| P7 | Usuário bloqueado pelo dono |
| P8 | Usuário cuja concessão foi revogada |
| P9 | Usuário cuja concessão expirou |
| P10 | Não autenticado |
| P11 | Administrador sem justificativa registrada |
| P12 | Parceiro comercial |

## 2. Casos por recurso

| # | Caso | Esperado |
|---|------|----------|
| PR-01 | Ponto `PRIVATE`, observador P6 | Recurso **não** aparece; 404 se consultado diretamente |
| PR-02 | Ponto `SHARED` com `APPROXIMATE`, observador P3 | Coordenada deslocada + raio declarado |
| PR-03 | Ponto `PUBLIC` com `WATER_BODY_ONLY` | Somente o corpo d'água |
| PR-04 | Captura `PUBLIC` de ponto `PRIVATE` | Captura visível; ponto **não** exposto |
| PR-05 | Observador P8 (revogado) | Sem acesso, imediatamente |
| PR-06 | Observador P7 (bloqueado) | Sem acesso, nem ao conteúdo público do bloqueador |
| PR-07 | Observador P11 | Sem coordenada exata por padrão; acesso gera auditoria |
| PR-08 | Observador P12 | Nenhum dado de localização de usuário |

## 3. Invariância entre caminhos

O mesmo recurso, acessado por caminhos diferentes, precisa dar **a mesma** precisão:

| # | Caso |
|---|------|
| PR-10 | Detalhe do recurso vs listagem |
| PR-11 | Feed vs perfil vs busca |
| PR-12 | Mapa vs sync/pull |
| PR-13 | Ranking vs detalhe da captura |
| PR-14 | Mensagem com referência vs acesso direto |
| PR-15 | Exportação do titular vs API |
| PR-16 | Resposta em cache vs sem cache |

Qualquer divergência é vazamento por caminho alternativo.

## 4. Jitter e inferência

| # | Caso | Esperado |
|---|------|----------|
| PR-20 | Consultar 100 vezes o mesmo recurso `APPROXIMATE` com o mesmo observador | **Sempre o mesmo valor** |
| PR-21 | Dois observadores diferentes, mesmo recurso | Valores diferentes entre si, estáveis cada um |
| PR-22 | Média de N leituras (averaging attack) | Não converge para o valor real |
| PR-23 | Mesmo recurso com precisões distintas em contas distintas | Não permite triangular o real |
| PR-24 | Alterar a precisão declarada e consultar de novo | Novo valor coerente, sem revelar o anterior |

## 5. Canais laterais

| # | Caso | Esperado |
|---|------|----------|
| PR-30 | Buscar coordenada em logs após um fluxo completo | **Nenhuma ocorrência** |
| PR-31 | Inspecionar eventos de analytics | Nenhuma coordenada |
| PR-32 | Inspecionar crash report simulado | Nenhuma coordenada |
| PR-33 | Inspecionar URLs, deep links e payloads de push | Nenhuma coordenada |
| PR-34 | Inspecionar mídia publicada | Sem EXIF de GPS |
| PR-35 | Mensagem de erro em recurso não autorizado | Sem informação geográfica; 404 |
| PR-36 | Cache servindo resposta a outro observador | Nunca ocorre |
| PR-37 | Exportação do titular | Contém as próprias coordenadas; nenhuma de terceiro acima do autorizado |

## 6. Autorização negativa

| # | Caso | Esperado |
|---|------|----------|
| PR-40 | Acessar recurso de outro usuário por id | 404 |
| PR-41 | Alterar recurso de outro usuário | 404/403 conforme a regra |
| PR-42 | Enumerar ids sequenciais | Não revela existência; rate limit |
| PR-43 | Filtrar por proximidade a ponto de terceiro | Rejeitado |
| PR-44 | Ordenar por distância a recurso não autorizado | Rejeitado |

## 7. Ciclo de concessão

| # | Caso | Esperado |
|---|------|----------|
| PR-50 | Conceder → ler → revogar → ler | Acesso cessa na terceira etapa |
| PR-51 | Concessão com prazo → aguardar expiração → ler | Sem acesso |
| PR-52 | Destinatário tenta repassar a concessão | Rejeitado |
| PR-53 | Sair do grupo com concessão derivada | Acesso cessa |
| PR-54 | Dispositivo offline com dado concedido, revogação emitida | Dado removido no próximo sync |

## 8. Automação

Estes testes rodam em CI a cada alteração que toque em endpoints com localização.
**Falha aqui bloqueia o merge** (`PRIVACY-GATE`).
