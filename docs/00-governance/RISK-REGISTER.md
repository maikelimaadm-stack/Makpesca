---
Status: REVIEW
Version: 0.2.0
Last Updated: 2026-09-21
Owners: Maike Lima (autoridade humana final)
Related ADRs: ADR-0009, ADR-0010, ADR-0011, ADR-0012, ADR-0013, ADR-0014, ADR-0020
Wave: cross-cutting (controle vivo; registrada em F0)
Lifecycle: LIVING
---

# Registro de Riscos

Escala: Likelihood `BAIXA|MÉDIA|ALTA`; Impact `BAIXO|MÉDIO|ALTO|CRÍTICO`;
Severity derivada; Status `ABERTO|MITIGANDO|ACEITO|FECHADO`.
Owner ainda não atribuído nominalmente — ver `OPEN-QUESTIONS.md` Q-001.

## 1. Privacidade e localização

| ID | Risco | Likelihood | Impact | Severity | Mitigação | Owner | Status |
|----|-------|-----------|--------|----------|-----------|-------|--------|
| R-001 | Vazamento de coordenada de ponto privado via resposta de API | MÉDIA | CRÍTICO | CRÍTICA | Degradação server-side antes da serialização; testes de contrato por perfil de observador | (a definir) | ABERTO |
| R-002 | Vazamento de GPS via EXIF em foto publicada | ALTA | ALTO | ALTA | Remoção de EXIF no pipeline de mídia antes de publicar; teste automatizado | (a definir) | ABERTO |
| R-003 | Reidentificação por ataque de média sobre jitter repetido | MÉDIA | ALTO | ALTA | Jitter estável por (objeto, observador); nunca re-sortear | (a definir) | ABERTO |
| R-004 | Triangulação por cruzamento de metadados (corpo d'água + horário + espécie) | MÉDIA | ALTO | ALTA | Coorte mínima e agregação temporal/espacial antes de publicar insight | (a definir) | ABERTO |
| R-005 | Coordenada exata em log, analytics ou crash report | ALTA | CRÍTICO | CRÍTICA | Proibição explícita + redator de campos sensíveis + varredura de logs | (a definir) | ABERTO |
| R-006 | Coordenada em URL, deep link ou payload de push | MÉDIA | ALTO | ALTA | Nunca em query string ou push; somente corpo autenticado | (a definir) | ABERTO |
| R-007 | Export/backup revelando ponto privado a terceiro | BAIXA | CRÍTICO | ALTA | Export só do titular; backup cifrado; acesso administrativo auditado | (a definir) | ABERTO |

## 2. Segurança

| ID | Risco | Likelihood | Impact | Severity | Mitigação | Owner | Status |
|----|-------|-----------|--------|----------|-----------|-------|--------|
| R-010 | IDOR/BOLA em recursos de ponto, captura, mensagem | ALTA | CRÍTICO | CRÍTICA | Autorização por objeto em todo handler; testes negativos obrigatórios | (a definir) | ABERTO |
| R-011 | Auth bypass / token mal validado | MÉDIA | CRÍTICO | CRÍTICA | Validação central, revogação, expiração curta + refresh | (a definir) | ABERTO |
| R-012 | Conta comprometida | MÉDIA | ALTO | ALTA | Sessões listáveis/revogáveis, alerta de novo dispositivo | (a definir) | ABERTO |
| R-013 | Upload abusivo (malware, conteúdo ilegal, arquivo gigante) | MÉDIA | ALTO | ALTA | Upload autorizado pela API, limites de tamanho/tipo, processamento isolado | (a definir) | ABERTO |
| R-014 | Scraping do acervo público e de lojas | ALTA | MÉDIO | MÉDIA | Rate limiting, paginação limitada, detecção de padrão | (a definir) | ABERTO |
| R-015 | Abuso de painel admin | BAIXA | CRÍTICO | ALTA | Menor privilégio, auditoria de toda ação, 2FA | (a definir) | ABERTO |
| R-016 | Supply chain (dependência comprometida) | MÉDIA | ALTO | ALTA | Lockfile, auditoria de dependências, mínimo de dependências | (a definir) | ABERTO |
| R-017 | Vazamento de secret em repositório ou log | MÉDIA | CRÍTICO | CRÍTICA | Secrets fora do código, varredura de segredo, rotação | (a definir) | ABERTO |

## 3. Offline e sincronização

| ID | Risco | Likelihood | Impact | Severity | Mitigação | Owner | Status |
|----|-------|-----------|--------|----------|-----------|-------|--------|
| R-020 | Duplicação de registro ao sincronizar | ALTA | ALTO | ALTA | Id gerado no cliente + idempotency key + unicidade no servidor | (a definir) | ABERTO |
| R-021 | Perda de dado criado offline | MÉDIA | CRÍTICO | CRÍTICA | Escrita local durável antes de responder à UI; outbox persistente | (a definir) | ABERTO |
| R-022 | Conflito entre dispositivos do mesmo usuário | MÉDIA | MÉDIO | MÉDIA | Versão de entidade + matriz de conflito por campo | (a definir) | ABERTO |
| R-023 | Delete que "ressuscita" por sync antigo | MÉDIA | MÉDIO | MÉDIA | Tombstones com retenção maior que a janela de sync | (a definir) | ABERTO |
| R-024 | Mídia órfã (registro sem arquivo ou arquivo sem registro) | ALTA | MÉDIO | MÉDIA | Hash, confirmação em duas fases, job de limpeza | (a definir) | ABERTO |
| R-025 | Clock skew corrompendo ordenação | MÉDIA | MÉDIO | MÉDIA | Tempo do servidor como autoridade; tempo do dispositivo guardado à parte | (a definir) | ABERTO |
| R-026 | Falha de migração do SQLite local com perda de dado | BAIXA | CRÍTICO | ALTA | Migrações versionadas, testes de upgrade, backup local antes de migrar | (a definir) | ABERTO |

## 4. Mapas e custo

| ID | Risco | Likelihood | Impact | Severity | Mitigação | Owner | Status |
|----|-------|-----------|--------|----------|-----------|-------|--------|
| R-030 | Violação de licença ao cachear/baixar tiles de provider proprietário | MÉDIA | CRÍTICO | CRÍTICA | Offline nunca assume tiles do provider online; ADR-0010 separado e bloqueante | (a definir) | ABERTO |
| R-031 | Custo de mapa cresce além do sustentável | ALTA | ALTO | ALTA | Teto de uso, cache de sessão permitido por licença, monitoramento de custo | (a definir) | ABERTO |
| R-032 | Custo de mídia (storage + egress) | ALTA | ALTO | ALTA | Compressão, derivativos, política de retenção, CDN com custo previsível | (a definir) | ABERTO |
| R-033 | Lock-in de provider de mapa | MÉDIA | ALTO | ALTA | Camada de abstração de mapa; dados geo próprios no PostGIS | (a definir) | ABERTO |
| R-034 | Limites de plataforma de hospedagem (timeout, payload, execução) | MÉDIA | ALTO | ALTA | API portável, jobs fora do request, ADR-0005 com caminho de saída | (a definir) | ABERTO |
| R-035 | PostGIS indisponível ou limitado no provider gerenciado | BAIXA | ALTO | MÉDIA | PostGIS é requisito de seleção de provider | (a definir) | ABERTO |

## 5. Escala e produto

| ID | Risco | Likelihood | Impact | Severity | Mitigação | Owner | Status |
|----|-------|-----------|--------|----------|-----------|-------|--------|
| R-040 | Feed não escala (fan-out) | MÉDIA | ALTO | ALTA | Começar com fan-out on read + limites; medir antes de otimizar | (a definir) | ABERTO |
| R-041 | Spam e conteúdo comercial não autorizado | ALTA | MÉDIO | MÉDIA | Rate limit, reputação, moderação, denúncia | (a definir) | ABERTO |
| R-042 | Assédio entre usuários | MÉDIA | ALTO | ALTA | Bloqueio, denúncia, restrição de mensagem para não seguidos | (a definir) | ABERTO |
| R-043 | Abuso de chat (spam, golpe, conteúdo ilegal) | MÉDIA | ALTO | ALTA | Limite de convite, denúncia no chat, retenção para apuração | (a definir) | ABERTO |
| R-044 | Localização falsificada (GPS spoofing) | ALTA | MÉDIO | MÉDIA | Marcar origem da localização; sinais antifraude; ranking com elegibilidade | (a definir) | ABERTO |
| R-045 | Fraude de ranking (captura inventada, foto reciclada) | ALTA | MÉDIO | MÉDIA | Hash de mídia, heurística, revisão manual de topo de ranking | (a definir) | ABERTO |
| R-046 | Sobrecarga de moderação | MÉDIA | ALTO | ALTA | Fila priorizada, triagem automática, limites de crescimento por região | (a definir) | ABERTO |
| R-047 | Consumo de bateria pelo uso de GPS/mapa | ALTA | MÉDIO | MÉDIA | Amostragem adaptativa, sem background location no MVP | (a definir) | ABERTO |
| R-048 | Restrições de background location nas lojas | MÉDIA | MÉDIO | MÉDIA | Evitar background location até haver caso de uso aprovado | (a definir) | ABERTO |

## 6. Comércio, afiliados e billing

| ID | Risco | Likelihood | Impact | Severity | Mitigação | Owner | Status |
|----|-------|-----------|--------|----------|-----------|-------|--------|
| R-050 | Inconsistência de billing (pago sem acesso / acesso sem pagar) | MÉDIA | ALTO | ALTA | Entitlement Service como fonte única; reconciliação periódica | (a definir) | ABERTO |
| R-051 | Webhook duplicado concedendo entitlement duplicado | ALTA | ALTO | ALTA | Idempotência por event id + estado desejado, não incremental | (a definir) | ABERTO |
| R-052 | Fraude de afiliado (auto-clique, click stuffing) | ALTA | ALTO | ALTA | Sinais de fraude, deduplicação, janela de atribuição, revisão antes de payout | (a definir) | ABERTO |
| R-053 | Fraude de atribuição entre parceiros | MÉDIA | MÉDIO | MÉDIA | Regra de atribuição explícita e auditável; log imutável de clicks | (a definir) | ABERTO |
| R-054 | Comissão duplicada | MÉDIA | ALTO | ALTA | Unicidade por (conversão externa, parceiro); conciliação | (a definir) | ABERTO |
| R-055 | Parceiro malicioso (dados falsos, uso indevido de dados de usuário) | MÉDIA | ALTO | ALTA | Verificação de parceiro, contrato, acesso mínimo, auditoria |(a definir) | ABERTO |
| R-056 | Oferta enganosa ao usuário | MÉDIA | ALTO | ALTA | Regras de oferta, validade obrigatória, denúncia, suspensão | (a definir) | ABERTO |

## 7. Operação

| ID | Risco | Likelihood | Impact | Severity | Mitigação | Owner | Status |
|----|-------|-----------|--------|----------|-----------|-------|--------|
| R-060 | Backup inexistente ou não testado | MÉDIA | CRÍTICO | CRÍTICA | Backup + restore test periódico com evidência | (a definir) | ABERTO |
| R-061 | Logs com dado sensível | ALTA | ALTO | ALTA | Política de log, redator, revisão de amostra | (a definir) | ABERTO |
| R-062 | Falha de migração em produção | MÉDIA | CRÍTICO | CRÍTICA | Migração reversível, staging idêntico, janela e runbook | (a definir) | ABERTO |
| R-063 | Lock-in de infraestrutura inicial (Supabase/Vercel) | ALTA | ALTO | ALTA | Boundaries + PORTABILITY-STRATEGY + custo de saída documentado | (a definir) | ABERTO |

## 8. Riscos de processo

| ID | Risco | Likelihood | Impact | Severity | Mitigação | Owner | Status |
|----|-------|-----------|--------|----------|-----------|-------|--------|
| R-070 | Congelar documento com decisão crítica ainda aberta | MÉDIA | ALTO | ALTA | `FREEZE = BLOCKED` na presença de item `BLOCKING` | (a definir) | ABERTO |
| R-071 | Implementação começar antes da liberação do gate | MÉDIA | ALTO | ALTA | `IMPLEMENTATION-READY-GATE` explícito e verificável | (a definir) | ABERTO |
| R-072 | Documentação divergir da implementação futura | ALTA | MÉDIO | MÉDIA | Gate de consistência por slice; docs atualizados no mesmo PR | (a definir) | ABERTO |
