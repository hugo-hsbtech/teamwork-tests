<!--
PRD - Product Requirements Document
Instanciado do template target-template.prd.md em 2026-06-07.
Part A herdada do RP-2026-001; Part B herdada do TA-2026-001 (escalado, assinado).
Dual sign-off comitado (Fase 4): PO (RP congelado) + CTO (Viavel com ressalvas).
Status: Accepted. Entregue ao PM em 2026-06-07. handoffReady.
-->

# PRD - Reserva de Salas de Reuniao
<!-- rev: 3 · updated: 2026-06-07 -->

> O PRD (Documento de Requisitos de Produto) e a **fusao** do **Pacote de Prontidao**
> (produto, de autoria do PO) com a **Avaliacao Tecnica** (tecnica, de autoria do CTO).
> E o **unico artefato que abre o downstream** (entregue ao **PM**).
> Cada metade preserva a autoria clara: o PO nao escreve a parte tecnica, o CTO
> nao reescreve a parte de produto. O PRD **costura, reconcilia e expoe** ao PM o que
> ele precisa para planejar, sem reescrever nenhuma das fontes. Veja `personas/02-po.md`
> paragrafos 2/10/11 e `templates/04-prd.md`.
>
> **Quando nao houve escalacao ao CTO:** o PRD e formado apenas pelo RP; a Parte B e
> disposicionada como "N/A - sem escalacao arquitetural".
>
> `PRD = RP (PO) + Avaliacao Tecnica (CTO)`

## Metadados
<!-- origination: id=meta; blocks=false; min-confidence=0; kind=meta -->

| Campo | Valor |
|---|---|
| **PRD ID** | PRD-2026-001 |
| **Versao** | v1 |
| **RP Vinculado** | RP-2026-001 v1 |
| **Avaliacao Tecnica Vinculada** | TA-2026-001 v1 |
| **Intake Vinculado** | INT-2026-001 |
| **Escalado?** | Sim (TA incorporado) |
| **Natureza da Demanda** | Hibrido |
| **Autores** | PO + CTO |
| **Status** | Accepted |
| **Idioma de saida** | pt-BR |
| **Entregue ao PM em** | 2026-06-07 |

## Historico de Revisoes
<!-- origination: id=revisions; blocks=false; min-confidence=0; kind=meta -->

| Versao | Data | Autor | Status | Resumo |
|---|---|---|---|---|
| v1 | 2026-06-07 | Doc Updater (Fase 2 - merge inherit) | Rascunho | PRD instanciado do template; Part A herdada do RP-2026-001 (a-objectives..a-edge-cases + success-metrics) e Part B herdada do TA-2026-001 (b-feasibility..b-adrs + effort-cost firme). Origin: inherited. Secoes derivadas (exec-summary, scope-reconciliation, consolidated-risk, inherited-readiness, handoff-gate) e sign-off pendentes (Fase 3/4). |
| v1 | 2026-06-07 | Doc Updater (Fase 3 - sintetizar & reconciliar) | Draft | Secoes derivadas preenchidas: scope-reconciliation (escopo do RP mantido integralmente), consolidated-risk (11 riscos RP+TA + dependencias externas), inherited-readiness (DISC-001 aberto), exec-summary, handoff-gate. Nota de reconciliacao do a-scope resolvida. sign-off pendente (Fase 4). |
| v1 | 2026-06-07 | Doc Updater (Fase 4 - dual sign-off) | Accepted | Dual sign-off comitado: PO (RP congelado) + CTO (veredito Viavel com ressalvas carregado do TA). Secoes promovidas a po_authored/cto_authored; dispositions discovery preservadas (DISC-001). Status=Accepted; entregue ao PM 2026-06-07. handoffReady. |

---

## Assinatura
<!-- origination: id=sign-off; blocks=true; min-confidence=85; kind=capture -->
> Rubrica: a fusao **so se fecha com assinatura dupla**. O PO assina a metade de produto
> (o RP esta congelado, `freezeReady`); o CTO assina a metade tecnica (o TA esta assinado,
> e o veredito de viabilidade e carregado do TA), ou o campo do CTO e um **N/A honesto** quando
> nao houve escalacao. O PRD nao pode ser congelado (`handoffReady`) sem esta linha resolvida.
> O veredito de viabilidade e **herdado do TA, nunca re-decidido aqui**. Um TA vetado
> nunca chega a esta secao (nao ha PRD em caso de veto). Limite alto: esta e a porta.

| Papel | Nome | Veredito | Data |
|---|---|---|---|
| **PO** (produto) | PO | RP Congelado (`freezeReady`) | 2026-06-07 |
| **CTO** (tecnico) | CTO | Viavel com ressalvas | 2026-06-07 |

**Proveniencia**
- **Confianca:** 90
- **Origem:** po_authored + cto_authored
- **Fonte:** RP-2026-001 congelado (PO) + TA-2026-001 veredito carregado (CTO)
- **Situacao:** respondida
- **Disposicao:** decided (dual sign-off comitado; handoffReady)
- **Observacao:** o veredito e carregado do TA, nunca re-decidido no PRD; ressalvas R1..R4 e DISC-001 viajam para a execucao.

---

## Resumo Executivo Combinado
<!-- origination: id=exec-summary; blocks=true; min-confidence=75; kind=derived; inputs=a-objectives,a-scope,b-feasibility,effort-cost,success-metrics -->
> Rubrica: 2 a 4 paragrafos sobre o problema, o que sera construido, a viabilidade tecnica e
> o resultado de negocio esperado. A visao de uma pagina para CEO/CFO/PM. **Sintetizado**
> a partir das secoes herdadas (nao acrescenta fatos novos, compoe os ja incorporados).
> Um bom resumo permite que o leitor que nao ler mais nada saiba por que esta demanda,
> o que ela entrega, se e viavel e qual resultado ela persegue.

**O problema.** A organizacao convive com conflito de agendamento (double-booking) cronico de salas: o agendamento se espalha por tres canais nao integrados (mural fisico, Google Forms e WhatsApp) sem nenhum mecanismo de anti-conflito. O resultado e um ritmo de cerca de 1,8 conflitos por semana (9 em 5 semanas), com impacto comercial ja quantificado: R$111 mil em negocios perdidos, R$90 mil em risco e um pipeline de aproximadamente R$700 mil de novos negocios exposto a adiamentos por conflito de agendamento. A secretaria/facilities atua como arbitro manual e gargalo a cada conflito.

**O que sera construido.** Um sistema digital de reserva de salas (natureza Hibrida: software-core novo + integracao + migracao de um processo informal) cujo nucleo e o anti-double-booking automatico sob a regra first-commit-wins: a primeira confirmacao persiste e a segunda recebe conflito, eliminando sobreposicoes parciais ou totais. O sistema inclui integracao uma-via com o Google Calendar (toda reserva confirmada/cancelada reflete em ate 2 minutos, sem retroalimentacao reversa), login social, reservas recorrentes com validacao por ocorrencia, e a migracao e descontinuacao dos canais manuais (mural, Forms e WhatsApp) em ate 2 semanas pos go-live.

**A viabilidade tecnica.** O CTO assinou o veredito "Viavel com ressalvas" (herdado da Avaliacao Tecnica, nunca re-decidido aqui). A arquitetura e solida: a integridade anti-conflito repousa sobre exclusao transacional no banco (nao read-then-write), e a sincronizacao com o Calendar e assincrona e desacoplada do commit. As ressalvas tem caminhos de resolucao conhecidos: o grant OAuth do Google Workspace e o modelo de credencial da Calendar API, mais a revisao LGPD (Juridico/DPO), confirmados no spike DISC-001 no inicio da execucao. Esforco firme de aproximadamente 54 dias-pessoa (mais spike DISC-001 de 2 a 4 dias, fora do total), com infra e custo recorrente modestos. Nao ha veto.

**O resultado esperado.** Resultados mensuraveis: zero novos double-bookings em 4 semanas pos go-live, zero novos adiamentos comerciais atribuiveis a conflito de sala em 8 semanas, e 100% das reservas migradas para o sistema digital em 2 semanas, protegendo o pipeline comercial de aproximadamente R$700 mil e estancando a perda de receita ja observada.

**Proveniencia**
- **Confianca:** 80
- **Origem:** po_authored (composicao do PO; antes synthesized)
- **Fonte:** a-objectives + a-scope + b-feasibility + effort-cost + success-metrics
- **Situacao:** respondida
- **Disposicao:** synthesized
- **Observacao:** nenhum fato novo; confianca limitada pelo input mais fraco (effort-cost 72) e pela ressalva R1 ainda aberta; sobe quando DISC-001 fecha.

---

## Parte A - Definicao de Produto (do Pacote de Prontidao · PO)

> Resumo das secoes-chave do RP, **herdado, nunca reescrito**. A fonte completa e o
> `RP-2026-001` vinculado; aqui esta o que o PM precisa para planejar. Cada secao-A e
> `Origin: inherited` (carregada do RP congelado em sua confianca preservada) e confirmada
> pelo PO.

### A.1 Objetivos e Resultado Esperado
<!-- origination: id=a-objectives; blocks=true; min-confidence=75; kind=capture -->
> Rubrica: os resultados mensuraveis que a demanda persegue, carregados do RP. Cada objetivo
> e um resultado (o que muda para o usuario/negocio), nao uma entrega (o que e construido).

1. **Eliminar o conflito de agendamento (double-booking):** zero novos conflitos nas 4 semanas seguintes ao go-live (monitoramento + ausencia de relatos da secretaria).
2. **Proteger o pipeline comercial:** zero novos adiamentos de negocios atribuiveis a conflito de sala nas 8 semanas seguintes (acompanhamento com a lideranca comercial, D02).
3. **Migrar 100% das reservas para o sistema digital:** mural e Forms descontinuados em ate 2 semanas pos go-live; todas as reservas exclusivamente no sistema (observacao direta + confirmacao da secretaria).
4. **Integracao em tempo real com o Google Calendar:** toda reserva confirmada/cancelada reflete no Calendar em ate 2 minutos (sincronizacao uma-via) (teste funcional de integracao).

Detalhamento: RP paragrafo 3.

**Proveniencia**
- **Confianca:** 85
- **Origem:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Fonte:** RP paragrafo 3
- **Situacao:** herdada
- **Disposicao:** inherited
- **Observacao:** metas/prazos propostos no RP; outcomes nao outputs.

### A.2 Escopo (final)
<!-- origination: id=a-scope; blocks=true; min-confidence=80; kind=capture -->
> Rubrica: os limites finais de incluido / excluido / adiado do RP congelado. Este e o
> escopo contra o qual o PM planeja (fixado no PRD; o downstream executa, nao redefine).
> Se `scope-reconciliation` alterou algo, isso reflete o escopo reconciliado (final).

**Incluido:** CRUD de reservas; integracao Google Calendar **uma via** (sistema para Calendar; reflete em ate 2 minutos; alteracoes no Calendar nao retroalimentam); login social (sem SSO); regras automaticas de anti-double-booking (sobreposicao parcial ou total); reservas recorrentes com validacao por ocorrencia (ocorrencias em conflito sinalizadas, serie nao rejeitada); migracao e descontinuacao do processo manual (mural, Forms e WhatsApp).

**Excluido:** Outlook/Microsoft 365; SSO corporativo; outros recursos fisicos; analytics avancado/relatorios; portal externo para visitantes.

**Adiado:** Outlook (Fase 2); analytics/relatorios (Fase 2); lembretes automaticos (Fase 2); SSO corporativo (Fase 3).

> Nota: escopo carregado do RP (C-Q02 sync uma-via; C-Q03 recorrencia). Reconciliacao RP x TA concluida (ver Reconciliacao de Escopo): **escopo do RP mantido integralmente**; a entregabilidade da integracao Google Calendar fica condicionada ao grant OAuth do Workspace (R1 / DISC-001).

**Proveniencia**
- **Confianca:** 83
- **Origem:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Fonte:** RP paragrafo 5
- **Situacao:** herdada
- **Disposicao:** inherited
- **Observacao:** reconciliacao final pendente (scope-reconciliation); qualquer adicao ao incluido dispara o risco R05.

### A.3 Personas / Jobs-to-be-done
<!-- origination: id=a-personas; blocks=true; min-confidence=70; kind=capture -->
> Rubrica: quem e impactado e o trabalho que cada persona contrata o produto para realizar,
> herdado do RP.

| Persona | Job-to-be-done | Impacto pos-entrega |
|---|---|---|
| Equipes internas (colaboradores) | Reservar sala com antecedencia e ter certeza da disponibilidade. | Zero risco de double-booking; disponibilidade em tempo real; confirmacao automatica. |
| Reunioes com clientes/externos | Conduzir reunioes com visitantes de forma profissional, sem imprevistos. | Reserva confirmada elimina conflito; credibilidade preservada. |
| Lideranca e diretoria | Garantir reunioes estrategicas no horario, sem interrupcoes por conflito. | Visibilidade de ocupacao; reservas com confirmacao; protegidas por anti-conflito automatico. |
| Secretaria / Facilities (stakeholder-chave de migracao) | Manter o processo ordenado, resolver conflitos, garantir a sala certa. | Sistema assume o papel de arbitro; secretaria deixa de ser gargalo. Adesao e validacao de usabilidade sao necessarias; o sistema deve ser mais simples que o Forms. |

Detalhamento: RP paragrafo 4.

**Proveniencia**
- **Confianca:** 76
- **Origem:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Fonte:** RP paragrafo 4
- **Situacao:** herdada
- **Disposicao:** inherited
- **Observacao:** conf 76 < 80 (entrevista rapida com a secretaria recomendada antes do gate).

### A.4 Jornada do Usuario (ponta a ponta)
<!-- origination: id=a-journey; blocks=true; min-confidence=70; kind=capture -->
> Rubrica: o fluxo principal que o usuario percorre de ponta a ponta, herdado do RP.
> E o fluxo do qual as Historias de Usuario derivam. Caminhos alternativos e o blueprint
> completo de servico permanecem no RP.

Fluxo principal (Jornada A - colaborador):

| # | Acao do usuario | Resultado esperado | Touchpoint |
|---|---|---|---|
| A1 | Acessa e realiza login social | Autenticado; acesso liberado | Tela de login |
| A2 | Consulta disponibilidade em tempo real | Salas disponiveis/indisponiveis exibidas | Tela de disponibilidade |
| A3 | Escolhe sala/horario; preenche dados | Formulario validado | Formulario de reserva |
| A4 | Confirma a reserva | Validacao anti-conflito; reserva criada e confirmada | Tela de confirmacao |
| A5 | (sistema) | Sincronizacao com Google Calendar em ate 2 min | Backstage - Calendar API |
| A6 | (sistema) | Participantes recebem convite do Calendar | E-mail / Calendar |

Jornadas de referencia (no RP paragrafo 6.5): B (secretaria em nome de terceiro, modelo flat), C (recorrente, validacao por ocorrencia), e ALT-1..ALT-5.

**Proveniencia**
- **Confianca:** 80
- **Origem:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Fonte:** RP paragrafo 6.5
- **Situacao:** herdada
- **Disposicao:** inherited
- **Observacao:** ALT-1 (sugestao de alternativas) sem decisao fechada (definir antes da implementacao).

### A.5 Regras de Negocio e Fluxos
<!-- origination: id=a-business-rules; blocks=true; min-confidence=70; kind=capture -->
> Rubrica: as regras, validacoes e transicoes de estado que o sistema deve impor (resumo
> ou referencia as secoes do RP). Suficiente para o PM dimensionar o trabalho sem surpresas.

Resumo das 16 regras (RN-01..RN-16) em 5 blocos; texto normativo completo em RP paragrafo 6:

- **Exclusividade / anti-double-booking (RN-01..05):** maxima 1 reserva ativa por sala/intervalo; sobreposicao parcial e conflito; validacao na confirmacao; sistema e fonte de verdade; sob concorrencia **first-commit-wins**. (C-Q01)
- **Permissoes (modelo flat) (RN-06):** qualquer usuario autenticado cria/edita/cancela qualquer reserva (campos "responsavel"/"participantes"); sem perfil admin. (C-Q04)
- **Parametros temporais (RN-09..12):** janela das 08h as 19h em dias uteis; duracao de 15 minutos a 8 horas; antecedencia maxima de aproximadamente 90 dias (valor exato a parametrizar); edicao/cancelamento ate o inicio. (C-Q05)
- **Precedencia FCFS (RN-13):** first-come, first-served; hierarquia nao sobrescreve; realocacao facilitada, mas nao automatica. (C-Q01)
- **Recorrentes (MVP) (RN-14..16):** series; validacao por ocorrencia; conflitos sinalizados; usuario decide. (C-Q03)

Fluxo de estado: Rascunho > Confirmada > Cancelada/Concluida; falha de sincronizacao mantem Confirmada (retry/backoff). Sincronizacao **uma via** (C-Q02): propaga em ate 2 minutos; alteracoes no Calendar nao retroalimentam.

**Proveniencia**
- **Confianca:** 88
- **Origem:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Fonte:** RP paragrafo 6
- **Situacao:** herdada
- **Disposicao:** inherited
- **Observacao:** antecedencia maxima (aproximadamente 90 dias) a parametrizar antes da implementacao.

### A.6 Historias de Usuario e Criterios de Aceite
<!-- origination: id=a-user-stories; blocks=true; min-confidence=80; kind=capture -->
> Rubrica: as historias com seus criterios primarios de aceite Given/When/Then, herdados do
> RP. Sao o que QA/UAT valida (devem ser testaveis). Criterios completos permanecem no RP.

| ID | Historia | Criterio primario (Given/When/Then) |
|---|---|---|
| US-01 | Como colaborador, quero login social (Google), para nao criar nova senha. | Dado conta Google valida, quando escolho "Entrar com Google", entao sou autenticado sem cadastro adicional. |
| US-02 [CENTRAL] | Como usuario autenticado, quero bloqueio automatico de reservas sobrepostas, para garantir a sala. | Dado Sala A confirmada 14h a 15h, quando tento confirmar 14h30 a 15h30 (sobreposicao parcial), entao o sistema bloqueia e nao cria a reserva. |
| US-03 | Como usuario autenticado, quero consultar disponibilidade em tempo real. | Dado autenticado, quando seleciono data/intervalo, entao vejo quais salas estao disponiveis/ocupadas. |
| US-04 | Como usuario autenticado, quero criar reserva (sala, data, horario, titulo, participantes). | Dado autenticado e sala disponivel, quando preencho e confirmo, entao a reserva e criada "Confirmada" e aparece na consulta. |
| US-05 | Como usuario autenticado, quero editar/cancelar qualquer reserva antes do inicio. | Dado reserva confirmada nao iniciada, quando cancelo, entao o slot e liberado, o evento e removido do Calendar e os participantes sao notificados. |
| US-06 | Como participante, quero que reserva/cancelamento reflita no meu Calendar. | Dado reserva confirmada com minha participacao, quando confirmada, entao em ate 2 minutos recebo convite no Calendar. |
| US-07 | Como usuario autenticado (incl. secretaria), quero reservar em nome de terceiro. | Dado autenticado, quando crio reserva com "responsavel" outro colaborador, entao fica vinculada a ele, ao menos tao simples quanto o Forms. |
| US-08 | Como usuario autenticado, quero criar serie recorrente. | Dado ocorrencias em conflito, quando o sistema valida, entao as sem conflito sao confirmadas, as em conflito sinalizadas, e a serie nao e descartada. |

Criterios completos: RP paragrafo 7.

**Proveniencia**
- **Confianca:** 88
- **Origem:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Fonte:** RP paragrafo 7
- **Situacao:** herdada
- **Disposicao:** inherited
- **Observacao:** US-05 (modelo flat) (considerar confirmacao explicita anti-cancelamento acidental antes da implementacao).

### A.7 Requisitos Nao-Funcionais (RNFs)
<!-- origination: id=a-nfrs; blocks=true; min-confidence=75; kind=capture -->
> Rubrica: os RNFs de produto declarados no RP (paragrafo 8), cada um com como e verificado. Quando
> escalado, cada um se emparelha com uma resposta de viabilidade em B.4 (mante-los consistentes).

| ID | Dimensao | Requisito | Verificacao |
|---|---|---|---|
| NFR-01 [CRITICO] | Confiabilidade/Integridade | Nunca duas reservas confirmadas sobrepostas na mesma sala, inclusive sob concorrencia. | Teste de concorrencia; implementacao atomica (TA) |
| NFR-02 | Desempenho/Sincronizacao | Reserva confirmada/cancelada reflete no Calendar em ate 2 minutos (uma via). | Teste funcional de integracao |
| NFR-03 | Desempenho/Resposta | Consulta ate 2 s (p95); confirmacao ate 3 s (p95). | Teste de carga |
| NFR-04 [CRITICO] | Usabilidade/Adocao | Criar reserva mais simples que o Forms atual; sem treinamento formal. | Validacao qualitativa com a secretaria (RP paragrafo 11) |
| NFR-05 | Usabilidade/Responsividade | Responsivo/mobile-friendly; mobile com 360px ou mais, tablet com 768px ou mais. | Fluxo critico testado em mobile |
| NFR-06 | Seguranca/Autenticacao | Acesso so via login social; reserva atribuivel a usuario; SSO fora. | Revisao de controle de acesso |
| NFR-07 | Seguranca/Privacidade | LGPD basico; base legal/retencao/exclusao a definir. | Revisao obrigatoria Juridico/DPO antes do release |
| NFR-08 | Compatibilidade/Interoperabilidade | Interopera so com Google Calendar (uma via); Outlook fora. | Testes de integracao |
| NFR-09 | Confiabilidade/Disponibilidade | Disponibilidade de 99% ou mais em horario comercial; sem SLA 24/7. | Testes de disponibilidade |
| NFR-10 | Eficiencia/Escala | Suporta aproximadamente 200 usuarios; pico das 10h as 16h. | Testes de carga |

Cada NFR se emparelha 1:1 com `b-nfr-feasibility` (invariante A.7 com B.4).

**Proveniencia**
- **Confianca:** 82
- **Origem:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Fonte:** RP paragrafo 8
- **Situacao:** herdada
- **Disposicao:** inherited
- **Observacao:** NFR-07 (LGPD) exige revisao Juridico/DPO antes do release.

### A.8 Casos de Borda e Modos de Falha
<!-- origination: id=a-edge-cases; blocks=true; min-confidence=70; kind=capture -->
> Rubrica: os casos de borda e modos de falha (RP paragrafo 9), cada um com comportamento esperado.
> O PM e os Tech Leads dimensionam os caminhos infelizes a partir daqui.

- **EC-01** Reservas concorrentes: first-commit-wins; a segunda recebe conflito com alternativa. (C-Q01)
- **EC-02** Falha da Calendar API: reserva confirmada/cancelada localmente; status "sincronizacao pendente"; retry/backoff; nada e revertido.
- **EC-03** Mural/Forms em paralelo pos go-live: canal antigo descontinuado em ate 2 semanas; reservas fora do sistema sao invalidas.
- **EC-04** Alteracao direta no Calendar: nao retroalimenta (uma via, C-Q02); slot permanece; UI alerta que Calendar e espelho.
- **EC-05** Recorrente com ocorrencia em conflito: validacao por ocorrencia; conflitos sinalizados; demais confirmadas. (C-Q03)
- **EC-06** Fuso/DST: horarios nao ambiguos com fuso local; intervalos ambiguos exigem confirmacao. (premissa mono-fuso a confirmar)
- **EC-07** Sala em manutencao: bloqueia novas reservas; existentes realocadas manualmente com notificacao.
- **EC-08** Externo sem login: nao reserva direto; organizador interno cria e convida via Calendar. (C-Q02)
- **EC-09** Edicao que cria conflito: rejeita, mantem original, informa conflito.
- **EC-10** Reserva em nome de terceiro: modelo flat (C-Q04); campo "responsavel"; sem admin.
- **EC-11** Sistema fora do ar: falha segura e visivel; nenhuma confirmacao falsa; sem fallback ao mural.
- **EC-12** Reserva no passado/alem da antecedencia: rejeitada com mensagem. (C-Q05)
- **EC-13** Divergencia silenciosa Calendar x sistema: sistema e fonte de verdade; nao detectada automaticamente; UI avisa que Calendar e espelho.

Detalhamento: RP paragrafo 9.

**Proveniencia**
- **Confianca:** 80
- **Origem:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Fonte:** RP paragrafo 9
- **Situacao:** herdada
- **Disposicao:** inherited
- **Observacao:** EC-06 (mono-fuso) (confirmar antes da implementacao).

---

## Parte B - Definicao Tecnica (da Avaliacao Tecnica · CTO)

> Resumo do TA, **herdado, nunca reescrito**. A fonte completa e o `TA-2026-001` vinculado.
> **Quando nao houve escalacao**, cada secao-B abaixo e disposicionada
> `Disposition: decided` com conteudo "N/A - sem escalacao arquitetural" (uma disposicao
> honesta que libera o gate). Veja references/reconciliation.md.

### B.1 Veredito de Viabilidade
<!-- origination: id=b-feasibility; blocks=true; min-confidence=80; kind=capture -->
> Rubrica: o veredito do CTO, **herdado do TA, nunca re-decidido no PRD**. Carrega o
> veredito e as ressalvas que devem ser mantidas. `Inviavel como escopo` nunca chega a um PRD
> (um veto devolve o RP para revisao de escopo). N/A quando nao escalado.

| Campo | Valor |
|---|---|
| **Veredito** | **Viavel com ressalvas** |
| **Ressalvas** | R1: admin do Workspace permite grant OAuth a apps de terceiros (`calendar.events`) e credencial/quotas (condicionado a DISC-001); R2: first-commit-wins via exclusao transacional (nao read-then-write); R3: sync estritamente uma-via, sem reconciliacao reversa; R4: revisao LGPD Juridico/DPO antes do release. |

**Proveniencia**
- **Confianca:** 86
- **Origem:** cto_authored (confirmado pelo CTO no sign-off; antes inherited)
- **Fonte:** TA-2026-001 paragrafo feasibility-verdict (cto_authored)
- **Situacao:** respondida
- **Disposicao:** inherited (decided - assinado sob ressalvas)
- **Observacao:** veredito carregado verbatim, nunca re-decidido; um veto so se materializaria se o admin do Workspace negasse o grant (R1).

### B.2 Natureza e Paisagem Tecnica
<!-- origination: id=b-nature-landscape; blocks=true; min-confidence=70; kind=capture -->
> Rubrica: o terreno que a engenharia decide, herdado do TA. Brownfield: resumo do
> **estado-atual** (padroes, integracoes, debito) com link ao `tech-landscape`.
> Greenfield: resumo da **fundacao** (stack escolhida + arquitetura alvo). N/A quando
> nao escalado.

| Campo | Valor |
|---|---|
| **Natureza** | Hibrido (processo informal: mural, Forms e WhatsApp com secretaria) + software-core novo (greenfield) + integracao Google Calendar |
| **Base de conhecimento** | `tech-landscape-room-reservation.md` (criada neste ciclo: semeada pelos ADRs greenfield + populada por DISC-001) |
| **Estado atual (brownfield)** | Processo manual (mural = fonte de verdade atual, Forms e WhatsApp); ambiente Workspace/OAuth nao documentado (condicionado a DISC-001); sem codigo legado/dados a migrar; processo sera descontinuado. |
| **Fundacao (greenfield)** | TypeScript/Node; backend NestJS/Express (REST); frontend React responsivo; PostgreSQL transacional (EXCLUSION constraint anti-overlap); worker async (transactional outbox); monorepo; PaaS gerenciada. |

**Proveniencia**
- **Confianca:** 78
- **Origem:** cto_authored (confirmado pelo CTO no sign-off; antes inherited)
- **Fonte:** TA paragrafo tech-classification + paragrafo tech-foundation + paragrafo current-state
- **Situacao:** respondida
- **Disposicao:** discovery (estado-atual/Workspace - DISC-001 aberto)
- **Observacao:** confianca limitada pelo estado-atual (54, condicionado a DISC-001); terreno Workspace/OAuth nao documentado ate o spike.

### B.3 Impacto Arquitetural e Integracoes
<!-- origination: id=b-arch-impact; blocks=true; min-confidence=75; kind=capture -->
> Rubrica: cada sistema/area tocado e a natureza do impacto, mais as integracoes necessarias
> sob a lente da viabilidade tecnica, herdado do TA. N/A quando nao escalado.

**Sistemas tocados:** novo sistema (criado); Google Calendar (consumido, uma via); mural fisico (migrado/descontinuado em ate 2 semanas); Google Forms (migrado/descontinuado em ate 2 semanas); WhatsApp (descontinuado como canal).

**Impacto por area:**

| Area | Impacto | Nota |
|---|---|---|
| Modelo de dados | Entidades novas (sala, reserva com intervalo `[inicio,fim)`, usuario, serie); exclusividade de intervalo como constraint de banco (`EXCLUDE USING gist`). | Sem legado. |
| Eventos/mensageria | Sincronizacao = efeito assincrono via outbox + worker (retry/backoff), desacoplado do commit. | EC-02; idempotencia por chave da reserva. |
| Frontend | UI responsiva/mobile-first (NFR-05); disponibilidade quase em tempo real; aviso "Calendar e espelho". | Re-fetch sob demanda atende ao MVP. |
| Seguranca | OAuth2/OIDC login social (NFR-06); credencial/escopo Calendar condicionado a DISC-001; LGPD basico (NFR-07, revisao DPO). | Separar OIDC de identidade da credencial de escrita; menor privilegio. |
| Desempenho/Escala | Aproximadamente 200 usuarios; restricao critica e corretude sob concorrencia (NFR-01), nao volume; ate 2s/ate 3s p95 (NFR-03); disponibilidade de 99% ou mais (NFR-09). | PaaS + banco gerenciado suficientes. |
| Multi-tenancy | N/A (organizacao unica). | Sem abstracao especulativa. |

**Integracoes:** Google Calendar (OAuth2 / `calendar.events`) (viavel com ressalvas: config Workspace condicionado a DISC-001); login social (OAuth2/OIDC) (viavel).

**Proveniencia**
- **Confianca:** 78
- **Origem:** cto_authored (confirmado pelo CTO no sign-off; antes inherited)
- **Fonte:** TA paragrafo affected-systems + paragrafo architectural-impact + paragrafo integrations
- **Situacao:** respondida
- **Disposicao:** inherited (decided; credencial Calendar condicionado a DISC-001)
- **Observacao:** modelo de credencial Calendar nao resolvido ate DISC-001.

### B.4 Viabilidade dos RNFs
<!-- origination: id=b-nfr-feasibility; blocks=true; min-confidence=75; kind=capture -->
> Rubrica: a resposta do CTO a cada RNF do RP (A.7 / RP paragrafo 8) sobre viabilidade e como,
> herdada do TA. Manter uma linha por RNF de A.7 para que o loop produto/tecnico fique fechado. N/A
> quando nao escalado.

| RNF (de A.7) | Viavel? | Abordagem | Ressalva |
|---|---|---|---|
| NFR-01 [CRITICO] | Sim | Exclusao transacional no banco (`EXCLUDE USING gist`/serializavel); first-commit-wins como invariante; harness de concorrencia (gate de release). | Nao negociavel; alto risco se feito na aplicacao. |
| NFR-02 | Com ressalvas | Worker async (fila + retry/backoff); folga ampla; reserva persiste independente do sync. | Condicionado a DISC-001: quotas/credencial. |
| NFR-03 | Sim | Indices + consulta simples; alvos confortaveis na escala. | Validar p95 no pico. |
| NFR-04 [CRITICO] | Com ressalvas | UX: fluxo mais curto que o Forms; validacao com a secretaria. | Validado por produto, nao arquitetura. |
| NFR-05 | Sim | Front responsivo validado nos breakpoints. | Testar em mobile real. |
| NFR-06 | Com ressalvas | Login social OAuth/OIDC; reserva atribuida a user_id; sem SSO. | Condicionado a DISC-001: consent/escopos/dominio. |
| NFR-07 | Com ressalvas | Criptografia em repouso; retencao de 12 meses; exclusao a pedido. | Revisao Juridico/DPO; bloqueante para release. |
| NFR-08 | Com ressalvas | So Calendar API, uma via; Outlook excluido; reusa worker/credencial. | Condicionado a DISC-001; risco de desvio de escopo (R05). |
| NFR-09 | Sim | PaaS gerenciada + app stateless; manutencao fora do horario. | Calendar API indisponivel nao derruba o sistema. |
| NFR-10 | Sim | Carga pequena; 1 instancia + banco dimensionado. | Confirmar em teste de carga. |

**Proveniencia**
- **Confianca:** 80
- **Origem:** cto_authored (confirmado pelo CTO no sign-off; antes inherited)
- **Fonte:** TA paragrafo nfr-feasibility (cto_authored)
- **Situacao:** respondida
- **Disposicao:** inherited (decided; NFR-02/06/08 com ressalvas condicionados a DISC-001; NFR-07 condicionado a DPO)
- **Observacao:** NFR-01/03/05/09/10 sem ressalva; NFR-02/06/08 condicionados a DISC-001; NFR-07 exige Juridico/DPO.

### B.5 Principais Alternativas Consideradas
<!-- origination: id=b-alternatives; blocks=false; min-confidence=0; kind=capture -->
> Rubrica: a logica por tras das decisoes tecnicas (o que foi descartado e por que) para
> que o downstream nao relitigie. Apenas as alternativas que o PM precisa conhecer. Herdado
> do TA; "-" com `Disposition: decided` se nenhuma / nao escalado.

| Alternativa | Por que NAO foi escolhida |
|---|---|
| Sincronizacao bidirecional Calendar com sistema | Fora do escopo (C-Q02); exige webhooks/reconciliacao; uma-via atende sem a complexidade. |
| Google Calendar como fonte de verdade (sem banco) | Calendar API nao garante exclusividade transacional/first-commit-wins (TA-Q03); o sistema precisa ser fonte de verdade (RN-04). |
| Persistencia NoSQL/documento | Exclusividade de intervalo exigiria coordenacao aplicacional fragil; escala modesta nao justifica; relacional resolve direto. |
| Validacao otimista sem trava transacional | Janela de corrida; nao garante first-commit-wins (RN-05, EC-01); transacao/serializavel e a unica que satisfaz NFR-01. |

**Proveniencia**
- **Confianca:** 76
- **Origem:** cto_authored (confirmado pelo CTO no sign-off; antes inherited)
- **Fonte:** TA paragrafo alternatives (cto_authored)
- **Situacao:** respondida
- **Disposicao:** inherited (decided)
- **Observacao:** secao nao bloqueante; previne relitigacao downstream.

### B.6 Restricoes Duras
<!-- origination: id=b-hard-constraints; blocks=true; min-confidence=75; kind=capture -->
> Rubrica: as condicoes inegociaveis que limitam o espaco da solucao e seu efeito no
> escopo, herdado do TA. Alimentam `scope-reconciliation`. "Nenhuma" com
> `Disposition: decided` se nenhuma; N/A quando nao escalado.

| Restricao | Efeito no escopo |
|---|---|
| Exclusividade transacional / first-commit-wins (NFR-01) | Define a persistencia: store transacional com nao sobreposicao; sem garantia transacional, descartado. |
| Sincronizacao uma-via sistema para Calendar | Sem webhooks de entrada, sem bidirecional; Calendar e espelho read-only. |
| So Google Calendar; sem Outlook; sem SSO | Login social e o unico modelo de identidade; inclusoes disparam R05 e reavaliacao do TA. |
| Conformidade LGPD basica (NFR-07) | Revisao Juridico/DPO obrigatoria antes do release; retencao/exclusao como aceite. |
| Dependencia da config do Google Workspace (grant OAuth) | Gate de Discovery (DISC-001); se negado, redefinir o escopo da integracao. |

**Proveniencia**
- **Confianca:** 80
- **Origem:** cto_authored (confirmado pelo CTO no sign-off; antes inherited)
- **Fonte:** TA paragrafo hard-constraints (cto_authored)
- **Situacao:** respondida
- **Disposicao:** inherited (decided; Workspace condicionado a DISC-001)
- **Observacao:** alimentam scope-reconciliation; a restricao de Workspace e o unico gatilho possivel de revisao de escopo.

### B.7 ADRs (nivel arquitetural)
<!-- origination: id=b-adrs; blocks=true; min-confidence=70; kind=capture -->
> Rubrica: as decisoes arquiteturais assinadas pelo CTO, herdadas do TA. ADRs detalhados
> ou de implementacao pertencem ao Tech Backlog do Tech Lead, nao aqui. N/A quando nao escalado.

| # | Decisao | Sign-off CTO |
|---|---|---|
| ADR-001 | Persistencia relacional transacional com nao sobreposicao (intervalos `[inicio,fim)` por sala; `EXCLUDE USING gist` ou serializavel). | ✓ |
| ADR-002 | Sincronizacao uma-via assincrona via transactional outbox + worker idempotente (retry/backoff). | ✓ |
| ADR-003 | Sistema = fonte de verdade; Calendar = espelho read-only; sem reconciliacao de volta neste release. | ✓ |
| ADR-004 | Autenticacao federada OAuth2/OIDC (login social Google); sem senha propria; sem SSO neste release. | ✓ |
| ADR-005 | Tempo em UTC com fuso explicito; premissa mono-fuso; tratar DST ambiguo (EC-06). | ✓ |
| ADR-006 | Modelo de credencial da Calendar API: A DECIDIR no spike DISC-001 (service account com delegacao de dominio vs delegacao por usuario). | - (condicionado a DISC-001) |

**Proveniencia**
- **Confianca:** 80
- **Origem:** cto_authored (confirmado pelo CTO no sign-off; antes inherited)
- **Fonte:** TA paragrafo adrs (cto_authored)
- **Situacao:** respondida
- **Disposicao:** inherited (decided ADR-001..005 ✓; discovery ADR-006)
- **Observacao:** ADR-006 nao definido; detalhamento fino vai ao Tech Backlog.

---

## Reconciliacao de Escopo
<!-- origination: id=scope-reconciliation; blocks=true; min-confidence=80; kind=derived; inputs=a-scope,b-feasibility,b-hard-constraints -->
> Rubrica: **reconciliar** o escopo do RP contra o veredito, ressalvas e restricoes duras
> do TA. Se o CTO impos restricoes ou ressalvas que alteraram o que o RP escopou, registrar
> exatamente o que mudou e por que, garantindo que A.2 reflita o escopo reconciliado
> (final). Se nada mudou (ou sem escalacao): "Escopo do RP mantido integralmente." Este e
> o trabalho de reconciliacao do PRD (derivado, computado das metades herdadas, nunca inventado).

| Item original (RP) | Alteracao pos Avaliacao Tecnica | Motivo |
|---|---|---|
| CRUD de reservas | Inalterado | Nenhuma restricao/ressalva do TA toca o item. |
| Integracao Google Calendar uma via (ate 2 minutos) | Inalterado (entregabilidade **condicionada** ao grant OAuth do Workspace) | Restricoes "sync uma-via" e R3 afirmam o item; "dependencia da config do Workspace" e R1 sao gate de Discovery (DISC-001) sobre a entregabilidade (dependencia, nao remocao/revisao de escopo). |
| Login social (sem SSO) | Inalterado | "So Google; sem Outlook; sem SSO" afirma o item; R1 condiciona apenas consent/escopos. |
| Anti-double-booking (sobreposicao parcial/total) | Inalterado | "Exclusividade transacional / first-commit-wins" e R2 especificam o mecanismo (ja em NFR-01/ADR-001), nao mudam escopo. |
| Reservas recorrentes (validacao por ocorrencia) | Inalterado | Nenhuma restricao toca o item. |
| Migracao/descontinuacao do processo manual | Inalterado | Nenhuma restricao toca o item. |
| Excluido: Outlook/M365; SSO; outros recursos; analytics; portal externo | Inalterado | "So Google; sem Outlook; sem SSO" confirma as exclusoes. |
| Adiado: Outlook (F2); analytics (F2); lembretes (F2); SSO (F3) | Inalterado | Nenhuma restricao altera os adiamentos. |
| Conformidade LGPD (NFR-07) | Inalterado | R4 (revisao Juridico/DPO antes do release) ja refletida em NFR-07; bloqueante de release, nao mudanca de escopo. |

**Sintese:** Escopo do RP **mantido integralmente**. As restricoes e ressalvas do TA afirmam ou condicionam itens ja escopados, sem adicionar, remover ou redefinir o escopo. A entregabilidade da integracao Google Calendar fica condicionada ao grant OAuth do Workspace (R1 / gate DISC-001): dependencia registrada em `inherited-readiness` e `consolidated-risk`. Nenhum item de a-scope foi alterado.

**Proveniencia**
- **Confianca:** 80
- **Origem:** po_authored (composicao do PO; antes synthesized)
- **Fonte:** a-scope (RP paragrafo 5) + b-feasibility (R1 a R4) + b-hard-constraints
- **Situacao:** respondida
- **Disposicao:** decided (escopo mantido integralmente)
- **Observacao:** entregabilidade da integracao condicionada a R1/DISC-001 (dependencia, nao remocao); se o grant for negado, redefinir o escopo (gatilho upstream).

---

## Visao Consolidada de Riscos e Dependencias
<!-- origination: id=consolidated-risk; blocks=true; min-confidence=75; kind=derived; inputs=a-edge-cases,b-arch-impact,b-hard-constraints -->
> Rubrica: uma unica tabela fundindo os **riscos de produto/negocio** (do RP, paragrafo 12) com os
> **riscos tecnicos** (do TA), cada um marcado por origem e tipo, com probabilidade, impacto
> e mitigacao. O PM planeja contra esta visao consolidada. Dependencias externas conhecidas sao
> listadas explicitamente. Derivado (composto das duas metades, sem novos riscos inventados).

| Risco | Origem | Tipo | Probabilidade | Impacto | Mitigacao |
|---|---|---|---|---|---|
| Baixa adocao / resistencia (usuarios voltam ao habito antigo) | RP | Produto/Adocao | Alta | Alto | NFR-04 [CRITICO]: fluxo mais simples que o Forms; validacao com a secretaria (RP paragrafo 11); secretaria como agente de mudanca. |
| Dependencia da secretaria na migracao | RP | Externo/Adocao | Media | Alto | Engajar a secretaria como stakeholder-chave (D01); modelo flat reduz dependencia de perfil unico. |
| Retorno ao mural/Forms em paralelo | RP | Produto/Adocao | Media-Alta | Alto | Descontinuacao formal do canal antigo em ate 2 semanas (EC-03); reservas fora do sistema sao invalidas (RN-04). |
| R$90k em risco nao recuperado | RP | Negocio | Media | Medio | Acompanhamento com a lideranca comercial (D02); zero novos adiamentos em 8 semanas. |
| Desvio de escopo de integracao (bidirecional/Outlook/SSO) | RP | Produto/Escopo | Baixa-Media | Medio | Escopo fixado (RP paragrafo 5; restricoes B.6); qualquer adicao dispara R05 e reavaliacao do TA; sincronizacao uma-via mantida. |
| Workspace nega/restringe grant OAuth (`calendar.events`) | TA | Externo/Integracao | Media | Alto | Antecipar DISC-001; plano B de credencial (TA-Q01); escalar ao admin cedo. **Gate** da integracao (D03). |
| Race condition no anti-double-booking | TA | Tecnica | Media | Alto | NFR-01: gravacao atomica via constraint/serializavel (RN-05); harness de concorrencia (EC-01, TA-Q03). |
| Quota/latencia da Calendar API vs ate 2 minutos | TA | Integracao | Baixa-Media | Medio | Worker async com backoff; margem de 2 minutos e folgada; monitorar quota (TA-Q04). |
| Divergencia silenciosa Calendar com sistema | TA | Dados | Media | Medio | Aviso na UI (Calendar e espelho: EC-04/EC-13); sistema e fonte de verdade (RN-04/C-Q02). |
| Fuso/DST | TA | Dados | Baixa | Medio | UTC com fuso explicito; bloquear intervalos ambiguos (EC-06); confirmar mono-fuso. |
| Falha de sincronizacao deixa estado inconsistente | TA | Integracao | Baixa | Medio | Outbox + retry idempotente; reserva confirmada localmente independe da sincronizacao (EC-02). |

**Dependencias externas conhecidas:** admin do Google Workspace (grant OAuth / DISC-001 / R1: unico gatilho possivel de revisao de escopo); Secretaria/Facilities (adesao, validacao UX/NFR-04, migracao: D01); Lideranca comercial (recuperacao do pipeline de R$90k, confirmar adiamentos: D02); Google Calendar API disponivel + integracao com riscos mitigados (D03, ligado a DISC-001).

**Proveniencia**
- **Confianca:** 78
- **Origem:** po_authored (composicao do PO; antes synthesized)
- **Fonte:** RP paragrafo 12 (R01 a R05 + D01 a D03) + TA tech-risks (6)
- **Situacao:** respondida
- **Disposicao:** decided (composto; nenhum risco novo inventado)
- **Observacao:** o risco de grant OAuth do Workspace (TA) e o unico que pode gatilhar revisao de escopo (escalar via DISC-001/D03).

---

## Esforco e Custo (firme)
<!-- origination: id=effort-cost; blocks=true; min-confidence=70; kind=capture -->
> Rubrica: a estimativa **firme** da Avaliacao Tecnica (substitui o numero preliminar do RP).
> Quando **nao escalado**, carregar a estimativa preliminar do RP e rotula-la preliminar
> (o Tech Lead a firma no breakdown). Uso interno (nao e um compromisso contratual
> ou voltado ao cliente).

| Area | Estimativa | Senioridade |
|---|---|---|
| Backend: nucleo de reservas | 12 dias | Pleno (revisao Senior) |
| Backend: anti-double-booking + recorrencia | 8 dias | Senior |
| Integracao / OAuth: Calendar + login social | 10 dias | Senior |
| Frontend: UI responsiva | 12 dias | Pleno |
| QA: incluindo harness de concorrencia | 8 dias | QA |
| LGPD basica + migracao/descontinuacao | 4 dias | Pleno |
| **Total (desenvolvimento)** | **aproximadamente 54 dias-pessoa** | (mais spike DISC-001 de 2 a 4 dias, fora do total) |

**Infra / Terceiros / Opex recorrente:** infra modesta (1 app host + 1 banco gerenciado + 1 worker; sem multi-regiao/Kubernetes); terceiros de baixo custo (Calendar API na quota gratuita: confirmar no spike; login social Google gratuito; sem licencas); opex recorrente baixo. O TCO cria fundacao reutilizavel (Outlook Fase 2, SSO Fase 3, analytics Fase 2). Estimativa firme substitui a preliminar do RP paragrafo 13 (deferida).

**Proveniencia**
- **Confianca:** 72
- **Origem:** cto_authored (confirmado pelo CTO no sign-off; antes inherited)
- **Fonte:** TA paragrafo effort-cost (cto_authored)
- **Situacao:** respondida
- **Disposicao:** inherited (decided; linha OAuth a re-firmar pos-DISC-001)
- **Observacao:** uso interno; nao e compromisso contratual; o PM trata a linha de integracao como sujeita a ajuste pos-spike.

---

## Prontidao Herdada e Disposicoes em Aberto
<!-- origination: id=inherited-readiness; blocks=true; min-confidence=70; kind=derived; inputs=a-scope,b-feasibility -->
> Rubrica: o que o PM precisa ver antes de planejar (as premissas ainda a validar, as
> incognitas de Discovery resolvidas ou em aberto, e as respostas delegadas com responsavel)
> que sobreviveram do upstream. Se uma premissa se mostrar falsa durante a execucao, a demanda
> e re-triada (gatilho de re-triagem no downstream). Derivado (carregado das disposicoes
> do RP/TA).

| Campo | Valor |
|---|---|
| **Premissas ainda a validar** | Lado-produto: nenhuma OPEN (RP resolvidas em D003+D005). Pontos de atencao ativos para o PM/implementacao: (1) EC-06 premissa de mono-fuso (ADR-005); (2) antecedencia maxima exata (aproximadamente 90 dias, RN-09..12) a parametrizar; (3) ALT-1 sugestao de alternativas (UX) a definir; (4) US-05 confirmacao anti-cancelamento acidental (modelo flat) a definir; (5) Persona 4 (secretaria) conf 76 (entrevista recomendada antes do gate). |
| **Incognitas de Discovery** | RP Discovery RESOLVIDO (D003+D005, 2026-06-06). TA Discovery **DISC-001 EM ABERTO**: ambiente Google Workspace/OAuth nao documentado (escopos concediveis, grant a apps de terceiros, modelo de credencial [ADR-006], quotas Calendar API). Gating: NFR-02/06/08 + ADR-006 + re-firmacao da estimativa de integracao. |
| **Requisitos delegados (com responsavel)** | (1) Avaliacao Tecnica: antes delegada pelo RP, agora ASSINADA (TA-2026-001, Viavel com ressalvas); delegacao encerrada. (2) Spike DISC-001: owner CTO/Tech Lead + TI da organizacao; de 2 a 4 dias; cobre R1. (3) Revisao LGPD (NFR-07/R4): owner Juridico/DPO; bloqueante antes do release. |

**Gatilho de re-triagem (downstream):** se uma premissa carregada se provar falsa na execucao (por exemplo: mono-fuso EC-06, ou grant OAuth do Workspace negado R1/DISC-001), a demanda e re-triada, nao corrigida em silencio.

**Proveniencia**
- **Confianca:** 80
- **Origem:** po_authored (composicao do PO; antes synthesized)
- **Fonte:** RP dispositions (D003+D005) + TA discovery-path (R1/R4, current-state, ADR-006) + DISC-001
- **Situacao:** respondida
- **Disposicao:** discovery (DISC-001 em aberto)
- **Observacao:** DISC-001 gate NFR-02/06/08 + ADR-006 + linha de integracao; product-side sem premissas OPEN; 5 pontos de atencao ativos.

---

## Criterios de Sucesso e Metricas (projetadas)
<!-- origination: id=success-metrics; blocks=true; min-confidence=75; kind=capture -->
> Rubrica: o baseline projetado (metricas primarias e guardrails; um guardrail e uma
> metrica que NAO deve piorar) herdado do RP, com meta, janela e confianca. E contra isso
> que `metrics.md` (projetado vs. realizado) compara pos-rollout.

| Tipo | Metrica | Baseline | Meta pos-rollout | Janela | Confianca |
|---|---|---|---|---|---|
| Primaria (lagging) | Double-bookings/semana | Aproximadamente 1,8/semana (9 em 5 semanas) | 0 | 4 semanas pos go-live | Alta |
| Primaria (lagging) | Novos adiamentos de negocios por conflito | 9 em 5 semanas | 0 | 8 semanas pos go-live | Media (depende de D02) |
| Leading | Adocao (% reservas no sistema) | 0% | 100% | 2 semanas pos go-live | Alta |
| Guardrail | Volume total de reservas/semana | a medir pre-go-live | nao cair vs baseline | Semana 1 | Media |
| Guardrail | Carga de remarcacao da secretaria | a medir pre-go-live | nao aumentar vs baseline | 4 semanas | Media |

Nota financeira (referencia, nao metrica do sistema): pipeline de aproximadamente R$700k; R$111k perdidos; R$90k em risco (monitorar com D02).

**Proveniencia**
- **Confianca:** 80
- **Origem:** po_authored (confirmado pelo PO no sign-off; antes inherited)
- **Fonte:** RP paragrafo 10
- **Situacao:** herdada
- **Disposicao:** inherited
- **Observacao:** guardrails dependem de medicao na semana pre-go-live (planejar coleta).

---

## Handoff ao PM - Gate de Aceite
<!-- origination: id=handoff-gate; blocks=true; min-confidence=80; kind=derived; inputs=sign-off,scope-reconciliation,consolidated-risk,inherited-readiness -->
> Rubrica: o checklist de entrega que o PM aceita (ou rejeita). O PM tem **autoridade
> explicita para rejeitar** o PRD e devolver com lacunas **especificas** (nao um generico
> "precisa de mais detalhes"); a rejeicao e o motivo entram no Historico de Revisoes, e o
> PO (ou CTO, dependendo da lacuna) endereça apenas as lacunas e incrementa a versao.
> Cada caixa deve ser verificavel a partir do documento fundido. Derivado (assegura que a
> fusao esta completa; nao inventa nada).

| Checklist de entrega | OK? |
|---|---|
| RP congelado (`freezeReady`) e referenciado | ✓ |
| Avaliacao Tecnica assinada (ou N/A justificado) | ✓ |
| Reconciliacao de escopo registrada | ✓ |
| Riscos e dependencias consolidados | ✓ |
| Dependencias externas explicitas | ✓ |
| Disposicoes em aberto visiveis | ✓ |

**Prioridade e contexto de negocio (por que esta demanda, agora):** Conflito de agendamento (double-booking) cronico, com ritmo de aproximadamente 1,8 conflitos por semana (9 em 5 semanas) e impacto comercial quantificado: R$111k ja perdidos, R$90k em risco, pipeline de aproximadamente R$700k acompanhado com a lideranca comercial (D02). O custo de esperar cresce a cada semana: cada conflito erode a credibilidade em reunioes com clientes e adia negocios. A integracao teve seus riscos mitigados e foi considerada viavel ("Viavel com ressalvas", TA-2026-001); o unico gatilho possivel de revisao de escopo e a negacao do grant OAuth pelo admin do Workspace (R1 / DISC-001). Escala modesta (aproximadamente 200 usuarios, janela das 08h as 19h, organizacao unica); a restricao critica e corretude sob concorrencia (NFR-01), nao volume. Migracao e descontinuacao do processo manual em ate 2 semanas pos go-live.

> Nota de autoridade: o PM tem autoridade explicita para rejeitar o PRD e devolver com lacunas especificas (nao um generico "precisa de mais detalhes"). A rejeicao e o motivo entram no Historico de Revisoes; o PO endereça lacunas de produto, o CTO as tecnicas (reabrindo apenas a metade afetada), e a versao e incrementada.

**Proveniencia**
- **Confianca:** 80
- **Origem:** po_authored (composicao do PO; antes synthesized)
- **Fonte:** sign-off + scope-reconciliation + consolidated-risk + inherited-readiness (+ meta, b-feasibility)
- **Situacao:** respondida
- **Disposicao:** synthesized
- **Observacao:** as 6 caixas sao verificaveis a partir das secoes correspondentes do documento fundido; dual sign-off comitado (PO + CTO): todas as caixas confirmadas.

<!-- END OF DOCUMENT -->
