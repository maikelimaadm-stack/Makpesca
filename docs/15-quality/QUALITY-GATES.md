---
Status: DRAFT
Version: 0.2.0
Last Updated: 2026-09-21
Owners: Maike Lima (autoridade humana final)
Related ADRs: todos
Lifecycle: LIVING
---

# Gates de Qualidade

**Falha de gate bloqueia.** Não existe liberação informal, exceção pontual ou
"passa mesmo assim". Liberar um gate exige decisão registrada em
`../00-governance/DECISION-REGISTRY.md`.

## 0. Vocabulário de estado (fechado)

Um gate tem **exatamente um** destes estados. Estados compostos como
"PASS (parcial)" ou "PASS (documental)" são **proibidos**: escondem se o gate
está satisfeito ou não.

| Estado | Significado |
|--------|-------------|
| `PASS` | Verificado e satisfeito para o escopo avaliado |
| `FAIL` | Verificado e reprovado; há defeito concreto a corrigir |
| `BLOCKED` | Não pode ser avaliado ou satisfeito por dependência externa em aberto |
| `PENDING` | Ainda não avaliado, ou avaliável apenas quando houver o artefato (ex.: código) |
| `NOT-APPLICABLE` | Não se aplica ao escopo avaliado |

**Aprovação humana não é estado de gate.** É registrada à parte, como
`HUMAN APPROVAL = PENDING | GRANTED`, com data e autoridade.

Todo gate declara também o seu **escopo de avaliação**: o gate pode estar `PASS`
para uma tranche e `BLOCKED` para outra. Ver §12 (`COST-GATE`) e §15.

## Estado atual dos gates

Escopo avaliado: **documentação MP-DOC-00 / candidatura de F0**. Não há código.

| Gate | Estado | Escopo | Motivo |
|------|--------|--------|--------|
| `DOC-CONSISTENCY` | **PENDING** | docs/ | Correções da rodada R1 aplicadas; vira `PASS` só após auditoria semântica final |
| `ARCH-CONSISTENCY` | **PENDING** | código | Fronteiras definidas, mas não há código para verificar |
| `DOMAIN-CONSISTENCY` | **PENDING** | código | Entidades e invariantes definidas; sem testes que as provem |
| `PRIVACY-GATE` | **PENDING** | código | Modelo definido; sem implementação nem testes |
| `OFFLINE-GATE` | **PENDING** | código | Contrato definido; sem implementação nem testes |
| `MAP-LICENSE-GATE` | **BLOCKED** | basemap offline (F5) | ADR-0010 `OPEN`; licenças não verificadas (Q-004, Q-005) |
| `API-PORTABILITY-GATE` | **PENDING** | API (F6) | Regras definidas; framework não decidido (Q-006) |
| `SECURITY-GATE` | **PENDING** | código | Baseline definido; sem implementação |
| `SOCIAL-SAFETY-GATE` | **PENDING** | social (F7) | Moderação definida; sem ferramentas |
| `COMMERCE-GATE` | **PENDING** | comércio (F8) | Regras definidas; modelo comercial aberto (Q-019) |
| `AFFILIATE-FRAUD-GATE` | **PENDING** | afiliados (F8) | Controles definidos; sem implementação |
| `COST-GATE` | **por escopo** | ver §12 | `BLOCKED` para F5/F8; `PENDING` para o núcleo; nunca global |
| `OPERABILITY-GATE` | **PENDING** | operação (F9) | Runbooks a escrever |
| `IMPLEMENTATION-READY-GATE` | **BLOCKED** | implementação | Ver §14 |

`HUMAN APPROVAL` (MP-DOC-00 / F0) = **PENDING** — autoridade: Maike Lima.

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

## 12. COST-GATE (scope-aware)

**Princípio:** custo desconhecido bloqueia **o que depende dele**, não o projeto inteiro.
Um custo de billing não verificado não pode impedir a marcação de um ponto offline.

**Regra de avaliação:** o gate é avaliado **por tranche** (onda ou slice). Para liberar
uma tranche, verificam-se apenas os providers e capacidades que **aquela tranche e o MVP
aprovado** efetivamente usam.

**Verifica, para cada provider no escopo da tranche:** custo unitário com **fonte e data**,
projeção por usuário ativo, teto e alerta configurados.
**Falha se:** a tranche depende de um provider cujo custo é desconhecido.
**Não falha por:** custo desconhecido de provider que a tranche não usa.

### Mapa de escopo

| Escopo | Providers avaliados | Estado atual | Bloqueia |
|--------|--------------------|--------------|----------|
| Núcleo (conta, ponto, captura, offline core, sync, mídia) | Banco, hospedagem da API, object storage | **PENDING** | MP-00..MP-12 |
| Mapa online (F5) | Provider de mapa online | **PENDING** | MP-06 |
| Basemap offline (F5) | Solução de mapa offline | **BLOCKED** (Q-004, Q-005) | MP-17 apenas |
| Social (F7) | Push, storage adicional | **PENDING** | MP-13..MP-18 |
| Billing / PRO (F8) | Lojas, agregador | **BLOCKED** (Q-010) | MP-19 apenas |
| Dados ambientais (F5/F8) | APIs ambientais | **BLOCKED** (Q-013) | MP-28, MP-29 apenas |
| Afiliados (F8) | — | **PENDING** (Q-019) | MP-20, MP-21 apenas |

Consequência explícita: **o `COST-GATE` do basemap offline, do billing e dos dados
ambientais não bloqueia o núcleo.** Nenhum desses providers entra na primeira tranche.

**O que continua valendo:** nenhum custo é ignorado. Cada escopo `BLOCKED` permanece
registrado em `../00-governance/OPEN-QUESTIONS.md` e bloqueia a sua própria onda/slice até
ser verificado com fonte e data.

## 13. OPERABILITY-GATE

**Verifica:** runbooks essenciais escritos e testados; backup com restore testado;
alertas definidos com destinatário; owners nomeados; kill switch funcionando.
**Falha se:** não houver quem responda a um incidente, ou o restore nunca tiver sido testado.
**Nota:** a autoridade humana final está definida (Maike Lima, ver
`../00-governance/PROJECT-CONSTITUTION.md` Art. 15). Faltam os runbooks e o teste de restore.

## 14. IMPLEMENTATION-READY-GATE

**Estado: BLOCKED.**

Este gate também é **scope-aware**: ele libera **a primeira tranche de implementação**, não
o produto inteiro. Cada tranche posterior é reavaliada.

Condições para liberar a **primeira tranche** (núcleo: conta, ponto, captura, offline core,
sync, geo-privacy):

| # | Condição | Estado |
|---|----------|--------|
| 1 | Ondas `F0`..`F4` e `F6` congeladas | Não — nenhuma congelada |
| 2 | Nenhum item `BLOCKING` aberto **nessas** ondas | Não (Q-006, Q-007, Q-008) |
| 3 | ADRs **dessas** ondas em `ACCEPTED` ou `REJECTED` | Não — ADR-0006, ADR-0007, ADR-0008 `OPEN` |
| 4 | `COST-GATE` do escopo do núcleo verificado | Não |
| 5 | Autoridade humana definida | **Sim** — Maike Lima (Q-001 resolvida) |
| 6 | Auditoria humana do MP-DOC-00 concluída | Não — `HUMAN APPROVAL = PENDING` |
| 7 | Slices do núcleo com critérios de aceite | Parcial |

**Fora do escopo da primeira tranche** (não a bloqueiam, mas bloqueiam as suas próprias):

| Item | Bloqueia |
|------|----------|
| `MAP-LICENSE-GATE` / ADR-0010 (Q-004, Q-005) | MP-17 e a onda F5 do basemap |
| ADR-0014 / billing (Q-010) | MP-19 e a onda F8 |
| ADR-0019 / mensageria (Q-012) | MP-23 e a onda F7 |
| ADR-0015, ADR-0016 (jobs, observabilidade) | MP-11 em diante — a reavaliar por tranche |
| Dados ambientais (Q-013) | MP-28, MP-29 |

Total de ADRs abertos no projeto: **8**. Destes, **3** (ADR-0006, ADR-0007, ADR-0008)
bloqueiam a primeira tranche; os demais bloqueiam apenas as suas ondas.

**Enquanto este gate estiver BLOCKED, implementação de produto é proibida.**

## 15. Regra de reprodução de estado

Estados de gate e contagens exibidos aqui são **derivados**. Antes de reproduzi-los em
relatório, PR ou resumo, recalcule-os a partir do SSOT correspondente
(`../00-governance/DECISION-REGISTRY.md`, `OPEN-QUESTIONS.md`, `DOCUMENT-STATUS.md` e os
próprios arquivos de ADR). Ver `../00-governance/DECISION-POLICY.md` §8.
