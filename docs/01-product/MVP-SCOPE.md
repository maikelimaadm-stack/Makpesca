---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0003, ADR-0011, ADR-0012
---

# Escopo do MVP

Regra: **não inflar o MVP.** O MVP existe para provar o ciclo central
(marcar → registrar → offline → sincronizar → compartilhar com controle) com segurança.

Classificação usada em todo o documento: `MVP` | `POST-MVP` | `FUTURE` | `NEEDS-DECISION`.

## 1. Dentro do MVP

### Conta e perfil
| Item | Classificação |
|------|---------------|
| Cadastro e login | MVP |
| Perfil básico (nome, foto, cidade/região, bio) | MVP |
| Exclusão e exportação de conta | MVP (LGPD) |
| Sessões revogáveis | MVP |

### Mapa
| Item | Classificação |
|------|---------------|
| Mapa online com posição atual | MVP |
| Pins de pontos próprios | MVP |
| Pins de pontos públicos | MVP |
| Clusters básicos | MVP |
| Busca/navegação por região | MVP |
| Camadas avançadas, rotas, batimetria | POST-MVP / FUTURE |

### Pontos
| Item | Classificação |
|------|---------------|
| Criar, editar, excluir ponto | MVP |
| Visibilidade `PRIVATE`/`SHARED`/`PUBLIC` | MVP |
| Precisão compartilhável | MVP |
| Compartilhar ponto com pessoa | MVP |
| Revogar compartilhamento | MVP |
| Favoritos | POST-MVP |

### Capturas
| Item | Classificação |
|------|---------------|
| Registrar captura (espécie, peso, comprimento, isca, técnica, data/hora) | MVP |
| Foto da captura (1..N, limite definido) | MVP |
| Vincular captura a ponto | MVP |
| Privacidade independente do ponto | MVP |
| Condições ambientais anexadas | POST-MVP |

### Offline
| Item | Classificação |
|------|---------------|
| **Offline core** (abrir, ler dados locais, GPS, criar ponto/captura, mídia, durabilidade, sync sem duplicar) | **MVP — constitucional** |
| SQLite local com dados do usuário | MVP |
| Criar ponto e captura offline | MVP |
| Fila de mídia com retomada | MVP |
| Região de mapa offline (basemap) | **NEEDS-DECISION** — depende de ADR-0010; **fora do offline core** |

### Sync
| Item | Classificação |
|------|---------------|
| Outbox + idempotência | MVP |
| Pull por cursor | MVP |
| Tombstones (delete convergente) | MVP |
| Resolução de conflito básica | MVP |
| Multi-dispositivo | MVP (simples) |

### Social mínimo
| Item | Classificação |
|------|---------------|
| Seguir/deixar de seguir | MVP |
| Feed simples (quem sigo + público da minha região) | MVP |
| Publicar captura | MVP |
| Comentário e reação | MVP |
| Denúncia e bloqueio | MVP (obrigatório com social) |
| Comunidades | POST-MVP |

### Web
| Item | Classificação |
|------|---------------|
| Landing | MVP |
| Login | MVP |
| Página pública de perfil e capturas públicas | MVP mínimo |
| Mapa web completo | POST-MVP |

### Plataforma
| Item | Classificação |
|------|---------------|
| API `/v1` com auth, validação, erros e idempotência | MVP |
| Logs estruturados + request id | MVP |
| Rate limiting básico | MVP |
| Backup + teste de restore | MVP |
| Admin mínimo para moderação | **NEEDS-DECISION** (Q-022) |

## 2. Explicitamente fora do MVP

Comunidades completas, grupos, mensagens, eventos, rankings, conquistas, desafios,
lojas parceiras, ofertas, afiliados, portal de parceiros, PRO/billing, inteligência de
pesca, dados ambientais avançados, admin completo.

Ver `POST-MVP-SCOPE.md` e `FUTURE-SCOPE.md`.

## 3. Critérios de aceite do MVP

0. O **offline core** funciona integralmente **sem** base cartográfica offline.
1. Usuário cria ponto e captura **sem rede** e não perde nada ao reabrir o app.
2. Sincronização repetida **não duplica** nenhum registro.
3. Coordenada de ponto `PRIVATE` **nunca** aparece em resposta de API para terceiro.
4. Publicar captura **não** publica o ponto.
5. Revogação de compartilhamento surte efeito imediato.
6. Exclusão de conta remove/anonimiza e propaga para dispositivos.
7. Nenhuma coordenada exata em log, analytics ou crash report.
8. Restore de backup testado com evidência.

## 4. Pré-condições

O MVP só pode ser implementado após liberação do `IMPLEMENTATION-READY-GATE`, com as ondas
F0..F6 congeladas. Ver `../16-roadmap/DOCUMENTATION-FREEZE-WAVES.md`.
