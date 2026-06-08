<!--
ROI Report · Iniciativa 20260606-1939-room-reservation-9ce274
Gerado pelo ROI Reporter em 2026-06-07.
Fonte de métricas: Cost Collector [ledger] + Metrics Analyst [artifact] + composites do orquestrador.
Toda estimativa de valor é derivada dos documentos — ver §4. Toda métrica de investimento (tokens,
USD, tempo de computação) está marcada como "não capturado" — ver banner abaixo e §5.
-->

# ROI da Iniciativa — room-reservation · Sistema de Reserva de Salas de Reunião
<!-- rev: 1 · updated: 2026-06-07 -->

> Análise fim-a-fim desta iniciativa: o que **custou** conduzir a demanda do sinal bruto
> até o PRD (tokens, modelos, USD, tempo — medidos pelo hook de captura de custo) e o
> **valor** que ela carrega (extraído dos documentos, grau estimado). Custo é medido;
> valor é estimativa; qualquer métrica não capturada declara o motivo.

> **AVISO — INVESTIMENTO NAO CAPTURADO.** O hook de captura de custo não registrou esta
> iniciativa: o arquivo `analytics/cost-ledger.jsonl` está ausente. Todas as métricas da
> família de investimento (tokens, USD, tempo de computação ativa, mix de modelos, taxa de
> cache, economia de cache, invocações de agentes) são **"não capturado"** neste relatório.
> As seções [artifact] — readiness, disposições, resultados de gate e valor — estão
> totalmente preenchidas. Se a infraestrutura de hook for ativada em uma re-execução futura,
> os preços em `pricing.json` (asOf 2026-06-05, Opus/Sonnet/Haiku) já estão disponíveis
> para computar o custo.

---

## 1 · Cabeçalho
<!-- id=header; source=[ledger]+[artifact] -->

| Campo | Valor |
|---|---|
| **Iniciativa** | `20260606-1939-room-reservation-9ce274` · projeto `room-reservation` |
| **Nome** | Sistema de Reserva de Salas de Reunião |
| **Status** | open [artifact] |
| **Idioma** | `pt-BR` [artifact] |
| **Fases alcancadas** | origination → intake → readiness → assessment → prd → delivered-to-pm [artifact] |
| **Lead time** | 2026-06-06T19:39:00Z → 2026-06-07T00:01:49Z (PRD congelado) · ~4h 23min calendário [artifact] |
| **Custo total** | não capturado — cost-ledger.jsonl ausente [ledger] |
| **Tokens totais** | não capturado — cost-ledger.jsonl ausente [ledger] |
| **Mix de modelos** | não capturado — cost-ledger.jsonl ausente [ledger] |
| **Readiness final** | **92** / 100 (fase prd) [artifact] |

---

## 2 · Detalhamento por fase
<!-- id=phases; source=[ledger]+[artifact]; uma linha por fase -->

> Células de custo (tokens, USD, spawns, rounds) dependem do cost-ledger e estao marcadas
> como **"nao capturado"** para todas as fases. Os campos [artifact] (wall-clock, readiness,
> resultado, disposicoes) estao preenchidos a partir de `initiative.json` e dos documentos
> congelados.

| Fase | Wall-clock [artifact] | Tokens [ledger] | USD [ledger] | Spawns [ledger] | Rounds [artifact] | Readiness [artifact] | Resultado | Disposicoes |
|---|---|---|---|---|---|---|---|---|
| **origination** | 19:39→21:22 (~1h 43min) | nao capturado | nao capturado | nao capturado | v1→v4 (4 revisoes) | 74 | Entregue ao intake; 3 debitos owes gerados (D001, D002, D003) | Misto: reais + assumptions/discoveries — ver §5 |
| **intake** | 21:57→00:01 (~2h 04min) | nao capturado | nao capturado | nao capturado | v3; D003 + D005 (2 rodadas de descoberta) | 100 | Triage: **Product Ready** (pos D003+D005); 1 supersedicao (Q002→Q005); 2 re-scorings | Real-answered dominante; TechAssessmentRef deferido para assessment |
| **readiness** | 00:01→01:11 (~1h 09min) | nao capturado | nao capturado | nao capturado | v1→v4 (4 revisoes); 8 confirmacoes C-Q01..C-Q08; 2 conflitos de auditoria resolvidos | 81 | Freeze **provisorio** → pleno (apos TA assinado); upgrade de freeze posterior | 10 NFRs, 13 edge cases, 6 ADRs confirmados |
| **assessment** | 00:00→00:00 (mesmo dia, 2026-06-07) | nao capturado | nao capturado | nao capturado | v1→v3 (3 revisoes); 16 entradas estruturadas; DISC-001 aberto | 88 | Veredito: **Viavel com ressalvas** (conf 86, cto_authored); signOffReady; sem veto | 4 ressalvas (R1..R4); DISC-001 escalado para execucao |
| **prd** | 00:00 (2026-06-07), entregue 2026-06-07 | nao capturado | nao capturado | nao capturado | v1 (3 sub-revisoes R01→R03); escalated=true | 92 | **PRD Accepted**; dual sign-off PO+CTO 2026-06-07; delivered-to-pm; downstreamReady | 2 debitos abertos (DISC-001 + LgpdReview) carregados para execucao |

**Observacoes sobre o caminho de gate:**
- Triagem inicial: Discovery (origination v1, antes das rodadas D003/D005).
- Triagem final: **Product Ready** — apos D003 (impacto quantificado, integracao de-arriscada) e D005 (valor R$ quantificado).
- Escalacao: D002 → TA Leve de-arriscado → TA assinado (Viavel com ressalvas) → merge no PRD com `escalated=true`.
- Freeze do RP: provisorio no inicio do assessment → **pleno** apos assinatura do TA-2026-001.

**Entradas Q### por fase [artifact]:**
- origination: 11 Q### canonicas
- intake: 12 Q### canonicas; 1 supersedicao (Q002→Q005); 2 re-scorings (Q002/Q004 via D003/D005)
- readiness: 8 confirmacoes (C-Q01..C-Q08)
- assessment: 16 entradas estruturadas (TC-001, DISC-001, IHER-001..006, VERDICT-001, ADR-APPROVALS, EFFORT-FIRMED, TA-Q01..Q05)
- prd: 7 Q### canonicas
- **Total canonico: 30 Q### proprias + 8 confirmacoes + 16 entradas de assessment**

**Eventos de retrabalho [artifact]: 6 no total**
- 1 supersedicao (Q002→Q005, intake)
- 2 re-scorings (Q002/Q004 via D003/D005, intake)
- 1 upgrade de freeze (RP provisorio→pleno no TA assinado)
- 2 conflitos de auditoria resolvidos (C2 premissas, C4 sync bidirecional→uma-via)
- Zero template restarts, zero rejeicoes do PM, zero vetos do CTO

---

## 3 · Drivers de custo
<!-- id=drivers; source=[ledger] -->

**Todas as metricas desta secao sao nao capturadas** — o cost-ledger.jsonl esta ausente.
O hook de captura de custo nao registrou esta iniciativa.

- **Top agentes por USD:** nao capturado — cost-ledger.jsonl ausente [ledger]
- **Top modelos por USD:** nao capturado — cost-ledger.jsonl ausente [ledger]
- **Disciplina de cache:** taxa de cache-hit = nao capturado; economia de cache = nao capturado [ledger]
- **Alavancagem de automacao:** tempo de computacao ativa / wall-clock = nao capturado [ledger]

**Nota sobre precos disponiveis:** caso o hook seja ativado em re-execucao futura, os precos
em `pricing.json` (asOf 2026-06-05) se aplicam: Sonnet 4.6 — input US$3,00/Mtok, output
US$15,00/Mtok, cache-read US$0,30/Mtok; Opus 4.x (4-5 a 4-8) — input US$5,00/Mtok,
output US$25,00/Mtok; Haiku 4.5 — input US$1,00/Mtok, output US$5,00/Mtok.

---

## 4 · Painel de ROI
<!-- id=roi; source=[ledger]+[artifact]; lado de valor = estimate -->

### 4.1 Composites
<!-- Composites que dependem de custo: nao capturados. Composites so-artifact: preenchidos. -->

| Composite | Valor | Fonte |
|---|---|---|
| **Custo-para-prontidao** | nao capturado — cost-ledger ausente | [ledger]+[artifact] |
| **Throughput — por dolar** | nao capturado — cost-ledger ausente | [ledger]+[artifact] |
| **Throughput — por hora (computacao ativa)** | nao capturado — cost-ledger ausente | [ledger]+[artifact] |
| **Throughput — por Mtok** | nao capturado — cost-ledger ausente | [ledger]+[artifact] |
| **ROI ancorado em valor** | nao computavel sem custo — cost-ledger ausente · **estimate** | valor [artifact] / custo [ledger] |
| **Gate savings** | nao aplicavel — demanda percorreu o pipeline completo; sem veto/reject; sem iniciativas-irmas para baseline comparavel | [ledger]+[artifact] |
| **Esforco documentado (proxy de custo)** | ~54 dias-pessoa + spike DISC-001 ~2-4 dias (estimativa firme do TA, cto_authored) [artifact] | TA-2026-001 |
| **Score de valor** | **82 / 100 · estimate** | [artifact] — ver §4.2 |
| **Readiness final** | **92 / 100** | [artifact] |
| **Postura valor/esforco** | Favoravel (estimate): impacto alto quantificado (R$700k pipeline, R$111k perdidos) vs. esforco modesto (~54 dp); MAS ROI em USD nao computavel sem cost-ledger | [artifact] |

> **Nota sobre gate savings:** a demanda foi triada inicialmente como Discovery, mas
> concluiu o pipeline completo (origination → intake → readiness → assessment → prd →
> delivered-to-pm) sem veto, rejeicao ou bloqueio de backlog antecipado. Gate savings
> nao se aplica neste caso — o gate funcionou como qualificador (elevou a triage para
> Product Ready), nao como interruptor antecipado de custo. Nao ha iniciativas-irmas
> comparaveis neste TEAMWORK_ROOT para baseline.

### 4.2 Detalhamento de valor (extraido dos documentos · estimate)
<!-- id=value; source=[artifact]; cite cada dimensao -->

| Dimensao | Peso | Score | Justificativa → Citacao |
|---|---|---|---|
| **Reach** | 25 | **78** | Afeta a empresa toda via conflitos de agenda (colaboradores, gestores, equipes comerciais) — alcance organizacional amplo, mas sem quantificacao de headcount exata. Risco de adocao (R01 Alta/Alto) e natureza hibrida (nao 100% digital) deprimem levemente o score. → origination-record §Problema / RP §Personas [artifact] |
| **Impacto / severidade da dor** | 30 | **90** | Impacto diretamente quantificado: 9 conflitos em 5 semanas, ~3 dias de atraso medio, 78% com negocio adiado, R$111k perdidos (2 negócios fechados adiados/perdidos), R$90k em risco (1 aberto), pipeline ~R$700k afetado. Score alto por ser o unique quantified-loss mais forte do pipeline. → D005 / intake-record §Valor / TA §Evidencias [artifact] |
| **Objetivos estrategicos** | 20 | **72** | Alinha-se a eficiencia operacional e suporte a receita comercial, mas o encaixe de visao e descrito como "tangencial" no criterio 3 da triagem — a iniciativa resolve infra interna, nao produto ou diferenciador de mercado diretamente. ADR-006 gated pode alterar escopo de integracao. → RP §Objetivos / intake-record §Triagem criterio 3 [artifact] |
| **Mensurabilidade** | 15 | **85** | Metricas de sucesso estao definidas e sao quantificaveis: zero-conflitos, reducao de 80% nos conflitos, tempo medio de reserva, uptime, adocao (>70% das reservas via sistema em 90 dias). NFR-01..10 documentados. Linha de re-firmacao da estimativa de integracao pende DISC-001. → RP §Metricas de sucesso / TA §NFRs [artifact] |
| **Confianca de valor** | 10 | **80** | Valor central (perda de receita) esta em disposicoes reais (nao assumption), validado em D005. Dois debitos abertos (DISC-001 / LGPD) introduzem incerteza residual: DISC-001 pode forcar revisao de escopo da integracao; LGPD e pre-condicao de release. Score nao maximo por esses riscos reais abertos. → assessment §Ressalvas R1+R4 / prd §owes [artifact] |
| **Score de valor** | — | **82 / 100** | Ponderado: (78×25 + 90×30 + 72×20 + 85×15 + 80×10) / 100 = (1950 + 2700 + 1440 + 1275 + 800) / 100 = 8165/100 = **81,65 ≈ 82** · **estimate-grade** |

**Dampeners honestos (nao descontados da pontuacao, mas sinalizados):**
- O valor quantificado (R$111k) e receita nova nao-recorrente ja perdida — irrecuperavel;
  o sistema previne perda futura, nao recupera o passado.
- R$90k em risco pode nao recuperar (R04 do assessment).
- Adocao e o maior risco isolado (R01 Alta/Alto) — sem adocao, o impacto realizado cai.
- DISC-001 aberto pode forcar revisao de escopo da linha de integracao (ADR-006 gated).

---

## 5 · Itens em aberto
<!-- id=open; source=[artifact] -->

### 5.1 Debitos pendentes (owes)

| Ref | Fase de origem | Para | Status | Descricao |
|---|---|---|---|---|
| **DISC-001** (DiscoverySpike) | assessment → prd | execucao | **aberto** | Spike Google Workspace/OAuth: documentar escopos concediveis, grant a apps de terceiros, modelo de credencial (ADR-006 gated), quotas Calendar API + finalizar caracterizacao do processo manual. Owner: CTO/Tech Lead + TI. Prazo estimado: ~2-4 dias. Condiciona NFR-02/06/08, ADR-006 e re-firmacao da linha de integracao. Ressalva R1 do veredito. [artifact — assessment/prd owes] |
| **LgpdReview** | prd | execucao | **aberto** | Revisao LGPD com Juridico/DPO: base legal, retencao de dados, exclusao a pedido (NFR-07 / ressalva R4). Pre-condicao de release — o produto nao pode entrar em producao sem esta revisao. [artifact — prd owes] |

**Debitos upstream resolvidos (para referencia):**

| Ref | Resolucao |
|---|---|
| DiscoveryDirecionada (D001/D003) | Resolvido: impacto quantificado, integracao de-arriscada, processo informal caracterizado. [artifact — intake owes] |
| DiscoveryValorRS (D005) | Resolvido: valor R$ quantificado (R$111k perdidos, R$90k em risco, pipeline ~R$700k). Re-triagem → Product Ready. [artifact — intake owes] |
| TechAssessmentRef (D002) | Resolvido/Assinado: TA-2026-001 assinado (Viavel com ressalvas, conf 86). Freeze do RP passa de provisorio a pleno. [artifact — readiness owes / assessment] |
| EffortEstimate | Resolvido: ~54 dias-pessoa + spike ~2-4 dias (cto_authored). [artifact — readiness owes / assessment] |
| GreenfieldConfirmation | Resolvido em D003: processo informal caracterizado como Hibrido (mural+Forms+WhatsApp). [artifact — origination owes] |

### 5.2 Disposicoes em aberto (risco carregado)

As disposicoes abaixo nao bloquearam o freeze mas representam incerteza levada para a execucao:

**Ressalvas do veredito de viabilidade (Viavel com ressalvas, conf 86):**
- **R1** — OAuth/Workspace gated: configuracao do Google Workspace para conceder OAuth a apps de terceiros nao confirmada. Destravada por DISC-001. [artifact — assessment §Ressalvas]
- **R2** — Exclusao transacional: atomicidade de reservas simultaneas requer first-commit-wins via exclusao transacional (ADR-001) — implementacao a validar em sprint inicial. [artifact — assessment §Ressalvas]
- **R3** — Sync uma-via confirmado: sincronizacao Google Calendar → sistema (nao bidirecional); simplicidade confirmada mas limita cenarios de uso. [artifact — assessment §Ressalvas]
- **R4** — LGPD/DPO: revisao juridica obrigatoria pre-release (LgpdReview owes). [artifact — assessment §Ressalvas]

**ADR gated:**
- **ADR-006** — Modelo de credencial OAuth: gated em DISC-001; nao aprovado. Decisao final pende resultado do spike. [artifact — assessment §ADRs]

**Riscos consolidados levados a execucao [artifact — assessment §Riscos]:**
- 5 riscos de produto: R01 (adocao, Alta/Alto — maior risco isolado), R02 (resistencia cultural), R03 (dados de reservas/historico), R04 (recuperacao de R$90k), R05 (dependencia de agenda corporativa)
- 6 riscos tecnicos: RT01 (quotas Calendar API), RT02 (latencia sync), RT03 (conflitos simultaneos), RT04 (autenticacao/seguranca), RT05 (migracao de dados), RT06 (disponibilidade)
- Dependencias externas: Google Calendar API (critica), infraestrutura TI interna, Juridico/DPO

**Cobertura de consistencia confirmada [artifact]:**
- 0 contradicoes A (RP) ↔ B (TA)
- Invariante A.7 ↔ B.4 = 10 NFRs em correspondencia 1:1
- A.2 ↔ reconciliacao de escopo: escopo do RP mantido integralmente no PRD

### 5.3 Metricas nao capturadas

As familias a seguir nao puderam ser computadas porque o cost-ledger.jsonl esta ausente
(o hook de captura de custo nao registrou esta iniciativa):

| Familia | Metricas afetadas | Motivo |
|---|---|---|
| **A · Investimento / consumo** | Tokens totais (por tipo/fase/agente), USD total (por fase/agente/modelo), mix de modelos, economia de cache, taxa de cache-hit, invocacoes de agentes, turns do orquestrador | cost-ledger.jsonl ausente em `analytics/` |
| **B · Tempo / duracao (parcial)** | Tempo de computacao ativa, gap de latencia humana, razao ativo/wall-clock | cost-ledger.jsonl ausente; wall-clock [artifact] esta disponivel via initiative.json |
| **E · Composites de ROI (parcial)** | Custo-para-prontidao, throughput por dolar/hora/Mtok, ROI ancorado em valor, disciplina de cache, alavancagem de automacao | dependem da familia A; apenas score de valor (estimate) e readiness (artifact) estao preenchidos |

**O que esta disponivel para uma re-execucao futura:** pricing.json (asOf 2026-06-05) com
taxas para Opus 4.x, Sonnet 4.x, Haiku 4.5; initiative.json com timestamps de todas as fases;
documentos congelados de todas as 5 fases. Ao ativar o hook e re-executar, todos os composites
de custo poderao ser calculados sem refazer a analise de valor.

---

<!-- END OF DOCUMENT -->
