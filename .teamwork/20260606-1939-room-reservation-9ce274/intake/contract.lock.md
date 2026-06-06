---
template: target-template.intake-record.md
template_hash: e93729d8e292a99e987b93b8dd5a139cec2d980f97f0e63ac02315ab50c6f8dd
template_version: v1
default_min_confidence: 70
generated: 2026-06-06
language: pt-BR
notes: Fresh run — no prior contract. 4 blocking sections gate the triage pass.
---

# Contract — Intake Record (Act 1 · Triage)

| id | section | kind | blocks | min-confidence | inputs | condition | rubric (one line) |
|----|---------|------|--------|----------------|--------|-----------|-------------------|
| meta | Metadados | meta | false | 0 | — | — | ID do registro, versão, origination vinculado, responsáveis e status preenchidos |
| revisions | Histórico de Revisão | meta | false | 0 | — | — | Pelo menos a entrada v1 com data e evento registrados |
| inherited-readiness | Prontidão recebida do origination | derived | false | 0 | demand-summary | — | Readiness Score do handoff, status dos requisitos bloqueantes e dispositions em aberto declarados |
| demand-summary | Demanda consolidada | capture | true | 70 | — | — | Todas as cinco dimensões (problema, alcance, impacto, urgência, prioridade) sintetizadas com confiança herdada do origination; problema descrito como dor, não solução |
| triage-criteria | Triagem — critérios avaliados | capture | true | 70 | demand-summary | — | Todos os cinco critérios com verdict + rationale + basis/source; ausência de avaliação em qualquer critério bloqueia o gate triageReady |
| triage-decision | Triagem — decisão de roteamento | capture | true | 80 | triage-criteria | — | Uma única decisão de roteamento (Product Ready / Discovery / Backlog / Rejeitar) com rationale defensável, basis/source e flag de reversibilidade; Submitter notificado |
| demand-nature | Natureza da demanda e Base de Conhecimento | capture | true | 70 | demand-summary | — | Classificação greenfield/brownfield/híbrido firmada pelo PO com sistema(s) afetado(s) e status da Base de Conhecimento declarados |
| cto-escalation | Escalada arquitetural ao CTO | derived | false | 0 | triage-decision,demand-nature | — | Flag de necessidade de Technical Assessment (Sim/Não) com breve justificativa; derivado de demand-nature e triage-decision |
| validated-assumptions | Premissas validadas na triagem | capture | false | 0 | demand-summary | — | Cada premissa do origination revisada com veredito do PO (Aceita / Rejeitada / A validar) e responsável para validação futura |
| constraints | Constraints reconhecidos | capture | false | 0 | demand-summary | — | Constraints herdados do origination listados por tipo (Tempo / Orçamento / Legal / Técnico / Escopo / Externo) com nota do PO |
| discovery | Discovery Brief | derived | false | 0 | triage-decision | triage-decision==Discovery | Preencher somente se decisão == Discovery: incógnitas, responsáveis, método e time-box declarados; resultado registrado ao encerrar |
| handoff | Handoff | derived | false | 0 | triage-decision | — | Caminho de handoff declarado conforme decisão: Product Ready → Ato 2; Discovery → brief aberto; Backlog/Rejeitar → Submitter notificado |

## Gate summary

`triageReady` (gate do Ato 1) é liberado quando **todas** as seções com `blocks=true` estão resolvidas
ou receberam disposição honesta (`assumption` / `discovery` / `deferred`):

| Seção bloqueante | min-confidence |
|-----------------|---------------|
| demand-summary | 70 |
| triage-criteria | 70 |
| triage-decision | 80 |
| demand-nature | 70 |

Apenas `triage-decision == Product Ready` abre o Ato 2. Os demais valores
(`Discovery`, `Backlog`, `Rejeitar`) encerram a passagem pelo PO neste Ato.

## Audit validation

Audit checklist status (Template Validator passed):
- Todas as 12 secoes carregam annotation com id, blocks, min-confidence, kind.
- Todas as secoes `capture` com min-confidence > 0 carregam bloco Provenance vertical.
- Todas as secoes `derived` declaram `inputs`; `discovery` declara `condition`.
- `blocks=true` atribuido exatamente às 4 secoes de alto risco da triagem.
- Rubrica auto-suficiente em todas as secoes.

<!-- END OF DOCUMENT -->
