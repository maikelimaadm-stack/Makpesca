---
Status: REVIEW
Version: 0.2.0
Last Updated: 2026-09-21
Owners: Maike Lima (autoridade humana final)
Related ADRs: —
Wave: cross-cutting (controle vivo; registrada em F0)
Lifecycle: LIVING
---

# Premissas

Premissa é o que assumimos **sem verificação completa**. Toda premissa aqui é candidata a
virar decisão (com ADR) ou risco (com mitigação). Nenhuma premissa pode ser congelada
como verdade.

| ID | Premissa | Origem | Verificação necessária | Se for falsa |
|----|----------|--------|------------------------|--------------|
| A-001 | O público-alvo inicial é o pescador amador brasileiro | Briefing | Pesquisa com usuários | Muda personas, idioma, catálogo e monetização |
| A-002 | Offline real é diferencial decisivo | Briefing | Entrevistas e concorrência | Reduz prioridade de F4/F5 e simplifica o produto |
| A-003 | Usuários querem compartilhar capturas, mas não pontos | Hipótese | Teste de produto | Muda defaults de privacidade |
| A-004 | Default de privacidade de ponto deve ser `PRIVATE` | Princípio de privacidade | Validar com usuários | Se falso, ainda mantemos `PRIVATE` por segurança |
| A-005 | Lojas de pesca locais têm interesse em divulgação digital | Hipótese comercial | Validação comercial | Inviabiliza receita de parceiros |
| A-006 | Conversão externa (site/WhatsApp) é suficiente no início | Briefing | Teste com parceiro piloto | Exigiria marketplace, muito mais caro |
| A-007 | ~R$ 19,90/mês é faixa aceitável para PRO | Briefing (referência) | Teste de preço | Reprecificar; não está congelado |
| A-008 | PostGIS cobre as consultas geoespaciais necessárias | Experiência do setor | Prova de conceito com dados reais | Exigiria índice/serviço geo dedicado |
| A-009 | Supabase gerenciado oferece PostGIS e PITR adequados | Premissa **não verificada** | Consultar documentação oficial com data | Troca de provider de banco |
| A-010 | Vercel comporta a API inicial dentro de seus limites | Premissa **não verificada** | Consultar limites oficiais com data | Hospedar em runtime de container |
| A-011 | Expo cobre GPS, mapa, SQLite e upload em background necessários | Premissa **não verificada** | Prova de conceito | Ejetar ou usar módulos nativos |
| A-012 | Volume inicial de usuários é baixo o bastante para fan-out on read | Estimativa | Medição em beta | Arquitetura de feed materializado antes |
| A-013 | Moderação manual é suficiente no início | Estimativa | Medir volume de denúncias | Ferramentas automáticas antecipadas |
| A-014 | Não haverá dados de menores de 13 anos no início | Decisão de produto pretendida | Política de cadastro | Obriga fluxo de consentimento parental |
| A-015 | Uma única região de banco atende a latência aceitável no Brasil | Estimativa | Medição | Replicação/regiões adicionais |

## Regra

Premissa marcada como **não verificada** não pode sustentar um documento `FROZEN`.
Antes do freeze da onda correspondente, cada uma deve virar: decisão verificada,
risco aceito com mitigação, ou pergunta aberta em `OPEN-QUESTIONS.md`.
