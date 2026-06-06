# QA Log — Room Reservation
<!-- LEDGER-WRITER MANAGED FILE — DO NOT EDIT MANUALLY -->

## Resumo de Prontidão

| Campo               | Valor                                          |
|---------------------|------------------------------------------------|
| Rev                 | R01                                            |
| Prontidão herdada   | 74 % (as-of-rev: origination)                  |
| Gate                | CLEAR                                          |
| Seções bloqueantes  | impacto não quantificado; viabilidade integração agenda corporativa; processo informal a caracterizar |
| Triagem             | COMPLETA — 5/5 critérios avaliados             |
| Roteamento          | DESCOBERTA DIRECIONADA (Discovery)             |
| CTO Escalation      | SIM — integração agenda corporativa (D002)     |
| Gerado em           | 2026-06-06                                     |

---

## Contexto da Iniciativa

Prontidão herdada do origination-record: **74 %**, gate CLEAR.
Idioma do projeto: pt-BR.
Natureza herdada (premissa origination): greenfield — **SUPERSEDIDA** por Q007 (híbrido confirmado pelo PO).
Escalação CTO antecipada: integração com agenda corporativa (Google/Outlook) carrega incógnitas — flag D002 propagado adiante.

---

## Entradas da Triagem — Ato 1

---

### Q001
- **Título:** Critério 1 — O problema é real?
- **Mode:** choice
- **Status:** answered
- **Targets:** triage-criterion-1
- **spawned-by:** origination Q001, Q003
- **Rationale:** Conflito de agendamento (double-booking) crônico, toda semana, caso conhecido — dor recorrente e coletiva, não sintoma isolado. Fundamentado em problema relatado no origination com conf 80.

| Campo        | Valor                                                                                     |
|--------------|-------------------------------------------------------------------------------------------|
| Choice       | Sim                                                                                       |
| Answer       | Problema real confirmado: double-booking crônico, semanal, relatado coletivamente.        |
| Disposition  | answered                                                                                  |
| Confidence   | 85                                                                                        |
| Source       | inherited — origination Q001/Q003 (conf 80)                                               |
| Hint         | —                                                                                         |

---

### Q002
- **Título:** Critério 2 — É recorrente / tem volume?
- **Mode:** choice
- **Status:** parked
- **Targets:** triage-criterion-2
- **spawned-by:** origination problem/originator
- **Rationale:** Recorrência semanal firme e reclamação coletiva confirmadas. Volume absoluto NÃO quantificado — tratado como premissa; item de discovery pendente.

| Campo        | Valor                                                                                                                   |
|--------------|-------------------------------------------------------------------------------------------------------------------------|
| Choice       | Sim                                                                                                                     |
| Answer       | Recorrência semanal confirmada; volume absoluto (nº de conflitos/semana, usuários afetados) não quantificado — premissa. |
| Disposition  | assumption                                                                                                              |
| Confidence   | 80                                                                                                                      |
| Source       | inherited — origination problem/originator                                                                              |
| Hint         | Quantificar volume absoluto na Descoberta para firmar esta premissa.                                                    |

---

### Q003
- **Título:** Critério 3 — Encaixa na visão do produto?
- **Mode:** choice
- **Status:** answered
- **Targets:** triage-criterion-3
- **spawned-by:** —
- **Rationale:** PO confirmou que reserva de salas não é core do produto, mas resolve dor interna real que vale endereçar. Sem sinal de visão no origination; decisão PO-authored.

| Campo        | Valor                                                                                                                          |
|--------------|--------------------------------------------------------------------------------------------------------------------------------|
| Choice       | Sim, tangencial mas vale                                                                                                       |
| Answer       | PO confirmou: não é core, mas é dor interna real e justifica o investimento. Encaixe tangencial aceito.                        |
| Disposition  | answered                                                                                                                       |
| Confidence   | 75                                                                                                                             |
| Source       | po_authored — decisão PO; sem sinal de visão no origination                                                                    |
| Hint         | —                                                                                                                              |

---

### Q004
- **Título:** Critério 4 — Impacto técnico / negócio suficiente?
- **Mode:** choice
- **Status:** parked
- **Targets:** triage-criterion-4
- **spawned-by:** origination Q006, Q010; origination constraints Q009
- **Rationale:** Técnico baixo-médio (CRUD de agenda), mas integração agenda corporativa traz incógnitas. Negócio confirmado em 4 eixos qualitativos (incl. negócios adiados) porém NÃO quantificado — premissa. A ser firmado na Descoberta.

| Campo        | Valor                                                                                                                                        |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| Choice       | Médio (provisório)                                                                                                                           |
| Answer       | Impacto negócio: 4 eixos qualitativos positivos (incl. negócios adiados), sem quantificação. Técnico: CRUD baixo-médio + integração com incógnitas. |
| Disposition  | assumption                                                                                                                                   |
| Confidence   | 65                                                                                                                                           |
| Source       | inherited — origination Q006/Q010 (premissa 65) + origination constraints Q009                                                               |
| Hint         | Firmar impacto quantificado e viabilidade de integração na Descoberta (D002 — CTO flag).                                                     |

---

### Q005
- **Título:** Critério 5 — Justifica agir agora?
- **Mode:** choice
- **Status:** answered
- **Targets:** triage-criterion-5
- **spawned-by:** —
- **Rationale:** PO decidiu que vale abrir Descoberta curta já para destravar (quantificar impacto + viabilidade da integração), apesar de pressão contínua sem prazo fixo.

| Campo        | Valor                                                                                                                             |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------|
| Choice       | Sim — Descoberta agora                                                                                                            |
| Answer       | PO comitou abertura de Descoberta Direcionada agora. Objetivo: quantificar impacto e verificar viabilidade de integração.         |
| Disposition  | answered                                                                                                                          |
| Confidence   | 80                                                                                                                                |
| Source       | po_authored — decisão PO                                                                                                          |
| Hint         | —                                                                                                                                 |

---

### Q006
- **Título:** Decisão de roteamento da triagem
- **Mode:** choice
- **Status:** answered
- **Targets:** triage-decision
- **spawned-by:** —
- **Rationale:** Fundamentos sólidos (problema/alcance/originador), encaixe tangencial na visão, MAS três itens travam o congelamento de escopo: (1) impacto não quantificado, (2) viabilidade da integração com agenda corporativa, (3) processo informal atual a caracterizar. PO comitou Descoberta no gate. Reversível: SIM (porta lateral, re-triar ao encerrar). Nota: só Product Ready abriria o Ato 2; Discovery faz curto-circuito — Ato 2 não roda.

| Campo        | Valor                                                                                                                                                                         |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Choice       | DESCOBERTA DIRECIONADA                                                                                                                                                        |
| Answer       | Roteamento: Discovery. Itens bloqueantes para congelamento de escopo: impacto não quantificado, viabilidade de integração (D002), processo informal a caracterizar. Gate PO comitado. |
| Disposition  | answered                                                                                                                                                                      |
| Confidence   | 85                                                                                                                                                                            |
| Source       | po_authored — decisão PO + origination D001                                                                                                                                   |
| Hint         | Re-triar ao encerrar a Descoberta. Ato 2 não roda neste ciclo.                                                                                                                |

---

### Q007
- **Título:** Natureza da demanda — greenfield, brownfield ou híbrido?
- **Mode:** choice
- **Status:** answered
- **Targets:** demand-nature
- **spawned-by:** —
- **Rationale:** PO confirmou que JÁ EXISTE um processo/ferramenta INFORMAL de reserva de salas hoje (planilha/quadro/calendário) — não é greenfield puro. É formalizar/migrar processo existente (superfície brownfield) com software-core novo, MAIS integração com agenda corporativa existente (Google/Outlook). SUPERSEDE premissa greenfield do origination (que era inferida). Base de Conhecimento: NÃO existe (conf 85) — exige discovery de documentação.

| Campo        | Valor                                                                                                                                                                                                                          |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Choice       | Híbrido                                                                                                                                                                                                                        |
| Answer       | Natureza: HÍBRIDO. Processo informal atual existe (planilha/quadro/calendário — a caracterizar). Software-core novo. Integração agenda corporativa (Google/Outlook) existente. Base de Conhecimento: NÃO existe — exige discovery. |
| Disposition  | answered                                                                                                                                                                                                                       |
| Confidence   | 78                                                                                                                                                                                                                             |
| Source       | po_authored — resposta PO + origination nature-signal/constraints                                                                                                                                                              |
| Hint         | Premissa greenfield do origination SUPERSEDIDA por esta entrada. Sistemas afetados: novo sistema de reserva de salas + processo informal atual (a caracterizar) + integração agenda corporativa. CTO flag D002 ativo.           |

---
<!-- END -->
