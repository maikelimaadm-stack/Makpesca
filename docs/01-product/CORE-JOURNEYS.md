---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0011, ADR-0012
---

# Jornadas Centrais

Jornadas descrevem **comportamento esperado**, não implementação.

## J1 — Preparar a pescaria (online, em casa)

1. Usuário abre o mapa e navega até a região onde vai pescar.
2. Consulta corpos d'água, pontos públicos, capturas públicas recentes e condições.
3. Baixa a região para uso offline **se houver basemap offline disponível** — recurso
   condicionado a ADR-0010 e ao `MAP-LICENSE-GATE` (Constituição, Art. 4-A). Quando
   existir, limites do plano se aplicam (ver `../12-billing/ENTITLEMENTS.md`).
4. Confere lojas parceiras no caminho e eventos da comunidade local.

**Critério de sucesso:** ao sair de casa, o app tem os **dados do usuário e os catálogos**
necessários para operar sem rede. A base cartográfica offline é um acréscimo condicional,
não parte do critério.

## J2 — Pescar sem sinal (offline, no campo)

1. Sem internet, o app abre e mostra os dados locais do usuário (pontos, capturas,
   catálogos). Se houver basemap offline baixado, ele é exibido; se não houver, o app
   funciona sem base cartográfica detalhada.
2. GPS fornece a posição atual.
3. Usuário marca um ponto novo (nome, tipo, observações). Ponto nasce `PRIVATE`.
4. Usuário registra uma captura: espécie, peso, comprimento, isca, técnica, horário, foto.
5. Fecha o app. Reabre. **Tudo continua lá.**

**Critério de sucesso:** zero perda, zero dependência de rede, feedback imediato — com ou
sem base cartográfica offline.

## J3 — Voltar e sincronizar

1. Dispositivo reconecta.
2. Outbox envia mutações pendentes com id de cliente e idempotency key.
3. Fotos sobem em fila própria, com retomada se a conexão cair.
4. Servidor confirma; app atualiza estado local; cursor avança.
5. **Nada duplica**, mesmo se o envio foi repetido.

**Critério de sucesso:** convergência entre dispositivo e servidor sem intervenção.

## J4 — Decidir o que compartilhar

1. Usuário abre uma captura sincronizada.
2. Escolhe publicar. A interface pergunta, separadamente:
   - publicar a captura? (visibilidade)
   - revelar a localização? (precisão: exata, aproximada, região, corpo d'água, oculta)
3. Publicação acontece com a precisão escolhida, aplicada no servidor.
4. Usuário pode reverter: despublicar ou reduzir a precisão depois.

**Critério de sucesso:** o usuário nunca revela o ponto sem ter decidido isso explicitamente.

## J5 — Compartilhar um ponto com alguém

1. Usuário escolhe um ponto `PRIVATE`.
2. Compartilha com pessoa, grupo ou participantes de um evento.
3. Define precisão e, se quiser, prazo.
4. O destinatário recebe apenas a precisão concedida.
5. O dono revoga a qualquer momento; o acesso cessa imediatamente (inclusive em cache).

**Critério de sucesso:** revogação eficaz e auditável.

## J6 — Participar da comunidade

1. Usuário entra em comunidades por região, rio, represa, espécie ou modalidade.
2. Vê feed com capturas e posts de quem segue e das comunidades.
3. Comenta, reage, salva.
4. Descobre pescadores da mesma região (com consentimento) e eventos próximos.

**Critério de sucesso:** relevância local; nada "genérico".

## J7 — Pescaria em grupo

1. Organizador cria um grupo ou usa um existente.
2. Cria um evento: data, horário, ponto de encontro, limite de participantes.
3. Participantes confirmam.
4. Organizador compartilha pontos autorizados só com participantes.
5. Depois do evento, fotos e capturas ficam vinculadas ao evento.

**Critério de sucesso:** coordenação sem vazar ponto para fora do grupo.

## J8 — Descobrir uma loja e usar uma oferta

1. Usuário vê lojas parceiras no mapa ou na busca.
2. Abre o perfil: endereço, horários, marcas, contato, ofertas.
3. Usa uma oferta: abre o site do parceiro, aciona o WhatsApp ou copia um cupom.
4. O clique é registrado com referral.
5. Se houver conversão informada/conciliada, gera comissão — sem duplicar.

**Critério de sucesso:** rastreio honesto e não intrusivo; usuário entende que é parceiro.

## J9 — Virar PRO

1. Usuário encontra limite do plano FREE (ex.: número de regiões offline).
2. Vê o que o PRO libera e o preço.
3. Assina pela loja do sistema operacional.
4. Entitlements são concedidos pelo Entitlement Service, não pelo app.
5. Troca de aparelho: restaura a assinatura e recupera os entitlements.

**Critério de sucesso:** nunca "pagou e não liberou"; nunca "liberou sem pagar".

## J10 — Exercer direitos sobre os dados

1. Usuário solicita exportação dos seus dados.
2. Recebe o conteúdo do qual é titular — incluindo pontos privados, que não vão a terceiros.
3. Solicita exclusão da conta.
4. Sistema remove ou anonimiza conforme `../04-data/DATA-LIFECYCLE.md`, propagando
   tombstones para os dispositivos.

**Critério de sucesso:** conformidade com LGPD comprovável.
