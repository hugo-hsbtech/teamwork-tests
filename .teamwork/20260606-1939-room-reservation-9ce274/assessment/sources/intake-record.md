<!--
TARGET TEMPLATE · Intake Record (default) — Ato 1 da jornada do PO (triagem)
Este arquivo é o contrato da fase de TRIAGEM. Cada seção preenchível carrega a anotação:
  <!-- origination: id=SECTION-ID; blocks=BOOL; min-confidence=N; kind=TYPE -->
e uma rubrica autocontida. O modelo de decisão da triagem e da decisão de roteamento
carrega (verdict | rationale | basis | source | reversible) conforme personas/02-po.md §4-6.
Confiança mínima padrão (X) = 70. Elevada por seção para campos de alto risco.
-->

# Registro de Intake — Sistema de Reserva de Salas de Reunião
<!-- rev: 3 · updated: 2026-06-06 -->

> O Registro de Intake é o **artefato do Ato 1 do PO: a triagem**. Ele recebe o
> registro de originação (`Product Ready`-candidato), atribui o ID `INT-AAAA-NNN` e
> registra a **decisão de roteamento** (Product Ready / Discovery / Backlog /
> Rejeitar) com justificativa rastreável. Ele **não** reescreve a captura — a
> referencia e a consolida. O aprofundamento de produto é o Ato 2 (Readiness
> Package). Só `Product Ready` abre o Ato 2.

## Metadados
<!-- origination: id=meta; blocks=false; min-confidence=0; kind=meta -->

| Campo | Valor |
|---|---|
| **ID do Registro** | INT-2026-001 |
| **Versão** | v3 |
| **Origination vinculado (origem)** | origination/output/humanized.md |
| **Registrado por (Submitter)** | Solicitante (canalizador) + reclamações coletivas internas |
| **Triado por (PO)** | PO (sessão de readiness, 2026-06-06) |
| **Data de triagem** | 2026-06-06 |
| **Status** | Triado — Product Ready |
| **Readiness Package vinculado** | RP-2026-001 (a ser criado no Ato 2) |

## Histórico de Revisão
<!-- origination: id=revisions; blocks=false; min-confidence=0; kind=meta -->

| Versão | Data | Evento | Resumo |
|---|---|---|---|
| v1 | 2026-06-06 | Intake formalizado | Triagem concluída — Descoberta Direcionada. |
| v2 | 2026-06-06 | Re-triagem pós-Descoberta (D003) | Re-triagem com achados da Descoberta (D003): 3 incógnitas fechadas; decisão mantida em Descoberta — pendente quantificar valor (R$) dos negócios adiados. |
| v3 | 2026-06-06 | Descoberta estendida encerrada (valor R$ dos negócios adiados quantificado); re-triagem → PRODUCT READY. Abre o Ato 2 (Readiness Package). | D005 encerrada: R$111k perdidos, R$90k em risco, pipeline ~R$700k. PO comitou Product Ready no gate de re-triagem (REVISIT-2). Ato 2 iniciado — Readiness Package RP-2026-001. |

---

## Prontidão recebida do origination
<!-- origination: id=inherited-readiness; blocks=false; min-confidence=0; kind=derived; inputs=demand-summary -->

> Retrato herdado do registro de originação no handoff. O PO não recalcula a captura —
> registra o que recebeu e o que segue em aberto (soft).

| Campo | Valor |
|---|---|
| **Readiness Score no handoff** | ~74% |
| **Requisitos bloqueantes** | Todos resolvidos por disposição honesta (`gateReady`) — Sim |
| **Dispositions em aberto** | 3 premissas a validar · 0 discovery formal (origination) · 0 delegados |

---

## Demanda consolidada
<!-- origination: id=demand-summary; blocks=true; min-confidence=70; kind=capture -->

> Resumo de uma tela, validado pelo PO contra o registro de originação (não é
> re-digitação — é a leitura do PO). Cada dimensão herda a confiança da captura.
> ⚠️ Problema = a dor, não a solução.

| Dimensão | Síntese | Confiança herdada |
|---|---|---|
| **Problema** (a dor, não a solução) | Conflito de agendamento (double-booking) crônico: pessoas marcam reuniões em salas já ocupadas, "vira confusão" toda semana, sem parar — dor coletiva e recorrente, não exceção isolada. | 80 |
| **Alcance** (quem é impactado) | Quatro perfis: equipes que disputam a sala · reuniões com clientes/externos (risco de imagem) · liderança e diretoria · facilities/recepção (retrabalho de remarcar). Alcance amplo e multi-perfil. | 76 |
| **Impacto de negócio** | Impacto totalmente quantificado (D003 + D005): ~9 conflitos em 5 semanas (~1,8/semana), dias úteis, pico 10h–16h. Reagendamento penaliza quem chegou por último — atraso médio ~3 dias para reencontrar agenda comum. 9 adiamentos de negócios com pipeline total envolvido de ~R$700k. **R$111k já PERDIDOS** (2 negócios que não fecham mais); **R$90k EM RISCO** (1 negócio aberto ainda travado). Todos de prospecção de novos negócios (receita nova, não recorrente). Nota de reconciliação: D003/Q009 apontou 7/9 conflitos; D005/Q012 (levantamento comercial posterior e dedicado) aponta 9 adiamentos — adotado 9 como valor mais recente; diferença não bloqueante. | ~90 |
| **Urgência** (por que agora) | Pressão contínua confirmada pelo solicitante; sem prazo ou gatilho específico. Custo de esperar: novos conflitos e mais retrabalho a cada semana. | 70 |
| **Prioridade declarada** | Não declarada. | — |

**Provenance**
- **Confidence:** ~90 (impacto totalmente quantificado em frequência, atraso, contagem e valor monetário R$ — D003 + D005)
- **Origin:** inherited + discovery (D003 + D005)
- **Source:** registro de originação (humanized.md) — Q001, Q003, Q004, Q006; D003 — Q008, Q009; D005 — Q012 (levantamento comercial 2026-06-06)
- **Status:** respondida
- **Disposition:** answered
- **Hint:** Impacto totalmente quantificado. Reconciliação D003 vs. D005 (7 vs. 9 adiamentos): adotado 9 — flag leve, não bloqueante.

---

## Triagem — critérios avaliados  ·  *(Ato 1 do PO)*
<!-- origination: id=triage-criteria; blocks=true; min-confidence=70; kind=capture; inputs=demand-summary -->

> O PO avalia cada critério (todos avaliados = `triageReady`). Cada veredito carrega
> o modelo de decisão: **verdict · rationale · basis · source**. Ver
> `references/triage.md` e `personas/02-po.md` §6.1.

| # | Critério | Veredito | Justificativa (rationale) | Base / Fonte |
|---|---|---|---|---|
| 1 | É um problema real (não sintoma isolado)? | **Sim** | Double-booking crônico com frequência semanal e reclamação coletiva confirmados. Dor recorrente documentada, não exceção isolada. | origination Q001/Q003 — confiança 80 |
| 2 | É recorrente / tem volume? | **Sim, volume QUANTIFICADO** | Recorrência e volume confirmados por dados de campo (D003): 9 conflitos em 5 semanas ≈ 1,8/semana, dias úteis, pico 10h–16h. Premissa anterior firmada como fato — não mais estimativa. | discovery — D003/Q008, levantamento de campo PO (2026-06-06); conf 88 |
| 3 | Encaixa na visão do produto? | **Sim, tangencial** | PO confirmou: reserva de salas não é core do produto, mas resolve dor interna real que justifica o investimento. Encaixe tangencial aceito. | po_authored — decisão PO (Q003); sem sinal de visão no origination |
| 4 | Qual o impacto técnico e de negócio? | **ALTO** *(totalmente quantificado — operacional + R$)* | Negócio: ~1,8 conflitos/sem, ~3 dias de atraso por conflito, 9 adiamentos com pipeline ~R$700k; R$111k já PERDIDOS (2 negócios); R$90k EM RISCO (1 negócio aberto) — todos de prospecção de novos negócios. Impacto de receita/relacionamento firmado como fato, agora com cifra R$ concreta. Técnico: de-arriscado — apenas Google Calendar (Outlook descartado), sem SSO corporativo, auth simples/login social aceitável; risco arquitetural reduzido. Impacto global: ALTO — totalmente quantificado. | discovery — D003/Q008/Q009/Q010 (levantamento de campo 2026-06-06); D005/Q012 (levantamento comercial 2026-06-06); conf 90 |
| 5 | Urgência e impacto justificam agir agora? | **Sim — Product Ready** | PO comitou Product Ready no gate de re-triagem (REVISIT-2). Descoberta encerrada (D003+D005); todos os critérios respondidos; impacto ALTO totalmente quantificado em R$; integração viável. Ato 2 aberto. | po_authored — decisão PO (REVISIT-2, 2026-06-06) |

**Provenance**
- **Confidence:** ~90 (todos os 5 critérios answered; critério 4 re-scored conf 85→90 após quantificação monetária completa via D005/Q012)
- **Origin:** po_authored (critérios 3 e 5) / inherited (critério 1) / discovery D003 (critérios 2 e 4) / discovery D005 (critério 4 — valor R$)
- **Source:** PO (sessão de triagem + REVISIT-2, 2026-06-06) + registro de originação + D003 Q008/Q009/Q010 (levantamento de campo) + D005/Q012 (levantamento comercial)
- **Status:** respondida (5/5 critérios avaliados — triageReady)
- **Disposition:** answered
- **Hint:** Todos os critérios totalmente respondidos. Critério 4 ALTO totalmente quantificado em R$. CTO flag de-arriscado: Technical Assessment leve (OAuth Google Calendar) deferred ao Ato 2.

---

## Triagem — decisão de roteamento
<!-- origination: id=triage-decision; blocks=true; min-confidence=80; kind=capture; inputs=triage-criteria -->

> **Uma** decisão de caminho, com justificativa obrigatória. Só `Product Ready`
> abre o Ato 2; as demais encerram a passagem pelo PO neste momento (curto-circuito).

| Campo | Valor |
|---|---|
| **Decisão (verdict)** | **PRODUCT READY** |
| **Justificativa (rationale)** | Descoberta encerrada (D003 + D005): todas as incógnitas resolvidas. Impacto ALTO e totalmente quantificado em R$: R$111k perdidos (2 negócios), R$90k em risco (1 negócio aberto), pipeline ~R$700k de novos negócios. Integração viável e de-arriscada (apenas Google Calendar, sem SSO, auth simples/login social aceitável). Processo atual caracterizado (Híbrido — mural + Forms + WhatsApp, mantido pela secretária). PO comitou Product Ready no gate de re-triagem (REVISIT-2). |
| **Base / Fonte (basis / source)** | Decisão do PO no gate de re-triagem REVISIT-2 (2026-06-06) — D003 encerrada (3/4 itens) + D005 encerrada (valor R$); todos os critérios answered |
| **Reversível?** | — (abre o Ato 2) |
| **Submitter notificado** | Sim — 2026-06-06 (roteamento Product Ready comunicado; Ato 2 iniciado) |

> **Gate da re-triagem REVISIT-2 (`triageReady`):** todos os critérios avaliados (5/5), todos answered. Descoberta (D003+D005) totalmente encerrada. Impacto ALTO quantificado em R$; integração de-arriscada. PO comitou `Product Ready` — Ato 2 (Readiness Package RP-2026-001) aberto.

**Provenance**
- **Confidence:** ~90
- **Origin:** po_authored
- **Source:** Decisão PO no gate de re-triagem REVISIT-2 (2026-06-06) — D003 + D005 encerradas; impacto totalmente quantificado (operacional + R$)
- **Status:** respondida
- **Disposition:** decided
- **Hint:** Abre o Ato 2 — Readiness Package RP-2026-001. Technical Assessment LEVE (OAuth Google Calendar) deferred ao RP.

---

## Natureza da demanda e Base de Conhecimento  ·  *(classificação — nasce aqui)*
<!-- origination: id=demand-nature; blocks=true; min-confidence=70; kind=capture; inputs=demand-summary -->

> **Por que esta seção existe.** Antes de qualquer avaliação técnica, é preciso
> saber se a demanda constrói **software novo** ou altera **software existente** —
> greenfield *decide* a fundação (stack, ADRs, estrutura); brownfield *descobre* o
> que já existe (padrões, integrações, dívida). Sem esta classificação, o CTO
> adivinha. A camada de IA/engenharia **não tem conhecimento implícito do código** —
> depende do que está declarado aqui. Semeada pelo sinal "Toca o quê" do
> registro de originação; é aqui que o PO a firma. Ver [`03-technical-assessment.md`].

| Campo | Valor |
|---|---|
| **Natureza** | **HÍBRIDO CONFIRMADO** — processo informal existente caracterizado (D003) + software-core novo + integração com Google Calendar |
| **Sistema(s) afetado(s)** | Novo sistema de reserva de salas + integração com Google Calendar + migração do processo manual (mural físico + Google Forms via WhatsApp + papel), mantido pela secretária |
| **Base de conhecimento existe?** | **Não** → exige discovery de documentação |
| **Referência da Base de Conhecimento** | — (futura: tech-landscape-room-reservation.md) |

> **Nota de SUPERSEDÊNCIA:** a premissa greenfield inferida no registro de originação
> (`nature-signal`, confiança 70, disposição inferida) foi **SUPERSEDIDA** por esta
> entrada. O PO confirmou (Q007) que já existe um processo/ferramenta informal de
> reserva de salas hoje. A demanda é **híbrida**: formalizar/migrar o processo
> existente (superfície brownfield) com software-core novo e integração com agenda
> corporativa existente.

> **Processo informal caracterizado (D003/Q011):** reserva atual feita por anotação
> em **PAPEL no MURAL** (fonte de verdade) + **Google Forms** (link enviado via
> **WhatsApp**); às vezes só no papel. Mantido pela **SECRETÁRIA**, que atua como
> árbitro/gestor da escala. O novo sistema substitui/migra esse processo manual
> (mural + Forms + WhatsApp). Stakeholder-chave de migração: secretária.

> **Brownfield/Híbrido** → o Technical Assessment deve **referenciar** a Base de
> Conhecimento existente; como ela não existe, a primeira tarefa técnica é
> **criá-la** (documentar o sistema/processo atual). Atenção à gestão de mudança:
> o sistema deve ser mais simples que o Forms atual para vencer inércia de adoção.

**Provenance**
- **Confidence:** ~85
- **Origin:** po_authored + discovery D003 (Q007 + Q011)
- **Source:** Resposta PO (Q007) + origination nature-signal + D003/Q011 (levantamento de campo 2026-06-06)
- **Status:** respondida
- **Disposition:** natureza HÍBRIDA confirmada; processo informal caracterizado (mural + Forms + WhatsApp, secretária); migração no escopo
- **Hint:** Gestão de mudança necessária — secretária é stakeholder-chave; sistema deve superar usabilidade do Forms atual. Base de Conhecimento a criar na primeira tarefa técnica.

---

## Escalada arquitetural ao CTO
<!-- origination: id=cto-escalation; blocks=false; min-confidence=0; kind=derived; inputs=triage-decision,demand-nature -->

**Necessária:** **SIM, porém DE-ARRISCADA** — integração confirmada apenas com Google Calendar (Outlook descartado); sem SSO corporativo; autenticação simples/login social é aceitável. As incógnitas arquiteturais amplas originais foram resolvidas pela Descoberta (D003/Q010). Resta um **Technical Assessment LEVE** para confirmar o fluxo OAuth do Google Calendar antes de congelar o escopo técnico.

> Flag D002 atualizado (2026-06-06). Escopo original da escalação era amplo (Google e/ou
> Outlook, SSO/OAuth, múltiplas plataformas); após D003, reduziu-se significativamente.
> A decisão autoritativa do `tech-assessment-ref` é tomada no Ato 2 (Readiness Package)
> pelo `hsb-escalation-flagger`; este flag viaja adiante com escopo de-arriscado.
> A **natureza híbrida** da demanda (acima) também viaja: o Technical Assessment deve
> mapear o processo informal existente (mural + Forms + WhatsApp, mantido pela secretária),
> não apenas definir a fundação do software novo.

---

## Premissas validadas na triagem
<!-- origination: id=validated-assumptions; blocks=false; min-confidence=0; kind=capture; inputs=demand-summary -->

> Premissas do origination que o PO revisou e o veredito de cada uma. As que
> sobrevivem viajam adiante explicitamente para o RP.

| Premissa (do origination) | Veredito do PO | A validar com |
|---|---|---|
| A magnitude do impacto (tempo perdido, reuniões prejudicadas, retrabalho) é estimativa qualitativa, não quantificada | **RESOLVIDA — totalmente quantificada (D003 + D005)** — frequência e custo operacional quantificados (D003): 9 conflitos/5sem ≈ 1,8/sem, ~3 dias de atraso por conflito. Valor monetário (R$) quantificado (D005/Q012): R$111k perdidos (2 negócios), R$90k em risco (1 negócio aberto), pipeline ~R$700k — todos de prospecção de novos negócios. | — (resolvida; impacto totalmente quantificado em operacional + R$) |
| "Negócios adiados" representa custo real de receita/relacionamento | **CONFIRMADA com valor R$ (D003/Q009 + D005/Q012)** — 9 adiamentos de negócios confirmados com valor monetário firme: R$111k perdidos (2 negócios que não fecham mais), R$90k em risco (1 negócio ainda travado), pipeline total ~R$700k de novos negócios. Nota de reconciliação: D003/Q009 apontou 7/9 conflitos; D005/Q012 (levantamento comercial posterior e dedicado) aponta 9 adiamentos — adotado 9 como mais recente; diferença não bloqueante. | — (resolvida; confirmada com valor R$) |
| Não existe nenhuma ferramenta formal de reserva de salas em uso hoje (greenfield / nova capacidade) | **REJEITADA — HÍBRIDO CONFIRMADO (D003/Q011)** — processo informal caracterizado: anotação em PAPEL no MURAL (fonte de verdade) + Google Forms (link via WhatsApp), às vezes só no papel; mantido pela secretária | — (incorporado em Natureza da demanda e Constraints; migração no escopo) |

---

## Constraints reconhecidos
<!-- origination: id=constraints; blocks=false; min-confidence=0; kind=capture; inputs=demand-summary -->

> Constraints que o downstream deve considerar desde o primeiro dia (herdados do
> origination, validados aqui).

| Constraint | Tipo | Nota do PO |
|---|---|---|
| Integração apenas com Google Calendar (Outlook descartado); sem SSO corporativo; autenticação simples/login social aceitável | Técnico | Requisito firme — de-arriscado (D003/Q010). Escopo de integração confirmado e reduzido. Technical Assessment LEVE para confirmar fluxo OAuth Google Calendar ainda indicado. CTO flag D002 atualizado. |
| Migração do processo manual (mural físico + Google Forms via WhatsApp + papel), mantido pela secretária | Escopo / Externo | Confirmado como requisito de escopo (D003/Q011). Secretária é stakeholder-chave de migração. Considerar gestão de mudança — sistema deve superar usabilidade do processo atual para vencer inércia de adoção. |

---

## Discovery Brief
<!-- origination: id=discovery; blocks=false; min-confidence=0; kind=derived; inputs=triage-decision; condition=triage-decision==Discovery -->

> Seção mantida como registro histórico das Descobertas (D003 + D005) que suportaram a decisão final. A condição `triage-decision==Discovery` foi superada pela re-triagem REVISIT-2 → **Product Ready**.

### O que está faltando

> D003 encerrada em 2026-06-06 com 3 de 4 incógnitas resolvidas. D005 encerrada em 2026-06-06 com o valor R$ dos negócios adiados quantificado. Descoberta totalmente encerrada (D003 + D005) — todos os itens resolvidos.

| # | Incógnita | Quem pode responder | Método | Time-box |
|---|---|---|---|---|
| 1 | Quantificar impacto: nº de choques/semana × min/evento; valor estimado dos negócios adiados | Admin/facilities + liderança comercial/diretoria | Observação de registros + entrevistas com partes interessadas | (parte do time-box D003) |
| 2 | Viabilidade da integração com agenda corporativa (Google/Outlook): plataforma(s), APIs, SSO/OAuth, modelo de sincronização | Tech Lead/CTO + TI | Revisão de viabilidade/arquitetura | (parte do time-box D003) |
| 3 | Caracterizar o processo informal atual: qual ferramenta (planilha, quadro, calendário?), como funciona, quem usa, volume de uso | Admin/facilities + PO | Entrevista / observação direta | (parte do time-box D003) |
| 4 | Valor (R$) dos negócios adiados — quantificar o custo de receita (contagem 9 adiamentos confirmada; faltava o valor financeiro) | Liderança comercial / financeiro | Levantamento comercial dedicado PO | (D005 — nova rodada de Descoberta) |

**Time-box do Discovery D003:** ~1 a 1,5 semana (2026-06-06 → ~2026-06-17) — encerrado em 2026-06-06 (3/4 itens)
**Time-box do Discovery D005:** encerrado em 2026-06-06 (1/1 item — valor R$ quantificado)

### Resultado do Discovery

| # | Incógnita | Resolução | Impacto no escopo |
|---|---|---|---|
| 1 | Quantificação do impacto | **RESOLVIDO (D003/Q008):** 9 conflitos/5sem (~1,8/sem), pico 10h–16h, ~3 dias de atraso médio por conflito — dados de campo confirmados | Confirma prioridade; impacto ALTO firmado como fato |
| 2 | Viabilidade da integração com agenda corporativa | **RESOLVIDO (D003/Q010):** apenas Google Calendar (Outlook descartado); sem SSO corporativo; auth simples/login social aceitável — viável e de baixo risco | Reduz escopo técnico; Technical Assessment LEVE suficiente (OAuth Google Calendar) |
| 3 | Caracterização do processo informal atual | **RESOLVIDO (D003/Q011):** mural físico (fonte de verdade) + Google Forms (link via WhatsApp) + papel; mantido pela secretária — superfície brownfield mapeada | Confirma natureza Híbrida; define escopo de migração; secretária = stakeholder-chave |
| 4 | Valor (R$) dos negócios adiados | **RESOLVIDO (D005/Q012):** pipeline ~R$700k envolvido; R$111k já PERDIDOS (2 negócios que não fecham mais); R$90k EM RISCO (1 negócio aberto ainda travado). Todos de prospecção de novos negócios (receita nova, não recorrente). Nota de reconciliação: Q009 apontou 7/9 conflitos; Q012 (levantamento comercial posterior e dedicado) aponta 9 adiamentos — adotado 9; diferença não bloqueante. | Impacto totalmente quantificado em R$; suporta justificativa de investimento executivo; destrava Product Ready |

**Novo caminho de decisão:** Discovery → (D003 — mantida) Discovery estendida → (D005 encerrada) **PRODUCT READY**

**Discovery D003 encerrado:** 2026-06-06 (3/4 itens resolvidos)
**Discovery D005 encerrado:** 2026-06-06 (1/1 item resolvido — valor R$ dos negócios adiados)
**Descoberta totalmente encerrada (D003 + D005):** 2026-06-06

---

## Handoff
<!-- origination: id=handoff; blocks=false; min-confidence=0; kind=derived; inputs=triage-decision -->

- **Decisão: PRODUCT READY** → inicia o Ato 2 (Readiness Package RP-2026-001). Descoberta totalmente encerrada (D003 + D005); impacto ALTO quantificado em R$; integração de-arriscada; processo atual caracterizado.
- **Technical Assessment LEVE (OAuth Google Calendar)** permanece devido/deferred ao Ato 2: D003 de-arriscou a integração (apenas Google, sem SSO, auth simples), mas o fluxo OAuth deve ser confirmado e documentado no Readiness Package antes de congelar o escopo técnico.
- **Ato 2 (Readiness Package RP-2026-001) INICIADO** — roteamento Product Ready confirmado pelo PO no gate de re-triagem REVISIT-2 (2026-06-06).
- **D003 encerrada:** 2026-06-06 — 3 de 4 incógnitas resolvidas (impacto operacional, viabilidade de integração, processo informal).
- **D005 encerrada:** 2026-06-06 — valor R$ dos negócios adiados quantificado: R$111k perdidos, R$90k em risco, pipeline ~R$700k.
- **Submitter notificado:** Sim — 2026-06-06 (decisão Product Ready comunicada; Ato 2 aberto).

<!-- END OF DOCUMENT -->
