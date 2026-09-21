---
Status: DRAFT
Version: 0.1.0
Last Updated: 2026-09-20
Owners: (a definir)
Related ADRs: ADR-0001, ADR-0012
---

# Estratégia de GPS

## 1. Usos previstos

| Uso | Precisão necessária | Frequência |
|-----|--------------------|------------|
| Mostrar posição no mapa | Média | Contínua enquanto o mapa está aberto |
| Marcar ponto | **Alta** | Sob demanda, com refinamento |
| Registrar captura | Alta | Sob demanda |
| Descobrir conteúdo próximo | Baixa (região basta) | Eventual |
| Distância até ponto/loja | Média | Eventual |

## 2. Permissões

| Plataforma | Estratégia |
|------------|-----------|
| Android | Solicitar precisão fina apenas quando necessária, com explicação prévia na interface |
| iOS | Solicitar "quando em uso"; explicar o motivo antes do diálogo do sistema |
| Background | **Não usar no MVP** (R-048); se algum dia for necessário, exige decisão própria e justificativa nas lojas |

Recusa de permissão não pode quebrar o app: o usuário ainda pode escolher o local no mapa
(`locationSource = MAP_PICK`).

## 3. Qualidade da leitura

Ao capturar posição para marcar ponto ou captura, registrar:

- coordenada;
- acurácia informada pelo sensor;
- instante da leitura;
- fonte (`GPS`, `MAP_PICK`, `IMPORT`, `MANUAL`);
- sinais de confiabilidade (mock location, salto impossível, acurácia absurda).

A interface deve mostrar a acurácia e permitir "aguardar melhor sinal" antes de confirmar.

## 4. Bateria

| Regra |
|-------|
| Amostragem adaptativa: alta só durante a ação de marcar |
| Parar de escutar quando o mapa não está visível |
| Nenhuma escuta contínua em background no MVP |
| Medir consumo em sessão típica de pesca (R-047) |

## 5. Falsificação de localização

Localização falsificada afeta ranking, desafios e confiança (R-044). Política:

1. sinalizar quando o sistema operacional indicar localização simulada;
2. detectar saltos fisicamente impossíveis entre registros;
3. **não** apagar o registro do usuário por suspeita;
4. marcar o registro como inelegível para ranking/desafio;
5. registrar sinal para análise antifraude.

## 6. Offline

GPS não depende de rede. Requisitos:

- obter posição sem conectividade;
- converter posição em região/corpo d'água de forma aproximada localmente (quando o
  catálogo estiver baixado), com correção posterior pelo servidor;
- nunca bloquear a marcação de ponto por falta de rede.

## 7. Privacidade

| Regra |
|-------|
| A posição atual do usuário **nunca** é enviada ao servidor de forma contínua |
| Consultas de conteúdo próximo usam coordenada **reduzida** (grade/região), não exata |
| A posição do usuário não é compartilhada com outros usuários sem ação explícita e temporária |
| Nenhum log registra a posição exata do usuário |
| Provider de dados ambientais recebe coordenada aproximada |

## 8. Precisão exibida

Quando o app exibe a posição de terceiros com precisão `APPROXIMATE`, a interface mostra
o raio de incerteza. Nunca desenhar um pino "exato" sobre um dado aproximado.
