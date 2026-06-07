<!--
SOURCES INDEX · Readiness Package Phase (Act 2)
room-reservation (INT-2026-001)
Generated: 2026-06-06
Language: pt-BR
-->

# Fontes Indexadas — Pacote de Prontidão (Ato 2)

> Índice normalizado das artefatos herdados do Ato 1 (Originação e Intake). Cada entrada descreve seu tipo, conteúdo-chave (especialmente impacto monetário, natureza Híbrida, restrição de integração de calendário, e premissas validadas que o RP deve levar adiante) e status de indexação.

| ID | Arquivo | Tipo | Conteúdo-Chave | Status |
|---|---|---|---|---|
| S001 | `origination-record.md` | Origination Record (v5 · canonical) | **Demanda consolidada:** conflito de agendamento (double-booking) crônico em salas de reunião. Recorrência semanal confirmada, impacto qualitativo em 4 eixos (tempo perdido operacional, reuniões importantes prejudicadas, retrabalho operacional, negócios adiados). **Confiança maturidade:** ~74% (impacto não quantificado, marcado premissa). **Restrições:** integração obrigatória com Google Calendar e/ou Outlook (requisito firme, questões de SSO e escopo pendentes no momento do origination). **Natureza-sinal:** nova capacidade (infere-se greenfield, embora com dúvida). **Triage:** Descoberta Direcionada (rascunho gerado por IA, confirmado pelo solicitante em D001/D002). **Premissas em aberto:** (1) impacto qualitativo sem quantificação (será validado); (2) negócios adiados é custo real de receita (será validado); (3) não existe ferramenta formal de reserva hoje (será validado). **Escalação arquitetural:** necessária (integração com incógnitas). **Briefing de Descoberta:** 4 incógnitas, prazo ~1-1,5 semana. | indexed |
| S002 | `intake-record.md` (v3 · final) | Intake Record (Ato 1 do PO — triagem) | **Triagem final:** PRODUCT READY (abre Ato 2). **Decisão do PO (REVISIT-2):** Descoberta encerrada (D003 + D005), todas as incógnitas resolvidas. **Impacto totalmente quantificado:** operacional + monetário. Frequência: 9 conflitos em 5 semanas (~1,8/semana, pico 10h–16h, ~3 dias de atraso médio por conflito). Valor monetário (R$): **R$111k já PERDIDOS** (2 negócios que não fecham mais), **R$90k EM RISCO** (1 negócio aberto ainda travado), pipeline total ~R$700k de novos negócios (prospecção = receita nova, não recorrente). Confiança: ~90. **Natureza HÍBRIDA CONFIRMADA (D004):** existe processo informal caracterizado — papel no mural (fonte de verdade) + Google Forms via WhatsApp + papel, mantido pela secretária. Novo sistema migra/substitui esse processo. **Restrição confirmada e de-arriscada:** apenas Google Calendar (Outlook descartado), sem SSO corporativo, autenticação simples/login social aceitável (D003/Q010). **Escalação ao CTO:** LEVE (Technical Assessment apenas para confirmar fluxo OAuth do Google Calendar). **Premissas validadas herdadas do origination:** (1) impacto RESOLVIDO — totalmente quantificado; (2) negócios adiados CONFIRMADA com valor R$; (3) greenfield REJEITADA — Híbrido confirmado; processo informal caracterizado. **Constraints reconhecidos:** integração apenas Google Calendar (de-arriscada), migração do processo manual (secretária = stakeholder-chave, gestão de mudança necessária). **Discovery D003/D005 encerrada:** 2026-06-06. **Handoff:** Ato 2 (Readiness Package RP-2026-001) INICIADO; Technical Assessment LEVE (OAuth Google Calendar) deferido ao Readiness Package antes do congelamento de escopo. | indexed |

---

## Resumo de Indexação

**Total de fontes indexadas:** 2
**Total de fontes não resolvidas:** 0

**Origens normalizadas:**
1. `origination/output/humanized.md` → `sources/origination-record.md` ✓
2. `intake/intake-record.md` → `sources/intake-record.md` ✓

**Contexto (referência, não copiado):**
- `decisions.md` (D001–D007) — referenciado nas descrições acima; viaja como contexto de decisão

---

## Notas Críticas para o Evidence Extractor (Ato 2)

### Impacto Monetário (R$) — Prioridade Máxima para RP

O **Intake Record (S002, v3)** carrega a quantificação final do impacto monetário, validada na Descoberta:

- **R$111.000 já PERDIDOS:** 2 negócios fechados que não conseguem mais fechar (perda de receita confirmada)
- **R$90.000 EM RISCO:** 1 negócio aberto que está travado por conflito de sala
- **Pipeline envolvido:** ~R$700.000 (prospecção de novos negócios — receita nova/não recorrente)
- **Operacional quantificado:** 9 conflitos em 5 semanas (~1,8/semana), ~3 dias de atraso médio de reagendamento, pico 10h–16h

Este é o valor monetário que destravou o gate Product Ready (D007). O RP deve levar este valor adiante como evidência de prioridade executiva.

### Natureza Híbrida — Mudança Crítica de Escopo

O **Intake Record (S002)** anula a premissa greenfield do Origination Record (S001) com evidência de descoberta:

- **Processo atual caracterizado:** mural físico (papel na parede = fonte de verdade) + Google Forms (link via WhatsApp) + anotação em papel
- **Operador:** secretária (stakeholder-chave de migração)
- **Escopo: NÃO apenas construir novo software** — deve migrar/formalizar o processo manual existente
- **Gestão de mudança necessária:** o novo sistema deve ser mais simples que o Forms atual para vencer inércia de adoção

O RP deve referenciar esta natureza híbrida no desenho arquitetural; o Technical Assessment deve mapear o processo existente (não apenas a fundação do software novo).

### Restrição de Integração — De-Arriscada (Scope Reducer)

O **Intake Record (S002, D003/Q010)** reduziu significativamente a incógnita arquitetural:

- **Integração apenas com Google Calendar** (Outlook descartado)
- **Sem SSO corporativo** (não é requisito)
- **Autenticação simples/login social é aceitável**
- **CTO flag:** LEVE (apenas confirmar fluxo OAuth Google Calendar)

Isto reduz o escopo técnico e a escalação ao CTO. O RP deve documentar este fluxo OAuth antes de congelar o escopo técnico, conforme handoff do Intake Record.

### Premissas Validadas que Viajam Adiante

Do **Origination Record (S001)**, 3 premissas foram herdadas:

1. **Impacto qualitativo não quantificado** → **RESOLVIDA (D003 + D005)** — R$ e operacional firmados
2. **"Negócios adiados" é custo real de receita** → **CONFIRMADA com valor R$ (D005/Q012)** — 9 adiamentos com R$111k perdido + R$90k em risco
3. **Greenfield (nenhuma ferramenta formal hoje)** → **REJEITADA — HÍBRIDO (D003/Q011)** — processo informal caracterizado (mural + Forms + WhatsApp)

O RP **herda nenhuma premissa aberta** — todas foram validadas ou incorporadas como escopo Híbrido. Isto é anomalia positiva: prioridade máxima para execução.

---

## Artefatos de Contexto (Não Indexados, Apenas Referenciados)

Estes artefatos viajam como contexto decisório mas não são fontes de descoberta para o RP:

- **decisions.md** — Registro de decisões entre frentes (D001–D007). Referencia o fluxo Origination → Intake → Readiness. O RP deve estar ciente de que D007 abre o Ato 2 e que todas as incógnitas de Descoberta foram encerradas antes de iniciar.

---

<!-- END OF SOURCES INDEX -->
