# Enrichment plan — Sistema de Reserva de Salas de Reunião
<!-- rev: 1 · updated: 2026-06-06 · source-doc-rev: 5 -->

> Read-only plan. The Visual Enricher renders these into output/enriched.md.
> Default render format: Mermaid-native (flowchart / pie / xychart-beta / gantt);
> an image asset only when no Mermaid type fits.

---

## V01 · section: problema + alcance · type: flowchart (Mermaid)
- **Clarifies:** o ciclo de dor do double-booking "hoje" — do conflito no calendário à confusão presencial — tornado visível como um fluxo sequencial com atores nomeados.
- **Data points:**
  - Dor central: conflito de agendamento (double-booking) — duas reuniões marcadas na mesma sala no mesmo horário — `source:` Q001
  - Frequência: toda semana / crônico, "já é caso conhecido no escritório" — `source:` Q003
  - Quatro perfis atingidos: equipes disputam a sala; reuniões com externos; liderança/diretoria; admin/facilities/recepção — `source:` Q004
  - Sem processo de resolução claro: "vira confusão" — `source:` Q001
  - Retrabalho de remarcar e "apagar incêndio" recai sobre admin/facilities — `source:` Q004, Q006
- **Evidence grade:** declared (sintomas observáveis confirmados pelo solicitante com frequência semanal).
- **Draft flag:** não — seção `problem` confidence=80, `reach` confidence=76; ambas acima de seus limiares.
- **Caption:** "Como o conflito de agendamento se manifesta hoje: do duplo-booking ao retrabalho semanal."
- **Render note:** representar como diagrama de fluxo com duas raias — "Antes do conflito" e "No momento do conflito / depois" — identificando cada ator pelos termos canônicos do glossário.

---

## V02 · section: alcance · type: flowchart (stakeholder map, Mermaid)
- **Clarifies:** os quatro perfis afetados e como a dor os atinge, tornando o alcance multi-perfil imediatamente visível em vez de listado em prosa.
- **Data points:**
  - Perfil A — Equipes que disputam a sala: transtorno direto de acesso ao espaço — `source:` Q004
  - Perfil B — Reuniões com clientes/externos: constrangimento, risco de imagem institucional — `source:` Q004
  - Perfil C — Liderança/diretoria: impacto quando suas próprias reuniões colidem — `source:` Q004
  - Perfil D — Admin/facilities/recepção: absorve retrabalho de remarcar e resolver — `source:` Q004
  - Alcance confirmado como "amplo e multi-perfil" pelo solicitante — `source:` target-document.md §reach
- **Evidence grade:** declared (todas as quatro opções selecionadas pelo solicitante).
- **Draft flag:** não — `reach` confidence=76, acima do limiar de 70.
- **Caption:** "Quem sente o conflito de agendamento e como: quatro perfis, impactos distintos."
- **Render note:** mapa centralizado no "conflito de agendamento" com quatro nós periféricos, cada um anotado com o tipo de impacto sofrido. Usar termos canônicos do glossário.

---

## V03 · section: impacto de negócio · type: flowchart (conceptual, Mermaid) — DRAFT
- **Clarifies:** os quatro eixos de custo do conflito de agendamento como um diagrama conceitual de causa-efeito, substituindo a lista em prosa por uma estrutura visual que mostra como cada eixo se origina do double-booking.
- **Data points:**
  - Eixo 1 — Tempo perdido: estimativa implícita de 15–30 min por evento, várias vezes/semana — `source:` Q006 (opção A)
  - Eixo 2 — Reuniões importantes prejudicadas: reuniões com clientes e diretoria, custo institucional elevado — `source:` Q006 (opção B)
  - Eixo 3 — Retrabalho operacional: carga sobre admin/facilities/recepção a cada ocorrência — `source:` Q006 (opção D)
  - Eixo 4 — Negócios adiados (container de maior gravidade potencial): decisões e fechamentos empurrados para frente; subsume custo de imagem/relacionamento — `source:` Q006 (Other), Q010
  - Nenhum eixo quantificado numericamente — `source:` target-document.md §impact, Q006 hint
- **Evidence grade:** estimated — eixos qualitativos confirmados pelo solicitante; magnitudes sem número.
- **Draft flag:** sim — `impact` confidence=65, abaixo do min-confidence=70; seção carregada como PREMISSA. Nenhum valor numérico existe. O visual deve ser explicitamente marcado DRAFT / PREMISSA QUALITATIVA.
- **Caption:** "Eixos de custo do conflito de agendamento — premissa qualitativa a quantificar na Descoberta. [RASCUNHO]"
- **Render note:** diagrama de causa-efeito (flowchart LR): nó raiz "conflito de agendamento (double-booking)" → quatro nós de eixo. Destacar "Negócios adiados" como dimensão de maior gravidade potencial. Incluir marcador visual DRAFT / sem quantificação. Não inserir números — o documento não os tem.

---

## V04 · section: maturidade recebida · type: radar (Mermaid) — DRAFT parcial
- **Clarifies:** o perfil de maturidade das cinco seções de captura em um único olhar, revelando que o elo fraco é exclusivamente o impacto.
- **Data points:**
  - Problema (problem): confiança 80 — `source:` target-document.md §readiness, §problem
  - Originador (originator): confiança 80 — `source:` target-document.md §readiness, §originator; Q007
  - Alcance (reach): confiança 76 — `source:` target-document.md §readiness, §reach; Q004
  - Urgência (urgency): confiança 70 — `source:` target-document.md §readiness, §urgency; Q008
  - Impacto (impact): confiança 65 (abaixo do limiar de 70) — `source:` target-document.md §readiness, §impact; Q006, Q010
  - Pontuação de maturidade geral: ~74% — `source:` target-document.md §readiness
- **Evidence grade:** declared (pontuações de confiança atribuídas pelo sistema de originação com base nas respostas do solicitante).
- **Draft flag:** sim — o eixo de impacto está abaixo do limiar; o radar mistura seções confirmadas com premissa. Marcar o eixo de impacto como PREMISSA no visual.
- **Caption:** "Perfil de maturidade da demanda por seção: cinco dimensões, um elo abaixo do limiar (impacto = 65)."
- **Render note:** radar com cinco eixos em escala 0–100; linha de referência pontilhada no limiar 70. Eixo "Impacto" plotado em cor diferenciada para indicar status de premissa. Maturidade geral (~74%) anotada abaixo do gráfico.

---

## V05 · section: triagem — decisão de roteamento · type: flowchart (Mermaid)
- **Clarifies:** o processo de decisão de triagem — dos critérios avaliados à decisão confirmada de Descoberta direcionada — como um diagrama de decisão, tornando o raciocínio de roteamento auditável de relance.
- **Data points:**
  - Critério: clareza do problema — forte (problem 80) — `source:` target-document.md §triage; Q001, Q003
  - Critério: alcance — forte (reach 76, quatro perfis incluindo externos e diretoria) — `source:` target-document.md §triage; Q004
  - Critério: impacto de negócio — fraco / não quantificado (impact 65, premissa) — `source:` target-document.md §triage; Q006, Q010
  - Critério: urgência — respondida / pressão contínua (urgency 70) — `source:` target-document.md §triage; Q008
  - Critério: maturidade das premissas — 3 premissas a validar + 1 incógnita técnica confirmada (integração com agenda corporativa) — `source:` target-document.md §triage; Q009
  - Decisão confirmada: Descoberta direcionada — `source:` Q011, target-document.md §triage (confirmado pelo solicitante em 2026-06-06, D001/D002)
  - Nota de tensão: fundamentos sustentariam "Pronto para Produto" se impacto qualitativo for aceito e integração tratada como risco de elaboração — `source:` target-document.md §triage
- **Evidence grade:** declared (decisão confirmada pelo solicitante, confidence=95).
- **Draft flag:** não — decisão confirmada pelo humano (substituiu rascunho de IA).
- **Caption:** "Decisão de triagem: Descoberta direcionada confirmada — dois itens genuínos de descoberta impedem congelamento de escopo."
- **Render note:** flowchart TD com dois ramos de avaliação (critérios fortes / elos fracos) convergindo para a caixa de decisão "Descoberta direcionada". Indicar os dois gatilhos específicos: (1) impacto não quantificado, (2) integração com agenda corporativa — requisito confirmado mas viabilidade desconhecida.

---

## V06 · section: briefing de descoberta · type: table (Mermaid ou tabela Markdown enriquecida)
- **Clarifies:** as quatro incógnitas do Discovery com sua urgência relativa, responsável e caixa-de-tempo recomendada — condensando o briefing em um painel de ação único.
- **Data points:**
  - Incógnita 1 — Magnitude quantificada do impacto (nº choques/semana × min/evento); caixa-de-tempo: 1 semana; investigar com admin/facilities/recepção — `source:` target-document.md §discovery; Q006
  - Incógnita 2 — "Negócios adiados" é custo real de receita/relacionamento?; caixa-de-tempo: 3 dias; investigar com liderança comercial/diretoria — `source:` target-document.md §discovery; Q006, Q010
  - Incógnita 3 — Viabilidade da integração com agenda corporativa (Google/Outlook): plataforma(s), APIs corporativas, SSO/OAuth, modelo de sincronização; caixa-de-tempo: 1 semana; investigar com Tech Lead/CTO + TI — `source:` target-document.md §discovery; Q009
  - Incógnita 4 — Existe ferramenta/processo informal hoje (greenfield vs. brownfield)?; caixa-de-tempo: 2 dias; confirmar com PO + admin/facilities — `source:` target-document.md §discovery; target-document.md §nature-signal
  - Caixa-de-tempo total sugerida: ~1 a 1,5 semana — `source:` target-document.md §discovery
- **Evidence grade:** derived (incógnitas derivadas do conjunto de premissas e restrições capturadas).
- **Draft flag:** não — as incógnitas são derivadas corretas das seções de captura; o briefing em si não é premissa.
- **Caption:** "Quatro incógnitas a resolver na Descoberta direcionada: prioridade, responsável e horizonte de tempo."
- **Render note:** tabela com colunas: Incógnita / Por que importa / Investigar com / Caixa-de-tempo. Destacar Incógnita 3 (integração com agenda) como gatilho de escalação arquitetural ao CTO. Incógnita 2 ("negócios adiados") sinalizada como dimensão de maior gravidade potencial.

---

## V07 · section: encaminhamento · type: flowchart (Mermaid)
- **Clarifies:** quem recebe o quê no encaminhamento pós-originação — PO, CTO/Tech Lead, admin/facilities, liderança comercial/diretoria — como um diagrama de handoff com responsabilidades explícitas.
- **Data points:**
  - Destino primário: PO / responsável pela triagem — confirmar roteamento e abrir descoberta curta — `source:` target-document.md §handoff
  - Escalação arquitetural: CTO / Tech Lead — revisão de viabilidade/arquitetura da integração com agenda corporativa (Google/Outlook), requisito confirmado (Q009) — `source:` target-document.md §handoff, §cto_escalation
  - Colaboradores (coleta de dados): admin/facilities/recepção — nº de choques/semana e minutos por evento — `source:` target-document.md §handoff; Q006
  - Colaboradores (validação de impacto): liderança comercial/diretoria — confirmar e exemplificar "negócios adiados" — `source:` target-document.md §handoff; Q010
  - A confirmar (greenfield): PO + admin/facilities — verificar ferramenta/processo informal existente — `source:` target-document.md §handoff, §assumptions
  - Roteamento confirmado pelo solicitante em 2026-06-06 — `source:` Q011
- **Evidence grade:** declared (roteamento confirmado, confidence=95).
- **Draft flag:** não — handoff derivado de decisão de triagem confirmada pelo humano.
- **Caption:** "Encaminhamento pós-originação: quatro destinos com responsabilidades distintas na Descoberta direcionada."
- **Render note:** flowchart LR partindo do nó "Originação concluída" para quatro raias de destino. Distinguir claramente: (a) destino decisório (PO), (b) escalação técnica (CTO/Tech Lead), (c) colaboradores de coleta, (d) colaboradores de validação de impacto. Indicar que execução aguarda início formal da fase de Descoberta.

---

<!-- END OF DOCUMENT -->
