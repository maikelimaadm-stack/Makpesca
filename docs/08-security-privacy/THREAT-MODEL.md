---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0008, ADR-0012, ADR-0014
---

# Modelo de Ameaças

Modelo geral do sistema. Para localização, ver `GEO-PRIVACY-THREAT-MODEL.md`.

## 1. Ativos

| # | Ativo | Valor |
|---|-------|-------|
| A1 | Coordenadas exatas de pontos privados | **Máximo** — vazamento é irreversível |
| A2 | Credenciais e sessões | Máximo |
| A3 | Conteúdo privado (capturas, mensagens, mídia) | Alto |
| A4 | Dados pessoais (e-mail, telefone, perfil) | Alto |
| A5 | Base de usuários e conteúdo público agregado | Médio (scraping) |
| A6 | Dados comerciais (conversões, comissões) | Médio-alto |
| A7 | Integridade de rankings e desafios | Médio |
| A8 | Disponibilidade da API | Médio-alto |
| A9 | Secrets de infraestrutura | Máximo |

## 2. Adversários

| # | Adversário | Motivação | Capacidade |
|---|-----------|-----------|------------|
| T1 | Curioso / pescador rival | Descobrir pontos alheios | Baixa; usa o app normalmente |
| T2 | Coletor de dados | Montar base de pontos para revender | Média; automação, várias contas |
| T3 | Assediador | Perseguir uma pessoa específica | Baixa-média; usa sinais do produto |
| T4 | Fraudador comercial | Comissão indevida | Média; automação, contas falsas |
| T5 | Fraudador de ranking | Prestígio ou prêmio | Baixa-média; localização falsa, fotos recicladas |
| T6 | Atacante oportunista | Qualquer ganho | Média; ferramentas automáticas |
| T7 | Insider | Acesso indevido a dados | Alta; acesso legítimo |
| T8 | Parceiro malicioso | Dados de usuários | Média; acesso legítimo restrito |
| T9 | Comprometimento de cadeia de suprimentos | Variada | Alta |

## 3. Ameaças por categoria (STRIDE resumido)

### Spoofing (falsificação de identidade)
| Ameaça | Mitigação |
|--------|-----------|
| Roubo de token | Vida curta, rotação, detecção de reuso, revogação |
| Conta falsa em massa | Verificação, limites, sinais de abuso |
| Falsificação de webhook | Verificação de assinatura |
| GPS spoofing | Sinais de confiabilidade + inelegibilidade em ranking |

### Tampering (adulteração)
| Ameaça | Mitigação |
|--------|-----------|
| Alteração de payload em trânsito | TLS |
| Manipulação de dados de conversão | Conciliação + antifraude |
| Alteração de mídia | Hash de conteúdo |
| Manipulação de versão no sync | Versão é do servidor |

### Repudiation (repúdio)
| Ameaça | Mitigação |
|--------|-----------|
| Negar ação administrativa | Auditoria imutável |
| Negar concessão de localização | Registro de concessão/revogação |
| Contestar comissão | Log de click e conciliação |

### Information disclosure (vazamento)
| Ameaça | Mitigação |
|--------|-----------|
| **Vazamento de coordenada privada** | Geo Privacy Service + testes de contrato |
| Vazamento por log/analytics/crash | Redação obrigatória |
| Vazamento por cache | Perfil do observador na chave |
| Vazamento por EXIF | Remoção no pipeline |
| Enumeração de recursos | 404 em vez de 403 |
| Scraping | Rate limit e limites de listagem |

### Denial of service
| Ameaça | Mitigação |
|--------|-----------|
| Flood de requisições | Rate limit, limites de área |
| Upload massivo | Limites por usuário e tamanho |
| Consulta geográfica cara | Área máxima e paginação |
| Fila de jobs entupida | Prioridade e limites |

### Elevation of privilege
| Ameaça | Mitigação |
|--------|-----------|
| IDOR/BOLA | Autorização por objeto |
| Escalada para admin | Escopos separados, 2FA, auditoria |
| Parceiro acessando outro parceiro | Isolamento verificado |
| Abuso de rota de sistema | Autenticação de sistema, origem restrita |

## 4. Superfícies de ataque

| Superfície | Riscos principais |
|------------|-------------------|
| API pública | BOLA, enumeração, abuso, injeção |
| App móvel | Extração de segredo, dados locais, engenharia reversa |
| Web | XSS, CSRF, clickjacking |
| Admin | Abuso de privilégio, conta comprometida |
| Portal de parceiros | Vazamento entre parceiros |
| Webhooks | Falsificação, replay, duplicação |
| Object storage | URL adivinhável, objeto público por engano |
| Dependências | Supply chain |
| Operação | Acesso indevido, erro humano |

## 5. Cenários prioritários

| # | Cenário | Impacto | Prioridade |
|---|---------|---------|-----------|
| C1 | Atacante obtém coordenadas de pontos privados por endpoint mal autorizado | Catastrófico | **1** |
| C2 | Coordenadas vazam por log/crash report | Catastrófico | **1** |
| C3 | Token roubado dá acesso persistente | Alto | 2 |
| C4 | Coletor automatiza download do acervo público e o revende | Alto | 2 |
| C5 | Fraude de comissão em escala | Médio-alto | 3 |
| C6 | Assédio usando sinais de localização aproximada | Alto | 2 |
| C7 | Insider consulta pontos privados sem motivo | Alto | 2 |
| C8 | Webhook duplicado concede PRO indevido | Médio | 3 |

## 6. Revisão

Este modelo é revisado a cada onda congelada e sempre que um novo recurso introduzir
superfície nova. Recurso novo sem análise de ameaça falha o `SECURITY-GATE`.
