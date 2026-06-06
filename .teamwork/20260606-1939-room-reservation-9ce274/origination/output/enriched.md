<!--
REGISTRO DE ORIGINAÇÃO · room-reservation
Gerado a partir de: target-template.origination-record.md
Linguagem de saída: pt-BR
-->

# Registro de originação: sistema de reserva de salas de reunião
<!-- rev: 5 · updated: 2026-06-06 -->

> Artefato formal de originação. Consolida a demanda capturada, registra o nível de maturidade com que ela chegou e carrega um rascunho de triagem (decisão de roteamento) sempre sinalizado para aprovação humana. Este documento é autocontido.

## Metadados
<!-- origination: id=meta; blocks=false; min-confidence=0; kind=meta -->

| Campo | Valor |
|---|---|
| **ID do registro** | INT-2026-001 |
| **Versão** | v1 |
| **Originador (solicitante)** | Solicitante (canalizador) + reclamações coletivas internas |
| **Triado por (responsável)** | Solicitante (canalizador da demanda), confirmado na sessão de originação |
| **Data de registro** | 2026-06-06 |
| **Data de triagem** | 2026-06-06 |
| **Situação** | Triado: Descoberta direcionada |
| **Linguagem de saída** | pt-BR |

## Histórico de revisões
<!-- origination: id=revisions; blocks=false; min-confidence=0; kind=meta -->

| Versão | Data | Evento | Resumo |
|---|---|---|---|
| v1 | 2026-06-06 | Originação rascunhada | Captura inicial via origination-brainstorm; seções de captura preenchidas a partir do ledger Q001-Q006. |
| v2 | 2026-06-06 | Atualização pós-checkpoint | Seções `originator`, `urgency`, `constraints` e `impact` atualizadas com respostas Q007-Q010. Conflito de eixo-imagem resolvido. Metadado Originador atualizado. |
| v3 | 2026-06-06 | Seções derivadas recompostas pelo Sintetizador | `readiness` atualizado para ~74% (urgência respondida Q008, reach 76, originator 80). `triage` recomposto: decisão Descoberta direcionada, confiança ~66, nota de tensão atualizada. `cto_escalation` promovida a SIM por integração com agenda confirmada (Q009). `handoff` e `discovery` alinhados à nova triagem. |
| v4 | 2026-06-06 | Confirmação humana da triagem (Q011) | Decisão de roteamento confirmada pelo solicitante em 2026-06-06 (D001/D002). Banner ⚠️ substituído por confirmação ✅ na triagem e no encaminhamento. Metadados de triagem preenchidos. Confiança do alcance alinhada de 75 para 76 (reconciliação cosmética). |

---

## Maturidade recebida
<!-- origination: id=readiness; blocks=false; min-confidence=0; kind=derived; inputs=problem,reach,impact,originator,urgency -->

> Retrato computado das seções capturadas.

| Campo | Valor |
|---|---|
| **Pontuação de maturidade** | ~74% |
| **Requisitos bloqueantes** | Sim: todos resolvidos por confiança ou disposição honesta. `problem` (80) acima do min-confidence=80; `originator` (80) e `reach` (76) acima do limiar; `impact` (65) abaixo do min-confidence=70, carregado como **PREMISSA** declarada (único elo abaixo do limiar). |
| **Disposições abertas** | 3 premissas a validar · 0 descoberta · 0 adiada |

**Racional de maturidade:** maturidade moderada-alta, limitada por um único elo fraco. Problema forte (80), originador firmado (demanda coletiva canalizada, 80), alcance amplo (76), urgência RESPONDIDA: pressão contínua confirmada (70), não mais inferida. Único elo abaixo do limiar: impacto (65, premissa), confirmado em 4 eixos qualitativos mas sem quantificação. Gate fecha por disposição honesta. Pontuação ~74% (média de 80 / 76 / 65 / 80 / 70), acima da rev anterior (~68%).

<!-- VISUAL (enrichment, additive): V04, Radar de maturidade por seção; cinco dimensões, eixo Impacto abaixo do limiar [RASCUNHO PARCIAL] -->

> **RASCUNHO: eixo Impacto abaixo do limiar (65 < 70); radar mistura seções confirmadas com premissa.**

```mermaid
radar
  title "Perfil de maturidade da demanda [RASCUNHO: Impacto = PREMISSA]"
  options
    max 100
  axes
    Problema, Originador, Alcance, Urgencia, Impacto
  data
    Confianca registrada
      80, 80, 76, 70, 65
    Limiar minimo
      70, 70, 70, 70, 70
```

**Legenda V04:** Pontuacao de maturidade geral: ~74%. O eixo "Impacto" (65) e o unico abaixo do limiar minimo de 70, carregado como PREMISSA declarada. Os demais eixos estao confirmados. Valores: Problema 80 | Originador 80 | Alcance 76 | Urgencia 70 | Impacto 65 (premissa).

*"Perfil de maturidade da demanda por seção: cinco dimensões, um elo abaixo do limiar (impacto = 65)."*

---

## Demanda consolidada

> Leitura em uma tela da demanda, cada dimensão carregando sua confiança herdada.

### Problema (a dor, não a solução)
<!-- origination: id=problem; blocks=true; min-confidence=80; kind=capture -->
> Rubrica: descrever a dor existente com sintomas observáveis: o que dói, para quem, como se manifesta hoje. Se nomear uma solução ("construir X"), a seção NÃO está satisfeita: reformular para a dor subjacente.

O problema central é o **conflito de agendamento** (double-booking): pessoas marcam reuniões em salas que já estão ocupadas por outra reunião no mesmo horário. Quando os dois grupos chegam à sala, "vira confusão": não há processo claro de resolução e a situação se repete. O conflito acontece **toda semana, sem parar** e já é caso conhecido no escritório, caracterizando uma dor crônica e rotineira, não uma exceção isolada. (Q001, Q003)

**Proveniência**
- **Confiança:** 80
- **Fonte:** Solicitante direto (Q001 + Q003)
- **Situação:** respondida
- **Disposição:** respondida
- **Observação:** Dor de conflito de agendamento (double-booking) confirmada com frequência semanal crônica, atingindo o min-confidence=80 da seção. Ainda sem quantificação de horas perdidas por evento. Frequência estabelece severidade como contínua.

<!-- VISUAL (enrichment, additive): V01, Fluxo de dor do double-booking: do conflito no calendário ao retrabalho semanal -->

```mermaid
flowchart TD
    subgraph Antes["Antes do conflito"]
        A1["Equipe A reserva sala\n(sem verificacao centralizada)"]
        A2["Equipe B reserva a mesma sala\nno mesmo horario"]
        A1 --- A2
    end

    subgraph Conflito["No momento do conflito"]
        B1["Ambas as equipes chegam a sala"]
        B2{"Sala ja ocupada\npor outro grupo"}
        B1 --> B2
    end

    subgraph Consequencias["Depois do conflito"]
        C1["Vira confusao:\nsem processo claro de resolucao"]
        C2["Reunioes com clientes/externos:\nconstrangimento e risco de imagem"]
        C3["Liderança/diretoria afetada\nquando suas proprias reunioes colidem"]
        C4["Admin/facilities/recepção:\nretrabalho de remarcar e resolver"]
    end

    Antes --> Conflito
    B2 --> C1
    C1 --> C2
    C1 --> C3
    C1 --> C4

    N1["Frequencia: toda semana, cronico\n'ja e caso conhecido no escritorio'\n(Q003)"]
    C4 -.->|"se repete sem parar"| N1
    N1 -.->|"proxima semana"| A1
```

*"Como o conflito de agendamento se manifesta hoje: do duplo-booking ao retrabalho semanal."*

### Originador e contexto
<!-- origination: id=originator; blocks=true; min-confidence=70; kind=capture -->
> Rubrica: quem levantou e em que situação (ex.: "COO, planejamento Q2"), e o canal por onde chegou.

A demanda é canalizada pelo **solicitante desta sessão**, mas a dor é **coletiva**: ele reúne e representa várias reclamações recorrentes de colegas. O canal de origem é bottom-up: reclamações internas acumuladas que tornaram o problema visível o suficiente para gerar uma proposta de solução. O solicitante não se identificou nominalmente, mas sua titularidade está clara: canalizador mais grupo de reclamantes internos. A origem não é uma diretriz top-down nem a dor de uma única pessoa. (Q005 + Q007)

**Proveniência**
- **Confiança:** 80
- **Fonte:** Solicitante direto (Q005 + Q007)
- **Situação:** respondida
- **Disposição:** respondida
- **Observação:** Papel do solicitante confirmado em Q007 como canalizador da demanda coletiva (opção B, "Fui eu + outros reclamantes"). A ausência de nome próprio não compromete o gate: origem confirmada (Q005), papel confirmado (Q007), pressão coletiva documentada. Demanda bottom-up; peso institucional moderado; pode demandar mais validação de partes interessadas para priorização formal.

### Quem é impactado (alcance)
<!-- origination: id=reach; blocks=true; min-confidence=70; kind=capture -->
> Rubrica: os perfis / segmentos / equipes que sentem a dor, cada um com *como* são afetados.

O conflito de salas atinge quatro perfis distintos, confirmados pelo solicitante: (Q004)

- **Equipes que disputam a sala:** transtorno direto para quem chegou para usar o espaço e encontrou outro grupo já ocupando.
- **Reuniões com clientes e externos:** o conflito gera constrangimento e risco de imagem institucional quando visitantes externos estão presentes.
- **Liderança e diretoria:** a gestão é diretamente impactada quando suas próprias reuniões colidem com outras.
- **Quem organiza o escritório (organização do escritório / facilities / recepção):** absorve o retrabalho de remarcar, negociar e resolver cada ocorrência.

O alcance é amplo e multi-perfil, o que eleva a urgência percebida.

**Proveniência**
- **Confiança:** 76
- **Fonte:** Solicitante direto (Q004)
- **Situação:** respondida
- **Disposição:** respondida
- **Observação:** Todas as quatro opções substantivas selecionadas pelo solicitante. A presença de reuniões com externos (imagem) e liderança/diretoria distingue esta dor de um problema puramente operacional interno. Seção atinge min-confidence=70. (Confiança ajustada de 75 para 76 em reconciliação cosmética com os valores citados na maturidade e na triagem.)

<!-- VISUAL (enrichment, additive): V02, Mapa de partes interessadas: quatro perfis afetados pelo conflito de agendamento -->

```mermaid
flowchart LR
    Centro["Conflito de agendamento\n(double-booking)\nconfianca 76 · Q004"]

    PA["Equipes que disputam a sala\nTranstorno direto de acesso ao espaco"]
    PB["Reunioes com clientes/externos\nConstrangimento · risco de imagem institucional"]
    PC["Lideranca e diretoria\nImpacto quando suas proprias reunioes colidem"]
    PD["Admin / Facilities / Recepcao\nRetrabalho de remarcar, negociar e resolver"]

    Centro --> PA
    Centro --> PB
    Centro --> PC
    Centro --> PD
```

*"Quem sente o conflito de agendamento e como: quatro perfis, impactos distintos."*

### Impacto de negócio
<!-- origination: id=impact; blocks=true; min-confidence=70; kind=capture -->
> Rubrica: valor nas dimensões aplicáveis (receita, retenção, operacional, competitivo, compliance), quantificado quando possível. Estimativas são aceitas se marcadas como baixa confiança com uma observação sobre o que as firmaria.

O custo do conflito de salas tem quatro eixos, todos confirmados pelo solicitante. Nenhuma dimensão foi quantificada numericamente; todos os valores abaixo são estimativas qualitativas a validar: (Q006 + Q010)

- **Tempo perdido (operacional):** a cada conflito de agendamento há pessoas paradas enquanto a reunião atrasa, com estimativa implícita de 15 a 30 minutos por evento, várias vezes por semana.
- **Reuniões importantes prejudicadas (institucional):** não são apenas reuniões rotineiras afetadas. Reuniões com clientes e com a diretoria são atingidas, com custo institucional mais elevado.
- **Retrabalho operacional:** a organização do escritório (facilities) absorve o esforço de remarcar e resolver cada ocorrência, gerando carga repetitiva sobre quem administra o espaço.
- **Negócios adiados (receita / relacionamento):** reuniões de negócio que não acontecem no horário previsto empurram decisões e fechamentos para frente, gerando custo de oportunidade em receita e relacionamento (**dimensão de maior gravidade potencial**). O custo de imagem/relacionamento com clientes e externos está **subsumido** neste eixo (confirmado pelo solicitante em Q010, não é dimensão separada).

Nenhum valor foi quantificado: não há número de conflitos por semana, minutos estimados por evento ou indicação de negócios concretamente adiados.

**Proveniência**
- **Confiança:** 65
- **Fonte:** Solicitante direto (Q006 + Q010)
- **Situação:** respondida
- **Disposição:** premissa
- **Observação:** Impacto qualitativo confirmado em quatro eixos; conflito de eixo-imagem RESOLVIDO via Q010: custo de imagem/relacionamento está subsumido em "negócios adiados", não é eixo à parte. Impacto permanece sem quantificação (único bloqueador residual do gate). Para firmar a confiança: (1) coletar nº de conflitos/semana × minutos perdidos por evento; (2) exemplos concretos de negócios adiados e valor estimado em receita ou relacionamento. "Negócios adiados" é a dimensão de maior gravidade; priorizar sua validação.

<!-- VISUAL (enrichment, additive): V03, Eixos de custo do conflito de agendamento (conceitual causa-efeito) [RASCUNHO / PREMISSA QUALITATIVA] -->

> **RASCUNHO: PREMISSA QUALITATIVA. Impacto confianca=65, abaixo do limiar 70. Nenhum valor numerico existe. Eixos confirmados qualitativamente pelo solicitante; magnitudes a quantificar na Descoberta.**

```mermaid
flowchart LR
    Raiz["Conflito de agendamento\n(double-booking)\n[RASCUNHO · confianca 65 · PREMISSA]"]

    E1["Tempo perdido\nOperacional\nestimativa: 15 a 30 min por evento\nvarias vezes por semana\nsem numero confirmado"]
    E2["Reunioes importantes prejudicadas\nInstitucional\nClientes e diretoria afetados\ncusto institucional elevado\nsem quantificacao"]
    E3["Retrabalho operacional\nAdmin / Facilities\ncarga repetitiva por ocorrencia\nsem quantificacao"]
    E4["Negocios adiados\nReceita / Relacionamento\nDIMENSAO DE MAIOR GRAVIDADE POTENCIAL\ndecisoes e fechamentos empurrados\ncusto de imagem subsumed aqui\nsem quantificacao"]

    Raiz --> E1
    Raiz --> E2
    Raiz --> E3
    Raiz --> E4
```

*"Eixos de custo do conflito de agendamento, premissa qualitativa a quantificar na Descoberta. [RASCUNHO]"*

### Urgência: por que agora
<!-- origination: id=urgency; blocks=false; min-confidence=70; kind=capture -->
> Rubrica: por que agora e o custo de esperar: uma janela, um prazo, um custo que se agrava.

A urgência é **pressão contínua**, confirmado diretamente pelo solicitante (Q008). Não há gatilho específico, prazo ou janela de oportunidade que motive a resolução agora: o que move é a persistência crônica do problema (frequência semanal confirmada em Q003) e o acúmulo de reclamações ao longo do tempo. A ausência de deadline é ela mesma a resposta. O custo de esperar é concreto: cada semana sem solução representa novos conflitos de agendamento, mais retrabalho operacional e mais reuniões importantes prejudicadas.

**Proveniência**
- **Confiança:** 70
- **Fonte:** Solicitante direto (Q008)
- **Situação:** respondida
- **Disposição:** respondida
- **Observação:** Urgência perguntada diretamente em Q008; solicitante escolheu opção A ("Pressão contínua"), substantiva, não escape-hatch. A natureza da urgência está estabelecida. Intensidade relativa dessa pressão frente a outras prioridades institucionais não foi capturada: não há como saber se o item está no topo da fila ou no backlog. Coerente com Q005 (reclamação recorrente) e Q003 (frequência semanal crônica).

### Prioridade declarada
<!-- origination: id=priority; blocks=false; min-confidence=0; kind=capture -->
> Rubrica: a prioridade declarada pelo solicitante **e** o motivo por trás dela (não apenas o rótulo).

**Nível:** Não declarado. **Motivo:** O solicitante não declarou prioridade durante a sessão de originação. Não foi perguntado explicitamente.

---

## Sinal de natureza: software novo vs. existente
<!-- origination: id=nature-signal; blocks=false; min-confidence=0; kind=capture -->

> Sinal leve que **semeia** a classificação greenfield (nova capacidade)/brownfield do PO na triagem (não exige certeza). Esta demanda parece ser uma **nova capacidade** (algo que não existe hoje) ou uma mudança em **algo que já funciona**? O PO firma a classificação formal no Registro de Intake.

**Toca:** Nova capacidade. A declaração de abertura ("quero um sistema para reservar salas") indica que não existe hoje nenhuma ferramenta ou processo formalizado de reserva de salas. Não há menção a sistema existente a ser alterado.

**Proveniência**
- **Confiança:** 70
- **Fonte:** inferida da declaração de abertura
- **Situação:** respondida
- **Disposição:** inferida
- **Observação:** Inferência a partir da ausência de qualquer menção a sistema atual. O PO deve confirmar se há alguma ferramenta informal (planilha, quadro, calendário compartilhado) em uso antes de classificar formalmente como greenfield (nova capacidade).

---

## Triagem: decisão de roteamento
<!-- origination: id=triage; blocks=false; min-confidence=0; kind=derived; inputs=problem,reach,impact,urgency,assumptions -->

> ✅ **DECISÃO CONFIRMADA pelo solicitante em 2026-06-06 (substitui o rascunho de IA).**

**Confiança · Disposição:** 95 · confirmada

Situação: Triado. Decisão firmada pelo solicitante (Q011, 2026-06-06). Referências ao ledger de decisões da iniciativa: D001 (Descoberta direcionada aprovada) e D002 (Escalação arquitetural confirmada).

### Critérios de triagem

| Critério | Avaliação |
|---|---|
| **Clareza do problema** | Forte: conflito de agendamento (double-booking) com sintomas observáveis e recorrência semanal (problem 80, Q001/Q003) |
| **Alcance** | Forte: quatro perfis, incluindo externos (imagem) e diretoria (reach 76, Q004) |
| **Impacto de negócio** | Fraco / não quantificado: quatro eixos qualitativos, nenhum valor quantificado; marcado **premissa** (impact 65, Q006/Q010). Item genuíno de descoberta. |
| **Urgência: por que agora** | Respondida: pressão contínua confirmada pelo solicitante (urgency 70, Q008); sem prazo específico, mas não mais inferida. |
| **Maturidade das premissas** | Aberta: 3 premissas materiais a validar + 1 incógnita técnica CONFIRMADA: viabilidade da integração com agenda corporativa (Google/Outlook, Q009). |

### Decisão de roteamento

| Campo | Valor |
|---|---|
| **Decisão** | Descoberta (Discovery), direcionada, CONFIRMADA |
| **Justificativa** | Quadro mais forte (problema, alcance, originador, urgência sólidos), mas persistem 2 itens genuínos de descoberta que impedem congelar escopo: (1) impacto não quantificado (premissa de VALOR) e (2) viabilidade da integração com agenda corporativa, agora requisito CONFIRMADO (Q009) e portanto incógnita técnica/arquitetural real. Decisão fica em Descoberta, estreitada a esses dois eixos, em vez de promover a "Pronto para Produto" prematuramente. |

> **Nota de tensão:** os fundamentos já sustentariam "Pronto para Produto": problema, alcance, originador e urgência são sólidos. O que segura são duas incógnitas materiais específicas: impacto qualitativo (premissa de valor) e integração com agenda corporativa (incerteza de viabilidade), não fraqueza geral. Se o responsável aceitar o impacto qualitativo E tratar a integração como risco de elaboração, pode promover diretamente; o rascunho recomenda Descoberta curta focada nesses dois itens.

<!-- VISUAL (enrichment, additive): V05, Arvore de decisao de triagem: criterios avaliados e decisao confirmada de Descoberta direcionada -->

```mermaid
flowchart TD
    Inicio["Avaliacao de triagem\nINT-2026-001"]

    Inicio --> CF["Criterios FORTES"]
    Inicio --> CF2["Criterios com LACUNAS"]

    CF --> P["Problema claro\ndouble-booking com recorrencia semanal\nproblem 80 · Q001/Q003"]
    CF --> R["Alcance amplo\n4 perfis: externos + diretoria incluidos\nreach 76 · Q004"]
    CF --> O["Originador firmado\ndemanda coletiva bottom-up\noriginator 80 · Q005/Q007"]
    CF --> U["Urgencia confirmada\npressao continua declarada pelo solicitante\nurgency 70 · Q008"]

    CF2 --> I["Impacto nao quantificado\n4 eixos qualitativos · sem numero\nimpact 65 · PREMISSA · Q006/Q010"]
    CF2 --> INT["Integracao com agenda corporativa\nrequisito CONFIRMADO · viabilidade desconhecida\nGoogle/Outlook · SSO/OAuth · Q009"]

    P & R & O & U & I & INT --> Decisao

    Decisao{"Decisao de roteamento"}
    Decisao -->|"Dois itens genuinos de descoberta\nimpedem congelar escopo"| D["Descoberta direcionada\nCONFIRMADA · confianca 95\nQ011 · D001 · D002\n2026-06-06"]

    D --> G1["Eixo 1: quantificar impacto\nPO + facilities + lideranca comercial"]
    D --> G2["Eixo 2: viabilidade da integracao\nCTO/Tech Lead + TI"]
```

*"Decisão de triagem: Descoberta direcionada confirmada, dois itens genuínos de descoberta impedem congelamento de escopo."*

---

## Escalação arquitetural
<!-- origination: id=cto_escalation; blocks=false; min-confidence=0; kind=derived; inputs=impact,constraints,assumptions -->

**Confiança · Disposição:** ~75 · inferida

Escalação ao CTO antes de congelar escopo? **SIM**: revisão de viabilidade/arquitetura da integração com agenda corporativa.

O núcleo é CRUD de agenda básico, sem gatilhos arquiteturais clássicos (sem pagamentos, multi-tenancy, segurança nova, IA/runtime, nova infraestrutura). A integração com agenda corporativa (Google Calendar e/ou Outlook) é agora **requisito CONFIRMADO** (Q009, constraints 72): integração com incógnitas (qual plataforma, APIs corporativas, SSO/OAuth, modelo de sincronização), exatamente o gatilho previsto. Confiança elevada porque `constraints` não está mais vazia.

**Razão (uma linha):** integração confirmada com agenda corporativa é integração com incógnitas, o que justifica revisão de viabilidade/arquitetura antes do congelamento de escopo.

---

## Premissas
<!-- origination: id=assumptions; blocks=false; min-confidence=0; kind=capture -->

> Condições assumidas como verdadeiras na captura. Cada uma carrega um veredicto proposto (rascunho) e quem a valida. Se alguma se provar falsa, a demanda é retriada.

| Premissa | Veredicto (rascunho) | Validar com |
|---|---|---|
| A magnitude do impacto (tempo perdido, reuniões prejudicadas, retrabalho) é estimativa qualitativa, não quantificada | A validar | PO + quem organiza as salas (organização do escritório / facilities): coletar nº de choques/semana e minutos por evento |
| "Negócios adiados" representa custo real de receita/relacionamento | A validar | Liderança comercial / diretoria: solicitar exemplos concretos de negócios ou decisões que foram adiados por conflito de sala e estimar impacto |
| Não existe nenhuma ferramenta formal de reserva de salas em uso hoje (greenfield / nova capacidade) | A validar | PO + organização do escritório / facilities: confirmar se há planilha, quadro, calendário compartilhado ou qualquer processo informal em uso |

---

## Restrições
<!-- origination: id=constraints; blocks=false; min-confidence=70; kind=capture -->

> Condições que limitam o espaço de solução, a respeitar independentemente do que for construído.

| Restrição | Tipo | Observação |
|---|---|---|
| A solução **precisa integrar com a agenda corporativa** (Google Calendar e/ou Outlook) | Técnica | Restrição firme declarada pelo solicitante (Q009). Desambiguação pendente: uma plataforma ou ambas? Há requisitos de SSO ou acesso a APIs corporativas? Detalhes de escopo, sem bloquear o gate de originação. |

Fora a integração com agenda corporativa, nenhuma outra restrição foi declarada: sem orçamento definido, sem prazo e sem restrições de complexidade informadas (Q009).

**Proveniência**
- **Confiança:** 72
- **Fonte:** Solicitante direto (Q009)
- **Situação:** respondida
- **Disposição:** respondida
- **Observação:** Restrição técnica confirmada: integração com Google Calendar e/ou Outlook é requisito firme. Impacto arquitetural relevante: reforça a avaliação de escalação ao CTO (decisão de stack/API de integração necessária). Gaps residuais de escopo: especificar qual plataforma (uma ou ambas) e se há SSO, a levantar no Discovery ou na elaboração do escopo.

---

## Briefing de descoberta
<!-- origination: id=discovery; blocks=false; min-confidence=0; kind=derived; inputs=triage; condition=triage.decision==Discovery -->

> Seção condicional, incluída porque `triage.decision==Discovery`.

| Incógnita | Por que importa | Como investigar | Prazo fechado | Resultado |
|---|---|---|---|---|
| Magnitude quantificada do impacto (nº choques/semana × min/evento) | Define se o valor justifica priorizar agora; hoje 100% qualitativo (impact 65, premissa) | Coletar registros / observação com organização do escritório / facilities / recepção | 1 semana | (em aberto) |
| "Negócios adiados" é custo real de receita / relacionamento? | Eixo de maior gravidade potencial, não comprovado | Entrevistar liderança comercial / diretoria por exemplos concretos | 3 dias | (em aberto) |
| Viabilidade da integração com agenda corporativa (Google Calendar / Outlook) | Requisito CONFIRMADO (Q009): gatilho de escalação arquitetural; definir plataforma(s), APIs corporativas, SSO/OAuth, modelo de sincronização | Revisão de viabilidade/arquitetura com Tech Lead/CTO + TI | 1 semana | (em aberto) |
| Existe ferramenta / processo informal hoje (greenfield / nova capacidade vs. brownfield)? | Define natureza da demanda e escopo | Confirmar com PO + organização do escritório / facilities | 2 dias | (em aberto) |

**Prazo fechado total sugerido:** ~1 a 1,5 semana.

> Nota: linha de urgência encerrada, respondida em Q008. Integração com agenda corporativa promovida de "possível gatilho" a requisito confirmado a investigar.

<!-- VISUAL (enrichment, additive): V06, Painel de incognitas da Descoberta: quatro itens com prioridade, responsavel e horizonte de tempo -->

| # | Incognita | Por que importa | Investigar com | Prazo | Prioridade |
|---|---|---|---|---|---|
| 1 | Magnitude quantificada do impacto (nº choques/semana x min/evento) | Define se o valor justifica priorizar agora; hoje 100% qualitativo (impact 65, premissa) | Admin / Facilities / Recepcao | 1 semana | Alta |
| 2 | "Negocios adiados" e custo real de receita/relacionamento? | **Dimensao de maior gravidade potencial**, nao comprovada | Lideranca comercial / Diretoria | 3 dias | Critica |
| 3 | Viabilidade da integracao com agenda corporativa (Google/Outlook): plataforma(s), APIs, SSO/OAuth, sincronizacao | Requisito CONFIRMADO (Q009) · **Gatilho de escalacao arquitetural ao CTO** | Tech Lead / CTO + TI | 1 semana | Critica |
| 4 | Existe ferramenta/processo informal hoje? (greenfield vs. brownfield) | Define natureza da demanda e escopo | PO + Admin / Facilities | 2 dias | Alta |

**Prazo total sugerido:** ~1 a 1,5 semana. Incognitas 2 e 3 sao criticas: uma define o valor de negocio do projeto; a outra determina se a arquitetura e viavel no escopo planejado.

*"Quatro incógnitas a resolver na Descoberta direcionada: prioridade, responsável e horizonte de tempo."*

---

## Encaminhamento
<!-- origination: id=handoff; blocks=false; min-confidence=0; kind=derived; inputs=triage -->

> ✅ **Roteamento CONFIRMADO pelo solicitante em 2026-06-06**: Descoberta direcionada. Execução pendente do início formal da fase de Descoberta.

- **Destino primário:** Product Owner / responsável pela triagem: confirmar roteamento e abrir descoberta curta focada em dois eixos: quantificação de impacto e viabilidade da integração com agenda.
- **Escalação arquitetural (CTO / Tech Lead):** acionar revisão de viabilidade/arquitetura da integração com agenda corporativa (Google/Outlook), requisito confirmado (Q009), antes do congelamento de escopo.
- **Colaboradores (organização do escritório / facilities / recepção):** coletar nº de choques/semana e minutos por evento.
- **Colaboradores (liderança comercial / diretoria):** confirmar e exemplificar "negócios adiados".
- **A confirmar (PO + organização do escritório / facilities):** verificar se já existe ferramenta / processo informal (planilha, quadro, calendário) antes de classificar como greenfield (nova capacidade).

<!-- VISUAL (enrichment, additive): V07, Diagrama de handoff pos-originacao: quatro destinos com responsabilidades distintas na Descoberta direcionada -->

```mermaid
flowchart LR
    Origem["Originacao concluida\nINT-2026-001\nroteamento CONFIRMADO · Q011\n2026-06-06"]

    Origem --> PO["PO / Responsavel pela triagem\nDestino primario\nConfirmar roteamento\nAbrir Descoberta curta\n(2 eixos: impacto + integracao)"]

    Origem --> CTO["CTO / Tech Lead\nEscalacao arquitetural\nRevisao de viabilidade/arquitetura\nintegracao Google/Outlook · Q009\nantes do congelamento de escopo"]

    Origem --> FAC["Admin / Facilities / Recepcao\nColaboradores de coleta\nColetar: nº choques/semana\ne minutos por evento"]

    Origem --> COM["Lideranca comercial / Diretoria\nColaboradores de validacao de impacto\nConfirmar e exemplificar\n'negocios adiados'"]

    PO -->|"A confirmar"| GRN["PO + Admin / Facilities\nVerificar ferramenta/processo\ninformal existente\n(planilha, quadro, calendario)\nantes de classificar como\ngreenfield / nova capacidade"]

    FAC -.->|"resultados alimentam"| PO
    COM -.->|"resultados alimentam"| PO
    CTO -.->|"resultado alimenta"| PO
```

*"Encaminhamento pós-originação: quatro destinos com responsabilidades distintas na Descoberta direcionada."*

<!-- END OF DOCUMENT -->
