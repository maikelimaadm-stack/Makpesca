---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0018
---

# Modelo Social

## 1. Princípio

Tudo gira em torno da pesca. **Não construímos um Instagram genérico.**
Todo recurso social precisa responder: "como isso serve a quem pesca?"

## 2. Objetos sociais

| Objeto | Descrição | Específico da pesca |
|--------|-----------|---------------------|
| Publicação de captura | Peixe registrado, publicado com controle de precisão | Sim — é o objeto central |
| Post de texto/foto | Relato, dúvida, dica | Contextualizado por comunidade/região |
| Post de evento | Divulgação de pescaria | Sim |
| Compartilhamento de ponto | Somente com autorização explícita | Sim |
| Comentário | Discussão sobre o conteúdo | — |
| Reação | Sinal leve de apreciação | — |
| Salvamento | Guardar para depois (dicas, locais públicos) | — |

## 3. Relações

| Relação | Tipo | Estado |
|---------|------|--------|
| Seguir | Assimétrica | MVP |
| Amizade mútua | Simétrica | **Decisão aberta (Q-002)** |
| Membro de comunidade | Muitos-para-muitos | Pós-MVP |
| Membro de grupo | Muitos-para-muitos, fechado | Pós-MVP |
| Bloqueio | Assimétrico e absoluto | MVP |

## 4. O que aparece no feed

Ver `FEED-MODEL.md`. Em resumo: quem eu sigo, comunidades que participo, conteúdo público
relevante da minha região, e eventos próximos.

Ordenação por relevância combina recência, proximidade geográfica (em nível de região) e
afinidade (espécie, corpo d'água) — **nunca** usando localização exata.

## 5. Privacidade no social

| Regra |
|-------|
| Publicar captura não publica o ponto (INV-G04) |
| Precisão é escolhida por publicação |
| Perfil tem visibilidade configurável |
| Estatísticas do perfil não revelam localização |
| "Pescadores próximos" exige consentimento explícito e usa região, nunca coordenada |
| Bloqueio remove acesso mútuo ao conteúdo |

## 6. Descoberta

| Mecanismo | Base |
|-----------|------|
| Por região | Região declarada no perfil + consentimento |
| Por espécie | Espécies favoritas e capturas públicas |
| Por corpo d'água | Capturas públicas associadas |
| Por comunidade | Participação |
| Por hashtag/tópico | Pós-MVP |
| Sugestão de pessoas | Pós-MVP, sempre com opção de sair |

Descoberta nunca revela localização acima do autorizado nem expõe quem optou por não
aparecer.

## 7. Qualidade do conteúdo

| Mecanismo | Fase |
|-----------|------|
| Denúncia e bloqueio | MVP (obrigatório) |
| Limites de publicação por janela | MVP |
| Moderação reativa | MVP |
| Reputação/confiança | Pós-MVP |
| Triagem automática | Pós-MVP |

## 8. O que não fazemos

- Feed puramente algorítmico opaco e viciante.
- Métricas de vaidade como eixo principal do produto.
- Recomendação baseada em localização exata.
- Conteúdo fora do domínio da pesca como foco.
- Recurso social sem ferramenta de moderação (P11).
