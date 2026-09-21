---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: —
---

# Denúncia e Bloqueio

## 1. Denúncia

### O que pode ser denunciado
Publicação, comentário, foto, perfil, mensagem, comunidade, grupo, evento, oferta de
parceiro, resultado de ranking/desafio.

### Motivos (lista fechada)
| Código | Motivo |
|--------|--------|
| `SPAM` | Spam ou comércio não autorizado |
| `HARASSMENT` | Assédio ou ameaça |
| `HATE` | Discurso de ódio |
| `SEXUAL` | Conteúdo sexual |
| `VIOLENCE` | Violência |
| `ILLEGAL_FISHING` | Pesca ilegal ostensiva |
| `ANIMAL_CRUELTY` | Crueldade animal |
| `PRIVACY` | Divulgação de local ou dado alheio sem autorização |
| `IMPERSONATION` | Personificação |
| `MISINFORMATION` | Informação falsa relevante |
| `OFF_TOPIC` | Fora do domínio da pesca |
| `OTHER` | Outro (com texto livre) |

### Regras
| Regra |
|-------|
| Denunciar leva poucos toques, de dentro do conteúdo |
| O denunciante recebe confirmação e, ao final, o desfecho geral |
| Identidade do denunciante nunca é revelada ao denunciado |
| Denúncia duplicada agrupa no mesmo caso |
| Denúncia em massa coordenada é detectada e não decide sozinha |
| Denúncia abusiva recorrente gera sanção ao denunciante |
| Toda denúncia gera caso rastreável (INV-T02) |

## 2. Bloqueio

### Efeitos imediatos
| Efeito |
|--------|
| Fim do follow nos dois sentidos |
| Fim de concessões de localização entre as partes |
| Conteúdo mutuamente invisível |
| Mensagens impedidas |
| Menções e comentários impedidos |
| Convites impedidos (grupo, evento, comunidade) |
| Remoção de listas de seguidores |

### Regras
| Regra |
|-------|
| O bloqueado não é notificado |
| Bloqueio é reversível pelo bloqueador |
| Em espaços compartilhados (comunidade), o conteúdo de cada um fica oculto para o outro |
| Bloqueio não apaga conteúdo já existente de terceiros |
| Administrador de comunidade bloqueado individualmente continua podendo moderar a comunidade, mas não interagir |

## 3. Silenciar (opcional, pós-MVP)

Alternativa mais leve: deixa de ver o conteúdo sem romper a relação nem sinalizar nada.
Útil para reduzir bloqueios desnecessários.

## 4. Restrições automáticas

| Gatilho | Ação |
|---------|------|
| Muitas denúncias procedentes em curto período | Redução de alcance + revisão prioritária |
| Conta nova com comportamento de spam | Limites mais rígidos |
| Padrão de coleta de dados | Rate limit agressivo + revisão |
| Menções em massa | Bloqueio temporário do recurso |

## 5. Transparência

O usuário sancionado recebe: o que aconteceu, qual regra foi violada, qual a duração e
como contestar. Sanção sem explicação destrói confiança e gera reincidência por
desconhecimento.

## 6. Suporte a vítimas

Quem sofre assédio tem caminho rápido: bloquear, denunciar, restringir quem pode interagir
e, se necessário, tornar o perfil privado — tudo em poucos toques, sem depender de
resposta da operação.
