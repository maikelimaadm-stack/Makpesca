---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0004, ADR-0013
---

# Backup e Restauração

> Capacidades do provider gerenciado (PITR, retenção, custo) são **premissa não verificada**
> (A-009). Verificar em documentação oficial com data antes do freeze de F3.

## 1. O que precisa de backup

| Ativo | Criticidade | Estratégia proposta |
|-------|-------------|---------------------|
| Banco PostgreSQL | **Crítica** | Backup gerenciado + PITR quando disponível |
| Mídia (object storage) | **Crítica** | Versionamento/replicação conforme provider |
| Configuração de ambiente | Alta | Infraestrutura declarada e versionada |
| Secrets | Alta | Cofre com procedimento de recuperação separado |
| Catálogos (espécies, corpos d'água) | Média | Reconstruíveis a partir da fonte, se licenciada |
| Logs | Baixa | Não são backup; têm retenção própria |

## 2. Objetivos (propostos, não validados)

| Objetivo | Valor proposto | Observação |
|----------|----------------|------------|
| **RPO** (perda máxima aceitável) | 15 minutos | Depende de PITR real do provider |
| **RTO** (tempo máximo de retorno) | 4 horas | Depende de procedimento testado |
| Retenção de backup | 30 dias | Custo a validar |
| Frequência de teste de restore | Trimestral | Com evidência registrada |

Esses números são **metas propostas**, não compromissos verificados.

## 3. Teste de restauração

Backup não testado não conta como backup (R-060). O teste precisa:

1. restaurar em ambiente isolado (nunca sobre produção);
2. verificar integridade referencial e contagens;
3. verificar geometria PostGIS (consultas espaciais funcionando);
4. verificar amostra de mídia correspondente aos registros;
5. medir o tempo real do procedimento;
6. registrar evidência com data e responsável.

## 4. Cenários cobertos

| Cenário | Resposta |
|---------|----------|
| Exclusão acidental de dados por bug | PITR até instante anterior |
| Migração destrutiva | Reversão + restore parcial |
| Perda de região do provider | Restore em outra região |
| Corrupção de mídia | Versionamento/replicação do storage |
| Perda de acesso a secrets | Procedimento de recuperação documentado |
| Ransomware/comprometimento | Backup isolado, imutável quando possível |

## 5. Privacidade nos backups

- Backup contém dados C4 (coordenadas exatas). Logo: cifrado em repouso, acesso auditado,
  retenção limitada.
- Restore para ambiente não-produtivo exige anonimização.
- Pedido de exclusão de conta não apaga backups já feitos; o compromisso é que o dado
  não retorne ao ambiente ativo e que os backups expirem conforme retenção.
  Isso precisa constar na política de privacidade ao usuário.

## 6. Recuperação do dispositivo

O SQLite local não é backup do servidor. Mas o dispositivo pode conter dados ainda não
sincronizados. Consequência: procedimento de incidente considera que dispositivos podem
reenviar mutações pendentes após o restore — a idempotência (INV-S01) protege contra
duplicação nesse cenário.

## 7. Runbook

O procedimento operacional passo a passo fica em
`../14-operations/RUNBOOK-BASELINE.md`.
