# ADR-0013 — Armazenamento de Mídia

- **Status:** PROPOSED
- **Date:** 2026-09-20
- **Onda:** F3

## Context
Capturas têm fotos; perfis e lojas têm imagens. Mídia é volumosa, cara em armazenamento e
egress, e precisa de upload retomável a partir de conexões ruins.

## Decision Drivers
- Nunca guardar imagem no banco relacional.
- Upload retomável e autorizado pela API.
- Custo de armazenamento e, sobretudo, de **egress**.
- Processamento assíncrono (EXIF, derivativos).
- URLs privadas autenticadas e expiráveis.
- Portabilidade (migrar arquivos depois é caro).

## Options Considered
| Opção | Prós esperados | Contras esperados |
|-------|----------------|-------------------|
| Supabase Storage | Integrado ao provider já previsto | Custo e limites a verificar; acoplamento |
| Cloudflare R2 | Egress historicamente favorável — **a verificar** | Mais um provider na conta |
| Amazon S3 (ou compatível) | Padrão de mercado, ecossistema | Custo de egress a verificar |
| Outro compatível com S3 | Flexibilidade | A avaliar |

**Nenhum preço foi verificado nesta missão.**

## Decision
Adotar **object storage atrás de `MediaStoragePort`**, com o provider específico em aberto
(Q-009). A decisão que **é** tomada agora:

1. mídia nunca no PostgreSQL;
2. upload sempre por ticket autorizado pela API;
3. bytes nunca passam pelo corpo da API;
4. hash de conteúdo verificado na confirmação;
5. EXIF removido no processamento assíncrono;
6. nome de objeto opaco;
7. mídia privada servida por URL autenticada e expirável;
8. API compatível com S3 é preferida, para reduzir custo de troca.

## Consequences
- `MEDIA-SYNC.md` define o fluxo completo.
- Jobs de processamento são necessários desde o MVP (ADR-0015).
- Limpeza de órfãos é obrigatória.

## Risks
- R-013 upload abusivo, R-024 órfãos, R-032 custo.
- Migração de volume grande de arquivos é cara — daí a preferência por API compatível.
- Objeto exposto publicamente por erro de configuração.

## Security Impact
Validação de tipo real, limites de tamanho, isolamento do processamento, nomes opacos.

## Privacy Impact
**Crítico:** EXIF com GPS é um dos vetores de vazamento mais prováveis (R-002).
Remoção obrigatória e testada. Mídia privada nunca em CDN pública.

## Offline Impact
Alto: a fila de mídia precisa sobreviver a fechamento do app e trocas de rede.

## Portability Impact
`MediaStoragePort` + preferência por API compatível com S3 reduzem o custo de troca.

## Cost Impact
Potencialmente o **segundo maior custo** do produto, depois do mapa. Mitigação: compressão
no cliente, derivativos, limites por plano e política de retenção.

## Operational Impact
Monitorar volume, custo por usuário ativo, órfãos e falhas de processamento.

## Open Questions
- Q-009: qual provider, com preço verificado?
- Limite de fotos por captura por plano?
- Política de retenção de originais?
- Onde ficam os derivativos e por quanto tempo?

## Evidence
Requisitos derivados de `MEDIA-SYNC.md`. Preços **não verificados**.

## Supersedes / Superseded By
— / —
