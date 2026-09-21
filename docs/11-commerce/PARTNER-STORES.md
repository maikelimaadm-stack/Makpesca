---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0021
---

# Lojas Parceiras

## 1. Domínio conceitual

| Entidade | Papel |
|----------|-------|
| `PartnerStore` | A loja parceira (pessoa jurídica) |
| `StoreLocation` | Unidade física, com endereço e coordenada |
| `PartnerProfile` | Apresentação pública da loja |
| `PartnerVerification` | Verificação e selo |
| `Offer` | Oferta divulgada |
| `ProductReference` | Referência a produto (sem catálogo completo no início) |
| `Brand` | Marca trabalhada |
| `Category` | Categoria de produto |
| `Campaign` | Campanha que agrupa ofertas |
| `Coupon` | Cupom vinculado |

## 2. Perfil público da loja

Logo, capa, fotos, endereço, localização no mapa, WhatsApp, telefone, site, horários de
funcionamento, marcas trabalhadas, categorias, produtos/ofertas em destaque, avaliações
(pós-MVP) e selo "Parceira Makpesca".

**A localização de loja é dado público** — é comércio, não ponto de pesca. Não passa pelas
regras de degradação.

## 3. Verificação

| Etapa | Descrição |
|-------|-----------|
| Cadastro | Dados da empresa e responsável |
| Verificação | Conferência de existência, dados cadastrais e titularidade |
| Aprovação | Manual no início |
| Selo | Concedido apenas após verificação |
| Revisão | Periódica e sob denúncia |
| Suspensão | Por violação de regras |

Selo sem verificação real destrói a confiança do usuário — é um compromisso, não um
adorno visual.

## 4. Regras para parceiros

| Regra |
|-------|
| Oferta precisa ser verdadeira, com condições e validade claras |
| Proibido spam a usuários |
| Proibido solicitar pontos de pesca de usuários |
| Proibido usar dados da plataforma fora da finalidade |
| Conteúdo patrocinado sempre identificado |
| Denúncias de usuários contra a loja são apuradas |

## 5. Dados que o parceiro **não** recebe

- Identidade dos usuários que viram suas ofertas.
- Localização de usuários.
- Pontos de pesca, capturas ou qualquer dado de pesca individual.
- Contato de usuários sem que o usuário inicie o contato.

O parceiro recebe **métricas agregadas**: visualizações, cliques, conversões conciliadas.

## 6. Avaliações (pós-MVP)

Se existirem: só quem teve interação registrada pode avaliar; loja pode responder;
avaliação passa por moderação; loja não pode remover avaliação negativa legítima.

## 7. Descoberta

Lojas aparecem: no mapa, na busca, na página da região, e em contexto (ex.: "lojas perto
deste corpo d'água"). A ordenação **não** é vendável de forma opaca — destaque pago, se
existir, é rotulado.

## 8. Riscos

| Risco | Mitigação |
|-------|-----------|
| Parceiro malicioso (R-055) | Verificação, contrato, acesso mínimo, auditoria |
| Oferta enganosa (R-056) | Regras, validade obrigatória, denúncia, suspensão |
| Loja inativa com dados desatualizados | Revisão periódica, sinalização |
| Concorrência desleal entre parceiros | Regras claras de destaque |
| Usuário confundir parceiro com Makpesca | Identificação visual clara |
