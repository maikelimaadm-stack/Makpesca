---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0003
---

# Versionamento da API

## 1. Esquema

Versão maior no caminho: `https://api.makpesca.com.br/v1/...`

Não usamos versão por cabeçalho como mecanismo principal: caminho é explícito, cacheável e
fácil de depurar.

## 2. O que é compatível (permitido dentro de `/v1`)

- adicionar endpoint;
- adicionar campo **opcional** em requisição;
- adicionar campo em resposta;
- adicionar valor novo em enumeração **de saída**, desde que documentado que clientes
  devem tolerar valores desconhecidos;
- relaxar validação;
- melhorar desempenho e mensagens de erro (sem mudar códigos).

## 3. O que é quebra (exige `/v2`)

- remover ou renomear campo;
- mudar tipo, unidade ou semântica de campo;
- tornar obrigatório um campo antes opcional;
- mudar código de erro de um caso existente;
- mudar comportamento de idempotência;
- mudar regra de autorização de forma que clientes válidos passem a falhar;
- mudar o formato do cursor de paginação de forma não transparente.

## 4. Depreciação

| Etapa | Regra |
|-------|-------|
| Anúncio | Campo/endpoint marcado como deprecado na OpenAPI, com data |
| Sinalização | Cabeçalho de depreciação na resposta |
| Janela | Prazo mínimo definido, considerando que apps móveis demoram a atualizar |
| Medição | Uso do recurso deprecado é medido por versão de cliente |
| Remoção | Só quando o uso cair abaixo do limiar definido **e** a janela terminar |

## 5. Versão do cliente

Todo cliente envia sua identificação (plataforma e versão) em cabeçalho. Com isso a API:

- mede uso por versão;
- aplica correções compatíveis para clientes antigos quando necessário;
- sinaliza atualização recomendada ou obrigatória.

Versão mínima suportada é decisão explícita, documentada e anunciada.

## 6. Versionamento dos catálogos e do protocolo de sync

- Catálogos têm versão própria; o cliente sincroniza por versão.
- O protocolo de sync tem versão própria dentro de `/v1`, porque pode evoluir sem quebrar
  o restante da API. Mudança incompatível de sync exige negociação de versão explícita.

## 7. Webhooks

Webhooks recebidos (billing, parceiros) e emitidos (para parceiros, no futuro) têm
versionamento independente e documentado, porque o emissor externo não segue o nosso ciclo.

## 8. Convivência de versões

`/v1` e `/v2` podem coexistir. Regras:

- ambas apontam para o mesmo domínio (nunca duas regras de negócio paralelas);
- a diferença fica na camada HTTP/DTO;
- a duplicação é temporária e tem data de fim planejada.
