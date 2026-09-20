---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0005, ADR-0006
---

# Portabilidade da API

## 1. Objetivo

A API precisa poder sair da hospedagem inicial (Vercel) sem reescrita de domínio,
sem mudança de contrato público e sem migração de dados (R-034, R-063).

## 2. Regras de portabilidade

| # | Regra |
|---|-------|
| 1 | Nenhum recurso proprietário da plataforma aparece no contrato público |
| 2 | A aplicação é um processo HTTP padrão, empacotável em container |
| 3 | Nada depende de sistema de arquivos efêmero da plataforma |
| 4 | Trabalho longo vai para fila, nunca para o request |
| 5 | Configuração vem de variáveis de ambiente validadas |
| 6 | Logs vão para saída padrão em formato estruturado |
| 7 | Nenhum estado em memória entre requisições (sessão, cache crítico, contador) |
| 8 | Roteamento definido pela aplicação, não por convenção de pastas da plataforma |
| 9 | Agendamentos declarados pela aplicação e trocáveis |
| 10 | Nenhum SDK da plataforma dentro de domínio ou aplicação |

## 3. Framework

A escolha do framework (ADR-0006) é avaliada, entre outros critérios, por:

- rodar tanto em ambiente serverless quanto em container/Node padrão;
- não exigir estrutura de pastas específica de uma plataforma;
- gerar OpenAPI a partir do mesmo esquema da validação;
- ter testes rápidos sem emulador de plataforma;
- ter comunidade e manutenção ativas.

Candidatos: Hono, Fastify, ou outro justificado. Nenhum foi avaliado com medição nesta
missão — ver Q-006.

## 4. Banco

- SQL padrão + PostGIS; nada específico de um fornecedor gerenciado.
- Migrações versionadas, reversíveis e executáveis fora da plataforma.
- Conexão por variável de ambiente; pooling configurável conforme o modelo de execução.
- Nenhuma regra de acesso do produto delegada a recurso do banco gerenciado em substituição
  à autorização da API.

## 5. Teste de saída

Antes do freeze de `F6`, responder:

1. O que é preciso para rodar a API em container em outro provedor?
2. Quais serviços da plataforma atual estão em uso e por quais ports estão isolados?
3. Quanto tempo e qual indisponibilidade a migração exigiria?
4. Há dado que só existe na plataforma atual?
5. Os jobs continuam funcionando fora dela?

Resposta ausente vira item em `OPEN-QUESTIONS.md`.

## 6. Sinais de alerta

- Código de domínio importando algo da plataforma.
- Endpoint que só funciona por causa de um comportamento específico do runtime.
- Job que depende do agendador proprietário sem abstração.
- Limite de execução contornado com truque em vez de fila.
- Configuração hardcoded para um ambiente da plataforma.

Qualquer um desses é falha do `API-PORTABILITY-GATE`.
