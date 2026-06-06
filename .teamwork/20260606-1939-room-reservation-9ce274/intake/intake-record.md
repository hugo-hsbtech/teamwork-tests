<!--
TARGET TEMPLATE · Intake Record (default) — Ato 1 da jornada do PO (triagem)
Este arquivo é o contrato da fase de TRIAGEM. Cada seção preenchível carrega a anotação:
  <!-- origination: id=SECTION-ID; blocks=BOOL; min-confidence=N; kind=TYPE -->
e uma rubrica autocontida. O modelo de decisão da triagem e da decisão de roteamento
carrega (verdict | rationale | basis | source | reversible) conforme personas/02-po.md §4-6.
Confiança mínima padrão (X) = 70. Elevada por seção para campos de alto risco.
-->

# Registro de Intake — Sistema de Reserva de Salas de Reunião
<!-- rev: 1 · updated: 2026-06-06 -->

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
| **Versão** | v1 |
| **Origination vinculado (origem)** | origination/output/humanized.md |
| **Registrado por (Submitter)** | Solicitante (canalizador) + reclamações coletivas internas |
| **Triado por (PO)** | PO (sessão de readiness, 2026-06-06) |
| **Data de triagem** | 2026-06-06 |
| **Status** | Triado |
| **Readiness Package vinculado** | — (não aplicável — decisão Discovery) |

## Histórico de Revisão
<!-- origination: id=revisions; blocks=false; min-confidence=0; kind=meta -->

| Versão | Data | Evento | Resumo |
|---|---|---|---|
| v1 | 2026-06-06 | Intake formalizado | Triagem concluída — Descoberta Direcionada. |

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
| **Impacto de negócio** | Quatro eixos qualitativos confirmados: tempo perdido (15-30 min/evento), reuniões importantes prejudicadas, retrabalho operacional (facilities), negócios adiados (custo de receita/relacionamento — maior gravidade potencial). Nenhum eixo quantificado. | 65 |
| **Urgência** (por que agora) | Pressão contínua confirmada pelo solicitante; sem prazo ou gatilho específico. Custo de esperar: novos conflitos e mais retrabalho a cada semana. | 70 |
| **Prioridade declarada** | Não declarada. | — |

**Provenance**
- **Confidence:** 74 (média ponderada das dimensões)
- **Origin:** inherited
- **Source:** registro de originação (humanized.md) — Q001, Q003, Q004, Q006, Q008, Q010
- **Status:** respondida
- **Disposition:** premissa (impacto — único eixo abaixo do limiar, sem quantificação)
- **Hint:** Quantificar impacto (nº de choques/semana × min/evento; valor de negócios adiados) na Descoberta.

---

## Triagem — critérios avaliados  ·  *(Ato 1 do PO)*
<!-- origination: id=triage-criteria; blocks=true; min-confidence=70; kind=capture; inputs=demand-summary -->

> O PO avalia cada critério (todos avaliados = `triageReady`). Cada veredito carrega
> o modelo de decisão: **verdict · rationale · basis · source**. Ver
> `references/triage.md` e `personas/02-po.md` §6.1.

| # | Critério | Veredito | Justificativa (rationale) | Base / Fonte |
|---|---|---|---|---|
| 1 | É um problema real (não sintoma isolado)? | **Sim** | Double-booking crônico com frequência semanal e reclamação coletiva confirmados. Dor recorrente documentada, não exceção isolada. | origination Q001/Q003 — confiança 80 |
| 2 | É recorrente / tem volume? | **Sim** *(premissa de volume)* | Recorrência semanal firme e origem coletiva confirmadas. Volume absoluto (nº de conflitos/semana, usuários afetados) não quantificado — tratado como premissa; item de Discovery. | inherited — origination problem/originator; volume: premissa (Q002 parked) |
| 3 | Encaixa na visão do produto? | **Sim, tangencial** | PO confirmou: reserva de salas não é core do produto, mas resolve dor interna real que justifica o investimento. Encaixe tangencial aceito. | po_authored — decisão PO (Q003); sem sinal de visão no origination |
| 4 | Qual o impacto técnico e de negócio? | **Médio** *(provisório — premissa)* | Negócio: 4 eixos qualitativos positivos (incl. negócios adiados), sem quantificação. Técnico: CRUD baixo-médio + integração com agenda corporativa (Google/Outlook) com incógnitas (APIs, SSO/OAuth, sincronização). | inherited — origination Q006/Q010 (premissa 65) + constraints Q009 (Q004 parked) |
| 5 | Urgência e impacto justificam agir agora? | **Sim — Descoberta agora** | PO decidiu abrir Descoberta Direcionada imediatamente para destravar: quantificar impacto e verificar viabilidade de integração, apesar de pressão contínua sem prazo fixo. | po_authored — decisão PO (Q005) |

**Provenance**
- **Confidence:** 77 (média: critérios 1/3/5 po_authored/herdados com conf ≥75; critérios 2/4 parked como premissa com conf 65-80)
- **Origin:** po_authored (critérios 3 e 5) / inherited (critérios 1, 2 e 4)
- **Source:** PO (sessão de triagem 2026-06-06) + registro de originação
- **Status:** respondida (5/5 critérios avaliados — triageReady)
- **Disposition:** premissa (critérios 2 e 4 — volume e impacto dependem de quantificação na Descoberta)
- **Hint:** Critérios 2 e 4 ficam como premissa até Discovery encerrar. Viabilidade de integração (critério 4) é item D002.

---

## Triagem — decisão de roteamento
<!-- origination: id=triage-decision; blocks=true; min-confidence=80; kind=capture; inputs=triage-criteria -->

> **Uma** decisão de caminho, com justificativa obrigatória. Só `Product Ready`
> abre o Ato 2; as demais encerram a passagem pelo PO neste momento (curto-circuito).

| Campo | Valor |
|---|---|
| **Decisão (verdict)** | **DESCOBERTA DIRECIONADA** (Discovery) |
| **Justificativa (rationale)** | Fundamentos sólidos: problema confirmado (80), alcance amplo (76), originador firme (80), urgência respondida (70). Três itens impedem o congelamento de escopo: (1) impacto não quantificado — premissa de valor; (2) viabilidade da integração com agenda corporativa (Google/Outlook) — requisito confirmado com incógnitas técnicas/arquiteturais; (3) processo informal atual a caracterizar (natureza híbrida confirmada). Encaixe tangencial na visão (não core). Decisão do PO no gate: Descoberta Direcionada. |
| **Base / Fonte (basis / source)** | Decisão do PO no gate de triagem (2026-06-06) + origination D001 (Descoberta Direcionada aprovada) e D002 (Escalação arquitetural confirmada) |
| **Reversível?** | Sim (porta lateral — Discovery/re-triagem ao encerrar) |
| **Submitter notificado** | Sim — 2026-06-06 |

> **Gate da triagem (`triageReady`):** todos os critérios avaliados (5/5). A decisão
> é **informada** — fundamentos sólidos levaram a Discovery, não fraqueza geral.
> Só `Product Ready` abriria o Ato 2; Discovery faz curto-circuito neste ciclo.

**Provenance**
- **Confidence:** 85
- **Origin:** po_authored
- **Source:** Decisão PO (2026-06-06) — Q006; origination D001/D002
- **Status:** respondida
- **Disposition:** decided
- **Hint:** Só Product Ready abriria o Ato 2. Discovery faz curto-circuito — Ato 2 não roda neste ciclo. Re-triar ao encerrar a Descoberta.

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
| **Natureza** | **Híbrido** — processo informal existente a formalizar/migrar + software-core novo + integração com agenda corporativa existente |
| **Sistema(s) afetado(s)** | Novo sistema de reserva de salas · processo informal atual (planilha/quadro/calendário — a caracterizar) · integração com agenda corporativa (Google Calendar e/ou Outlook) |
| **Base de conhecimento existe?** | **Não** → exige discovery de documentação |
| **Referência da Base de Conhecimento** | — (futura: tech-landscape-room-reservation.md) |

> **Nota de SUPERSEDÊNCIA:** a premissa greenfield inferida no registro de originação
> (`nature-signal`, confiança 70, disposição inferida) foi **SUPERSEDIDA** por esta
> entrada. O PO confirmou (Q007) que já existe um processo/ferramenta informal de
> reserva de salas hoje. A demanda é **híbrida**: formalizar/migrar o processo
> existente (superfície brownfield) com software-core novo e integração com agenda
> corporativa existente. A primeira tarefa técnica deve incluir documentar o processo
> informal atual.

> **Brownfield/Híbrido** → o Technical Assessment deve **referenciar** a Base de
> Conhecimento existente; como ela não existe, a primeira tarefa técnica é
> **criá-la** (documentar o sistema/processo atual) — registrado como item de Discovery.

**Provenance**
- **Confidence:** 78
- **Origin:** po_authored
- **Source:** Resposta PO (Q007) + origination nature-signal + constraints Q009
- **Status:** respondida
- **Disposition:** natureza confirmada; processo informal a caracterizar é item de Discovery
- **Hint:** Caracterizar a ferramenta/processo informal atual (planilha, quadro ou calendário compartilhado). CTO flag D002 ativo para integração com agenda corporativa.

---

## Escalada arquitetural ao CTO
<!-- origination: id=cto-escalation; blocks=false; min-confidence=0; kind=derived; inputs=triage-decision,demand-nature -->

**Necessária:** **SIM** — a integração com agenda corporativa (Google Calendar e/ou Outlook) é um requisito firme confirmado (Q009) que carrega incógnitas arquiteturais: plataforma(s) envolvida(s), APIs corporativas, SSO/OAuth, modelo de sincronização. Esta é a condição exata de gatilho para revisão de viabilidade/arquitetura.

> Flag antecipado (D002, 2026-06-06). A decisão autoritativa do `tech-assessment-ref`
> é tomada no Ato 2 (Readiness Package) pelo `hsb-escalation-flagger`; este é um
> early flag herdado adiante. A **natureza híbrida** da demanda (acima) também
> viaja: o Technical Assessment deve mapear o processo informal existente, não apenas
> definir a fundação do software novo.

---

## Premissas validadas na triagem
<!-- origination: id=validated-assumptions; blocks=false; min-confidence=0; kind=capture; inputs=demand-summary -->

> Premissas do origination que o PO revisou e o veredito de cada uma. As que
> sobrevivem viajam adiante explicitamente para o RP.

| Premissa (do origination) | Veredito do PO | A validar com |
|---|---|---|
| A magnitude do impacto (tempo perdido, reuniões prejudicadas, retrabalho) é estimativa qualitativa, não quantificada | **A validar** — item de Discovery | Admin/facilities + liderança comercial/diretoria: coletar nº de choques/semana × min/evento e exemplos de negócios adiados |
| "Negócios adiados" representa custo real de receita/relacionamento | **A validar** — item de Discovery | Liderança comercial / diretoria: solicitar exemplos concretos de negócios ou decisões adiados por conflito de sala |
| Não existe nenhuma ferramenta formal de reserva de salas em uso hoje (greenfield / nova capacidade) | **Rejeitada / Revisada** — PO confirmou (Q007) que processo informal JÁ EXISTE; natureza reclassificada como HÍBRIDA | — (já incorporado na seção Natureza da demanda acima) |

---

## Constraints reconhecidos
<!-- origination: id=constraints; blocks=false; min-confidence=0; kind=capture; inputs=demand-summary -->

> Constraints que o downstream deve considerar desde o primeiro dia (herdados do
> origination, validados aqui).

| Constraint | Tipo | Nota do PO |
|---|---|---|
| Integração com agenda corporativa (Google Calendar e/ou Outlook) | Técnico | Requisito firme declarado pelo solicitante (Q009). Dimensionar escopo na Descoberta: uma plataforma ou ambas? Há SSO/OAuth? Acesso a APIs corporativas? CTO flag D002 ativo. |

---

## Discovery Brief
<!-- origination: id=discovery; blocks=false; min-confidence=0; kind=derived; inputs=triage-decision; condition=triage-decision==Discovery -->

> Seção incluída porque a decisão de roteamento é **Discovery**.

### O que está faltando

| # | Incógnita | Quem pode responder | Método | Time-box |
|---|---|---|---|---|
| 1 | Quantificar impacto: nº de choques/semana × min/evento; valor estimado dos negócios adiados | Admin/facilities + liderança comercial/diretoria | Observação de registros + entrevistas com partes interessadas | (parte do time-box) |
| 2 | Viabilidade da integração com agenda corporativa (Google/Outlook): plataforma(s), APIs, SSO/OAuth, modelo de sincronização | Tech Lead/CTO + TI | Revisão de viabilidade/arquitetura | (parte do time-box) |
| 3 | Caracterizar o processo informal atual: qual ferramenta (planilha, quadro, calendário?), como funciona, quem usa, volume de uso | Admin/facilities + PO | Entrevista / observação direta | (parte do time-box) |

**Time-box do Discovery:** ~1 a 1,5 semana (2026-06-06 → ~2026-06-17)

### Resultado do Discovery

| # | Incógnita | Resolução | Impacto no escopo |
|---|---|---|---|
| 1 | Quantificação do impacto | (em aberto) | — |
| 2 | Viabilidade da integração com agenda corporativa | (em aberto) | — |
| 3 | Caracterização do processo informal atual | (em aberto) | — |

**Novo caminho de decisão:** Discovery → (a definir) Product Ready / Backlog / Rejeitar

**Discovery encerrado:** em aberto

---

## Handoff
<!-- origination: id=handoff; blocks=false; min-confidence=0; kind=derived; inputs=triage-decision -->

- **Decisão: Discovery** → abrir o Discovery Brief acima; ao encerrar a Descoberta, re-triar.
- **Escalação ao CTO (D002)** permanece devida: Technical Assessment da integração com agenda corporativa (Google/Outlook) deve ser iniciado em paralelo à Descoberta.
- **Ato 2 (Readiness Package) NÃO inicia neste ciclo** — aguarda re-triagem pós-Discovery com decisão `Product Ready`.
- **Submitter notificado:** Sim — 2026-06-06 (roteamento para Descoberta Direcionada comunicado).

<!-- END OF DOCUMENT -->
