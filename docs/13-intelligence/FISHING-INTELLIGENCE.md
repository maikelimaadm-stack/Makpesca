---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0012
---

# Inteligência de Pesca

## 1. Promessa

Transformar o acervo de capturas e condições em informação útil: quando ir, o que usar,
o que esperar. É o principal valor percebido do PRO — e o maior risco de privacidade
do produto.

## 2. Insights previstos

| Insight | Base | Risco de privacidade |
|---------|------|----------------------|
| Atividade por espécie ao longo do ano | Capturas públicas agregadas | Baixo |
| Melhor horário por espécie/região | Capturas + horário | Médio |
| Isca mais registrada por espécie/região | Capturas | Baixo |
| Relação com condições ambientais | Capturas + snapshot ambiental | Médio |
| Tendências regionais por temporada | Agregação regional | Médio |
| **Padrões pessoais do usuário** | Dados do próprio usuário | **Baixo** (é dele) |
| Sugestão de planejamento | Combinação dos acima | Médio |

Observação importante: o insight **pessoal** (sobre os próprios dados do usuário) é o mais
seguro e possivelmente o mais valioso. Deve vir primeiro.

## 3. Portão obrigatório antes de publicar qualquer insight agregado

```
CONSENT → ELIGIBILITY → SPATIAL AGGREGATION → TEMPORAL AGGREGATION
        → MINIMUM COHORT → REIDENTIFICATION CHECK → publicar
```

| Etapa | Regra |
|-------|-------|
| **CONSENT** | Só entram dados de usuários que consentiram explicitamente (opt-in) |
| **ELIGIBILITY** | Só capturas públicas, moderadas e sem sinal de fraude |
| **SPATIAL AGGREGATION** | Nunca ponto; sempre célula/região com tamanho mínimo |
| **TEMPORAL AGGREGATION** | Nunca instante; sempre janela (ex.: faixa de horário, semana) |
| **MINIMUM COHORT** | Número mínimo de usuários e de registros distintos (k mínimo — Q-023) |
| **REIDENTIFICATION CHECK** | Verificar se o insight isola alguém; se isolar, suprimir |

**Falhar qualquer etapa = insight não é publicado.** Não existe exceção "só dessa vez".

## 4. Regras invioláveis

| # | Regra |
|---|-------|
| 1 | Insight nunca revela ponto individual |
| 2 | Insight nunca permite inferir quem registrou |
| 3 | Dados de pontos privados **não entram** em insight agregado |
| 4 | Usuário pode sair da base de insights a qualquer momento |
| 5 | Exclusão de dado de origem reflete no próximo recálculo |
| 6 | Insight não é vendido a terceiros (`NON-GOALS` §8) |
| 7 | Insight é apresentado como estimativa, com base e limitações explícitas |

## 5. Honestidade estatística

O produto **não** promete prever pescaria. O que a base oferece é: o que outras pessoas
registraram, em quais condições, com que frequência. Apresentar isso como previsão seria
desonesto e geraria frustração.

Cada insight exibe: período considerado, quantidade de registros, região e a ressalva de
que se baseia em registros voluntários (portanto enviesados).

## 6. Viés conhecido

| Viés | Efeito |
|------|--------|
| Só quem publica entra na base | Regiões e espécies populares dominam |
| Registro voluntário | Capturas ruins são subnotificadas |
| Distribuição desigual de usuários | Região com poucos usuários gera insight frágil |
| Sazonalidade incompleta no início | Primeiros anos têm base curta |

Esses vieses devem ser comunicados, não escondidos.

## 7. Fase

Futuro. Depende de: base instalada suficiente, consentimento implementado, agregação com
coorte mínima validada e dados ambientais confiáveis.

Antes disso, entregar **insights pessoais** (sobre os próprios dados), que não dependem
de coorte e já entregam valor.
