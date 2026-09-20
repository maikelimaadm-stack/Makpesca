---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0009, ADR-0010
---

# Estratégia de Mapa Online e Offline

## 1. Regra central

> **Mapa online e mapa offline são decisões separadas.**
> Escolher o Google para online **não** autoriza usar dados do Google offline.

Assumir que "já que usamos X online, podemos cachear X offline" é o erro mais caro
possível aqui: pode violar termos de uso e inviabilizar o recurso central do produto
depois de construído (R-030).

## 2. Online

| Item | Estado |
|------|--------|
| Candidato preferencial | Google Maps Platform (ADR-0009, `PROPOSED`) |
| Motivo | Qualidade de base, cobertura no Brasil, satélite, maturidade de SDK |
| Riscos | Custo por uso (R-031), lock-in (R-033), restrição de cache |
| Mitigação | Camada de mapa isolada; dados do produto independentes |

## 3. Offline

| Item | Estado |
|------|--------|
| Decisão | **ABERTA** — ADR-0010 |
| Restrição dura | Não assumir download/cache permanente de tiles de provider proprietário |
| Necessidade | Download por região, funcionamento sem rede, atualização, tamanho controlado |
| Bloqueia | Onda `F5` e o recurso "mapas offline" do MVP/PRO |

### O que precisa ser respondido antes de decidir

1. Qual solução permite, **por licença escrita**, armazenar e usar dados cartográficos
   offline no aplicativo? (com citação e data)
2. Qual o custo por região/por usuário/por atualização?
3. Qual a qualidade da base no Brasil, especialmente hidrografia?
4. Há imagem de satélite offline? Sob qual licença?
5. Qual o tamanho em disco por região típica?
6. Funciona em React Native para Android e iOS com manutenção ativa?
7. Qual a atribuição obrigatória na interface?
8. Como atualizar uma região já baixada?

## 4. Candidatos a avaliar

Ver `MAP-PROVIDER-MATRIX.md`. Em linhas gerais, o espaço de solução inclui: renderizador
open-source com dados compatíveis com OSM, serviços de tiles com licença de uso offline
explícita, formatos de pacote de tiles e combinações (base offline + satélite online).

**Nenhum deles foi verificado nesta missão.** Toda avaliação exige fonte e data.

## 5. Modelo híbrido (hipótese de trabalho)

Hipótese a validar, não decisão:

| Situação | Base cartográfica |
|----------|-------------------|
| Com rede | Provider online (melhor qualidade, satélite) |
| Sem rede, região baixada | Pacote offline licenciado |
| Sem rede, região não baixada | Estado vazio explícito + dados do produto ainda funcionam |

Nesse modelo, a interface precisa deixar claro qual base está em uso, porque a aparência
muda.

## 6. Regiões offline

| Aspecto | Definição proposta |
|---------|--------------------|
| Unidade | Polígono/área escolhida pelo usuário, com tamanho máximo |
| Limite FREE | Número reduzido de regiões (valor a definir) |
| Limite PRO | Maior número/área (valor a definir) |
| Atualização | Manual, com indicação de dados desatualizados |
| Armazenamento | Exibido ao usuário, removível |
| Expiração | Depende da licença do provider escolhido |

## 7. O que nunca fazemos

- Cachear tiles além do que a licença permite.
- Redistribuir tiles entre usuários.
- Extrair dados de um provider para montar base própria sem direito.
- Prometer "mapa offline" na loja de aplicativos antes de ADR-0010 estar `ACCEPTED`.

## 8. Estado do gate

`MAP-LICENSE-GATE` = **BLOCKED** enquanto ADR-0010 estiver `OPEN`.
