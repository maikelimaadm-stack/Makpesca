---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: todos
---

# Gates de Qualidade

**Falha de gate bloqueia.** Não existe liberação informal, exceção pontual ou
"passa mesmo assim". Liberar um gate exige decisão registrada em
`../00-governance/DECISION-REGISTRY.md`.

## Estado atual dos gates

| Gate | Estado | Motivo |
|------|--------|--------|
| `DOC-CONSISTENCY` | **PASS (parcial)** | Documentação criada e internamente referenciada; auditoria humana pendente |
| `ARCH-CONSISTENCY` | **PASS (documental)** | Sem código para verificar; fronteiras definidas |
| `DOMAIN-CONSISTENCY` | **PASS (documental)** | Entidades e invariantes definidas |
| `PRIVACY-GATE` | **PENDING** | Modelo definido; sem implementação nem testes |
| `OFFLINE-GATE` | **PENDING** | Contrato definido; sem implementação nem testes |
| `MAP-LICENSE-GATE` | **BLOCKED** | ADR-0010 aberto; licenças não verificadas (Q-004, Q-005) |
| `API-PORTABILITY-GATE` | **PENDING** | Regras definidas; framework não decidido (Q-006) |
| `SECURITY-GATE` | **PENDING** | Baseline definido; sem implementação |
| `SOCIAL-SAFETY-GATE` | **PENDING** | Moderação definida; sem ferramentas |
| `COMMERCE-GATE` | **PENDING** | Regras definidas; modelo comercial aberto (Q-019) |
| `AFFILIATE-FRAUD-GATE` | **PENDING** | Controles definidos; sem implementação |
| `COST-GATE` | **BLOCKED** | Nenhum custo verificado com fonte (mapas, mídia, billing) |
| `OPERABILITY-GATE` | **PENDING** | Runbooks a escrever; owners indefinidos (Q-001) |
| `IMPLEMENTATION-READY-GATE` | **BLOCKED** | Depende de todos acima |

---

## 1. DOC-CONSISTENCY

**Verifica:** links válidos, SSOT único por assunto, ausência de contradição entre
documentos, cabeçalhos de status presentes, termos conforme o glossário.
**Falha se:** dois documentos afirmam coisas incompatíveis, ou um assunto tem dois SSOTs.

## 2. ARCH-CONSISTENCY

**Verifica:** cliente não acessa banco; domínio sem SDK; DTO ≠ ORM; dependências entre
pacotes respeitadas; adapters sem regra de negócio.
**Falha se:** qualquer fronteira do `COMPONENT-BOUNDARIES` for atravessada.

## 3. DOMAIN-CONSISTENCY

**Verifica:** entidades documentadas conferem com o uso; invariantes com teste;
linguagem do glossário aplicada; tradução entre contextos explícita.
**Falha se:** invariante sem teste (quando houver código) ou entidade usada sem definição.

## 4. PRIVACY-GATE

**Verifica:** toda serialização de localização passa pelo Geo Privacy Service; matriz de
`PRIVACY-TEST-MATRIX.md` passando; nenhuma coordenada em log/analytics/crash/URL/push;
EXIF removido; cache com perfil na chave.
**Falha se:** um único caso da matriz falhar.
**Este gate nunca é dispensado.**

## 5. OFFLINE-GATE

**Verifica:** matriz de `OFFLINE-TEST-MATRIX.md` passando; cenário de referência completo;
idempotência comprovada; nenhuma perda de dados.
**Falha se:** houver duplicação, perda ou fila travada sem visibilidade.

## 6. MAP-LICENSE-GATE

**Verifica:** para cada uso cartográfico, existe base legal documentada com fonte e data;
uso offline coberto por licença explícita; atribuição implementada.
**Falha se:** qualquer célula de `../06-maps-location/MAP-PROVIDER-MATRIX.md` relevante
estiver como `A VERIFICAR`.
**Estado: BLOCKED.**

## 7. API-PORTABILITY-GATE

**Verifica:** nenhum recurso proprietário da hospedagem no contrato; aplicação
empacotável; jobs fora do request; configuração por ambiente; teste de saída respondido.
**Falha se:** a API só funcionar na plataforma atual.

## 8. SECURITY-GATE

**Verifica:** baseline de `../08-security-privacy/SECURITY-BASELINE.md` atendido; testes
de autorização negativa; sem secrets no repositório; dependências auditadas; ameaças do
recurso novo analisadas.
**Falha se:** qualquer item obrigatório do baseline estiver ausente.

## 9. SOCIAL-SAFETY-GATE

**Verifica:** todo recurso social tem denúncia, bloqueio e caminho de moderação; limites
anti-spam; capacidade de moderação compatível com o alcance do recurso.
**Falha se:** recurso social for lançado sem ferramenta de abuso.

## 10. COMMERCE-GATE

**Verifica:** ofertas com validade e condições; conteúdo patrocinado rotulado; isolamento
entre parceiros; nenhum dado de usuário exposto a parceiro; casos de
`COMMERCE-TEST-MATRIX.md` passando.
**Falha se:** parceiro puder acessar dado que não é dele.

## 11. AFFILIATE-FRAUD-GATE

**Verifica:** idempotência de click e conversão; unicidade `(parceiro, pedido)`; janela de
atribuição explícita; antifraude antes da aprovação; conciliação antes do payout;
log imutável.
**Falha se:** for possível gerar comissão duplicada ou pagar sem conciliação.

## 12. COST-GATE

**Verifica:** custo unitário conhecido, com fonte e data, para mapa, mídia, banco,
hospedagem, dados ambientais e billing; projeção por usuário ativo; teto e alerta
configurados.
**Falha se:** houver recurso em produção com custo desconhecido.
**Estado: BLOCKED** — nenhum custo foi verificado.

## 13. OPERABILITY-GATE

**Verifica:** runbooks essenciais escritos e testados; backup com restore testado;
alertas definidos com destinatário; owners nomeados; kill switch funcionando.
**Falha se:** não houver quem responda a um incidente, ou o restore nunca tiver sido testado.

## 14. IMPLEMENTATION-READY-GATE

**Estado: BLOCKED.**

Só é liberado quando **todos** os itens abaixo forem verdadeiros:

| # | Condição | Estado |
|---|----------|--------|
| 1 | Ondas `F0`..`F6` congeladas | Não |
| 2 | Nenhum item `BLOCKING` aberto nessas ondas | Não (Q-001, Q-004, Q-005) |
| 3 | ADRs das ondas em `ACCEPTED` ou `REJECTED` | Não (7 ADRs `OPEN`) |
| 4 | `MAP-LICENSE-GATE` resolvido ou escopo ajustado para não depender dele | Não |
| 5 | `COST-GATE` com custos verificados | Não |
| 6 | Owners nomeados | Não |
| 7 | Auditoria humana do MP-DOC-00 concluída | Não |
| 8 | Slices definidos com critérios de aceite | Parcial |

**Enquanto este gate estiver BLOCKED, implementação de produto é proibida.**
