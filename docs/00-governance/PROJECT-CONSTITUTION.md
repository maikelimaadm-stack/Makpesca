---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0003, ADR-0011, ADR-0012
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

O aplicativo móvel deve funcionar sem rede para: consultar mapa de região baixada,
obter posição GPS, criar ponto, registrar captura, anexar foto, reabrir o app e
encontrar tudo preservado. Sincronizar é consequência, não pré-requisito.

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
