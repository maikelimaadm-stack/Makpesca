---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: —
---

# Personas

> Personas são hipóteses de trabalho derivadas do briefing, **não pesquisa de campo
> validada**. Ver `../00-governance/ASSUMPTIONS.md` (A-001).

## Persona 1 — Pescador amador frequente ("o dono do ponto")

- Pesca várias vezes por mês, geralmente nos mesmos rios/represas.
- Tem pontos que considera patrimônio pessoal e **não** quer divulgar.
- Já perdeu marcações salvas em papel, GPS antigo ou anotações no celular.
- Usa celular Android intermediário; sinal fraco ou ausente no local de pesca.

**Precisa de:** marcar ponto rápido, offline, com confiança de que não vaza.
**Teme:** que o app publique seus pontos; perder o histórico.
**Recurso decisivo:** ponto privado + offline confiável.

## Persona 2 — Pescador social ("o que posta")

- Gosta de mostrar capturas, comparar com amigos, participar de ranking.
- Segue outros pescadores, entra em comunidades do seu estado e da espécie preferida.

**Precisa de:** publicar captura com foto bonita sem revelar o local.
**Teme:** parecer amador; ter foto copiada.
**Recurso decisivo:** publicação de captura com controle de precisão.

## Persona 3 — Pescador iniciante ("o que não sabe onde ir")

- Começou há pouco, não conhece espécies, iscas nem locais.
- Depende de informação pública, lojas e de quem já pesca.

**Precisa de:** descobrir regiões, corpos d'água públicos, espécies, iscas e lojas.
**Teme:** ir longe e não pegar nada; comprar o equipamento errado.
**Recurso decisivo:** descoberta por região + conteúdo da comunidade + lojas parceiras.

## Persona 4 — Organizador de pescaria / guia

- Organiza saídas em grupo, torneios informais e leva clientes.
- Precisa combinar ponto de encontro, horário, participantes e equipamento.

**Precisa de:** grupos, eventos, compartilhamento pontual e controlado de localização.
**Teme:** desencontro; divulgar pontos de trabalho.
**Recurso decisivo:** eventos + grupos + compartilhamento temporário.

## Persona 5 — Loja de pesca parceira

- Loja física ou pequena rede, vende equipamentos e iscas.
- Faz vendas por WhatsApp e site próprio.

**Precisa de:** aparecer no mapa para pescadores da região; divulgar ofertas; medir retorno.
**Teme:** pagar por divulgação sem resultado comprovado.
**Recurso decisivo:** perfil de loja + ofertas + relatório de cliques e conversões.

## Persona 6 — Operação Makpesca (interna)

- Modera conteúdo, verifica parceiros, apura denúncias, concilia comissões.

**Precisa de:** painel admin, auditoria e ferramentas de moderação.
**Teme:** volume de denúncias sem ferramenta; erro irreversível em produção.
**Recurso decisivo:** admin com auditoria.

## Anti-persona

- Quem quer coletar e revender pontos de pesca de terceiros.
- Quem quer rastrear pessoas.
- Quem quer usar o app como canal de spam comercial.

O produto é desenhado para **não** servir a esses usos.
