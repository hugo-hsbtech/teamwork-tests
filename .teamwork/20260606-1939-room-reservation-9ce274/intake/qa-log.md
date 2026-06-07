# QA Log — Room Reservation
<!-- LEDGER-WRITER MANAGED FILE — DO NOT EDIT MANUALLY -->

## Resumo de Prontidão

| Campo               | Valor                                                                                         |
|---------------------|-----------------------------------------------------------------------------------------------|
| Rev                 | R03                                                                                                                                                        |
| Prontidão herdada   | 74 % (as-of-rev: origination)                                                                                                                              |
| Gate                | CLEAR                                                                                                                                                      |
| Seções bloqueantes  | nenhuma — todos os bloqueantes resolvidos; D003 encerrada; D005 encerrada; impacto TOTALMENTE QUANTIFICADO (incl. R$)                                      |
| Triagem             | REVISIT-2 — D005 encerrada; impacto monetário firmado; quadro suporta Product Ready (todos critérios answered, nenhum parked remanescente)                 |
| Roteamento          | DESCOBERTA DIRECIONADA (Discovery) — D003 ENCERRADA; D005 ENCERRADA — re-triagem formal indicada → Product Ready                                           |
| CTO Escalation      | SIM (de-arriscado) — apenas Google Calendar, auth simples; Technical Assessment leve indicado                                                              |
| Gerado em           | 2026-06-06                                                                                                                                                 |

---

## Contexto da Iniciativa

Prontidão herdada do origination-record: **74 %**, gate CLEAR.
Idioma do projeto: pt-BR.
Natureza herdada (premissa origination): greenfield — **SUPERSEDIDA** por Q007 (híbrido confirmado pelo PO).
Escalação CTO antecipada: integração com agenda corporativa (Google/Outlook) carrega incógnitas — flag D002 propagado adiante.
Revisit R02 (2026-06-06): D003 encerrada. Descoberta de campo respondeu Q008–Q011. Critérios Q002 e Q004 re-scored de parked/assumption para answered. Bloqueantes de triage zerados. Quadro suporta Product Ready após re-triagem formal.
Revisit R03 (2026-06-06): D005 encerrada. Q012 respondida com valor monetário firmado (R$111k perdidos, R$90k em risco, pipeline R$700k). Q004 re-scored para conf 90 com impacto totalmente quantificado em R$. Último item de descoberta fechado. Todos os critérios answered. Quadro suporta Product Ready — nenhum parked remanescente.

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
- **Status:** answered
- **Targets:** triage-criterion-2
- **spawned-by:** origination problem/originator
- **Follow-ups:** Q008
- **Rationale:** Recorrência semanal firme e reclamação coletiva confirmadas. Volume absoluto AGORA QUANTIFICADO via D003 (levantamento de campo): 9 conflitos em 5 semanas ≈ 1,8/semana. Premissa firmada como fato.

| Campo        | Valor                                                                                                                                                           |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Choice       | Sim                                                                                                                                                             |
| Answer       | Volume quantificado (D003): 9 conflitos em 5 semanas ≈ 1,8/semana, dias úteis, pico 10h–16h. Recorrência confirmada como fato de campo, não mais premissa.      |
| Disposition  | answered                                                                                                                                                        |
| Confidence   | 88                                                                                                                                                              |
| Source       | discovery — D003/Q008, levantamento de campo PO (2026-06-06)                                                                                                   |
| Hint         | Premissa anterior (conf 80, assumption) firmada por dados de campo. Ver Q008 para detalhes completos do impacto.                                                |

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
- **Status:** answered
- **Targets:** triage-criterion-4
- **spawned-by:** origination Q006, Q010; origination constraints Q009
- **Follow-ups:** Q008, Q009, Q010, Q012
- **Rationale:** Negócio AGORA QUANTIFICADO via D003: ~1,8 conflitos/semana, ~3 dias de atraso por conflito, 78% geram negócio adiado (custo de receita/relacionamento confirmado como fato). Técnico DE-ARRISCADO: apenas Google Calendar (não Outlook), sem SSO corporativo, auth simples/social aceitável — escopo de integração muito menor que o temido. VALOR MONETÁRIO FIRMADO via D005/Q012: R$111k perdidos (2 negócios já não fecham), R$90k em risco (1 negócio ainda travado), pipeline total envolvido ~R$700k. Impacto consolidado: ALTO — totalmente quantificado, não mais premissa em nenhum eixo.

| Campo        | Valor                                                                                                                                                                                                                                                                               |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Choice       | Alto                                                                                                                                                                                                                                                                                |
| Answer       | Negócio: ~1,8 conflitos/sem, ~3 dias de atraso/conflito, 78% geram negócio adiado — impacto de receita/relacionamento confirmado. VALOR MONETÁRIO: R$111k perdidos (2 negócios fechados sem retorno), R$90k em risco (1 negócio aberto travado), pipeline ~R$700k envolvido. Todos de prospecção de novos negócios (receita nova, não recorrente). Técnico: apenas Google Calendar, sem SSO, auth simples — risco arquitetural reduzido. Impacto global: ALTO (totalmente quantificado). |
| Disposition  | answered                                                                                                                                                                                                                                                                            |
| Confidence   | 90                                                                                                                                                                                                                                                                                  |
| Source       | discovery — D003/Q008/Q009/Q010, levantamento de campo PO (2026-06-06); D005/Q012, levantamento comercial PO (2026-06-06)                                                                                                                                                           |
| Hint         | Premissa anterior (Médio provisório, conf 65, assumption) superada por dados de campo. Conf elevada de 85→90 após quantificação monetária completa via Q012. CTO flag de-arriscado: Technical Assessment leve ainda indicado (apenas Google, sem SSO). Ver Q009/Q010/Q012 para detalhes. |

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

## Entradas da Descoberta — D003 (encerrada em 2026-06-06)

---

### Q008
- **Título:** Descoberta D003 #1 — Quantificação do impacto operacional
- **Mode:** open
- **Status:** answered
- **Targets:** triage-criterion-2, triage-criterion-4, impact-quantification
- **spawned-by:** D003; Q002 (volume não quantificado); Q004 (impacto não quantificado)
- **Rationale:** Volume e custo do double-booking eram premissa não firmada (Q002 parked, Q004 parked). Discovery de campo foi necessária para transformar qualitativo em quantitativo e sustentar decisão de investimento.

| Campo        | Valor                                                                                                                                                                                                                     |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Choice       | —                                                                                                                                                                                                                         |
| Answer       | 9 conflitos de sala nas últimas 5 semanas (≈ 1,8/semana), em dias úteis, pico entre 10h e 16h. Custo por conflito: a reunião é reagendada para quem chegou por último, com atraso médio de ~3 dias para reencontrar agenda comum dos envolvidos. |
| Disposition  | answered                                                                                                                                                                                                                  |
| Confidence   | 90                                                                                                                                                                                                                        |
| Source       | discovery — levantamento de campo PO/D003 (2026-06-06)                                                                                                                                                                    |
| Hint         | Dados de campo. Firma Q002 e eleva Q004 de Médio provisório para ALTO. Base quantitativa para ROI e priorização.                                                                                                          |

---

### Q009
- **Título:** Descoberta D003 #2 — Negócios adiados confirmados
- **Mode:** open
- **Status:** answered
- **Targets:** triage-criterion-4, business-impact
- **spawned-by:** D003; Q004 (impacto de negócio não quantificado)
- **Rationale:** O eixo de maior gravidade do impacto (negócios adiados) era premissa qualitativa no origination. Discovery de campo foi necessária para confirmar ou refutar.

| Campo        | Valor                                                                                                                                                                               |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Choice       | —                                                                                                                                                                                   |
| Answer       | 7 dos 9 conflitos (≈ 78%) resultaram em negócio adiado nas 5 semanas (≈ 1,4/semana). Eixo de maior gravidade do impacto confirmado como FATO, não mais premissa.                   |
| Disposition  | answered                                                                                                                                                                            |
| Confidence   | 90                                                                                                                                                                                  |
| Source       | discovery — levantamento de campo PO/D003 (2026-06-06)                                                                                                                             |
| Hint         | Confirma custo de receita/relacionamento. Dado crítico para justificativa de investimento e urgência. Reforça impacto ALTO em Q004. NOTA DE RECONCILIAÇÃO: esta entrada aponta "7 de 9 conflitos com negócio adiado"; Q012 (levantamento comercial dedicado posterior) aponta "9 adiamentos" como número total. Adotar 9 adiamentos como valor mais recente e detalhado — diferença pode refletir múltiplos adiamentos por conflito ou critério distinto de contagem. Flag para confirmação leve, NÃO bloqueante. Ver Q012. |

---

### Q010
- **Título:** Descoberta D003 #3 — Viabilidade e escopo da integração com agenda
- **Mode:** open
- **Status:** answered
- **Targets:** triage-criterion-4, integration-scope, cto-escalation
- **spawned-by:** D003; Q004 (integração com incógnitas); Q007 (CTO flag D002)
- **Rationale:** Incógnita arquitetural crítica: integração com Google e/ou Outlook, com ou sem SSO, definia complexidade técnica e risco. Era o principal driver da escalação CTO (D002).

| Campo        | Valor                                                                                                                                                                                                                                    |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Choice       | —                                                                                                                                                                                                                                        |
| Answer       | Integração viável e de-arriscada: apenas Google Calendar (Outlook descartado); SEM SSO corporativo; autenticação simples ou login social simples é aceitável. Escopo de integração muito menor que o cenário temido.                     |
| Disposition  | answered                                                                                                                                                                                                                                 |
| Confidence   | 88                                                                                                                                                                                                                                       |
| Source       | discovery — levantamento de campo PO/D003 (2026-06-06)                                                                                                                                                                                   |
| Hint         | Risco arquitetural reduzido significativamente. CTO flag de-arriscado: Technical Assessment leve ainda indicado (confirmar OAuth Google Calendar), mas as incógnitas-chave foram resolvidas. Atualiza header CTO Escalation.             |

---

### Q011
- **Título:** Descoberta D003 #4 — Caracterização do processo informal atual
- **Mode:** open
- **Status:** answered
- **Targets:** demand-nature, process-migration, brownfield-surface
- **spawned-by:** D003; Q007 (processo informal "planilha/quadro/calendário — a caracterizar")
- **Rationale:** Q007 confirmou natureza híbrida mas deixou o processo informal sem detalhamento. Discovery necessária para entender o que o novo sistema substitui/migra.

| Campo        | Valor                                                                                                                                                                                                                                                         |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Choice       | —                                                                                                                                                                                                                                                             |
| Answer       | Processo atual HÍBRIDO: reserva feita por anotação em PAPEL no MURAL (fonte de verdade) + Google Forms (link enviado via WhatsApp); às vezes só no papel. Mantido pela SECRETÁRIA, que atua como árbitro/gestor da escala. O novo sistema substitui/migra esse processo manual (mural + Forms + WhatsApp). |
| Disposition  | answered                                                                                                                                                                                                                                                      |
| Confidence   | 88                                                                                                                                                                                                                                                            |
| Source       | discovery — levantamento de campo PO/D003 (2026-06-06)                                                                                                                                                                                                        |
| Hint         | Confirma e detalha Q007 (híbrido). Superfície brownfield: mural físico + Google Forms + WhatsApp + papel. Stakeholder-chave de migração: secretária. Implicação de UX/adoção: o sistema deve ser mais simples que o Forms atual para vencer inércia.           |

---

## Encerramento de Descoberta — D003

| Campo                  | Valor                                                                          |
|------------------------|--------------------------------------------------------------------------------|
| Descoberta             | D003                                                                           |
| Status                 | ENCERRADA                                                                      |
| Data de encerramento   | 2026-06-06                                                                     |
| Fonte dos resultados   | PO / levantamento de campo                                                     |
| Questões respondidas   | Q008, Q009, Q010, Q011                                                         |
| Critérios re-scored    | Q002 (parked→answered, conf 80→88), Q004 (parked→answered, conf 65→85, Médio→ALTO) |
| Bloqueantes zerados    | impacto não quantificado; viabilidade integração agenda; processo informal     |
| CTO flag               | De-arriscado — apenas Google Calendar, auth simples; Technical Assessment leve |
| Próximo passo          | Re-triagem formal (Ato 1 Revisit) → avaliar Product Ready                      |

---

## Entradas da Descoberta Estendida — D005 (encerrada em 2026-06-06)

---

### Q012
- **Título:** Descoberta D005 — Valor monetário dos negócios adiados (DiscoveryValorRS)
- **Mode:** open
- **Status:** answered
- **Targets:** triage-criterion-4, business-impact, impact-quantification
- **spawned-by:** D005 (Descoberta estendida — item DiscoveryValorRS); Q009 (negócios adiados confirmados, valor R$ não quantificado)
- **Rationale:** Q009 confirmou qualitativamente que 78% dos conflitos geram negócio adiado, mas não quantificou o valor monetário em jogo. D005 foi aberta para fechar este último item de descoberta e transformar o impacto em cifra R$ concreta, necessária para justificativa de investimento e priorização executiva.

| Campo        | Valor                                                                                                                                                                                                                                                                                                                                                |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Choice       | —                                                                                                                                                                                                                                                                                                                                                    |
| Answer       | 9 adiamentos totais com ~R$700k de pipeline envolvido (valor total em jogo). Destes: 2 NEGÓCIOS PERDIDOS = R$111k (receita já perdida — não fecham mais); 1 NEGÓCIO EM ABERTO = R$90k (ainda travado por falta de agenda comum). Todos classificados como prospecção de novos negócios (receita nova, não recorrente). Fonte: levantamento comercial dedicado PO. |
| Disposition  | answered                                                                                                                                                                                                                                                                                                                                             |
| Confidence   | 90                                                                                                                                                                                                                                                                                                                                                   |
| Source       | discovery — D005/DiscoveryValorRS, levantamento comercial PO (2026-06-06)                                                                                                                                                                                                                                                                            |
| Hint         | RECONCILIAÇÃO com Q009: Q009 aponta "7 de 9 conflitos" com negócio adiado; este levantamento comercial (posterior e dedicado) aponta 9 adiamentos. Adotar 9 como número mais recente e detalhado — diferença pode refletir múltiplos adiamentos por conflito ou critério distinto de contagem. Flag para confirmação leve, NÃO bloqueante. Fecha o último item de D005. Atualiza Q004 (conf 85→90, impacto totalmente quantificado em R$). |

---

## Encerramento de Descoberta Estendida — D005

| Campo                  | Valor                                                                                                                                          |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| Descoberta             | D005 (estendida)                                                                                                                               |
| Status                 | ENCERRADA                                                                                                                                      |
| Data de encerramento   | 2026-06-06                                                                                                                                     |
| Fonte dos resultados   | PO / levantamento comercial dedicado                                                                                                           |
| Questões respondidas   | Q012                                                                                                                                           |
| Critérios re-scored    | Q004 (conf 85→90; impacto totalmente quantificado em R$ — R$111k perdidos, R$90k em risco, pipeline ~R$700k)                                   |
| Bloqueantes zerados    | valor monetário dos negócios adiados (DiscoveryValorRS) — último item pendente                                                                 |
| Nota de reconciliação  | Divergência de contagem Q009 (7/9) vs. Q012 (9 adiamentos): adotar 9 como mais recente; flag leve, NÃO bloqueante                             |
| Estado pós-fechamento  | TODOS os critérios de triagem answered; nenhum parked remanescente; impacto totalmente quantificado (operacional + monetário)                  |
| Próximo passo          | Re-triagem formal conclusiva (Ato 1 REVISIT-2) → Product Ready                                                                                |

---
<!-- END -->
