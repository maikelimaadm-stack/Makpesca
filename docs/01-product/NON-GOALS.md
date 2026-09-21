---
Status: REVIEW
Version: 0.2.0
Last Updated: 2026-09-21
Owners: Maike Lima (autoridade humana final)
Related ADRs: ADR-0010
Wave: F0
Lifecycle: FREEZE-CONTROLLED
---

# Não-Objetivos

O que o Makpesca **não** é. Estes itens não entram por conveniência de implementação nem
por pedido isolado — mudá-los exige decisão registrada.

## 1. Não é uma rede social genérica
Não replicamos Instagram/Facebook com tema de peixe. Todo recurso social precisa servir a
quem pesca. Conteúdo fora do domínio é ruído e pressiona moderação.

## 2. Não é um catálogo colaborativo de pontos alheios
O produto **não** existe para coletar pontos de terceiros e redistribuí-los. Pontos são do
usuário; divulgação é ato voluntário e reversível.

## 3. Não é rastreador de pessoas
Não há localização contínua de usuários em tempo real no MVP nem no pós-MVP. Qualquer
compartilhamento é pontual, consentido, com precisão escolhida e revogável.

## 4. Não é aplicativo de navegação náutica certificado
Nenhuma informação do app serve para navegação de segurança. Não substitui carta náutica,
sonda ou instrumento oficial. Isso deve aparecer como aviso ao usuário.

## 5. Não é marketplace completo (no início)
Sem carrinho, sem checkout interno, sem custódia de pagamento, sem logística.
O comércio começa como: perfil de loja, oferta, cupom, link/WhatsApp e rastreio de conversão.

## 6. Não é fonte oficial de regulação de pesca
Não publicamos regras de defeso, licenças ou limites legais como verdade oficial sem fonte
licenciada e responsável identificável.

## 7. Não é plataforma de apostas ou premiação financeira
Desafios e rankings não operam como aposta. Premiação, se existir, é patrocinada e regida
por regulamento próprio.

## 8. Não é serviço de dados para terceiros
Não vendemos dados de localização de usuários. Não expomos base de pontos a parceiros.
Insights, se existirem, são agregados, anônimos e passam por verificação de reidentificação.

## 9. Não é plataforma sem moderação
Não lançamos recurso social sem denúncia, bloqueio e caminho de moderação.

## 10. Não promete base cartográfica offline antes de decidir
Enquanto ADR-0010 estiver `OPEN` e o `MAP-LICENSE-GATE` `BLOCKED`, "mapas offline" não é
recurso prometido — nem em documentação, nem em interface, nem em loja de aplicativos.
O **offline core** (marcar, registrar, não perder, sincronizar) continua sendo promessa
firme. Ver Constituição, Art. 4 e 4-A.

## 11. Não é software acoplado a um provider
Supabase, Vercel e Google são infraestrutura inicial, não arquitetura. O produto não pode
se tornar impossível de migrar.
