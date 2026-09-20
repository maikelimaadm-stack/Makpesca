---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0011
---

# Resolução de Conflitos

## 1. Quando existe conflito

Conflito ocorre quando o `baseVersion` enviado pelo cliente não corresponde à versão atual
no servidor. Isso acontece com: dois dispositivos do mesmo usuário, edição offline longa,
ou reprocessamento após restore.

## 2. Estratégias disponíveis

| Estratégia | Quando usar |
|------------|-------------|
| **LWW por campo** (last write wins) | Campos independentes e de baixo risco |
| **Merge por campo** | Alterações em campos diferentes |
| **Preferir servidor** | Campos que o servidor deriva (região, corpo d'água, contadores) |
| **Preferir cliente** | Campos que só o dispositivo conhece (dados capturados no campo) |
| **Preferir mais restritivo** | **Sempre** para privacidade |
| **Perguntar ao usuário** | Conflito semântico relevante |
| **Delete vence** | Exclusão sobre edição concorrente |

## 3. Matriz de conflito

### Spot (ponto)
| Campo | Estratégia | Justificativa |
|-------|------------|---------------|
| `name`, `description`, `tags` | Merge por campo; empate → LWW | Baixo risco |
| `location` | Preferir a leitura com melhor qualidade (`locationSource` + acurácia); empate → perguntar | Dado de campo é valioso |
| `visibility` | **Mais restritivo vence** (`PRIVATE` > `SHARED` > `PUBLIC`) | Privacidade nunca degrada por acidente |
| `sharedPrecision` | **Mais restritivo vence** (`HIDDEN` > `WATER_BODY_ONLY` > `REGION` > `APPROXIMATE` > `EXACT`) | Idem |
| `waterBodyId`, `regionId` | Preferir servidor | Derivados |
| Exclusão | Delete vence | Convergência |

### Catch (captura)
| Campo | Estratégia |
|-------|------------|
| Medidas, espécie, isca, técnica, notas | Merge por campo; empate → LWW |
| `mediaIds` | **União** (não perder foto) |
| `location`, `caughtAt` | Preferir registro `LIVE` sobre `MANUAL_LATER` |
| `visibility`, `sharedPrecision` | Mais restritivo vence |
| `publicationStatus` | Despublicar vence sobre publicar |
| Exclusão | Delete vence |

### Trip / preferências
| Campo | Estratégia |
|-------|------------|
| Participantes | União, com validação de autorização no servidor |
| Preferências do usuário | LWW por chave |

### Nunca conflitam no cliente
Concessões de localização, entitlements, moderação, dados de terceiros: **o servidor é
autoridade única**. O cliente aplica o que recebe.

## 4. Regra de ouro da privacidade

> Em qualquer conflito que envolva visibilidade ou precisão, **vence o estado mais
> restritivo**, mesmo que seja o mais antigo.

Consequência aceita: um usuário pode precisar repetir a ação de tornar algo público.
Isso é preferível a expor algo por acidente.

## 5. Conflito com exclusão

| Cenário | Resultado |
|---------|-----------|
| Dispositivo A edita, B exclui | Exclusão vence; A recebe tombstone |
| Dispositivo A exclui, servidor já excluiu | `duplicate`, sem erro |
| Dispositivo offline recria entidade excluída | Rejeitado; tombstone tem precedência (INV-S06) |

## 6. Quando perguntar ao usuário

Perguntar só quando: o conflito muda conteúdo que o usuário reconhece, não há regra segura,
e a decisão errada perde informação. A pergunta mostra as duas versões com data e
dispositivo de origem, e permite manter ambas (criando uma cópia) como saída segura.

## 7. Registro

Todo conflito resolvido gera evento observável (tipo, entidade, estratégia aplicada),
**sem conteúdo sensível**. Taxa de conflito é métrica de saúde do sync.
