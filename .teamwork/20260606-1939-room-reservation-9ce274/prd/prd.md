<!--
PRD — Product Requirements Document
Instanciado do template target-template.prd.md em 2026-06-07.
Part A herdada do RP-2026-001; Part B herdada do TA-2026-001 (escalado, assinado).
Dual sign-off comitado (Fase 4): PO (RP congelado) + CTO (Viável com ressalvas).
Status: Accepted. Entregue ao PM em 2026-06-07. handoffReady.
-->

# PRD — Reserva de Salas de Reunião
<!-- rev: 3 · updated: 2026-06-07 -->

> O PRD (Documento de Requisitos de Produto) é a **fusão** do **Pacote de Prontidão**
> (produto, de autoria do PO) com a **Avaliação Técnica** (técnica, de autoria do CTO).
> É o **único artefato que abre o downstream** — entregue ao **PM**.
> Cada metade preserva a autoria clara: o PO não escreve a parte técnica, o CTO
> não reescreve a parte de produto. O PRD **costura, reconcilia e expõe** ao PM o que
> ele precisa para planejar — sem reescrever nenhuma das fontes. Veja `personas/02-po.md`
> §2/§10/§11 e `templates/04-prd.md`.
>
> **Quando não houve escalação ao CTO:** o PRD é formado apenas pelo RP; a Parte B é
> disposicionada como "N/A — sem escalação arquitetural".
>
> `PRD = RP (PO) + Avaliação Técnica (CTO)`

## Metadados
<!-- origination: id=meta; blocks=false; min-confidence=0; kind=meta -->

| Campo | Valor |
|---|---|
| **PRD ID** | PRD-2026-001 |
| **Versão** | v1 |
| **RP Vinculado** | RP-2026-001 v1 |
| **Avaliação Técnica Vinculada** | TA-2026-001 v1 |
| **Intake Vinculado** | INT-2026-001 |
| **Escalado?** | Sim (TA incorporado) |
| **Natureza da Demanda** | Híbrido |
| **Autores** | PO + CTO |
| **Status** | Accepted |
| **Idioma de saída** | pt-BR |
| **Entregue ao PM em** | 2026-06-07 |

## Histórico de Revisões
<!-- origination: id=revisions; blocks=false; min-confidence=0; kind=meta -->

| Versão | Data | Autor | Status | Resumo |
|---|---|---|---|---|
| v1 | 2026-06-07 | Doc Updater (Fase 2 — merge inherit) | Rascunho | PRD instanciado do template; Part A herdada do RP-2026-001 (a-objectives..a-edge-cases + success-metrics) e Part B herdada do TA-2026-001 (b-feasibility..b-adrs + effort-cost firme). Origin: inherited. Seções derivadas (exec-summary, scope-reconciliation, consolidated-risk, inherited-readiness, handoff-gate) e sign-off pendentes (Fase 3/4). |
| v1 | 2026-06-07 | Doc Updater (Fase 3 — sintetizar & reconciliar) | Draft | Seções derivadas preenchidas: scope-reconciliation (escopo do RP mantido integralmente), consolidated-risk (11 riscos RP+TA + dependências externas), inherited-readiness (DISC-001 aberto), exec-summary, handoff-gate. Nota de reconciliação do a-scope resolvida. sign-off pendente (Fase 4). |
| v1 | 2026-06-07 | Doc Updater (Fase 4 — dual sign-off) | Accepted | Dual sign-off comitado: PO (RP congelado) + CTO (veredito Viável com ressalvas carregado do TA). Seções promovidas a po_authored/cto_authored; dispositions discovery preservadas (DISC-001). Status=Accepted; entregue ao PM 2026-06-07. handoffReady. |

---

## Assinatura
<!-- origination: id=sign-off; blocks=true; min-confidence=85; kind=capture -->
> Rubrica: a fusão **só se fecha com assinatura dupla**. O PO assina a metade de produto
> (o RP está congelado — `freezeReady`); o CTO assina a metade técnica (o TA está assinado —
> o veredito de viabilidade é carregado do TA), ou o campo do CTO é um **N/A honesto** quando
> não houve escalação. O PRD não pode ser congelado (`handoffReady`) sem esta linha resolvida.
> O veredito de viabilidade é **herdado do TA, nunca re-decidido aqui**. Um TA vetado
> nunca chega a esta seção — não há PRD em caso de veto. Limite alto: esta é a porta.

| Papel | Nome | Veredito | Data |
|---|---|---|---|
| **PO** (produto) | PO | RP Congelado (`freezeReady`) | 2026-06-07 |
| **CTO** (técnico) | CTO | Viável com ressalvas | 2026-06-07 |

**Provenance**
- **Confidence:** 90
- **Origin:** po_authored + cto_authored
- **Source:** RP-2026-001 congelado (PO) + TA-2026-001 veredito carregado (CTO)
- **Status:** respondida
- **Disposition:** decided (dual sign-off comitado; handoffReady)
- **Hint:** o veredito é carregado do TA, nunca re-decidido no PRD; ressalvas R1..R4 e DISC-001 viajam para a execução.

---

## Resumo Executivo Combinado
<!-- origination: id=exec-summary; blocks=true; min-confidence=75; kind=derived; inputs=a-objectives,a-scope,b-feasibility,effort-cost,success-metrics -->
> Rubrica: 2–4 parágrafos — o problema, o que será construído, a viabilidade técnica e
> o resultado de negócio esperado. A visão de uma página para CEO/CFO/PM. **Sintetizado**
> a partir das seções herdadas (não acrescenta fatos novos — compõe os já incorporados).
> Um bom resumo permite que o leitor que não ler mais nada saiba por que esta demanda,
> o que ela entrega, se é viável e qual resultado ela persegue.

**O problema.** A organização sofre com double-booking crônico de salas: o agendamento se espalha por três canais não-integrados — mural físico, Google Forms e WhatsApp — sem nenhum mecanismo de anti-conflito. O resultado é um ritmo de ~1,8 conflitos por semana (9 em 5 semanas), com impacto comercial já quantificado: R$111 mil em negócios perdidos, R$90 mil em risco e um pipeline de ~R$700 mil de novos negócios exposto a adiamentos por choque de sala. A secretária/facilities atua como árbitro manual e gargalo a cada conflito.

**O que será construído.** Um sistema digital de reserva de salas — natureza Híbrida (software-core novo + integração + migração de um processo informal) — cujo núcleo é o anti-double-booking automático sob a regra first-commit-wins: a primeira confirmação persiste e a segunda recebe conflito, eliminando sobreposições parciais ou totais. Inclui integração uma-via com o Google Calendar (toda reserva confirmada/cancelada reflete em ≤2 minutos, sem retroalimentação reversa), login social, reservas recorrentes com validação por ocorrência, e a migração e descontinuação dos canais manuais (mural + Forms + WhatsApp) em até 2 semanas pós go-live.

**A viabilidade técnica.** O CTO assinou o veredito "Viável com ressalvas" (herdado da Avaliação Técnica, nunca re-decidido aqui). A arquitetura é sólida: a integridade anti-conflito repousa sobre exclusão transacional no banco (não read-then-write), e a sincronização com o Calendar é assíncrona e desacoplada do commit. As ressalvas têm caminhos de resolução conhecidos — o grant OAuth do Google Workspace e o modelo de credencial da Calendar API, mais a revisão LGPD (Jurídico/DPO) — confirmadas no spike DISC-001 no início da execução. Esforço firme ~54 dias-pessoa (+ spike DISC-001 ~2–4 dias, fora do total), com infra e custo recorrente modestos. Não há veto.

**O resultado esperado.** Resultados mensuráveis: zero novos double-bookings em 4 semanas pós go-live, zero novos adiamentos comerciais atribuíveis a conflito de sala em 8 semanas, e 100% das reservas migradas para o sistema digital em 2 semanas — protegendo o pipeline comercial de ~R$700 mil e estancando a perda de receita já observada.

**Provenance**
- **Confidence:** 80
- **Origin:** po_authored (composição do PO; antes synthesized)
- **Source:** a-objectives + a-scope + b-feasibility + effort-cost + success-metrics
- **Status:** respondida
- **Disposition:** synthesized
- **Hint:** nenhum fato novo; confiança limitada pelo input mais fraco (effort-cost 72) e pela ressalva R1 ainda aberta; sobe quando DISC-001 fecha.

---

## Parte A — Definição de Produto (do Pacote de Prontidão · PO)

> Resumo das seções-chave do RP — **herdado, nunca reescrito**. A fonte completa é o
> `RP-2026-001` vinculado; aqui está o que o PM precisa para planejar. Cada seção-A é
> `Origin: inherited` (carregada do RP congelado em sua confiança preservada) e confirmada
> pelo PO.

### A.1 Objetivos e Resultado Esperado
<!-- origination: id=a-objectives; blocks=true; min-confidence=75; kind=capture -->
> Rubrica: os resultados mensuráveis que a demanda persegue, carregados do RP. Cada objetivo
> é um resultado (o que muda para o usuário/negócio), não uma entrega (o que é construído).

1. **Eliminar o double-booking:** zero novos conflitos nas 4 semanas seguintes ao go-live (monitoramento + ausência de relatos da secretária).
2. **Proteger o pipeline comercial:** zero novos adiamentos de negócios atribuíveis a conflito de sala nas 8 semanas seguintes (acompanhamento com a liderança comercial, D02).
3. **Migrar 100% das reservas para o sistema digital:** mural e Forms descontinuados em até 2 semanas pós go-live; todas as reservas exclusivamente no sistema (observação direta + confirmação da secretária).
4. **Integração em tempo real com o Google Calendar:** toda reserva confirmada/cancelada reflete no Calendar em até 2 minutos (sync uma via) — teste funcional de integração.

Detalhamento: RP §3.

**Provenance**
- **Confidence:** 85
- **Origin:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Source:** RP §3
- **Status:** herdada
- **Disposition:** inherited
- **Hint:** metas/prazos propostos no RP; outcomes não outputs.

### A.2 Escopo (final)
<!-- origination: id=a-scope; blocks=true; min-confidence=80; kind=capture -->
> Rubrica: os limites finais de incluído / excluído / adiado do RP congelado. Este é o
> escopo contra o qual o PM planeja — fixado no PRD; o downstream executa, não redefine.
> Se `scope-reconciliation` alterou algo, isso reflete o escopo reconciliado (final).

**Incluído:** CRUD de reservas; integração Google Calendar **uma via** (sistema→Calendar; reflete em ≤2 min; alterações no Calendar não retroalimentam); login social (sem SSO); regras automáticas de anti-double-booking (sobreposição parcial ou total); reservas recorrentes com validação por ocorrência (ocorrências em conflito sinalizadas, série não rejeitada); migração e descontinuação do processo manual (mural + Forms + WhatsApp).

**Excluído:** Outlook/Microsoft 365; SSO corporativo; outros recursos físicos; analytics avançado/relatórios; portal externo para visitantes.

**Adiado:** Outlook (Fase 2); analytics/relatórios (Fase 2); lembretes automáticos (Fase 2); SSO corporativo (Fase 3).

> Nota: escopo carregado do RP (C-Q02 sync uma via; C-Q03 recorrência). Reconciliação RP×TA concluída (ver Reconciliação de Escopo): **escopo do RP mantido integralmente**; a entregabilidade da integração Google Calendar fica condicionada ao grant OAuth do Workspace (R1 / DISC-001).

**Provenance**
- **Confidence:** 83
- **Origin:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Source:** RP §5
- **Status:** herdada
- **Disposition:** inherited
- **Hint:** reconciliação final pendente (scope-reconciliation); qualquer adição ao incluído dispara o risco R05.

### A.3 Personas / Jobs-to-be-done
<!-- origination: id=a-personas; blocks=true; min-confidence=70; kind=capture -->
> Rubrica: quem é impactado e o trabalho que cada persona contrata o produto para realizar,
> herdado do RP.

| Persona | Job-to-be-done | Impacto pós-entrega |
|---|---|---|
| Equipes internas (colaboradores) | Reservar sala com antecedência e ter certeza da disponibilidade. | Zero risco de double-booking; disponibilidade em tempo real; confirmação automática. |
| Reuniões com clientes/externos | Conduzir reuniões com visitantes de forma profissional, sem imprevistos. | Reserva confirmada elimina conflito; credibilidade preservada. |
| Liderança e diretoria | Garantir reuniões estratégicas no horário, sem interrupções por conflito. | Visibilidade de ocupação; reservas com confirmação; protegidas por anti-conflito automático. |
| Secretária / Facilities (stakeholder-chave de migração) | Manter o processo ordenado, resolver conflitos, garantir a sala certa. | Sistema assume o papel de árbitro; secretária deixa de ser gargalo. Adesão e validação de usabilidade são necessárias; o sistema deve ser mais simples que o Forms. |

Detalhamento: RP §4.

**Provenance**
- **Confidence:** 76
- **Origin:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Source:** RP §4
- **Status:** herdada
- **Disposition:** inherited
- **Hint:** conf 76 < 80 — entrevista rápida com a secretária recomendada antes do gate.

### A.4 Jornada do Usuário (ponta a ponta)
<!-- origination: id=a-journey; blocks=true; min-confidence=70; kind=capture -->
> Rubrica: o fluxo do happy path que o usuário percorre de ponta a ponta, herdado do RP —
> o fluxo do qual as Histórias de Usuário derivam. Caminhos alternativos e o blueprint
> completo de serviço permanecem no RP.

Happy path (Jornada A — colaborador):

| # | Ação do usuário | Resultado esperado | Touchpoint |
|---|---|---|---|
| A1 | Acessa e realiza login social | Autenticado; acesso liberado | Tela de login |
| A2 | Consulta disponibilidade em tempo real | Salas disponíveis/indisponíveis exibidas | Tela de disponibilidade |
| A3 | Escolhe sala/horário; preenche dados | Formulário validado | Formulário de reserva |
| A4 | Confirma a reserva | Validação anti-conflito; reserva criada e confirmada | Tela de confirmação |
| A5 | (sistema) | Sincronização com Google Calendar em ≤2 min | Backstage — Calendar API |
| A6 | (sistema) | Participantes recebem convite do Calendar | E-mail / Calendar |

Jornadas de referência (no RP §6.5): B (secretária em nome de terceiro, modelo flat), C (recorrente, validação por ocorrência), e ALT-1..ALT-5.

**Provenance**
- **Confidence:** 80
- **Origin:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Source:** RP §6.5
- **Status:** herdada
- **Disposition:** inherited
- **Hint:** ALT-1 (sugestão de alternativas) sem decisão fechada — definir antes da implementação.

### A.5 Regras de Negócio e Fluxos
<!-- origination: id=a-business-rules; blocks=true; min-confidence=70; kind=capture -->
> Rubrica: as regras, validações e transições de estado que o sistema deve impor — resumo
> ou referência às seções do RP. Suficiente para o PM dimensionar o trabalho sem surpresas.

Resumo das 16 regras (RN-01..RN-16) em 5 blocos; texto normativo completo em RP §6:

- **Exclusividade / anti-double-booking (RN-01..05):** máx. 1 reserva ativa por sala/intervalo; sobreposição parcial é conflito; validação na confirmação; sistema é fonte de verdade; sob concorrência **first-commit-wins**. (C-Q01)
- **Permissões — modelo flat (RN-06):** qualquer usuário autenticado cria/edita/cancela qualquer reserva (campos "responsável"/"participantes"); sem perfil admin. (C-Q04)
- **Parâmetros temporais (RN-09..12):** janela 08h–19h dias úteis; duração 15 min–8 h; antecedência máx. ~90 dias (valor exato a parametrizar); edição/cancelamento até o início. (C-Q05)
- **Precedência FCFS (RN-13):** first-come, first-served; hierarquia não sobrescreve; realocação facilitada mas não automática. (C-Q01)
- **Recorrentes — MVP (RN-14..16):** séries; validação por ocorrência; conflitos sinalizados; usuário decide. (C-Q03)

Fluxo de estado: Rascunho → Confirmada → Cancelada/Concluída; falha de sync mantém Confirmada (retry/backoff). Sincronização **uma via** (C-Q02): propaga ≤2 min; alterações no Calendar não retroalimentam.

**Provenance**
- **Confidence:** 88
- **Origin:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Source:** RP §6
- **Status:** herdada
- **Disposition:** inherited
- **Hint:** antecedência máx. (~90 dias) a parametrizar antes da implementação.

### A.6 Histórias de Usuário + Critérios de Aceite
<!-- origination: id=a-user-stories; blocks=true; min-confidence=80; kind=capture -->
> Rubrica: as histórias com seus critérios primários de aceite Given/When/Then, herdados do
> RP. São o que QA/UAT valida — devem ser testáveis. Critérios completos permanecem no RP.

| ID | História | Critério primário (Given/When/Then) |
|---|---|---|
| US-01 | Como colaborador, quero login social (Google), para não criar nova senha. | Dado conta Google válida, quando escolho "Entrar com Google", então sou autenticado sem cadastro adicional. |
| US-02 [CENTRAL] | Como usuário autenticado, quero bloqueio automático de reservas sobrepostas, para garantir a sala. | Dado Sala A confirmada 14h–15h, quando tento confirmar 14h30–15h30 (sobreposição parcial), então o sistema bloqueia e não cria a reserva. |
| US-03 | Como usuário autenticado, quero consultar disponibilidade em tempo real. | Dado autenticado, quando seleciono data/intervalo, então vejo quais salas estão disponíveis/ocupadas. |
| US-04 | Como usuário autenticado, quero criar reserva (sala, data, horário, título, participantes). | Dado autenticado e sala disponível, quando preencho e confirmo, então a reserva é criada "Confirmada" e aparece na consulta. |
| US-05 | Como usuário autenticado, quero editar/cancelar qualquer reserva antes do início. | Dado reserva confirmada não iniciada, quando cancelo, então o slot é liberado, o evento é removido do Calendar e os participantes são notificados. |
| US-06 | Como participante, quero que reserva/cancelamento reflita no meu Calendar. | Dado reserva confirmada com minha participação, quando confirmada, então em ≤2 min recebo convite no Calendar. |
| US-07 | Como usuário autenticado (incl. secretária), quero reservar em nome de terceiro. | Dado autenticado, quando crio reserva com "responsável" outro colaborador, então fica vinculada a ele, ao menos tão simples quanto o Forms. |
| US-08 | Como usuário autenticado, quero criar série recorrente. | Dado ocorrências em conflito, quando o sistema valida, então as sem conflito são confirmadas, as em conflito sinalizadas, e a série não é descartada. |

Critérios completos: RP §7.

**Provenance**
- **Confidence:** 88
- **Origin:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Source:** RP §7
- **Status:** herdada
- **Disposition:** inherited
- **Hint:** US-05 (modelo flat) — considerar confirmação explícita anti-cancelamento acidental antes da implementação.

### A.7 Requisitos Não-Funcionais (RNFs)
<!-- origination: id=a-nfrs; blocks=true; min-confidence=75; kind=capture -->
> Rubrica: os RNFs de produto declarados no RP (§8), cada um com como é verificado. Quando
> escalado, cada um se emparelha com uma resposta de viabilidade em B.4 — mantê-los consistentes.

| ID | Dimensão | Requisito | Verificação |
|---|---|---|---|
| NFR-01 [CRÍTICO] | Confiabilidade/Integridade | Nunca duas reservas confirmadas sobrepostas na mesma sala, inclusive sob concorrência. | Teste de concorrência; implementação atômica (TA) |
| NFR-02 | Desempenho/Sincronização | Reserva confirmada/cancelada reflete no Calendar em ≤2 min (uma via). | Teste funcional de integração |
| NFR-03 | Desempenho/Resposta | Consulta ≤2 s (p95); confirmação ≤3 s (p95). | Teste de carga |
| NFR-04 [CRÍTICO] | Usabilidade/Adoção | Criar reserva mais simples que o Forms atual; sem treinamento formal. | Validação qualitativa com a secretária (RP §11) |
| NFR-05 | Usabilidade/Responsividade | Responsivo/mobile-friendly; mobile ≥360px, tablet ≥768px. | Fluxo crítico testado em mobile |
| NFR-06 | Segurança/Autenticação | Acesso só via login social; reserva atribuível a usuário; SSO fora. | Revisão de controle de acesso |
| NFR-07 | Segurança/Privacidade | LGPD básico; base legal/retenção/exclusão a definir. | Revisão obrigatória Jurídico/DPO antes do release |
| NFR-08 | Compatibilidade/Interoperabilidade | Interopera só com Google Calendar (uma via); Outlook fora. | Testes de integração |
| NFR-09 | Confiabilidade/Disponibilidade | ≥99% em horário comercial; sem SLA 24/7. | Testes de disponibilidade |
| NFR-10 | Eficiência/Escala | Suporta ~200 usuários; pico 10h–16h. | Testes de carga |

Cada NFR se emparelha 1:1 com `b-nfr-feasibility` (invariante A.7 ↔ B.4).

**Provenance**
- **Confidence:** 82
- **Origin:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Source:** RP §8
- **Status:** herdada
- **Disposition:** inherited
- **Hint:** NFR-07 (LGPD) exige revisão Jurídico/DPO antes do release.

### A.8 Casos de Borda e Modos de Falha
<!-- origination: id=a-edge-cases; blocks=true; min-confidence=70; kind=capture -->
> Rubrica: os casos de borda e modos de falha (RP §9), cada um com comportamento esperado.
> O PM e os Tech Leads dimensionam os caminhos infelizes a partir daqui.

- **EC-01** Reservas concorrentes → first-commit-wins; a 2ª recebe conflito com alternativa. (C-Q01)
- **EC-02** Falha da Calendar API → reserva confirmada/cancelada localmente; "sincronização pendente"; retry/backoff; nada é revertido.
- **EC-03** Mural/Forms em paralelo pós go-live → canal antigo descontinuado em ≤2 semanas; reservas fora do sistema inválidas.
- **EC-04** Alteração direta no Calendar → não retroalimenta (uma via, C-Q02); slot permanece; UI alerta que Calendar é espelho.
- **EC-05** Recorrente com ocorrência em conflito → validação por ocorrência; conflitos sinalizados; demais confirmadas. (C-Q03)
- **EC-06** Fuso/DST → horários não-ambíguos com fuso local; intervalos ambíguos exigem confirmação. (premissa mono-fuso a confirmar)
- **EC-07** Sala em manutenção → bloqueia novas reservas; existentes realocadas manualmente com notificação.
- **EC-08** Externo sem login → não reserva direto; organizador interno cria e convida via Calendar. (C-Q02)
- **EC-09** Edição que cria conflito → rejeita, mantém original, informa conflito.
- **EC-10** Reserva em nome de terceiro → modelo flat (C-Q04); campo "responsável"; sem admin.
- **EC-11** Sistema fora do ar → falha segura e visível; nenhuma confirmação falsa; sem fallback ao mural.
- **EC-12** Reserva no passado/além da antecedência → rejeitada com mensagem. (C-Q05)
- **EC-13** Divergência silenciosa Calendar×sistema → sistema é fonte de verdade; não detectada automaticamente; UI avisa que Calendar é espelho.

Detalhamento: RP §9.

**Provenance**
- **Confidence:** 80
- **Origin:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Source:** RP §9
- **Status:** herdada
- **Disposition:** inherited
- **Hint:** EC-06 (mono-fuso) — confirmar antes da implementação.

---

## Parte B — Definição Técnica (da Avaliação Técnica · CTO)

> Resumo do TA — **herdado, nunca reescrito**. A fonte completa é o `TA-2026-001` vinculado.
> **Quando não houve escalação**, cada seção-B abaixo é disposicionada
> `Disposition: decided` com conteúdo "N/A — sem escalação arquitetural" (uma disposição
> honesta que libera o gate). Veja references/reconciliation.md.

### B.1 Veredito de Viabilidade
<!-- origination: id=b-feasibility; blocks=true; min-confidence=80; kind=capture -->
> Rubrica: o veredito do CTO, **herdado do TA — nunca re-decidido no PRD**. Carrega o
> veredito + as ressalvas que devem ser mantidas. `Inviável como escopo` nunca chega a um PRD
> (um veto devolve o RP para re-escopo). N/A quando não escalado.

| Campo | Valor |
|---|---|
| **Veredito** | **Viável com ressalvas** |
| **Ressalvas** | R1 — admin do Workspace permite grant OAuth a apps de terceiros (`calendar.events`) + credencial/quotas (gated DISC-001); R2 — first-commit-wins via exclusão transacional (não read-then-write); R3 — sync estritamente uma-via, sem reconciliação reversa; R4 — revisão LGPD Jurídico/DPO antes do release. |

**Provenance**
- **Confidence:** 86
- **Origin:** cto_authored (confirmado pelo CTO no sign-off; antes inherited)
- **Source:** TA-2026-001 §feasibility-verdict (cto_authored)
- **Status:** respondida
- **Disposition:** inherited (decided — assinado sob ressalvas)
- **Hint:** veredito carregado verbatim, nunca re-decidido; um veto só se materializaria se o admin do Workspace negasse o grant (R1).

### B.2 Natureza e Paisagem Técnica
<!-- origination: id=b-nature-landscape; blocks=true; min-confidence=70; kind=capture -->
> Rubrica: o terreno que a engenharia decide, herdado do TA. Brownfield → resumo do
> **estado atual** (padrões, integrações, débito) com link ao `tech-landscape`.
> Greenfield → resumo da **fundação** (stack escolhida + arquitetura alvo). N/A quando
> não escalado.

| Campo | Valor |
|---|---|
| **Natureza** | Híbrido — processo informal (mural+Forms+WhatsApp, secretária) + software-core novo (greenfield) + integração Google Calendar |
| **Base de conhecimento** | `tech-landscape-room-reservation.md` — criada neste ciclo (semeada pelos ADRs greenfield + populada por DISC-001) |
| **Estado atual (brownfield)** | Processo manual (mural = fonte de verdade atual + Forms + WhatsApp); ambiente Workspace/OAuth não documentado (gated DISC-001); sem código legado/dados a migrar; processo será descontinuado. |
| **Fundação (greenfield)** | TypeScript/Node; backend NestJS/Express (REST); frontend React responsivo; PostgreSQL transacional (EXCLUSION constraint anti-overlap); worker async (transactional outbox); monorepo; PaaS gerenciada. |

**Provenance**
- **Confidence:** 78
- **Origin:** cto_authored (confirmado pelo CTO no sign-off; antes inherited)
- **Source:** TA §tech-classification + §tech-foundation + §current-state
- **Status:** respondida
- **Disposition:** discovery (estado atual/Workspace — DISC-001 aberto)
- **Hint:** confiança limitada pelo current-state (54, gated); terreno Workspace/OAuth não documentado até o spike.

### B.3 Impacto Arquitetural e Integrações
<!-- origination: id=b-arch-impact; blocks=true; min-confidence=75; kind=capture -->
> Rubrica: cada sistema/área tocado e a natureza do impacto, mais as integrações necessárias
> sob a lente da viabilidade técnica — herdado do TA. N/A quando não escalado.

**Sistemas tocados:** novo sistema (criado); Google Calendar (consumido, uma via); mural físico (migrado/descontinuado ≤2 sem); Google Forms (migrado/descontinuado ≤2 sem); WhatsApp (descontinuado como canal).

**Impacto por área:**

| Área | Impacto | Nota |
|---|---|---|
| Modelo de dados | Entidades novas (sala, reserva intervalo `[início,fim)`, usuário, série); exclusividade de intervalo como constraint de banco (`EXCLUDE USING gist`). | Sem legado. |
| Eventos/mensageria | Sync = efeito assíncrono via outbox + worker (retry/backoff), desacoplado do commit. | EC-02; idempotência por chave da reserva. |
| Frontend | UI responsiva/mobile-first (NFR-05); disponibilidade quase real-time; aviso "Calendar é espelho". | Re-fetch sob demanda atende MVP. |
| Segurança | OAuth2/OIDC login social (NFR-06); credencial/escopo Calendar gated DISC-001; LGPD básico (NFR-07, revisão DPO). | Separar OIDC de identidade da credencial de escrita; menor privilégio. |
| Desempenho/Escala | ~200 usuários; constraint crítica é corretude sob concorrência (NFR-01), não volume; ≤2s/≤3s p95 (NFR-03); ≥99% (NFR-09). | PaaS + banco gerenciado suficientes. |
| Multi-tenancy | N/A — organização única. | Sem abstração especulativa. |

**Integrações:** Google Calendar (OAuth2 / `calendar.events`) — viável com ressalvas (config Workspace gated DISC-001); login social (OAuth2/OIDC) — viável.

**Provenance**
- **Confidence:** 78
- **Origin:** cto_authored (confirmado pelo CTO no sign-off; antes inherited)
- **Source:** TA §affected-systems + §architectural-impact + §integrations
- **Status:** respondida
- **Disposition:** inherited (decided; credencial Calendar gated DISC-001)
- **Hint:** modelo de credencial Calendar não resolvido até DISC-001.

### B.4 Viabilidade dos RNFs
<!-- origination: id=b-nfr-feasibility; blocks=true; min-confidence=75; kind=capture -->
> Rubrica: a resposta do CTO a cada RNF do RP (A.7 / RP §8) — viável? e como — herdada do
> TA. Manter uma linha por RNF de A.7 para que o loop produto↔técnico fique fechado. N/A
> quando não escalado.

| RNF (de A.7) | Viável? | Abordagem | Ressalva |
|---|---|---|---|
| NFR-01 [CRÍTICO] | Sim | Exclusão transacional no banco (`EXCLUDE USING gist`/serializável); first-commit-wins como invariante; harness de concorrência (gate de release). | Não-negociável; alto risco se feito na aplicação. |
| NFR-02 | Com ressalvas | Worker async (fila + retry/backoff); folga ampla; reserva persiste independente do sync. | Gated DISC-001: quotas/credencial. |
| NFR-03 | Sim | Índices + consulta simples; alvos confortáveis na escala. | Validar p95 no pico. |
| NFR-04 [CRÍTICO] | Com ressalvas | UX: fluxo mais curto que o Forms; validação com a secretária. | Validado por produto, não arquitetura. |
| NFR-05 | Sim | Front responsivo validado nos breakpoints. | Testar em mobile real. |
| NFR-06 | Com ressalvas | Login social OAuth/OIDC; reserva atribuída a user_id; sem SSO. | Gated DISC-001: consent/escopos/domínio. |
| NFR-07 | Com ressalvas | Criptografia em repouso; retenção ~12 meses; exclusão a pedido. | Revisão Jurídico/DPO; bloqueante p/ release. |
| NFR-08 | Com ressalvas | Só Calendar API, uma via; Outlook excluído; reusa worker/credencial. | Gated DISC-001; risco de scope creep (R05). |
| NFR-09 | Sim | PaaS gerenciada + app stateless; manutenção fora do horário. | Calendar API indisponível não derruba o sistema. |
| NFR-10 | Sim | Carga pequena; 1 instância + banco dimensionado. | Confirmar em teste de carga. |

**Provenance**
- **Confidence:** 80
- **Origin:** cto_authored (confirmado pelo CTO no sign-off; antes inherited)
- **Source:** TA §nfr-feasibility (cto_authored)
- **Status:** respondida
- **Disposition:** inherited (decided; NFR-02/06/08 com ressalvas gated DISC-001; NFR-07 gated DPO)
- **Hint:** NFR-01/03/05/09/10 sem ressalva; NFR-02/06/08 gated; NFR-07 exige Jurídico/DPO.

### B.5 Principais Alternativas Consideradas
<!-- origination: id=b-alternatives; blocks=false; min-confidence=0; kind=capture -->
> Rubrica: a lógica por trás das decisões técnicas — o que foi descartado e por quê — para
> que o downstream não re-litige. Apenas as alternativas que o PM precisa conhecer. Herdado
> do TA; "—" com `Disposition: decided` se nenhuma / não escalado.

| Alternativa | Por que NÃO foi escolhida |
|---|---|
| Sincronização bidirecional Calendar↔sistema | Fora do escopo (C-Q02); exige webhooks/reconciliação; uma-via atende sem a complexidade. |
| Google Calendar como fonte de verdade (sem banco) | Calendar API não garante exclusividade transacional/first-commit-wins (TA-Q03); o sistema precisa ser fonte de verdade (RN-04). |
| Persistência NoSQL/documento | Exclusividade de intervalo exigiria coordenação aplicacional frágil; escala modesta não justifica; relacional resolve direto. |
| Validação otimista sem trava transacional | Janela de corrida; não garante first-commit-wins (RN-05, EC-01); transação/serializável é a única que satisfaz NFR-01. |

**Provenance**
- **Confidence:** 76
- **Origin:** cto_authored (confirmado pelo CTO no sign-off; antes inherited)
- **Source:** TA §alternatives (cto_authored)
- **Status:** respondida
- **Disposition:** inherited (decided)
- **Hint:** seção não-bloqueante; previne re-litigação downstream.

### B.6 Restrições Duras
<!-- origination: id=b-hard-constraints; blocks=true; min-confidence=75; kind=capture -->
> Rubrica: as condições inegociáveis que limitam o espaço da solução e seu efeito no
> escopo — herdado do TA. Alimentam `scope-reconciliation`. "Nenhuma" com
> `Disposition: decided` se nenhuma; N/A quando não escalado.

| Restrição | Efeito no escopo |
|---|---|
| Exclusividade transacional / first-commit-wins (NFR-01) | Define a persistência: store transacional com não-sobreposição; sem garantia transacional → descartado. |
| Sincronização uma-via sistema→Calendar | Sem webhooks de entrada, sem bidirecional; Calendar é espelho read-only. |
| Só Google Calendar; sem Outlook; sem SSO | Login social é o único modelo de identidade; inclusões disparam R05 + reavaliação do TA. |
| Conformidade LGPD básica (NFR-07) | Revisão Jurídico/DPO obrigatória antes do release; retenção/exclusão como aceite. |
| Dependência da config do Google Workspace (grant OAuth) | Gate de Discovery (DISC-001); se negado, re-escopar a integração. |

**Provenance**
- **Confidence:** 80
- **Origin:** cto_authored (confirmado pelo CTO no sign-off; antes inherited)
- **Source:** TA §hard-constraints (cto_authored)
- **Status:** respondida
- **Disposition:** inherited (decided; Workspace gated DISC-001)
- **Hint:** alimentam scope-reconciliation; a restrição de Workspace é o único gatilho possível de re-escopo.

### B.7 ADRs (nível arquitetural)
<!-- origination: id=b-adrs; blocks=true; min-confidence=70; kind=capture -->
> Rubrica: as decisões arquiteturais assinadas pelo CTO, herdadas do TA. ADRs detalhados /
> de implementação pertencem ao Tech Backlog do Tech Lead, não aqui. N/A quando não escalado.

| # | Decisão | Sign-off CTO |
|---|---|---|
| ADR-001 | Persistência relacional transacional com não-sobreposição (intervalos `[início,fim)` por sala; `EXCLUDE USING gist` ou serializável). | ✓ |
| ADR-002 | Sync uma-via assíncrona via transactional outbox + worker idempotente (retry/backoff). | ✓ |
| ADR-003 | Sistema = fonte de verdade; Calendar = espelho read-only; sem reconciliação de volta neste release. | ✓ |
| ADR-004 | Autenticação federada OAuth2/OIDC (login social Google); sem senha própria; sem SSO neste release. | ✓ |
| ADR-005 | Tempo em UTC com fuso explícito; premissa mono-fuso; tratar DST ambíguo (EC-06). | ✓ |
| ADR-006 | Modelo de credencial da Calendar API — A DECIDIR no spike DISC-001 (service account c/ delegação de domínio vs delegação por usuário). | — (gated DISC-001) |

**Provenance**
- **Confidence:** 80
- **Origin:** cto_authored (confirmado pelo CTO no sign-off; antes inherited)
- **Source:** TA §adrs (cto_authored)
- **Status:** respondida
- **Disposition:** inherited (decided ADR-001..005 ✓; discovery ADR-006)
- **Hint:** ADR-006 não-settled; breakdown fino vai ao Tech Backlog.

---

## Reconciliação de Escopo
<!-- origination: id=scope-reconciliation; blocks=true; min-confidence=80; kind=derived; inputs=a-scope,b-feasibility,b-hard-constraints -->
> Rubrica: **reconciliar** o escopo do RP contra o veredito, ressalvas e restrições duras
> do TA. Se o CTO impôs restrições ou ressalvas que alteraram o que o RP escopo, registrar
> exatamente o que mudou e por quê — e garantir que A.2 reflita o escopo reconciliado
> (final). Se nada mudou (ou sem escalação): "Escopo do RP mantido integralmente." Este é
> o trabalho de reconciliação do PRD — é `derived`, computado das metades herdadas,
> nunca inventado.

| Item original (RP) | Alteração pós Avaliação Técnica | Motivo |
|---|---|---|
| CRUD de reservas | Inalterado | Nenhuma restrição/ressalva do TA toca o item. |
| Integração Google Calendar uma via (≤2 min) | Inalterado (entregabilidade **condicionada** ao grant OAuth do Workspace) | Restrições "sync uma-via" e R3 afirmam o item; "dependência da config do Workspace" + R1 são gate de Discovery (DISC-001) sobre a entregabilidade — dependência, não remoção/re-escopo. |
| Login social (sem SSO) | Inalterado | "Só Google; sem Outlook; sem SSO" afirma o item; R1 condiciona apenas consent/escopos. |
| Anti-double-booking (sobreposição parcial/total) | Inalterado | "Exclusividade transacional / first-commit-wins" e R2 especificam o mecanismo (já em NFR-01/ADR-001), não mudam escopo. |
| Reservas recorrentes (validação por ocorrência) | Inalterado | Nenhuma restrição toca o item. |
| Migração/descontinuação do processo manual | Inalterado | Nenhuma restrição toca o item. |
| Excluído: Outlook/M365; SSO; outros recursos; analytics; portal externo | Inalterado | "Só Google; sem Outlook; sem SSO" confirma as exclusões. |
| Adiado: Outlook (F2); analytics (F2); lembretes (F2); SSO (F3) | Inalterado | Nenhuma restrição altera os adiamentos. |
| Conformidade LGPD (NFR-07) | Inalterado | R4 (revisão Jurídico/DPO antes do release) já refletida em NFR-07; bloqueante de release, não mudança de escopo. |

**Síntese:** Escopo do RP **mantido integralmente**. As restrições e ressalvas do TA afirmam ou condicionam itens já escopados, sem adicionar/remover/re-escopar. A entregabilidade da integração Google Calendar fica condicionada ao grant OAuth do Workspace (R1 / gate DISC-001) — dependência registrada em `inherited-readiness` e `consolidated-risk`. Nenhum item de a-scope foi alterado.

**Provenance**
- **Confidence:** 80
- **Origin:** po_authored (composição do PO; antes synthesized)
- **Source:** a-scope (RP §5) + b-feasibility (R1–R4) + b-hard-constraints
- **Status:** respondida
- **Disposition:** decided (escopo mantido integralmente)
- **Hint:** entregabilidade da integração condicionada a R1/DISC-001 (dependência, não remoção); se o grant for negado, re-escopar (gatilho upstream).

---

## Visão Consolidada de Riscos e Dependências
<!-- origination: id=consolidated-risk; blocks=true; min-confidence=75; kind=derived; inputs=a-edge-cases,b-arch-impact,b-hard-constraints -->
> Rubrica: uma única tabela fundindo os **riscos de produto/negócio** (do RP, §12) com os
> **riscos técnicos** (do TA) — cada um marcado por origem e tipo, com probabilidade, impacto
> e mitigação. O PM planeja contra esta visão consolidada. Listar explicitamente as
> dependências externas conhecidas. `derived` — composto das duas metades, sem novos riscos
> inventados.

| Risco | Origem | Tipo | Probabilidade | Impacto | Mitigação |
|---|---|---|---|---|---|
| Baixa adoção / resistência (usuários voltam ao hábito antigo) | RP | Produto/Adoção | Alta | Alto | NFR-04 [CRÍTICO] — fluxo mais simples que o Forms; validação com a secretária (RP §11); secretária como agente de mudança. |
| Dependência da secretária na migração | RP | Externo/Adoção | Média | Alto | Engajar a secretária como stakeholder-chave (D01); modelo flat reduz dependência de perfil único. |
| Retorno ao mural/Forms em paralelo | RP | Produto/Adoção | Média-Alta | Alto | Descontinuação formal do canal antigo em ≤2 sem (EC-03); reservas fora do sistema inválidas (RN-04). |
| R$90k em risco não recuperado | RP | Negócio | Média | Médio | Acompanhamento com a liderança comercial (D02); zero novos adiamentos em 8 sem. |
| Scope creep de integração (bidirecional/Outlook/SSO) | RP | Produto/Escopo | Baixa-Média | Médio | Escopo fixado (RP §5; restrições B.6); qualquer adição dispara R05 + reavaliação do TA; sync uma-via mantida. |
| Workspace nega/restringe grant OAuth (`calendar.events`) | TA | Externo/Integração | Média | Alto | Antecipar DISC-001; plano B de credencial (TA-Q01); escalar ao admin cedo. **Gate** da integração (D03). |
| Race condition no anti-double-booking | TA | Técnica | Média | Alto | NFR-01: gravação atômica via constraint/serializável (RN-05); harness de concorrência (EC-01, TA-Q03). |
| Quota/latência da Calendar API vs ≤2 min | TA | Integração | Baixa-Média | Médio | Worker async c/ backoff; ≤2 min tem folga; monitorar quota (TA-Q04). |
| Divergência silenciosa Calendar↔sistema | TA | Dados | Média | Médio | Aviso na UI (Calendar é espelho — EC-04/EC-13); sistema é fonte de verdade (RN-04/C-Q02). |
| Fuso/DST | TA | Dados | Baixa | Médio | UTC c/ fuso explícito; bloquear intervalos ambíguos (EC-06); confirmar mono-fuso. |
| Falha de sync deixa estado inconsistente | TA | Integração | Baixa | Médio | Outbox + retry idempotente; reserva confirmada localmente independe do sync (EC-02). |

**Dependências externas conhecidas:** Admin do Google Workspace (grant OAuth / DISC-001 / R1 — único gatilho possível de re-escopo); Secretária/Facilities (onboarding, validação UX/NFR-04, migração — D01); Liderança comercial (recuperação do pipeline R$90k, confirmar adiamentos — D02); Google Calendar API disponível + OAuth de-arriscado (D03, ligado a DISC-001).

**Provenance**
- **Confidence:** 78
- **Origin:** po_authored (composição do PO; antes synthesized)
- **Source:** RP §12 (R01–R05 + D01–D03) + TA tech-risks (6)
- **Status:** respondida
- **Disposition:** decided (composto; nenhum risco novo inventado)
- **Hint:** o risco de grant OAuth do Workspace (TA) é o único que pode gatilhar re-escopo — escalar via DISC-001/D03.

---

## Esforço e Custo (firme)
<!-- origination: id=effort-cost; blocks=true; min-confidence=70; kind=capture -->
> Rubrica: a estimativa **firme** da Avaliação Técnica (substitui o número preliminar do RP).
> Quando **não escalado**, carregar a estimativa preliminar do RP e rotulá-la preliminar
> (o Tech Lead a firma no breakdown). Uso interno apenas — não é um compromisso contratual
> ou voltado ao cliente.

| Área | Estimativa | Senioridade |
|---|---|---|
| Backend — núcleo de reservas | 12 dias | Pleno (revisão Sênior) |
| Backend — anti-double-booking + recorrência | 8 dias | Sênior |
| Integração / OAuth — Calendar + login social | 10 dias | Sênior |
| Frontend — UI responsiva | 12 dias | Pleno |
| QA — incl. harness de concorrência | 8 dias | QA |
| LGPD básica + migração/descontinuação | 4 dias | Pleno |
| **Total (desenvolvimento)** | **~54 dias-pessoa** | (+ spike DISC-001 ~2–4 dias, fora do total) |

**Infra / Terceiros / Opex recorrente:** infra modesta (1 app host + 1 banco gerenciado + 1 worker; sem multi-região/Kubernetes); terceiros baixo (Calendar API na quota gratuita — confirmar no spike; login social Google gratuito; sem licenças); opex recorrente baixo. TCO cria fundação reutilizável (Outlook Fase 2, SSO Fase 3, analytics Fase 2). Estimativa firme substitui a preliminar do RP §13 (deferida).

**Provenance**
- **Confidence:** 72
- **Origin:** cto_authored (confirmado pelo CTO no sign-off; antes inherited)
- **Source:** TA §effort-cost (cto_authored)
- **Status:** respondida
- **Disposition:** inherited (decided; linha OAuth a re-firmar pós-DISC-001)
- **Hint:** uso interno; não é compromisso contratual; o PM trata a linha de integração como sujeita a ajuste pós-spike.

---

## Prontidão Herdada e Disposições em Aberto
<!-- origination: id=inherited-readiness; blocks=true; min-confidence=70; kind=derived; inputs=a-scope,b-feasibility -->
> Rubrica: o que o PM precisa ver antes de planejar — as premissas ainda a validar, as
> incógnitas de Discovery (resolvidas ou em aberto) e as respostas delegadas (com responsável)
> que sobreviveram do upstream. Se uma premissa se mostrar falsa durante a execução, a demanda
> é re-triada (gatilho de re-triagem no downstream). `derived` — carregada das disposições
> do RP/TA.

| Campo | Valor |
|---|---|
| **Premissas ainda a validar** | Lado-produto: nenhuma OPEN (RP resolvidas em D003+D005). Pontos de atenção ativos para o PM/implementação: (1) EC-06 premissa de mono-fuso (ADR-005); (2) antecedência máxima exata (~90 dias, RN-09..12) a parametrizar; (3) ALT-1 sugestão de alternativas (UX) a definir; (4) US-05 confirmação anti-cancelamento acidental (modelo flat) a definir; (5) Persona 4 (secretária) conf 76 — entrevista recomendada antes do gate. |
| **Incógnitas de Discovery** | RP Discovery RESOLVIDO (D003+D005, 2026-06-06). TA Discovery **DISC-001 EM ABERTO** — ambiente Google Workspace/OAuth não documentado (escopos concedíveis, grant a apps de terceiros, modelo de credencial [ADR-006], quotas Calendar API). Gating: NFR-02/06/08 + ADR-006 + re-firmação da estimativa de integração. |
| **Requisitos delegados (com responsável)** | (1) Avaliação Técnica — antes delegada pelo RP, agora ASSINADA (TA-2026-001, Viável com ressalvas); delegação encerrada. (2) Spike DISC-001 — owner CTO/Tech Lead + TI da organização; ~2 a 4 dias; cobre R1. (3) Revisão LGPD (NFR-07/R4) — owner Jurídico/DPO; bloqueante antes do release. |

**Gatilho de re-triagem (downstream):** se uma premissa carregada se provar falsa na execução (ex.: mono-fuso EC-06, ou grant OAuth do Workspace negado R1/DISC-001), a demanda é re-triada, não corrigida em silêncio.

**Provenance**
- **Confidence:** 80
- **Origin:** po_authored (composição do PO; antes synthesized)
- **Source:** RP dispositions (D003+D005) + TA discovery-path (R1/R4, current-state, ADR-006) + DISC-001
- **Status:** respondida
- **Disposition:** discovery (DISC-001 em aberto)
- **Hint:** DISC-001 gate NFR-02/06/08 + ADR-006 + linha de integração; product-side sem premissas OPEN, 5 pontos de atenção ativos.

---

## Critérios de Sucesso e Métricas (projetadas)
<!-- origination: id=success-metrics; blocks=true; min-confidence=75; kind=capture -->
> Rubrica: o baseline projetado — métricas primárias e guardrails (um guardrail é uma
> métrica que NÃO deve piorar) — herdado do RP, com meta, janela e confiança. É contra isso
> que `metrics.md` (projetado vs. realizado) compara pós-rollout.

| Tipo | Métrica | Baseline | Meta pós-rollout | Janela | Confiança |
|---|---|---|---|---|---|
| Primária (lagging) | Double-bookings/semana | ~1,8/sem (9/5sem) | 0 | 4 sem pós go-live | Alta |
| Primária (lagging) | Novos adiamentos de negócios por conflito | 9 em 5 sem | 0 | 8 sem pós go-live | Média (depende de D02) |
| Leading | Adoção (% reservas no sistema) | 0% | 100% | 2 sem pós go-live | Alta |
| Guardrail | Volume total de reservas/semana | a medir pré-go-live | não cair vs baseline | Semana 1 | Média |
| Guardrail | Carga de remarcação da secretária | a medir pré-go-live | não aumentar vs baseline | 4 sem | Média |

Nota financeira (referência, não métrica do sistema): pipeline ~R$700k; R$111k perdidos; R$90k em risco (monitorar com D02).

**Provenance**
- **Confidence:** 80
- **Origin:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Source:** RP §10
- **Status:** herdada
- **Disposition:** inherited
- **Hint:** guardrails dependem de medição na semana pré-go-live — planejar coleta.

---

## Handoff ao PM — Gate de Aceite
<!-- origination: id=handoff-gate; blocks=true; min-confidence=80; kind=derived; inputs=sign-off,scope-reconciliation,consolidated-risk,inherited-readiness -->
> Rubrica: o checklist de entrega que o PM aceita (ou rejeita). O PM tem **autoridade
> explícita para rejeitar** o PRD e devolvê-lo com lacunas **específicas** (não um genérico
> "precisa de mais detalhes"); a rejeição e o motivo entram no Histórico de Revisões, e o
> PO (ou CTO, dependendo da lacuna) endereça apenas as lacunas e incrementa a versão.
> Cada caixa deve ser verificável a partir do documento fundido. `derived` — assegura que a
> fusão está completa; não inventa nada.

| Checklist de entrega | OK? |
|---|---|
| RP congelado (`freezeReady`) e referenciado | ✓ |
| Avaliação Técnica assinada (ou N/A justificado) | ✓ |
| Reconciliação de escopo registrada | ✓ |
| Riscos e dependências consolidados | ✓ |
| Dependências externas explícitas | ✓ |
| Disposições em aberto visíveis | ✓ |

**Prioridade e contexto de negócio (por que esta demanda, agora):** Double-booking crônico (~1,8 conflitos/semana — 9 em 5 semanas) com impacto comercial quantificado: R$111k já perdidos, R$90k em risco, pipeline ~R$700k acompanhado com a liderança comercial (D02). O custo de esperar cresce a cada semana — cada conflito erode a credibilidade em reuniões com clientes e adia negócios. A integração foi de-arriscada e considerada viável ("Viável com ressalvas", TA-2026-001); o único gatilho possível de re-escopo é a negação do grant OAuth pelo admin do Workspace (R1 / DISC-001). Escala modesta (~200 usuários, janela 08h–19h, organização única); a restrição crítica é corretude sob concorrência (NFR-01), não volume. Migração e descontinuação do processo manual em ≤2 semanas pós go-live.

> Nota de autoridade: o PM tem autoridade explícita para rejeitar o PRD e devolvê-lo com lacunas específicas (não um genérico "precisa de mais detalhes"). A rejeição e o motivo entram no Histórico de Revisões; o PO endereça lacunas de produto, o CTO as técnicas (reabrindo apenas a metade afetada), e a versão é incrementada.

**Provenance**
- **Confidence:** 80
- **Origin:** po_authored (composição do PO; antes synthesized)
- **Source:** sign-off + scope-reconciliation + consolidated-risk + inherited-readiness (+ meta, b-feasibility)
- **Status:** respondida
- **Disposition:** synthesized
- **Hint:** as 6 caixas são verificáveis a partir das seções correspondentes do documento fundido; dual sign-off comitado (PO + CTO) — todas as caixas confirmadas.

<!-- END OF DOCUMENT -->
