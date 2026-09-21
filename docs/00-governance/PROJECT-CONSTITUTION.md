---
Status: REVIEW
Version: 0.2.0
Last Updated: 2026-09-21
Owners: Maike Lima (autoridade humana final)
Related ADRs: ADR-0003, ADR-0011, ADR-0012
Wave: F0
Lifecycle: FREEZE-CONTROLLED
---

# Constituição do Projeto MAKPESCA

Regras estruturais do projeto. São as regras mais caras de mudar: alterar qualquer
artigo exige ADR de superseção aprovado e registro em `DECISION-REGISTRY.md`.

## Artigo 1 — Ordem de trabalho

```
DOCUMENTAR → AUDITAR → CORRIGIR → CONGELAR POR ONDAS → DEFINIR SLICES
          → IMPLEMENTAR → TESTAR → CERTIFICAR → LANÇAR
```

Nenhuma etapa pode ser pulada. Implementação sem documentação congelada da onda
correspondente é violação constitucional.

## Artigo 2 — API é a única fronteira de negócio

Mobile, Web, Admin e Portal de Parceiros **nunca** falam com PostgreSQL/Supabase
diretamente para regra de negócio, leitura sensível ou escrita de domínio.

```
CLIENTES → api.makpesca.com.br → Application/Domain → Ports/Adapters → Infraestrutura
```

Consequência prática: não existe "atalho" de client SDK para tabela.

## Artigo 3 — Geo-privacy é server-side

Coordenada exata de ponto privado ou restrito **nunca** sai da API para um cliente
sem autorização. Esconder no frontend não é privacidade. A degradação de precisão
acontece no servidor, antes da serialização da resposta.

## Artigo 4 — Offline-first é contrato, não otimização

O **OFFLINE APP CORE** é constitucional. O aplicativo móvel deve, sem rede:

1. abrir;
2. acessar os dados locais do usuário;
3. obter posição por GPS, conforme a capacidade do aparelho e a permissão concedida;
4. criar e editar ponto;
5. registrar captura;
6. anexar mídia;
7. fechar e reabrir sem perda;
8. garantir que toda operação aceita é durável;
9. sincronizar quando a rede retornar;
10. reenviar sem duplicar;
11. tratar conflitos de forma definida.

Sincronizar é consequência, não pré-requisito.

### Artigo 4-A — Base cartográfica offline **não** é matéria constitucional

O **OFFLINE CARTOGRAPHIC BASEMAP** (a base de mapa exibível sem rede) é uma
**decisão separada e ainda aberta**: depende de ADR-0010, do `MAP-LICENSE-GATE` e da
onda F5.

Consequências obrigatórias:

- o basemap offline **não é promessa contratual** enquanto ADR-0010 estiver `OPEN`;
- nenhum documento de F0/F1 pode tratá-lo como garantia;
- o produto **não pode anunciá-lo** antes da decisão;
- se não houver solução legal e viável, o **OFFLINE APP CORE continua valendo
  integralmente**, operando sem base cartográfica detalhada.

"Offline real" permanece diferencial do produto — e refere-se ao **core**, não ao basemap.

## Artigo 5 — Sincronização é idempotente

Toda escrita sincronizável usa identificador gerado no cliente e chave de idempotência.
Repetir a operação não duplica. Falha parcial não corrompe.

## Artigo 6 — Domínio é independente de provider

O núcleo de domínio não importa SDK de Supabase, Google, provedor de billing, storage
ou autenticação. Providers entram por portas e adaptadores.

## Artigo 7 — Portabilidade

Supabase e Vercel são infraestrutura inicial, não arquitetura. O projeto deve poder
sair de ambos sem reescrever domínio. Toda decisão de provider registra custo de saída.

## Artigo 8 — Decisões vivem em ADRs

Decisão relevante (stack, provider, protocolo, modelo de dados estrutural, política de
privacidade) exige ADR. Decisão não registrada não existe.

## Artigo 9 — FROZEN não muda silenciosamente

Documento congelado só muda por superseção explícita, com rastro.

## Artigo 10 — Gates bloqueiam

Falha de gate bloqueia. Não existe liberação informal.

Gate é avaliado **por escopo**: um gate pode estar satisfeito para uma tranche e
bloqueado para outra. Um custo, licença ou decisão em aberto bloqueia **o que depende
dele**, não o projeto inteiro. Ver `../15-quality/QUALITY-GATES.md` §0 e §12.

## Artigo 11 — Sem invenção

Dado externo (preço, licença, limite de plano, termo de uso) exige fonte e data de
consulta. Sem isso, o item é `NEEDS-DECISION` e permanece aberto.

## Artigo 12 — Simplicidade

Overengineering é defeito. Abstração só se justifica por risco real de portabilidade,
privacidade, segurança ou custo documentado.

## Artigo 13 — Dados sensíveis

Localização exata de pescador e de ponto privado é dado de sensibilidade elevada.
Recebem tratamento de segurança equivalente a credencial: não vazam em log, analytics,
crash report, URL, push, cache ou export não autorizado.

## Artigo 14 — Estado atual

`IMPLEMENTATION-READY-GATE` = **BLOCKED**. Implementação de produto é proibida até
liberação formal registrada em `DECISION-REGISTRY.md`.

## Artigo 15 — Autoridade e ownership (SSOT)

Este artigo é o **SSOT de ownership** do projeto.

| Papel | Responsável |
|-------|-------------|
| **Product Owner / Final Decision Authority** | **Maike Lima** |
| Autoridade humana final de arquitetura e governança | **Maike Lima**, até delegação formal |

Regras:

1. **Maike Lima** é a autoridade humana final para decisões de produto, arquitetura e
   governança, incluindo congelar ondas, aceitar ADRs e liberar gates.
2. Delegação de qualquer parte dessa autoridade só vale se **registrada** em
   `DECISION-REGISTRY.md`, com data e escopo.
3. **Agentes de IA são executores e revisores — nunca owners finais.** Um agente pode
   propor, auditar, documentar e apontar bloqueios; não pode aceitar ADR, congelar onda,
   liberar gate, aprovar PR, mergear nem decidir por conta própria.
4. Um artefato cujo congelamento está em jogo **não pode ficar sem owner**. Documentos
   fora do conjunto de congelamento da onda podem manter `Owners: (a definir)` até serem
   incluídos em uma onda.
5. Aprovação humana é registrada separadamente dos gates, como
   `HUMAN APPROVAL = PENDING | GRANTED`, com data e autoridade.
