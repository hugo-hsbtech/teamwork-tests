---
doc-id: QA-TA-2026-001
rev: 3
phase: technical-assessment
demand-ref: TA-2026-001
linked-rp: RP-2026-001 v1
linked-intake: INT-2026-001
created: 2026-06-07
last-modified: 2026-06-07
last-commit: 2026-06-07 (Phase 4 — CTO commitments)
language: pt-BR
---

# Ledger Q&A — Avaliação Técnica · TA-2026-001

## Sumário de Prontidão (Auditor de Confiança — canônico)

> Este cabeçalho é propriedade exclusiva do Confidence Auditor.
> O Ledger Writer o inicializa como placeholder e o atualiza somente
> a partir do veredito canônico do Auditor. Packager e Gap Reporter
> citam o número a partir daqui.

| Campo              | Valor                       |
|--------------------|-----------------------------|
| Prontidão (%)      | 88                          |
| as-of-rev          | 3                           |
| Gate               | FECHADO — signOffReady = true (Assinado sob ressalvas: Viável com ressalvas) |
| Observação         | DISC-001 e ADR-006 são follow-ups de execução, não bloqueadores de freeze. Linha Integração/OAuth a re-firmar após spike (pós-sign-off). |

---

## Registro de Entradas

<!-- ═══════════════════════════════════════════════════════
     TC-001 — Classificação Técnica (decisão governante)
     ═══════════════════════════════════════════════════════ -->

### TC-001 — Classificação Técnica (Decisão Governante)

```
Tipo:          classificação-técnica
Status:        decided
Disposition:   decided
Confidence:    88
Origin:        inherited (triagem) + confirmed (lente técnica)
Source:        intake-record demand-nature D003/Q011 · RP §14 tech-assessment-ref · sources-index KB-001
as-of-rev:     1
```

**Natureza:** HÍBRIDO

**Caminhos ativos:**

| Caminho          | Papel                                                                                                                         |
|------------------|-------------------------------------------------------------------------------------------------------------------------------|
| tech-foundation  | DEFINE a fundação greenfield — arquitetura, stack, modelo de dados e infraestrutura partindo do zero                          |
| current-state    | DESCOBRE o terreno existente — ambiente Google Workspace/OAuth da organização (não documentado) + processo manual mural+Forms+WhatsApp a migrar |

**Rationale:**
A classificação HÍBRIDO foi herdada da triagem (demand-nature D003/Q011) e confirmada sem override pela lente técnica (hsb-tech-classifier). Os dois caminhos coexistem porque:
(a) não há sistema digital legado de reservas — portanto a fundação técnica é genuinamente greenfield;
(b) há um contexto organizacional existente e não documentado (Google Workspace, políticas OAuth, processo manual via mural + Forms + WhatsApp com secretária como árbitro) que o sistema deve descobrir e absorver antes de ser projetado.
A KB `tech-landscape-room-reservation.md` referenciada como KB-001 no sources-index **não existe** — esse gap é o gatilho do spike DISC-001 (ver abaixo). O caminho current-state permanece **gated** nesse spike: nenhuma decisão de arquitetura que dependa do contexto do Google Workspace pode ser tomada antes de DISC-001 ser concluído.

**Targets:** CTO / Tech Lead · hsb-landscape-keeper (criar KB)

**Follow-ups:** DISC-001

---

<!-- ═══════════════════════════════════════════════════════
     DISC-001 — Discovery Spike (pré-requisito de KB)
     ═══════════════════════════════════════════════════════ -->

### DISC-001 — Discovery Spike: Terrain Técnico (Pré-requisito de KB)

```
Tipo:          discovery-spike
Status:        open
Disposition:   discovery
Confidence:    —
Origin:        spawned (TC-001)
spawned-by:    TC-001
Source:        TC-001 · RP §14 tech-assessment-ref · sources-index KB-001 (ausente)
as-of-rev:     1
```

**Rationale:**
A KB `tech-landscape-room-reservation.md` (KB-001) não existe. Sem ela, o caminho current-state do HÍBRIDO permanece sem embasamento factual. O spike deve produzir essa KB como artefato primário, desbloqueando:
- os pontos (a) e (d) do TA LEVE (Google Workspace + processo manual);
- a confiança mínima de 75 exigida para current-state;
- as decisões de viabilidade de integrações (Google Calendar OAuth/service account).

**Escopo do spike:**

| Sub-área | Questões a investigar |
|----------|-----------------------|
| (a) Google Workspace | Escopos OAuth concedíveis a apps de terceiros; modelo de credencial preferido (service account com delegação de domínio vs. delegação por usuário); quotas e limites da Calendar API; políticas de aprovação de apps no Admin Console |
| (b) Processo manual | Fluxo atual via mural de reservas + Google Forms + WhatsApp; papel da secretária como árbitro de conflitos; regras implícitas de prioridade/cancelamento; volume de transações (reservas/dia) |

**Owner:** CTO / Tech Lead + TI da organização · secretária (processo manual)

**Time-box sugerido:** ~2–4 dias úteis

**Gates desbloqueados ao concluir:**
- `current-state` (confidence mín. 75)
- Pontos (a) e (d) do TA LEVE
- Colunas de viabilidade de `integrations` (IHER-001, IHER-002)

**Hint:** hsb-landscape-keeper deve criar `tech-landscape-room-reservation.md` com os achados do spike. Enquanto DISC-001 estiver aberto, nenhuma decisão de arquitetura dependente de Google Workspace deve ser finalizada.

---

<!-- ═══════════════════════════════════════════════════════
     FASE 2 — Herança (carry-forward, Origin: inherited)
     ═══════════════════════════════════════════════════════ -->

## Seção: Herança Fase 2 — Carry-forward do RP/Intake

> Todas as entradas abaixo foram carregadas pelo hsb-stage-inheritor a partir do
> RP-2026-001 v1 e do INT-2026-001 com confiança preservada.
> Colunas marcadas como "pendente CTO" aguardam resposta do CTO para mudar status.

---

### IHER-001 — PO Questions (TA-Q01..TA-Q05)

```
Tipo:          inherited-section
Status:        open
Disposition:   pending-cto
Confidence:    85
Origin:        inherited
Source:        RP §14 tech-assessment-ref · dependência D03
as-of-rev:     1
```

**Rationale:**
O RP §14 e a dependência D03 exportaram cinco questões PO para avaliação técnica (TA-Q01 a TA-Q05). A confiança 85 reflete o fato de que as perguntas e seu contexto estão bem delimitados no RP, mas as **respostas** ainda não foram fornecidas pelo CTO. Nenhuma dessas questões bloqueia a classificação TC-001, mas bloqueiam decisões downstream de arquitetura e backlog.

**Questões herdadas:** TA-Q01, TA-Q02, TA-Q03, TA-Q04, TA-Q05 (conforme RP §14)

**Pendências:** Respostas do CTO para TA-Q01..TA-Q05.

**Hint:** Quando o CTO responder, atualizar status para `answered` e registrar Choice/Answer/Disposition individuais por questão.

---

### IHER-002 — Integrações (Google Calendar + OAuth/login social)

```
Tipo:          inherited-section
Status:        open
Disposition:   pending-cto
Confidence:    83
Origin:        inherited
Source:        RP §14 tech-assessment-ref · INT-2026-001
as-of-rev:     1
```

**Rationale:**
O RP identificou duas integrações nucleares: Google Calendar (reserva/bloqueio de slots) e login social/OAuth (autenticação via conta Google da organização). A confiança 83 reflete identificação clara no RP mas viabilidade técnica ainda não validada — a coluna de viabilidade é de responsabilidade do CTO e está **gated em DISC-001** (modelo de credencial e escopos OAuth dependem do spike).

**Integrações herdadas:**
- Google Calendar API (criação/consulta/cancelamento de eventos de sala)
- Login social / OAuth (Google Workspace como IdP)

**Pendências:** Coluna de viabilidade preenchida pelo CTO após DISC-001.

**Hint:** Bloquear decisão de service account vs. user-delegation até DISC-001 concluído.

---

### IHER-003 — Sistemas Afetados

```
Tipo:          inherited-section
Status:        open
Disposition:   inferred
Confidence:    83
Origin:        inherited
Source:        RP §14 tech-assessment-ref · INT-2026-001
as-of-rev:     1
```

**Rationale:**
O RP mapeou os sistemas afetados com base no processo atual e na proposta de solução. Confiança 83 por identificação direta no RP sem ambiguidade relevante.

**Sistemas herdados:**

| Sistema | Papel |
|---------|-------|
| Novo sistema de reservas | Criado do zero (greenfield) |
| Google Calendar | Consumido via API (leitura/escrita de eventos de sala) |
| Mural de reservas físico | A ser migrado / descontinuado |
| Google Forms | A ser migrado / descontinuado |
| WhatsApp (canal informal) | A ser migrado / descontinuado |

**Pendências:** Confirmação do CTO sobre descontinuação formal de mural/Forms/WhatsApp (impacto em mudança organizacional).

---

### IHER-004 — Viabilidade de NFRs (NFR-01..NFR-10)

```
Tipo:          inherited-section
Status:        open
Disposition:   pending-cto
Confidence:    82
Origin:        inherited
Source:        RP §8
as-of-rev:     1
```

**Rationale:**
O RP §8 listou dez requisitos não-funcionais (NFR-01 a NFR-10). A herança traz o enunciado de cada NFR com confiança 82 (texto claro, contexto bem estabelecido). As colunas **Viável?**, **Como** e **Risco** são de responsabilidade do CTO no TA e estão todas pendentes.

**NFRs herdados:** NFR-01, NFR-02, NFR-03, NFR-04, NFR-05, NFR-06, NFR-07, NFR-08, NFR-09, NFR-10 (conforme RP §8 — uma linha por NFR).

**Pendências:** CTO preenche Viável?/Como/Risco para cada NFR.

**Hint:** NFRs relacionados a disponibilidade e integrações Google dependem indiretamente de DISC-001.

---

### IHER-005 — Testabilidade e Observabilidade (EC-01..EC-13)

```
Tipo:          inherited-section
Status:        open
Disposition:   pending-cto
Confidence:    80
Origin:        inherited
Source:        RP §9
as-of-rev:     1
```

**Rationale:**
O RP §9 definiu treze critérios de aceitação/edge-cases (EC-01 a EC-13) que servem como dados e cenários de teste. Confiança 80 reflete completude razoável no RP mas ausência de estratégia técnica de teste e telemetria — ambas são responsabilidade do CTO no TA.

**Cenários herdados:** EC-01..EC-13 (conforme RP §9, usados como dados/ambiente de teste).

**Pendências:** CTO define estratégia de teste, telemetria e política de logs para cada cenário.

---

### IHER-006 — Esforço e Custo

```
Tipo:          inherited-section
Status:        open
Disposition:   deferred
Confidence:    —
Origin:        inherited
Source:        RP §13
as-of-rev:     1
```

**Rationale:**
O RP §13 registrou o contexto de esforço/custo como **deferido** — o PO não forneceu número preliminar e a estimativa firme é de responsabilidade exclusiva do CTO no TA. A herança preserva esse status de deferimento sem atribuir confiança numérica, pois não há dado a avaliar ainda.

**Pendências:** CTO fornece estimativa firme (story points, horas ou outra unidade) após DISC-001 e após respostas TA-Q01..TA-Q05.

**Hint:** Estimativa de esforço/custo não deve ser finalizada antes de DISC-001 concluído (escopo de integração Google Workspace ainda não dimensionado).

---

<!-- ═══════════════════════════════════════════════════════
     FASE 4 — Comprometimentos do CTO (Phase 4 commitments)
     Rev 2 · 2026-06-07
     ═══════════════════════════════════════════════════════ -->

## Seção: Fase 4 — Comprometimentos do CTO

---

<!-- ───────────────────────────────────────────────────────
     VERDICT-001 — Veredito de Viabilidade
     ─────────────────────────────────────────────────────── -->

### VERDICT-001 — Veredito de Viabilidade (CTO)

```
Tipo:          feasibility-verdict
Status:        answered
Disposition:   answered
Confidence:    86
Origin:        cto_authored
Source:        CTO · Phase 4 commitments · 2026-06-07
as-of-rev:     2
spawned-by:    TC-001 · IHER-001 · IHER-002 · IHER-006
```

**Veredito:** Viável com ressalvas

**Rationale:**
O CTO avaliou o conjunto de questões técnicas herdadas (TA-Q01..TA-Q05), as integrações (IHER-002), os NFRs e o esforço (IHER-006) e emitiu veredito de viabilidade "Viável com ressalvas" com confiança 86 (acima do limiar 85). O veredito é condicionado a quatro ressalvas ativas:

| ID | Ressalva | Gating |
|----|----------|--------|
| R1 | Admin do Workspace deve permitir grant OAuth a apps de terceiros; escopo `calendar.events`; credencial e quotas a confirmar | gated DISC-001 |
| R2 | First-commit-wins implementado via exclusão transacional (sem lock distribuído) | ADR-001 aprovado |
| R3 | Sincronização estritamente uma-via (sistema → Calendar); sem webhooks de entrada | ADR-003 aprovado |
| R4 | Revisão LGPD pelo Jurídico/DPO obrigatória antes do release | gate de release |

**Artefatos gerados pelo veredito:**

| Artefato | ID | Status |
|----------|----|--------|
| Hard-constraints | 5 (derivados das ressalvas + ADRs) | aprovados |
| ADR-001 (exclusão transacional) | ADR-001 | cto_authored ✓ |
| ADR-002 | ADR-002 | cto_authored ✓ |
| ADR-003 (sync uma-via, outbox+worker) | ADR-003 | cto_authored ✓ |
| ADR-004 | ADR-004 | cto_authored ✓ |
| ADR-005 | ADR-005 | cto_authored ✓ |
| ADR-006 (modelo de credencial Calendar) | ADR-006 | gated DISC-001 |
| Discovery Spike | DISC-001 | open (pós-sign-off) |
| KB tech-landscape | hsb-landscape-keeper criar | pendente criação |

**Decisão de assinatura:**
ASSINAR AGORA + criar KB documentando terreno conhecido + lacunas OAuth ligadas a DISC-001. Dívida TechAssessmentRef do RP descarregada como `signed`.

**Follow-ups:** DISC-001 (spike), ADR-006 (gated), KB-001 (hsb-landscape-keeper)

---

<!-- ───────────────────────────────────────────────────────
     ADR-APPROVALS — ADR-001..ADR-006 (CTO)
     ─────────────────────────────────────────────────────── -->

### ADR-APPROVALS — Aprovações de ADRs (CTO)

```
Tipo:          adr-approval-batch
Status:        answered
Disposition:   answered
Confidence:    90
Origin:        cto_authored
Source:        CTO · Phase 4 commitments · 2026-06-07
as-of-rev:     2
spawned-by:    VERDICT-001
```

**Rationale:**
O CTO promoveu ADR-001..ADR-005 a `cto_authored` (aprovados). ADR-006 (modelo de credencial Calendar) permanece `gated` em DISC-001 — não pode ser aprovado até o spike de discovery ser concluído e o modelo de credencial confirmado (service account com delegação de domínio vs. delegação por usuário autenticado).

| ADR | Título | Status CTO |
|-----|--------|-----------|
| ADR-001 | Exclusão transacional (first-commit-wins) | cto_authored ✓ |
| ADR-002 | (a confirmar título pelo tech lead) | cto_authored ✓ |
| ADR-003 | Sync uma-via outbox+worker, sem webhooks | cto_authored ✓ |
| ADR-004 | (a confirmar título pelo tech lead) | cto_authored ✓ |
| ADR-005 | (a confirmar título pelo tech lead) | cto_authored ✓ |
| ADR-006 | Modelo de credencial Calendar (service account vs. user-delegation) | gated DISC-001 |

**Hint:** ADR-006 deve ser reaberto e finalizado pelo CTO imediatamente após DISC-001 concluído.

---

<!-- ───────────────────────────────────────────────────────
     EFFORT-FIRMED — Estimativa Firme (CTO)
     ─────────────────────────────────────────────────────── -->

### EFFORT-FIRMED — Estimativa Firme de Esforço (CTO)

```
Tipo:          effort-estimate
Status:        answered
Disposition:   answered
Confidence:    80
Origin:        cto_authored
Source:        CTO · Phase 4 commitments · 2026-06-07
as-of-rev:     2
spawned-by:    IHER-006
supersedes:    IHER-006 (deferido)
```

**Rationale:**
O CTO promoveu a estimativa de esforço de `deferred` (IHER-006) para `cto_authored` com valor firme. A linha de Integração/OAuth é a única parcela ainda sujeita a re-firmação após DISC-001, pois o escopo de credencial e quotas não está fechado até o spike.

**Estimativa firme:**

| Parcela | Esforço | Observação |
|---------|---------|-----------|
| Desenvolvimento total | ~54 dias-pessoa | Firme (cto_authored) |
| Discovery Spike (DISC-001) | ~2–4 dias | Time-box firme |
| Linha Integração/OAuth | a re-firmar | Gated DISC-001 |

**Hint:** IHER-006 considerado `answered` (substituído por EFFORT-FIRMED); status de IHER-006 atualizado abaixo.

---

<!-- ───────────────────────────────────────────────────────
     TA-Q01 — Viabilidade da Integração Google Calendar
     ─────────────────────────────────────────────────────── -->

### TA-Q01 — Viabilidade da Integração Google Calendar (CTO)

```
Tipo:          po-question
Mode:          open
Status:        answered
Choice:        —
Disposition:   answered
Confidence:    82
Origin:        cto_authored
Source:        CTO · Phase 4 commitments · 2026-06-07
as-of-rev:     2
spawned-by:    IHER-001
```

**Pergunta:** A integração com Google Calendar é viável no ambiente Workspace da organização?

**Answer:**
Viável. Escopo requerido: `calendar.events`. Credencial padrão: delegação por usuário autenticado (alternativa: service account com delegação de domínio). Pré-condição: grant de OAuth pelo admin do Workspace (R1). Decisão de modelo de credencial gated em DISC-001 (ADR-006).

**Hint:** Viabilidade confirmada em princípio; confirmação de quotas e grant admin pendente em DISC-001. R1 permanece ativa até DISC-001 concluído.

---

<!-- ───────────────────────────────────────────────────────
     TA-Q02 — Sincronização em tempo-real vs. eventual
     ─────────────────────────────────────────────────────── -->

### TA-Q02 — Sincronização em Tempo-real vs. Eventual (CTO)

```
Tipo:          po-question
Mode:          open
Status:        answered
Choice:        —
Disposition:   answered
Confidence:    88
Origin:        cto_authored
Source:        CTO · Phase 4 commitments · 2026-06-07
as-of-rev:     2
spawned-by:    IHER-001
```

**Pergunta:** A sincronização com o Calendar deve ser em tempo-real ou eventual é aceitável?

**Answer:**
Confirmado: sincronização eventual, uma-via, via outbox + worker assíncrono. Sem webhooks de entrada do Calendar para o sistema. Decisão formalizada em ADR-003 (cto_authored ✓). R3 ativa: qualquer alteração feita diretamente no Calendar não reflete no sistema — comunicar aos usuários.

**Hint:** ADR-003 aprovado; sem dependência de DISC-001 para esta questão.

---

<!-- ───────────────────────────────────────────────────────
     TA-Q03 — Conflitos de reserva simultânea
     ─────────────────────────────────────────────────────── -->

### TA-Q03 — Conflitos de Reserva Simultânea (CTO)

```
Tipo:          po-question
Mode:          open
Status:        answered
Choice:        —
Disposition:   answered
Confidence:    88
Origin:        cto_authored
Source:        CTO · Phase 4 commitments · 2026-06-07
as-of-rev:     2
spawned-by:    IHER-001
```

**Pergunta:** Como tratar conflitos de reserva simultânea (dois usuários tentando reservar o mesmo slot ao mesmo tempo)?

**Answer:**
Confirmado: first-commit-wins via exclusão transacional — o árbitro é a constraint do banco, não validação read-then-write de aplicação. Mecanismo: constraint de exclusão de intervalos no banco relacional (ex.: `EXCLUDE USING gist` sobre `(sala, tstzrange)`) ou transação serializável. NÃO lock pessimista de aplicação. Formalizado em ADR-001 (cto_authored ✓). Gate de release: harness de concorrência deve ser executado e aprovado antes do deploy em produção (R2).

**Hint:** ADR-001 aprovado. Harness de concorrência é gate de release — incluir no critério de aceite de release.

---

<!-- ───────────────────────────────────────────────────────
     TA-Q04 — SLA de latência de confirmação
     ─────────────────────────────────────────────────────── -->

### TA-Q04 — SLA de Latência de Confirmação (CTO)

```
Tipo:          po-question
Mode:          open
Status:        answered
Choice:        —
Disposition:   answered
Confidence:    80
Origin:        cto_authored
Source:        CTO · Phase 4 commitments · 2026-06-07
as-of-rev:     2
spawned-by:    IHER-001
```

**Pergunta:** Qual o SLA de latência aceitável para confirmação de reserva para o usuário?

**Answer:**
Latência ≤2 minutos é alcançável com worker assíncrono (margem confortável). Confirmação de quotas da Calendar API pendente em DISC-001 (R1) — quotas excessivamente restritivas poderiam impactar o SLA em pico de uso.

**Hint:** SLA firme em ≤2 min; confirmar quotas no DISC-001 antes de garantir o SLA em SLA formal. R1 aplica-se indiretamente.

---

<!-- ───────────────────────────────────────────────────────
     TA-Q05 — Dependência D03 (integração condicionada)
     ─────────────────────────────────────────────────────── -->

### TA-Q05 — Dependência D03 e Condicionamento OAuth (CTO)

```
Tipo:          po-question
Mode:          open
Status:        parked
Choice:        —
Disposition:   discovery
Confidence:    —
Origin:        cto_authored
Source:        CTO · Phase 4 commitments · 2026-06-07
as-of-rev:     2
spawned-by:    IHER-001
```

**Pergunta:** A dependência D03 (integração com sistema externo / Google Calendar) foi reconhecida e tratada?

**Answer:**
D03 reconhecida. Integração condicionada ao grant OAuth pelo admin do Workspace (R1). Status: gated DISC-001. Nenhuma decisão de arquitetura dependente de Google Workspace pode ser finalizada antes do spike. ADR-006 permanece gated.

**Hint:** TA-Q05 marcado como `parked` (discovery) porque a resolução depende de DISC-001, um spike externo ainda aberto. Retornar para `answered` após DISC-001 concluído e grant OAuth confirmado.

---

<!-- ───────────────────────────────────────────────────────
     Atualização de status das entradas herdadas
     ─────────────────────────────────────────────────────── -->

## Atualização de Status — Herança (Rev 2)

> As entradas IHER abaixo tiveram seus status atualizados em Rev 2
> com base nos comprometimentos do CTO em Phase 4. Os blocos originais
> na seção "Herança Fase 2" são preservados sem edição (never delete).

| Entrada | Status anterior | Status Rev 2 | Observação |
|---------|----------------|--------------|-----------|
| IHER-001 (PO Questions TA-Q01..TA-Q05) | open / pending-cto | answered (Q01..Q04) / parked (Q05) | Respostas registradas em TA-Q01..TA-Q05 acima |
| IHER-002 (Integrações) | open / pending-cto | parked (discovery) | Viabilidade em princípio confirmada (TA-Q01); gated DISC-001 para modelo de credencial (ADR-006) |
| IHER-003 (Sistemas Afetados) | open / inferred | open / inferred | Sem nova informação em Phase 4; manter aberto |
| IHER-004 (NFRs) | open / pending-cto | open / pending-cto | Não abordados explicitamente em Phase 4; manter aberto |
| IHER-005 (Testabilidade) | open / pending-cto | open / pending-cto | Não abordados explicitamente em Phase 4; manter aberto |
| IHER-006 (Esforço e Custo) | open / deferred | answered | Substituído por EFFORT-FIRMED (cto_authored ~54 dp + spike 2–4 d; linha OAuth a re-firmar) |

---

<!-- END OF DOCUMENT -->
