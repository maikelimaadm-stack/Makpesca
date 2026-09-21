---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: —
---

# Política de Segredos

## 1. Regra zero

**Nenhum segredo entra no repositório.** Nem em código, nem em documentação, nem em
exemplo, nem em teste, nem em histórico do Git.

## 2. O que é segredo

Chaves de API, tokens de serviço, credenciais de banco, chaves de assinatura, webhooks
secrets, chaves de push, credenciais de loja de aplicativos, chaves de cofre, certificados
privados, sementes de jitter do Geo Privacy Service.

## 3. Onde vivem

| Contexto | Local |
|----------|-------|
| Desenvolvimento local | Arquivo local ignorado pelo Git, com valores de desenvolvimento |
| CI | Cofre de segredos da plataforma de CI |
| Ambientes de execução | Variáveis de ambiente injetadas pela plataforma / cofre |
| Dispositivo do usuário | Keystore/Keychain do sistema operacional |
| Documentação | **Nunca** — apenas o nome da variável |

## 4. No repositório entra apenas

- nomes de variáveis;
- arquivo de exemplo sem valores reais;
- descrição do que cada variável faz e quem a fornece.

## 5. Rotação

| Situação | Prazo |
|----------|-------|
| Suspeita de exposição | Imediato |
| Saída de pessoa com acesso | Imediato |
| Rotina | Periódica, definida por tipo de credencial |
| Após incidente | Obrigatória, com registro |

## 6. Chaves no cliente

Algumas chaves precisam ir para o aplicativo (ex.: chave de SDK de mapa). Tratamento:

1. tratar como **pública** — presuma que será extraída;
2. restringir por aplicativo, pacote/bundle, origem e API habilitada;
3. monitorar uso e definir alerta de consumo anômalo;
4. nunca usar a mesma chave para servidor e cliente;
5. nunca colocar no cliente chave que permita escrita ou leitura de dados de usuário.

## 7. Detecção

- Varredura de segredos no repositório (histórico incluído) antes do primeiro código.
- Verificação automática em CI, bloqueando o merge quando detectar padrão de segredo.
- Revisão manual em PR que toque em configuração.

## 8. Se um segredo vazar

1. rotacionar imediatamente;
2. revogar o segredo antigo;
3. avaliar o que pode ter sido acessado com ele;
4. registrar incidente (`INCIDENT-RESPONSE.md`);
5. remover do histórico quando aplicável — **sabendo que remover do histórico não
   substitui a rotação**;
6. revisar por que entrou.

## 9. Segredos de privacidade

A semente usada na degradação determinística de coordenadas (jitter estável) é **segredo
crítico**: se vazar, permite recalcular o deslocamento e recuperar coordenadas reais a
partir de dados aproximados. Rotacioná-la muda todos os valores aproximados publicados —
por isso, rotação exige plano específico.
