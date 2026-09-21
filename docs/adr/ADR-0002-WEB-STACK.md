# ADR-0002 — Stack Web

- **Status:** PROPOSED
- **Date:** 2026-09-20
- **Onda:** F2

## Context
Três aplicações web: pública (`makpesca.com.br`), admin (`admin.`) e parceiros
(`partners.`). A pública precisa de conteúdo indexável (SEO) para descoberta orgânica;
admin e parceiros são aplicações internas autenticadas.

## Decision Drivers
- SEO na web pública.
- Compartilhamento de tipos com a API.
- Velocidade de desenvolvimento.
- Reuso de componentes entre as três aplicações.
- Custo de hospedagem.

## Options Considered
| Opção | Prós | Contras |
|-------|------|---------|
| **Next.js + TypeScript** | Renderização no servidor para SEO, ecossistema maduro, mesma linguagem | Acoplamento maior a uma plataforma de hospedagem se usado sem cuidado |
| SPA (React/Vite) | Simples, sem servidor | SEO ruim para a web pública |
| Remix / outro framework full-stack | Alternativas válidas | Menor familiaridade; ganho não evidente |
| Astro | Excelente para conteúdo | Menos adequado para admin/parceiros interativos |

## Decision
Adotar **Next.js + TypeScript** para as três aplicações, conforme o briefing.
Admin e parceiros podem usar renderização no cliente onde SEO não importa.

## Consequences
- Componentes compartilhados em `packages/ui`.
- Mesmo contrato de API dos demais clientes.
- Web e mobile consomem a mesma API — nenhuma regra duplicada.

## Risks
- Usar recursos de servidor do Next.js como "backend paralelo" quebraria o Art. 2 da
  Constituição. **Regra: o Next.js não implementa regra de negócio.**
- Acoplamento à plataforma de hospedagem.

## Security Impact
CORS restrito, cabeçalhos de segurança, proteção contra XSS e CSRF, sessões seguras.

## Privacy Impact
Páginas públicas exibem apenas conteúdo público, já degradado pelo servidor.
Nenhuma coordenada em URL ou em HTML renderizado além do autorizado.

## Offline Impact
Baixo. A web não é offline-first.

## Portability Impact
Next.js é portátil entre hospedagens, desde que não se dependa de recursos proprietários.

## Cost Impact
A verificar conforme a hospedagem.

## Operational Impact
Três aplicações a implantar e monitorar; mesmo pipeline.

## Open Questions
- Q-021: o MVP inclui web pública além da landing?
- Como separar claramente "renderização" de "regra de negócio" na revisão de código?

## Evidence
Baseado no briefing. Sem medição própria.

## Supersedes / Superseded By
— / —
