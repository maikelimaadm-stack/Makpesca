---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0010, ADR-0011
---

# Contrato Offline-First

Este documento é **contrato**, não aspiração. Se o comportamento aqui não acontecer,
o produto falhou.

## 0. Dois escopos distintos

| Escopo | Natureza | Depende de |
|--------|----------|-----------|
| **OFFLINE APP CORE** | **Constitucional** (Art. 4). Contrato firme deste documento | nada em aberto |
| **OFFLINE CARTOGRAPHIC BASEMAP** | Recurso **candidato** (Art. 4-A) | ADR-0010 `OPEN` + `MAP-LICENSE-GATE` `BLOCKED` |

Tudo neste documento é contrato do **core**, exceto onde marcado como condicional.
Se ADR-0010 concluir que não há solução legal e viável, o core continua valendo integralmente,
operando **sem base cartográfica detalhada**.

## 1. Cenário de referência

```
[baixar região — condicional] → ficar sem internet → obter GPS →
consultar dados locais (e o basemap, se existir) →
criar ponto → registrar captura → anexar foto → fechar o app →
reabrir o app → dados continuam lá → reconectar → sincronizar →
sem duplicar → uploads retomados → conflitos tratados → convergência
```

Cada seta acima é um requisito testável, **exceto a primeira**, que é condicional ao
ADR-0010. Ver `../15-quality/OFFLINE-TEST-MATRIX.md`.

## 2. O que funciona 100% offline

| Função | Offline | Observação |
|--------|---------|------------|
| Abrir o app e autenticar sessão já estabelecida | Sim | Sessão válida em cache seguro |
| Ver dados locais (pontos, capturas, catálogos) sobre o mapa | Sim | **Core** — não depende de ADR-0010 |
| Ver base cartográfica de região baixada | **Condicional** | **Não é core** — depende de ADR-0010 |
| Obter posição GPS | Sim | Hardware, não rede |
| Criar/editar/excluir ponto próprio | Sim | |
| Registrar captura com fotos | Sim | |
| Consultar catálogos (espécies, iscas, técnicas) | Sim | Sincronizados previamente |
| Ver pontos e capturas próprios | Sim | |
| Ver pontos de terceiros já concedidos e baixados | Sim | Na precisão autorizada |
| Editar rascunho de publicação | Sim | Publicação efetiva exige rede |

## 3. O que exige rede

| Função | Motivo |
|--------|--------|
| Login inicial / renovação de credencial expirada | Segurança |
| Publicar conteúdo social | Moderação e distribuição |
| Feed, comunidades, mensagens | Dados de terceiros |
| Condições ambientais atuais | Fonte externa |
| Compra e restauração de assinatura | Loja |
| Baixar nova região | Dados cartográficos |
| Receber concessões novas de terceiros | Servidor |

## 4. Garantias

| ID | Garantia |
|----|----------|
| OFF-1 | Nenhum dado criado offline é perdido por fechamento do app, crash ou reinício do aparelho |
| OFF-2 | A interface só confirma a criação depois da escrita local durável |
| OFF-3 | O usuário sempre vê o estado de sincronização de cada item (pendente, enviando, sincronizado, erro) |
| OFF-4 | Nenhum registro é duplicado por reenvio |
| OFF-5 | Upload de mídia é retomável e sobrevive a troca de rede |
| OFF-6 | Sem rede, o app nunca trava esperando resposta nem exibe erro que sugira perda de dado |
| OFF-7 | Exclusões feitas offline convergem e não retornam |
| OFF-8 | Precisão de localização de terceiros em cache nunca excede a autorizada |
| OFF-9 | Entitlements têm validade em cache com prazo definido; expiração não revoga acesso já pago sem confirmação |

## 5. Limites explícitos

- Offline **não** significa base cartográfica detalhada: o basemap offline é condicional
  (Art. 4-A) e sua ausência não descumpre este contrato.
- Offline **não** significa acesso a dados de terceiros nunca baixados.
- Offline **não** contorna limites de plano (ex.: número de regiões).
- Offline **não** garante edição concorrente livre de conflito — ver `CONFLICT-RESOLUTION.md`.
- Sessão expirada exige rede para renovar; o app deve preservar os dados locais e continuar
  permitindo criação, com envio pendente.

## 6. Experiência esperada

| Situação | Comportamento |
|----------|---------------|
| Sem rede ao criar captura | Salva local, marca "pendente", sem erro alarmante |
| Rede volta | Sincroniza em segundo plano, sem exigir ação |
| Falha permanente de um item | Item fica visível com motivo e opção de reenviar |
| Conflito detectado | Resolução automática quando segura; pergunta ao usuário quando não |
| Espaço em disco insuficiente | Aviso claro antes de capturar mídia (e antes de baixar região, se o recurso existir) |

## 7. Requisito de teste

Nenhum slice de offline é aceito sem os cenários obrigatórios da
`../15-quality/OFFLINE-TEST-MATRIX.md` passando, incluindo o teste de "app morto no meio
do upload".
