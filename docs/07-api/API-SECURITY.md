---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0008
---

# Segurança da API

## 1. Autenticação

| Regra |
|-------|
| Toda rota exige autenticação, salvo lista explícita de rotas públicas |
| Token de acesso de vida curta + refresh de vida longa e revogável |
| Refresh armazenado no keystore/keychain do dispositivo, nunca em storage comum |
| Revogação de sessão tem efeito imediato no servidor |
| Rotação de refresh a cada uso, com detecção de reutilização (indício de roubo) |
| Falha de autenticação não distingue "usuário inexistente" de "senha errada" |

## 2. Autorização

| Regra |
|-------|
| Verificação por objeto em **todo** acesso (INV-A01) |
| Identificador na rota nunca implica permissão (IDOR/BOLA — R-010) |
| Autorização acontece no domínio/aplicação, não apenas na borda |
| Escopos separados: usuário, admin, parceiro, sistema |
| Parceiro só acessa dados do próprio parceiro |
| Admin exige privilégio explícito + auditoria |
| Negação sensível responde 404 (ver `API-ERROR-CONTRACT.md` §3) |

## 3. Validação de entrada

- Esquema estrito por endpoint; campos desconhecidos rejeitados.
- Limites de tamanho por campo e por requisição.
- Rejeição de tipos inesperados (evita coerção implícita).
- Sanitização de texto exibido (defesa contra injeção no cliente web).
- Consultas ao banco sempre parametrizadas — concatenação de SQL é proibida.
- Consultas geográficas com limite de área para evitar varredura da base.

## 4. Rate limiting e abuso

| Alvo | Limite |
|------|--------|
| Autenticação | Rígido, por IP e por conta |
| Criação de conteúdo | Por usuário e por janela |
| Listagens públicas | Por usuário e por IP (anti-scraping — R-014) |
| Sync | Por dispositivo, com backpressure |
| Upload de mídia | Por usuário, por tamanho acumulado |
| Endpoints de parceiro | Por parceiro |
| Webhooks recebidos | Por origem, com verificação de assinatura |

Resposta 429 informa quando tentar novamente. O cliente respeita.

## 5. Transporte

- HTTPS obrigatório; sem exceção, sem fallback.
- HSTS no domínio da API.
- Considerar fixação de certificado no app móvel (decisão a avaliar: aumenta segurança,
  aumenta risco operacional).

## 6. Cabeçalhos e CORS

- CORS restrito às origens dos nossos apps web.
- Sem `*` em produção.
- Cabeçalhos de segurança padrão nas respostas de conteúdo web.

## 7. Uploads

| Regra |
|-------|
| Upload sempre autorizado por ticket emitido pela API |
| Validação de tipo real do arquivo, não apenas da extensão |
| Limite de tamanho aplicado no ticket |
| Processamento isolado do restante do sistema |
| Nome de objeto opaco, não adivinhável |
| Leitura de mídia privada por URL autenticada e expirável |

## 8. Webhooks recebidos

- Assinatura verificada antes de qualquer processamento.
- Idempotência por identificador do evento (R-051).
- Processamento assíncrono: responder rápido, processar depois.
- Replay antigo rejeitado por janela de tempo.
- Origem restrita quando o provider permitir.

## 9. Segredos

Nenhum segredo no cliente. Chave de provider de mapa no cliente é inevitável em alguns
casos — nesse caso, restringir por aplicativo/origem e monitorar uso.
Ver `../08-security-privacy/SECRETS-POLICY.md`.

## 10. Privacidade na API

| Regra |
|-------|
| Nenhuma resposta serializa localização sem o Geo Privacy Service |
| Nenhuma coordenada em query string, path, redirect ou push |
| Cache de resposta com localização tem o perfil do observador na chave (INV-G07) |
| Logs sem corpo de requisição de rotas sensíveis |
| `requestId` para suporte, sem dado pessoal |

## 11. Observabilidade de segurança

Eventos a registrar: falhas de autenticação em sequência, uso de refresh reutilizado,
negações de autorização repetidas no mesmo recurso, 429 recorrente, upload rejeitado,
acesso administrativo a dado C4.
