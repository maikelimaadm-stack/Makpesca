---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0010, ADR-0014, ADR-0018, ADR-0020
---

# Escopo Pós-MVP

O que entra depois que o ciclo central do MVP estiver estável em produção.

## 1. Social ampliado
| Item | Depende de |
|------|-----------|
| Comunidades regionais e temáticas | Feed e moderação do MVP estáveis |
| Ranking local por comunidade | Antifraude mínimo |
| Perfil ampliado (espécies favoritas, estatísticas, atividade) | Modelo de capturas maduro |
| Descoberta de pessoas por região | Consentimento explícito de visibilidade |
| Hashtags/tópicos | Moderação |
| Salvar e compartilhar publicações | — |

## 2. Grupos e eventos
| Item | Depende de |
|------|-----------|
| Grupos públicos e privados | Comunidades |
| Convites e papéis (admin/membro) | — |
| Eventos / pescarias em grupo | Grupos |
| Compartilhamento de ponto com participantes de evento | Geo-privacy congelada (F3) |
| Calendário e confirmação de presença | Eventos |

## 3. Mapas offline avançados
| Item | Depende de |
|------|-----------|
| Download de região com solução licenciada | **ADR-0010** (bloqueante) |
| Múltiplas regiões, atualização de região | ADR-0010 |
| Camadas adicionais (corpos d'água detalhados) | Fonte de dados licenciada |

## 4. Makpesca PRO e billing
| Item | Depende de |
|------|-----------|
| Planos FREE/PRO | Entitlement Service |
| Compra via App Store / Google Play | ADR-0014 |
| Restore, grace period, webhooks idempotentes | ADR-0014 |
| Limites diferenciados (regiões offline, pontos, histórico) | ENTITLEMENTS |

## 5. Comércio
| Item | Depende de |
|------|-----------|
| Lojas parceiras com perfil e unidades | Verificação de parceiro |
| Ofertas e cupons | Regras de oferta |
| Rastreamento de cliques e referrals | ATTRIBUTION |
| Comissões e relatórios | Conciliação |
| Portal de parceiros (`partners.makpesca.com.br`) | ADR-0021 |

## 6. Gamificação
| Item | Depende de |
|------|-----------|
| Conquistas | Histórico de capturas |
| Rankings por espécie/região/período | Antifraude |
| Desafios com período e regras | Rankings |

## 7. Mensagens
| Item | Depende de |
|------|-----------|
| Mensagem individual e em grupo | ADR-0019 |
| Envio de captura, ponto autorizado e localização autorizada | Geo-privacy congelada |
| Denúncia e bloqueio no chat | Moderação |

## 8. Web ampliada
| Item | Depende de |
|------|-----------|
| Mapa web completo | Mapa mobile estável |
| Explorar regiões, comunidades, perfis públicos | Social ampliado |
| Página de espécies e conteúdo público (SEO) | Catálogo de espécies |

## 9. Operação
| Item | Depende de |
|------|-----------|
| Admin completo | Volume de moderação |
| Feature flags e rollout gradual | ADR-0016 |
| Jobs assíncronos consolidados | ADR-0015 |
| Observabilidade completa (métricas, traces) | ADR-0016 |
