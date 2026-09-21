---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0021
---

# Portal de Parceiros

`partners.makpesca.com.br`

## 1. Propósito

Dar ao parceiro autonomia para manter perfil, ofertas e acompanhar resultados — sem
acesso a dados de usuários.

## 2. Funcionalidades

| Área | Conteúdo |
|------|----------|
| Perfil | Logo, capa, fotos, descrição, marcas, categorias, contatos |
| Unidades | Endereços, coordenadas, horários, telefones |
| Ofertas | Criar, editar, agendar, encerrar |
| Cupons | Códigos, validade, limites |
| Campanhas | Agrupamento de ofertas por período |
| Cliques | Volume por oferta e período |
| Conversões | Conversões informadas e conciliadas |
| Comissões | Valores, estado, período |
| Relatórios | Exportação agregada |
| Dados cadastrais | Empresa, responsável, dados de pagamento |
| Verificação | Estado e pendências |
| Suporte | Canal de atendimento |

## 3. Acesso e segurança

| Regra |
|-------|
| Conta de parceiro separada da conta de usuário final |
| Papéis dentro do parceiro (proprietário, operador) |
| Isolamento estrito entre parceiros (INV-A05) |
| Auditoria de ações do parceiro |
| 2FA recomendado, obrigatório para dados financeiros |
| Sessões revogáveis |

## 4. Privacidade

O portal **nunca** exibe: identidade de usuários, localização de usuários, dados de pesca
individuais, ou qualquer informação que permita identificar quem clicou.

Métricas são agregadas e, quando o volume for muito baixo, suprimidas para não permitir
identificação por dedução (mesma lógica de coorte mínima).

## 5. Fluxo de trabalho do parceiro

```
cadastro → verificação → perfil publicado → criar oferta →
usuários veem → cliques registrados → conversões informadas/conciliadas →
comissões calculadas → payout
```

## 6. Arquitetura

Aplicação web separada (`apps/partners`), consumindo a **mesma** API com escopo de
parceiro. Não há banco próprio nem regra paralela.

## 7. Fase

Pós-MVP. Antes disso, a operação do parceiro é manual, feita pela equipe Makpesca.
Isso é aceitável enquanto o número de parceiros for pequeno e evita construir um portal
antes de validar o modelo comercial.
