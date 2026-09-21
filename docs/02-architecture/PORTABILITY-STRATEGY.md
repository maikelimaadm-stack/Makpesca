---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0004, ADR-0005, ADR-0008, ADR-0013
---

# Estratégia de Portabilidade

## 1. Princípio

Supabase, Vercel e Google são **infraestrutura inicial**, não arquitetura. O projeto
precisa poder sair de cada um sem reescrever domínio. Portabilidade não é gratuita —
por isso é limitada ao que tem risco real.

## 2. Nível de abstração por provider

| Provider | Abstração | Justificativa |
|----------|-----------|---------------|
| PostgreSQL | **Baixa** — usamos SQL/PostGIS à vontade | Postgres é padrão e portátil entre hospedagens |
| Supabase (como hospedagem de Postgres) | **Alta** — nada específico do produto Supabase no domínio | Trocar hospedagem sem trocar banco |
| Supabase Auth (se escolhido) | **Alta** — atrás de `AuthPort` | Migração de identidade é o risco mais caro |
| Vercel | **Alta** — a API não depende de APIs proprietárias de runtime | Limites de plataforma e custo |
| Object Storage | **Alta** — `MediaStoragePort` | Egress e custo variam muito |
| Mapa online | **Média** — camada de mapa isolada no cliente | SDKs diferem bastante |
| Mapa offline | **Alta** — decisão ainda aberta | Não pode contaminar o produto |
| Billing | **Alta** — `BillingPort` + Entitlement Service próprio | Fonte de verdade de acesso é nossa |
| Dados ambientais | **Alta** — `EnvironmentalDataPort` | Fontes mudam, licenças mudam |
| Observabilidade | **Média** — logging estruturado próprio | Formato é nosso; destino é trocável |
| Push | **Alta** — `PushPort` | — |

## 3. O que nunca é específico de provider

1. Identificadores de domínio (UUID gerados por nós, não pelo provider).
2. Modelo de dados de negócio.
3. Regras de privacidade e autorização.
4. Contrato de API pública.
5. Protocolo de sincronização.
6. Formato de log estruturado.

## 4. Custo de saída (a manter atualizado)

| Saída | Custo estimado | Principal obstáculo |
|-------|----------------|---------------------|
| Trocar hospedagem do Postgres | Médio | Migração de dados + janela de indisponibilidade |
| Sair da Vercel | Médio | Empacotamento, jobs, variáveis, domínios |
| Trocar provider de auth | **Alto** | Credenciais, refresh tokens, identidades federadas |
| Trocar object storage | Médio-alto | Volume de arquivos + egress + reescrita de referências |
| Trocar provider de mapa online | Médio | Reescrita da camada de mapa nos clientes |
| Trocar solução de billing | Alto | Assinaturas ativas e reconciliação |

Nenhum número foi verificado. Valores são qualitativos até haver medição.

## 5. Teste de portabilidade

Antes de congelar a onda `F2`, a documentação deve responder, para cada provider:

1. Qual port o isola?
2. O que quebraria se ele sumisse amanhã?
3. Quanto tempo levaria a substituição?
4. Há dado que só existe lá?

Se alguma resposta for "não sei", o item vai para `OPEN-QUESTIONS.md`.

## 6. Antipadrões proibidos

- Usar recurso proprietário do banco gerenciado (ex.: regras de acesso no client SDK)
  como substituto de autorização na API.
- Guardar arquivo em coluna de banco.
- Identificador de usuário emitido pelo provider como chave primária de domínio.
- Lógica de negócio em função serverless específica de plataforma.
- Cache de tiles de provider proprietário fora do que a licença permite.
