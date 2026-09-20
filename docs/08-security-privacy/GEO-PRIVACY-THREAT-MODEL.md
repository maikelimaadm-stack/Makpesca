---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0012
---

# Modelo de Ameaças de Geo-Privacidade

O ativo mais valioso do produto é a **coordenada exata de um ponto privado**.
Vazamento é irreversível: não existe "desfazer" para uma coordenada divulgada.

Regra de negócio correspondente: `../06-maps-location/GEO-PRIVACY.md`.

## 1. Vetores de vazamento

### V1 — API
| Ameaça | Mitigação |
|--------|-----------|
| Endpoint que serializa a entidade crua | DTO explícito + Geo Privacy Service único |
| Endpoint novo esquece a degradação | Testes de contrato por perfil de observador em **todo** endpoint com `Geo = sim` |
| Filtro que revela por eliminação | Filtros aplicados após a degradação; nunca retornar "existe mas não mostro" quando isso é sensível |
| Ordenação por distância a um ponto privado | Proibido ordenar por distância a recurso não autorizado |
| Campo de erro revelando proximidade | Erros sem dado geográfico |
| Resposta 403 revelando existência | Usar 404 |

### V2 — Logs
| Ameaça | Mitigação |
|--------|-----------|
| Corpo de requisição logado | Rotas sensíveis não logam corpo |
| Coordenada em mensagem de erro | Redação por nome de campo + revisão |
| Log de consulta SQL com parâmetros | Proibido em produção |
| Log de terceiros (provider) | Verificar o que o SDK registra |

### V3 — Analytics
| Ameaça | Mitigação |
|--------|-----------|
| Evento com lat/lng | Proibição explícita + revisão de eventos |
| Propriedade de usuário com localização | Só região com coorte mínima |
| Ferramenta de terceiro capturando payload | Nenhuma ferramenta que capture respostas da API |

### V4 — Crash reports
| Ameaça | Mitigação |
|--------|-----------|
| Estado da tela com coordenadas no relatório | Filtro no SDK de crash; nunca anexar estado bruto |
| Breadcrumb com navegação e parâmetros | Sanitizar parâmetros |

### V5 — URL, deep link, push
| Ameaça | Mitigação |
|--------|-----------|
| Coordenada em query string | **Proibido** — fica em histórico, referrer, proxy, log |
| Deep link com coordenada | Usar identificador opaco; resolver no servidor com autorização |
| Push com coordenada no payload | Payload mínimo; conteúdo sensível só dentro do app autenticado |

### V6 — Cache
| Ameaça | Mitigação |
|--------|-----------|
| Cache compartilhado entre observadores | Perfil de autorização na chave (INV-G07) |
| CDN cacheando resposta autenticada | Nenhuma resposta autenticada em CDN pública |
| Cache local com precisão acima da autorizada | Cliente só recebe o já degradado |

### V7 — Exportação e backup
| Ameaça | Mitigação |
|--------|-----------|
| Export do titular incluindo dados de terceiros | Export só do que é do titular |
| Backup acessível a quem não deveria | Cifragem + acesso auditado |
| Dump para ambiente de teste | Anonimização obrigatória |

### V8 — Administração
| Ameaça | Mitigação |
|--------|-----------|
| Admin curioso consultando pontos | Motivo registrado + auditoria + acesso raro |
| Tela administrativa exibindo mapa completo | Exibir degradado por padrão; acesso exato sob justificativa |
| Consulta direta ao banco | Acesso ao banco de produção restrito e auditado |

### V9 — EXIF e mídia
| Ameaça | Mitigação |
|--------|-----------|
| Foto publicada com GPS embutido | Remoção no pipeline (INV-G08) + teste automatizado |
| Miniatura preservando metadados | Derivativos gerados sem metadados |
| Download do original por terceiro | Original privado não é servido a terceiros |

### V10 — Ataques de inferência

Estes não exploram um bug: exploram a matemática da degradação.

| Ataque | Descrição | Mitigação |
|--------|-----------|-----------|
| **Averaging attack** | Coletar N leituras aproximadas do mesmo ponto e tirar a média, convergindo para o real | Jitter **determinístico** por (recurso, observador); nunca re-sortear (INV-G06) |
| **Repeated jitter inference** | Comparar leituras em contas diferentes para triangular | Jitter também depende do observador; limitar criação de contas; detectar padrão de coleta |
| **Triangulação por metadados** | Cruzar corpo d'água + espécie + horário + condições para reduzir o espaço possível | Reduzir granularidade temporal em conteúdo público; não publicar combinação que isole |
| **Correlação com capturas públicas** | Usuário publica várias capturas com `REGION`; a interseção revela o ponto | Alertar o usuário sobre acumulação; considerar limite de publicações por região/período |
| **Diferença entre precisões** | Obter o mesmo recurso por dois caminhos com precisões distintas | Uma única fonte de degradação; consistência entre endpoints |
| **Coorte pequena em insight** | Insight regional revela o único pescador daquela região | Coorte mínima + verificação de reidentificação |
| **Rastro temporal** | Sequência de capturas revela trajeto | Não publicar trajeto; capturas publicadas não expõem ordem exata |

## 2. Requisitos derivados

| ID | Requisito |
|----|-----------|
| GP-R1 | Um único componente decide e aplica precisão |
| GP-R2 | Jitter determinístico por (recurso, observador), com semente secreta do servidor |
| GP-R3 | Todo endpoint com localização tem teste por perfil de observador |
| GP-R4 | Nenhum campo geográfico em log, analytics, crash, URL ou push |
| GP-R5 | Cache de localização inclui o perfil na chave |
| GP-R6 | EXIF removido antes de publicar |
| GP-R7 | Acesso administrativo a coordenada exata é auditado e justificado |
| GP-R8 | Insight passa por coorte mínima e verificação de reidentificação |
| GP-R9 | Revogação tem efeito imediato, incluindo instrução de remoção aos dispositivos |
| GP-R10 | A interface nunca apresenta dado aproximado como exato |

## 3. Testes obrigatórios

Ver `../15-quality/PRIVACY-TEST-MATRIX.md`. Nenhum slice que toque em localização passa
sem esses testes.

## 4. Resposta a vazamento

Vazamento de coordenada é incidente de severidade máxima. Ver `INCIDENT-RESPONSE.md`:
contenção imediata, avaliação de alcance, notificação aos titulares e à autoridade quando
aplicável (LGPD), e revisão do controle que falhou.
