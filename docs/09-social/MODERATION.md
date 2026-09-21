---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: —
---

# Moderação

## 1. Princípio

**Nenhum recurso social é lançado sem ferramenta de moderação** (P11).
Denúncia e bloqueio nascem junto com o primeiro recurso social, no MVP.

## 2. O que é moderável

Publicações, comentários, fotos, perfis (nome, bio, foto), comunidades, grupos, eventos,
mensagens (mediante denúncia), ofertas de parceiros e conteúdo de ranking/desafio.

## 3. Políticas de conteúdo (esqueleto)

| Categoria | Tratamento |
|-----------|-----------|
| Conteúdo ilegal | Remoção imediata + cooperação legal |
| Assédio, ameaça, discurso de ódio | Remoção + sanção |
| Conteúdo sexual ou violento | Remoção |
| Spam e comércio não autorizado | Remoção + limite |
| Desinformação sobre regras de pesca | Rotulagem/remoção conforme fonte oficial |
| Crueldade animal além da prática de pesca | **Política específica necessária** |
| Pesca ilegal ostensiva (espécie protegida, defeso, área proibida) | **Política específica necessária** |
| Divulgação de ponto alheio sem autorização | Remoção |
| Personificação | Remoção + verificação |
| Conteúdo fora do domínio | Redução de alcance ou remoção |

> As duas políticas marcadas como necessárias exigem apoio jurídico e de especialistas do
> setor. Entram como pendência em `../00-governance/OPEN-QUESTIONS.md`.

## 4. Fluxo

```
denúncia ou detecção → triagem → caso → decisão → ação → notificação → recurso
```

| Etapa | Regra |
|-------|-------|
| Triagem | Prioriza por gravidade e reincidência |
| Caso | Agrupa denúncias sobre o mesmo alvo |
| Decisão | Registrada com motivo e responsável |
| Ação | Proporcional: nenhuma, aviso, remoção, redução de alcance, suspensão, banimento |
| Notificação | Autor informado do que foi removido e por quê |
| Recurso | Caminho de contestação com revisão por outra pessoa |

## 5. Ações disponíveis

| Ação | Escopo |
|------|--------|
| Remover conteúdo | Item |
| Ocultar conteúdo pendente de análise | Item |
| Reduzir alcance | Autor ou item |
| Restringir recurso (comentar, mensagem, publicar) | Autor, temporário |
| Suspender conta | Autor, temporário |
| Banir conta | Autor, permanente |
| Remover administrador de comunidade | Comunidade |
| Suspender parceiro | Parceiro |

## 6. Moderação em camadas

| Camada | Quem | Poder |
|--------|------|-------|
| Autor | Usuário | Apaga o próprio conteúdo |
| Comunidade/grupo | Administradores locais | Regras locais, dentro do seu espaço |
| Plataforma | Operação Makpesca | Regras gerais; sobrepõe decisões locais |
| Automação | Sistema | Limites, detecção de padrão, triagem |

## 7. Privacidade na moderação

| Regra |
|-------|
| Moderador vê o necessário para decidir, não mais |
| Coordenada exata não é exibida por padrão em ferramenta de moderação |
| Acesso a conteúdo privado exige caso aberto e é auditado |
| Identidade do denunciante não é revelada ao denunciado |
| Decisões registradas com autor e motivo |

## 8. Capacidade operacional

Moderação é trabalho humano e escala mal (R-046). Mitigações: limites de criação de
conteúdo, priorização automática, resposta rápida a categorias graves, métricas de fila
e crescimento controlado por região.

**Se a fila de moderação não for sustentável, o recurso social correspondente é reduzido
ou pausado** — não se lança algo que não se consegue moderar.

## 9. Métricas

Denúncias por 1.000 publicações, tempo até a primeira ação, taxa de reversão em recurso,
reincidência por autor, categorias mais frequentes.
