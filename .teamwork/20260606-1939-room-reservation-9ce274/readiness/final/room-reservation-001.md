# Readiness Package: Sistema de Reserva de Salas de Reuniao

> O Readiness Package (RP) e a **definicao de pronto de produto**: o output do PO.
> Ele e auto-suficiente: visao, problema, escopo, regras, jornadas de usuario, historias, NFRs,
> edge cases, criterios e metricas. O RP **nao** contem secoes de autoria do CTO; a
> avaliacao tecnica vive no Technical Assessment (referenciado abaixo). O RP herda
> a camada de confianca do Origination vinculado; o que entrou como premissa ou incognita
> e resolvido ou carregado explicitamente na secao "Prontidao herdada".

## Metadados

| Campo | Valor |
|---|---|
| **ID do Pacote** | RP-2026-001 |
| **Versao** | v1 |
| **Origination vinculado** | INT-2026-001 |
| **Responsavel** | PO (Ato 2) |
| **Natureza da demanda** | HIBRIDO: processo informal existente (mural fisico + Google Forms via WhatsApp, mantido pela secretaria) + software-core novo + integracao com Google Calendar |
| **Base de conhecimento** | `tech-landscape-room-reservation.md` · A criar (nao existe) |
| **Escalada ao CTO** | SIM: LEVE (Technical Assessment OAuth Google Calendar, adiada) |
| **Status** | Rascunho |
| **Data de congelamento (freeze)** | (pendente) |
| **Idioma de saida** | pt-BR |

## Historico de Revisao

| Versao | Data | Autor | Status | Resumo |
|---|---|---|---|---|
| v1 | 2026-06-07 | Doc Updater (Stage Inheritor) | Rascunho | Criacao do RP a partir do template; secoes herdadas preenchidas (I001-I011); secoes de produto deixadas como placeholders para Fase B2. |
| v2 | 2026-06-07 | Doc Updater (Fase B2) | Rascunho | Cinco secoes de produto preenchidas com rascunho IA do Section Drafter: regras de negocio (Secao 6), jornada do usuario (Secao 6.5), user stories (Secao 7), NFRs (Secao 8), edge cases (Secao 9). Todas abaixo do limiar de confianca; loop de confirmacao do PO pendente. |
| v3 | 2026-06-07 | Doc Updater (Escalation Flagger) | Rascunho | Secao tech-assessment-ref refinada com disposicao autoritativa do Escalation Flagger: gatilhos presentes e ausentes detalhados, escopo do TA LEVE (4 pontos), contexto Hibrido, nota operacional de freeze provisorio. Status=requisitado · Disposicao=adiada · Freeze=PROVISORIO. |
| v4 | 2026-06-07 | Doc Updater (Act 2: confirm loop) | Rascunho | 5 secoes de produto promovidas de rascunho IA para po_authored com confirmacoes C-Q01..C-Q08 do PO: regras de negocio (conf 88), jornada do usuario (conf 80), user stories (conf 88), NFRs (conf 82), edge cases (conf 80). Conflitos C4 (sync uma via), C1 (rotulo readiness 74%) e C2 (premissas product) corrigidos. Estimativa de esforco mantida como adiada honesta (nao-bloqueante). |

---

## Prontidao herdada e disposicoes em aberto

| Campo | Valor |
|---|---|
| **Readiness Score no handoff do origination (nao e o score atual do RP)** | ~74%: score de passagem de fase calculado pelo Stage Inheritor; o score canonico atual vira da proxima rodada do Confidence Auditor |
| **Premissas ainda a validar** | NENHUMA: todas as 3 premissas do origination resolvidas em D003 + D005: (1) impacto quantificado operacional e em R$ [D003/Q008 + D005/Q012]; (2) "negocios adiados" confirmado com valor firme [D005/Q012]; (3) natureza greenfield rejeitada, demanda Hibrida confirmada [D003/Q011]. |
| **Incognitas de Discovery** | RESOLVIDAS: Discovery totalmente encerrado (D003 + D005, 2026-06-06): impacto operacional quantificado, viabilidade de integracao de-arriscada (somente Google Calendar), processo informal caracterizado, valor R$ dos negocios adiados firmado. |
| **Premissas de Discovery/origination** | NENHUMA aberta (resolvidas em D003+D005); as decisoes de produto do RP foram confirmadas pelo PO no confirm loop (C-Q01..C-Q08). |
| **Requisitos delegados (com dono)** | Technical Assessment LEVE (OAuth Google Calendar): dono CTO/Tech Lead; adiado, nao-bloqueante para Fase B2. |

---

## Secao 1: Resumo executivo

A empresa tem um problema cronico de **conflito de agendamento** (double-booking) em suas salas de reuniao. Toda semana, sem parar, dois grupos chegam a mesma sala no mesmo horario e "vira confusao": nenhum mecanismo impede o duplo agendamento, e o processo atual de reserva, que mistura anotacao manual no mural fisico e um Google Forms enviado por WhatsApp gerenciado pela secretaria, nao consegue garantir exclusividade de horario nem alertar sobre conflitos em tempo real.

O impacto foi quantificado em campo: cerca de 9 conflitos em 5 semanas (media de 1,8 por semana), com atraso medio de ~3 dias por conflito para reencontrar agenda comum. Desses conflitos, 9 reunioes de negocio foram adiadas, envolvendo um pipeline total de aproximadamente **R$ 700 mil** em prospeccao de novos negocios. Do total afetado, **R$ 111 mil ja foram perdidos** (dois negocios que nao fecham mais) e **R$ 90 mil estao em risco** (um negocio ainda em aberto, travado pelo conflito). A dor atinge quatro perfis: equipes internas que disputam o espaco, reunioes com clientes e externos (risco de imagem), lideranca e diretoria, e a propria secretaria/facilities, que absorve o retrabalho de remarcar.

Sera construido um **sistema digital de reserva de salas** integrado ao Google Calendar, de natureza Hibrida: migra o processo manual atual (mural + Forms + WhatsApp) para um fluxo digital com regras automaticas de anti-conflito. A secretaria e o stakeholder-chave da migracao; o sistema precisa ser mais simples de usar do que o Google Forms atual para vencer a inercia de adocao. A integracao com o Google Calendar e **uma via (sistema -> Calendar; o sistema e a fonte de verdade)**: reservas criadas ou canceladas no sistema refletem automaticamente no Calendar em ate 2 minutos; alteracoes feitas diretamente no Google Calendar nao retroalimentam o sistema neste release. A autenticacao sera simples (login social); SSO corporativo e integracao com Outlook estao fora do escopo deste release.

O resultado esperado e a **eliminacao dos conflitos de agendamento** e a **protecao do pipeline comercial**: zero novos double-bookings apos o rollout, 100% das reservas centralizadas no sistema (mural e Forms descontinuados) e, no horizonte de 8 semanas, zero novos adiamentos de negocios causados por conflito de sala. O criterio executivo de sucesso e direto: nenhum novo double-booking ocorre apos o go-live.

---

## Secao 2: Contexto e problema (a dor, nao a solucao)

### Cenario atual

O processo de reserva de salas de reuniao e inteiramente manual e informal. A **fonte de verdade** e um **mural fisico** onde as reservas sao anotadas em papel. Para solicitar uma reserva, os usuarios preenchem um **Google Forms** cujo link circula via **WhatsApp**, ou simplesmente anotam diretamente no papel. A **secretaria** atua como arbitro e gestora desse processo: ela valida os conflitos, remarca reunioes e mantem a coerencia do mural. Nao ha sistema digital, regra automatica, notificacao em tempo real ou integracao com a agenda digital dos participantes. O processo existe, funciona de forma informal, e tem a secretaria como elo central.

### Limitacoes

O processo manual tem quatro limitacoes estruturais que o tornam incapaz de prevenir conflitos:

1. **Nao previne double-booking automaticamente.** Duas reservas para o mesmo horario e sala podem ser feitas sem qualquer alerta; o conflito so e descoberto quando os grupos aparecem fisicamente na sala.
2. **Depende de uma pessoa-chave.** A secretaria e o unico ponto de controle; na ausencia dela, o processo fica sem arbitro e os conflitos nao tem resolucao definida.
3. **Nao e auditavel nem rastreaval.** Nao ha registro historico consultavel de reservas, cancelamentos ou conflitos. Cada ocorrencia comeca do zero.
4. **Nao integra com a agenda digital.** As reservas no mural nao aparecem automaticamente no Google Calendar dos participantes, criando desconexao entre o espaco fisico e a agenda pessoal.

### Dor do cliente

O conflito de agendamento (double-booking) acontece **toda semana, sem parar**: dor cronica e recorrente, nao excecao isolada. Quando dois grupos chegam a mesma sala no mesmo horario, "vira confusao"; nao ha protocolo claro de resolucao e a situacao se repete. Quatro perfis sao diretamente afetados:

- **Equipes internas que disputam a sala:** transtorno imediato para quem encontrou o espaco ja ocupado; a reuniao atrasa ou nao acontece no horario.
- **Reunioes com clientes e externos:** constrangimento institucional quando visitantes estao presentes; risco de imagem e de relacionamento comercial.
- **Lideranca e diretoria:** suas proprias reunioes estao sujeitas ao mesmo conflito, sem tratamento preferencial pelo processo atual.
- **Secretaria/facilities:** absorve o retrabalho de remarcar, negociar e resolver cada ocorrencia; e o unico ponto de controle do processo e stakeholder-chave de qualquer migracao.

### Impacto de negocio

O impacto foi **totalmente quantificado** em campo (Discovery D003 + D005, 2026-06-06):

- **Frequencia:** ~9 conflitos em 5 semanas, equivalente a **1,8 conflitos por semana**, concentrados em dias uteis, pico entre 10h e 16h.
- **Atraso por conflito:** atraso medio de **~3 dias** para reencontrar agenda comum apos um conflito.
- **Negocios afetados:** 9 reunioes de negocios adiadas, envolvendo um **pipeline total de ~R$ 700 mil** em prospeccao de novos negocios (receita nova, nao recorrente).
- **Perdas confirmadas:** **R$ 111 mil ja perdidos**, dois negocios que nao fecham mais por conta dos adiamentos encadeados.
- **Valor em risco:** **R$ 90 mil em risco**, um negocio ainda em aberto e travado.

O eixo de maior gravidade e o de negocios adiados: o custo de imagem e de relacionamento com clientes externos esta subsumido neste eixo (confirmado em D003/Q010). O impacto operacional (tempo perdido, retrabalho da secretaria) e real, mas secundario frente a exposicao de receita.

---

## Secao 3: Objetivos e resultado esperado

1. **Eliminar o conflito de agendamento (double-booking):** zero novos double-bookings registrados nas 4 semanas seguintes ao rollout. Verificavel por monitoramento de conflitos no proprio sistema e por ausencia de relatos presenciais da secretaria e dos usuarios.

2. **Interromper novos adiamentos comerciais causados por conflito de sala:** zero novos adiamentos de negocios atribuiveis a conflito de sala nas 8 semanas seguintes ao rollout. Verificavel por acompanhamento com a lideranca comercial (D02).

3. **Migrar 100% das reservas para o sistema digital:** mural fisico e Google Forms descontinuados em ate 2 semanas apos o go-live; todas as reservas criadas, consultadas e canceladas exclusivamente pelo novo sistema. Verificavel por observacao direta e confirmacao da secretaria.

4. **Integrar com o Google Calendar em tempo real:** toda reserva criada ou cancelada no sistema deve refletir automaticamente no Google Calendar dos participantes em ate 2 minutos. Verificavel por teste funcional de integracao.

---

## Secao 4: Personas impactadas / jobs-to-be-done

### Persona 1: equipes internas que disputam a sala

**Job-to-be-done:** reservar uma sala de reuniao com antecedencia e ter a certeza de que ela estara disponivel no horario marcado, sem surpresas.

**Impacto hoje:** chegam a sala e encontram outro grupo ja ocupando o espaco; a reuniao atrasa ou nao acontece. Nao ha visibilidade previa de disponibilidade; a reserva no mural nao garante exclusividade.

**Impacto pos-entrega:** conseguem verificar disponibilidade em tempo real, criar a reserva pelo sistema e receber confirmacao; conflito de agendamento deixa de existir como risco operacional.

---

### Persona 2: reunioes com clientes e externos

**Job-to-be-done:** conduzir reunioes com visitantes externos de forma profissional, em um ambiente preparado e reservado, sem imprevistos.

**Impacto hoje:** um conflito de agendamento em reuniao com clientes gera constrangimento institucional e risco de imagem; o processo atual nao tem protecao especial para reunioes com externos.

**Impacto pos-entrega:** a reserva confirmada pelo sistema elimina o risco de double-booking e protege a credibilidade da empresa perante clientes e parceiros.

---

### Persona 3: lideranca e diretoria

**Job-to-be-done:** garantir que reunioes estrategicas e de alta prioridade acontecam no horario planejado, sem interrupcoes causadas por conflito de espaco.

**Impacto hoje:** as reunioes da lideranca nao tem tratamento diferenciado no processo atual; estao sujeitas ao mesmo double-booking que qualquer outro grupo.

**Impacto pos-entrega:** visibilidade de ocupacao em tempo real; possibilidade de reservar com antecedencia e com confirmacao; reunioes estrategicas protegidas por regra automatica de anti-conflito.

---

### Persona 4: secretaria / facilities (stakeholder-chave de migracao)

**Job-to-be-done:** manter o processo de reservas funcionando de forma ordenada, resolver conflitos quando ocorrem e garantir que a sala certa esteja disponivel para cada reuniao.

**Impacto hoje:** e o unico ponto de controle do processo; absorve todo o retrabalho de remarcar e negociar a cada conflito; o processo depende de sua presenca e disponibilidade.

**Impacto pos-entrega:** o sistema assume a funcao de arbitro de conflitos automaticamente; a secretaria deixa de ser o gargalo operacional do processo. E o stakeholder-chave da migracao: sua adesao e validacao de usabilidade sao necessarias para o sucesso do rollout. O sistema deve ser mais simples de operar do que o Google Forms atual.

---

## Secao 5: Escopo incluido e excluido

### Incluido

- **CRUD de reservas:** criar, consultar, editar e cancelar reservas de salas de reuniao.
- **Integracao com o Google Calendar (uma via: sistema -> Calendar; o sistema e a fonte de verdade):** toda reserva criada ou cancelada no sistema reflete automaticamente no Google Calendar dos participantes em ate 2 min; alteracoes feitas diretamente no Google Calendar nao retroalimentam o sistema neste release.
- **Autenticacao simples (login social):** acesso ao sistema via autenticacao simplificada; sem SSO corporativo.
- **Regras automaticas de anti-double-booking:** o sistema impede a criacao de reservas conflitantes (mesma sala, mesmo horario) automaticamente, sem intervencao humana.
- **Reservas recorrentes (series):** o sistema suporta criacao de series recorrentes; a validacao de conflito ocorre ocorrencia a ocorrencia; ocorrencias em conflito sao sinalizadas (a serie nao e rejeitada integralmente).
- **Migracao do processo manual:** substituicao e descontinuacao do mural fisico e do Google Forms como instrumentos de reserva; o novo sistema e o unico canal de reservas apos o rollout.

### Excluido

- **Integracao com Outlook / Microsoft 365:** fora do escopo deste release (Outlook descartado em D003/Q010); pode entrar em fase futura.
- **SSO corporativo:** autenticacao simples/login social e suficiente; SSO e escopo futuro.
- **Outros recursos fisicos:** o sistema reserva exclusivamente salas de reuniao; outros recursos (estacionamento, equipamentos, etc.) estao fora do escopo.
- **Analytics avancado e relatorios de uso:** sem dashboards de utilizacao ou relatorios historicos neste release.
- **Portal externo para visitantes:** agendamento por clientes ou externos diretamente no sistema esta fora do escopo.

### Adiado (fases futuras)

- **Integracao com Outlook:** fase futura, apos estabilizacao com Google Calendar.
- **Analytics e relatorios de ocupacao:** dashboards de uso de salas, historico de conflitos, metricas operacionais; Fase 2.
- **Lembretes automaticos:** notificacoes de lembrete antes da reserva; Fase 2.
- **SSO corporativo:** autenticacao empresarial; Fase 3.

---

## Secao 6: Regras de negocio e fluxos

### Bloco 1: exclusividade e anti-double-booking

- **RN-01:** Uma sala em um determinado intervalo de tempo pode ter no maximo uma reserva ativa; sobreposicao de reservas e proibida.
- **RN-02:** A validacao de conflito ocorre no momento da **confirmacao** da reserva; tentativas de confirmar uma reserva que sobreponha outra ativa sao recusadas pelo sistema.
- **RN-03:** O sistema considera **sobreposicao parcial**, nao apenas horarios identicos, para fins de conflito; qualquer intersecao de intervalos configura conflito. (Decisao firmada: C-Q01.)
- **RN-04:** O **sistema e a fonte de verdade** de disponibilidade; mural fisico e Google Forms sao descontinuados apos o go-live e nao geram reservas validas.
- **RN-05:** Sob criacao concorrente (dois usuarios confirmando a mesma sala no mesmo instante), o sistema adota a politica **first-commit-wins**: a primeira confirmacao persiste; a segunda recebe conflito.

### Bloco 2: permissoes (modelo flat)

- **RN-06:** Qualquer usuario autenticado via login social pode criar, consultar, editar e cancelar **qualquer** reserva no sistema, inclusive reservas criadas por outros usuarios. Nao existe perfil admin especial. (Decisao firmada: C-Q04.)
- **RN-07:** ~~[premissa]~~ **Removido**: distincao de perfil secretaria/admin eliminada. A secretaria opera como qualquer usuario autenticado; cria reservas em nome de terceiros usando os campos "responsavel" e "participantes" disponiveis a todos. (C-Q04.)
- **RN-08:** ~~[premissa]~~ **Removido**: sem perfil admin diferenciado neste release. (C-Q04.)

### Bloco 3: parametros temporais (firmados)

- **RN-09:** O sistema aceita reservas dentro da janela de **08h as 19h em dias uteis**. (Firmado: C-Q05; validacao obrigatoria no sistema.)
- **RN-10:** A duracao minima de uma reserva e de **15 minutos**; a duracao maxima e de **8 horas**. (Firmado: C-Q05.)
- **RN-11:** Reservas devem ser criadas para datas **futuras**; a antecedencia maxima permitida e de aproximadamente **90 dias** corridos. (Firmado: C-Q05. Valor exato a parametrizar antes da implementacao.)
- **RN-12:** Edicao e cancelamento de uma reserva sao permitidos ate o **momento de inicio** da reserva; edicao revalida o conflito contra as demais reservas ativas.

### Bloco 4: precedencia e desempate (FCFS firmado)

- **RN-13:** A politica de precedencia e **FCFS (first-come, first-served)**: a primeira confirmacao vence, independentemente de hierarquia ou perfil. Lideranca e diretoria **nao** sobrescrevem automaticamente reservas ja confirmadas. Caso desejem a sala, podem **solicitar realocacao** via secretaria ou sistema: fluxo facilitado, mas nao automatico nem garantido. (Decisao firmada pelo PO: C-Q01.)

### Bloco 5: reservas recorrentes (MVP)

- **RN-14:** O sistema suporta criacao de **series recorrentes** de reservas. (Decisao firmada: C-Q03.)
- **RN-15:** A validacao de conflito de uma serie recorrente ocorre **ocorrencia a ocorrencia**; ocorrencias em conflito sao **sinalizadas** ao usuario; o sistema nao rejeita a serie inteira por causa de uma ocorrencia em conflito.
- **RN-16:** O usuario decide individualmente o que fazer com as ocorrencias sinalizadas como conflitantes (aceitar as sem conflito, remover as em conflito, ou cancelar a serie).

### Fluxo de transicao de estado da reserva

```
Rascunho -> Confirmada -> Cancelada
                      \-> Concluida
```

- **Rascunho -> Confirmada:** o sistema executa a validacao anti-conflito; se nao houver intersecao com reserva ativa na mesma sala, confirma e dispara a sincronizacao com o Google Calendar.
- **Confirmada -> Cancelada:** libera o slot; remove o evento no Google Calendar; notifica participantes. A liberacao do slot ocorre imediatamente no sistema (fonte de verdade), independentemente do status da sincronizacao.
- **Confirmada -> Concluida:** transicao automatica apos o termino do intervalo reservado.
- **Falha de sincronizacao:** a reserva permanece **Confirmada** como fonte de verdade; o sistema sinaliza sincronizacao pendente e realiza retry com backoff.

### Fluxo de conflito

1. Usuario seleciona sala e intervalo.
2. Sistema consulta reservas ativas para a sala no intervalo solicitado.
3. Se houver intersecao: bloqueia a confirmacao e informa o conflito (e, se aplicavel, sugere alternativas).
4. Se nao houver intersecao: confirma a reserva (sob concorrencia, a checagem e a gravacao sao atomicas).

### Sincronizacao com o Google Calendar (uma via, firmada)

- Toda transicao **Confirmada** ou **Cancelada** propaga para o Google Calendar em ate **<=2 minutos**. (Firmado: C-Q08.)
- O sistema e a **fonte de verdade**; o Google Calendar e espelho de leitura.
- Alteracoes feitas diretamente no Google Calendar **nao refletem** de volta no sistema neste release: sincronizacao e **uma via** (sistema -> Calendar). (Decisao firmada pelo PO: C-Q02. Remove premissa anterior.)

---

## Secao 6.5: Jornadas do usuario (ponta a ponta)

### Jornada A: colaborador (caminho principal)

| # | Gatilho / Acao do usuario | Resultado esperado | Touchpoint / Tela | Pre-condicao |
|---|---|---|---|---|
| A1 | Usuario acessa o sistema e realiza login social | Usuario autenticado; acesso ao sistema liberado | Tela de login | Conta Google/social valida |
| A2 | Consulta disponibilidade de salas em tempo real | Sistema exibe salas disponiveis no intervalo selecionado | Tela de disponibilidade | Usuario autenticado |
| A3 | Escolhe sala e horario; preenche dados da reserva (titulo, participantes etc.) | Formulario de reserva preenchido; dados validados | Formulario de reserva | Sala e intervalo selecionados |
| A4 | Confirma a reserva | Sistema executa validacao anti-conflito; reserva criada e confirmada | Tela de confirmacao | Sem sobreposicao com reservas ativas |
| A5 | (acao do sistema) | Sincronizacao automatica com o Google Calendar em <=2 minutos | Bastidores: API Google Calendar | Reserva confirmada; credenciais OAuth validas |
| A6 | (acao do sistema) | Participantes recebem convite do Google Calendar | E-mail / Google Calendar | Sincronizacao A5 concluida |

### Jornada B: secretaria reservando em nome de terceiro (modelo flat)

| # | Gatilho / Acao | Resultado esperado | Touchpoint / Tela | Pre-condicao |
|---|---|---|---|---|
| B1 | Secretaria recebe pedido de reserva (presencial ou via WhatsApp) e acessa o sistema | Secretaria autenticada como usuario comum (sem perfil admin especial) | Tela de login | Conta Google/social valida |
| B2 | Cria reserva preenchendo o campo "responsavel" com o nome do solicitante e adicionando os participantes | Reserva registrada com o solicitante como responsavel; secretaria como criadora operacional | Formulario de reserva: campos "responsavel" e "participantes" disponiveis a qualquer usuario | Usuario autenticado |
| B3 | Confirma a reserva | Sistema valida anti-conflito; confirma; dispara sync com Google Calendar; solicitante recebe convite | Tela de confirmacao | Sem conflito no intervalo |

Esta jornada **substitui o papel de arbitro manual** que a secretaria exerce hoje no mural e no Forms. Nao exige perfil diferenciado; qualquer usuario autenticado pode criar reservas em nome de terceiros. (C-Q04.)

### Jornada C: reserva recorrente (serie)

| # | Gatilho / Acao do usuario | Resultado esperado | Touchpoint / Tela | Pre-condicao |
|---|---|---|---|---|
| C1 | Usuario autenticado seleciona "reserva recorrente" | Sistema apresenta opcoes de recorrencia (diaria, semanal, etc.) e periodo da serie | Formulario de reserva: secao recorrencia | Usuario autenticado |
| C2 | Preenche dados da serie (sala, horario, frequencia, data de fim) e confirma | Sistema valida cada ocorrencia individualmente | Formulario de reserva | Sala e intervalo selecionados |
| C3 | Sistema apresenta resultado da validacao | Ocorrencias sem conflito: confirmadas. Ocorrencias em conflito: sinalizadas. Serie nao e rejeitada integralmente | Tela de resultado da serie | Validacao concluida |
| C4 | Usuario decide individualmente sobre as ocorrencias sinalizadas | Ocorrencias confirmadas seguem para sync no Google Calendar; ocorrencias rejeitadas ficam pendentes ou sao removidas pelo usuario | Tela de gestao da serie | Resultado C3 apresentado |

### Caminhos alternativos e de saida

- **ALT-1: sala indisponivel / conflito na confirmacao:** sistema bloqueia a confirmacao e informa o conflito; [premissa] sugere alternativas de sala ou horario disponiveis.
- **ALT-2: cancelamento:** usuario cancela reserva confirmada; o sistema libera o slot imediatamente, remove o evento no Google Calendar e notifica participantes.
- **ALT-3: edicao de reserva:** usuario edita dados ou horario; o sistema revalida conflito e, se aprovado, re-sincroniza com o Calendar.
- **ALT-4: falha de sincronizacao com o Google Calendar:** a reserva permanece confirmada no sistema (fonte de verdade: sync uma via confirmada, C-Q02); sistema sinaliza "sincronizacao pendente" e realiza retry com backoff. Alteracoes feitas diretamente no Google Calendar nao retroalimentam o sistema (ver Secao 9, EC-02 e EC-04).
- **ALT-5: habito antigo (mural / Forms):** canal descontinuado apos ate 2 semanas do go-live; reservas no canal antigo nao sao reconhecidas como validas pelo sistema.

### Blueprint de servico parcial

| Camada | Elementos |
|---|---|
| **Frente (visivel ao usuario)** | Tela de disponibilidade em tempo real; formulario de criacao/edicao; confirmacao de reserva; convite enviado ao Google Calendar dos participantes |
| **Bastidores (sistema)** | Calculo de disponibilidade; validacao anti-double-booking (atomica); chamada a API Google Calendar via OAuth; retry em caso de falha de sync |
| **Suporte / Pessoas** | Secretaria: deixa de manter o mural fisico e passa a usar o sistema para reservas em nome de terceiros; Technical Assessment OAuth Google Calendar: adiado (nao-bloqueante para Fase B2) |

---

## Secao 7: User stories + criterios de aceite

> Nota: estas historias derivam 1:1 dos passos da Jornada (Secao 6.5).

---

### US-01: autenticacao via login social

**Como** qualquer colaborador da empresa,
**quero** acessar o sistema de reservas usando minha conta Google (login social),
**para** nao precisar criar e memorizar uma nova senha.

**Criterios de aceite:**

- **Dado** que sou um colaborador com conta Google valida,
  **quando** acesso o sistema e escolho "Entrar com Google",
  **entao** sou autenticado e redirecionado para a tela principal do sistema sem etapas adicionais de cadastro.

- **Dado** que nao possuo conta Google ou o login social falha,
  **quando** tento acessar o sistema,
  **entao** recebo mensagem de erro clara e nao acesso o sistema.

---

### US-02: bloqueio de conflito (anti-double-booking) [CENTRAL]

**Como** qualquer usuario autenticado,
**quero** que o sistema impeca automaticamente a criacao de reservas sobrepostas para a mesma sala,
**para** ter a garantia de que a sala estara disponivel no horario reservado.

**Criterios de aceite:**

- **Dado** que a Sala A esta confirmada das 14h as 15h,
  **quando** tento confirmar uma nova reserva para a Sala A das 14h30 as 15h30 (sobreposicao parcial),
  **entao** o sistema bloqueia a confirmacao, exibe mensagem de conflito e nao cria a reserva.

- **Dado** que a Sala A esta confirmada das 14h as 15h,
  **quando** confirmo uma reserva para a Sala A das 15h as 16h (adjacente, sem sobreposicao),
  **entao** o sistema aceita e confirma a reserva normalmente.

- **Dado** que dois usuarios tentam confirmar a mesma sala no mesmo instante (concorrencia),
  **quando** as duas confirmacoes chegam simultaneamente,
  **entao** a primeira e confirmada e a segunda recebe mensagem de conflito (first-commit-wins).

---

### US-03: consultar disponibilidade de salas

**Como** qualquer usuario autenticado,
**quero** consultar a disponibilidade de salas em tempo real,
**para** escolher sala e horario antes de criar uma reserva.

**Criterios de aceite:**

- **Dado** que estou autenticado,
  **quando** seleciono uma data e um intervalo de horario,
  **entao** o sistema exibe quais salas estao disponiveis e quais estao ocupadas naquele intervalo.

- **Dado** que uma reserva e confirmada por outro usuario,
  **quando** consulto a disponibilidade em seguida,
  **entao** a sala recem-reservada aparece como indisponivel no intervalo correspondente.

---

### US-04: criar reserva

**Como** qualquer usuario autenticado,
**quero** criar uma reserva de sala informando os dados necessarios (sala, data, horario de inicio e fim, titulo e participantes),
**para** garantir o uso exclusivo da sala no periodo escolhido.

**Criterios de aceite:**

- **Dado** que estou autenticado e a sala esta disponivel no intervalo,
  **quando** preencho todos os campos obrigatorios e confirmo,
  **entao** a reserva e criada com status "Confirmada" e aparece imediatamente na consulta de disponibilidade.

- **Dado** que nao preencho um campo obrigatorio,
  **quando** tento confirmar,
  **entao** o sistema exibe erro de validacao e nao cria a reserva.

---

### US-05: editar ou cancelar reserva (modelo flat)

**Como** qualquer usuario autenticado,
**quero** editar ou cancelar qualquer reserva existente antes do seu inicio,
**para** liberar ou ajustar o slot sem depender de perfil especial ou intervencao de terceiros.

**Criterios de aceite:**

- **Dado** que sou um usuario autenticado e ha uma reserva confirmada que ainda nao iniciou,
  **quando** edito o horario e confirmo a edicao,
  **entao** o sistema revalida o conflito; se nao houver sobreposicao, a reserva e atualizada e re-sincronizada com o Google Calendar.

- **Dado** que edito o horario e ha conflito com outra reserva ativa,
  **quando** confirmo a edicao,
  **entao** o sistema rejeita a edicao, mantem os dados originais e informa o conflito.

- **Dado** que sou um usuario autenticado e ha uma reserva confirmada,
  **quando** cancelo a reserva,
  **entao** o slot e liberado imediatamente, o evento e removido do Google Calendar e os participantes sao notificados.

> **Nota de produto (C-Q04):** o modelo flat de permissoes aumenta o risco de cancelamentos acidentais. Considerar confirmacao explicita antes de cancelar (exclusao logica ou dialogo de confirmacao de dois passos): decisao de UX a definir antes da implementacao.

---

### US-06: sincronizacao com o Google Calendar

**Como** participante de uma reuniao reservada no sistema,
**quero** que a reserva e seu cancelamento reflitam automaticamente no meu Google Calendar,
**para** nao precisar inserir os compromissos manualmente na agenda.

**Criterios de aceite:**

- **Dado** que uma reserva e confirmada com minha participacao,
  **quando** a confirmacao ocorre,
  **entao** em ate 2 minutos recebo convite de evento no Google Calendar com os dados da reserva.

- **Dado** que uma reserva confirmada e cancelada,
  **quando** o cancelamento ocorre,
  **entao** em ate 2 minutos o evento e removido do meu Google Calendar.

- **Dado** que a API do Google Calendar esta indisponivel no momento da confirmacao,
  **quando** a confirmacao ocorre,
  **entao** a reserva e confirmada no sistema (fonte de verdade) e sinaliza "sincronizacao pendente"; o sistema realiza retry ate concluir a sincronizacao (ver Secao 9, EC-02).

---

### US-07: reserva em nome de terceiro (modelo flat)

**Como** qualquer usuario autenticado (incluindo a secretaria),
**quero** criar uma reserva informando outro colaborador como responsavel e adicionando participantes,
**para** atender pedidos recebidos por WhatsApp ou pessoalmente sem que o solicitante precise acessar o sistema diretamente e sem necessitar de perfil especial.

**Criterios de aceite:**

- **Dado** que estou autenticado,
  **quando** crio uma reserva preenchendo o campo "responsavel" com outro colaborador e confirmo,
  **entao** a reserva e criada vinculada ao responsavel indicado e o processo e ao menos tao simples quanto preencher o Google Forms atual.

- **Dado** que a reserva e criada em nome de terceiro,
  **quando** a confirmacao ocorre,
  **entao** o responsavel indicado (e os participantes) recebem o convite do Google Calendar; o responsavel aparece como dono da reserva.

---

### US-08: reserva recorrente (serie)

**Como** qualquer usuario autenticado,
**quero** criar uma serie de reservas recorrentes (ex.: reuniao semanal toda terca-feira as 10h),
**para** nao precisar criar manualmente cada ocorrencia individualmente.

**Criterios de aceite:**

- **Dado** que estou autenticado,
  **quando** crio uma reserva recorrente informando frequencia, horario e data de fim da serie,
  **entao** o sistema cria todas as ocorrencias da serie e valida cada uma individualmente quanto a conflitos.

- **Dado** que algumas ocorrencias da serie estao em conflito com reservas existentes,
  **quando** o sistema conclui a validacao,
  **entao** as ocorrencias sem conflito sao confirmadas; as ocorrencias em conflito sao sinalizadas (nao rejeitadas); a serie nao e descartada integralmente.

- **Dado** que ocorrencias foram sinalizadas como conflitantes,
  **quando** visualizo o resultado da criacao da serie,
  **entao** o sistema apresenta quais ocorrencias estao em conflito e me permite decidir individualmente (manter, remover ou resolver cada ocorrencia).

---

## Secao 8: Requisitos nao-funcionais (NFRs)

> Dimensoes ISO/IEC 25010 aplicaveis a este release. Todos os itens abaixo foram confirmados pelo PO no confirm loop (C-Q06..C-Q08). Viabilidade e "como" sao do Technical Assessment, nao descritos aqui.

| ID | Dimensao ISO/IEC 25010 | Requisito de qualidade | Observacao |
|---|---|---|---|
| NFR-01 | **Confiabilidade / Integridade** [CRITICO] | O sistema nunca permite duas reservas confirmadas sobrepostas na mesma sala, inclusive sob concorrencia de acessos. Propriedade nao-negociavel. | Verificavel por teste de concorrencia; implementacao atomica (TA) |
| NFR-02 | **Desempenho / Sincronizacao** | Toda reserva confirmada ou cancelada deve refletir no Google Calendar em **<=2 minutos** (sync uma via: sistema -> Calendar). | Ancora: Objetivo 4 deste RP; viabilidade e do TA; firmado C-Q08 |
| NFR-03 | **Desempenho / Tempo de resposta** | Consulta de disponibilidade: resposta em **<=2 s** (p95); confirmacao de reserva: **<=3 s** (p95). | Requisito firmado pelo PO: C-Q08. Criterio de aceite mensuravel nos testes de carga |
| NFR-04 | **Usabilidade / Adocao** [CRITICO] | Criar uma reserva no sistema deve ser **mais simples do que preencher o Google Forms atual**; secretaria e usuario comum devem conseguir criar uma reserva sem treinamento formal. | Verificavel por validacao qualitativa com a secretaria (criterio de aceite da Secao 11) |
| NFR-05 | **Usabilidade / Responsividade** | O sistema deve ser **responsivo e adaptado para dispositivos moveis** (fluxo atual ocorre majoritariamente via WhatsApp/celular). Breakpoints minimos: mobile >= 360px, tablet >= 768px. | Requisito firmado pelo PO: C-Q07. Fluxo critico de reserva testado em dispositivo movel antes do release |
| NFR-06 | **Seguranca / Autenticacao** | Acesso somente via **login social** autenticado; cada reserva e atribuivel a um usuario identificado. SSO corporativo esta fora deste release. | Alinhado ao escopo da Secao 5 |
| NFR-07 | **Seguranca / Privacidade** | Dados de participantes (nome, e-mail, horarios de presenca) tratados conforme **LGPD** basico: requisito deste release. Base legal a definir (legitimo interesse ou consentimento); politica de retencao a estabelecer (ex.: 12 meses apos a reuniao); mecanismo de exclusao a pedido previsto. | Requisito firmado pelo PO: C-Q06. Revisao obrigatoria com Juridico/DPO antes do release |
| NFR-08 | **Compatibilidade / Interoperabilidade** | O sistema interopera exclusivamente com a **API do Google Calendar** neste release (uma via: sistema -> Calendar); integracao com Outlook esta fora do escopo. | Alinhado ao escopo da Secao 5; TA OAuth adiado |
| NFR-09 | **Confiabilidade / Disponibilidade** | Disponibilidade **>=99%** durante o horario comercial; sem requisito de SLA 24/7. | Requisito firmado pelo PO: C-Q08. Criterio de aceite mensuravel nos testes de disponibilidade |
| NFR-10 | **Eficiencia / Escala** | O sistema deve suportar ate **~200 usuarios**, com pico de carga no horario comercial (10h-16h). | Requisito firmado pelo PO: C-Q08. Dimensionamento baseado no perfil da empresa |

**Dimensoes nao aplicaveis neste release:** Manutenibilidade e Portabilidade sao tratadas no nivel do Technical Assessment (TA), nao do RP de produto.

---

## Secao 9: Edge cases e modos de falha

| ID | Cenario | Comportamento esperado do sistema |
|---|---|---|
| EC-01 | **Reservas concorrentes (condicao de corrida):** dois usuarios confirmam a mesma sala no mesmo instante | Exclusividade transacional: first-commit-wins (firmado, C-Q01). A primeira gravacao persiste; a segunda recebe resposta de conflito e mensagem com alternativa de horario/sala. |
| EC-02 | **Falha da API do Google Calendar:** a API esta indisponivel no momento da confirmacao ou cancelamento | A reserva e confirmada (ou cancelada) **localmente no sistema** (fonte de verdade); o sistema sinaliza status "sincronizacao pendente" e executa retry com backoff ate concluir a sincronizacao. Nenhuma acao e revertida por falha de sync. (C-Q02.) |
| EC-03 | **Dupla fonte durante a transicao:** mural fisico ou Google Forms usados em paralelo ao sistema no periodo pos go-live | Canal antigo descontinuado formalmente apos ate 2 semanas do go-live; reservas feitas fora do sistema nao sao reconhecidas como validas. Retirada fisica do mural e encerramento do Forms sao passos do plano de migracao. |
| EC-04 | **Alteracao feita diretamente no Google Calendar:** usuario edita ou cancela o evento no Calendar sem atuar no sistema | O sistema e a fonte de verdade (sync uma via, C-Q02): alteracoes feitas no Google Calendar **nao retroalimentam** o sistema neste release. O slot permanece ocupado no sistema mesmo que o evento tenha sido editado no Calendar. Recomendar aviso na UI alertando que o Calendar e espelho (somente leitura). |
| EC-05 | **Reserva recorrente com ocorrencia em conflito:** uma das ocorrencias de uma reserva recorrente colide com reserva existente | Dentro do MVP (firmado, C-Q03: RN-14/15/16): o sistema valida cada ocorrencia individualmente e sinaliza quais estao em conflito; as demais sao confirmadas. O usuario decide individualmente sobre as ocorrencias conflitantes. |
| EC-06 | **Fuso horario / horario de verao (DST):** usuario cria reserva em horario ambiguo (transicao DST) | O sistema exibe e armazena horarios de forma nao-ambigua, com indicacao do fuso local. Reservas nao devem ser criadas em intervalos ambiguos sem confirmacao explicita. (Premissa de mono-fuso: confirmar antes da implementacao.) |
| EC-07 | **Sala em manutencao:** sala indisponivel por manutencao ou bloqueio administrativo | Estado de manutencao bloqueia criacao de novas reservas para a sala; reservas existentes devem ser realocadas manualmente (requer notificacao aos responsaveis). |
| EC-08 | **Participante externo sem login:** cliente ou visitante externo tenta criar reserva no sistema | Externos **nao reservam** salas diretamente (portal externo esta fora do escopo deste release). O organizador interno cria a reserva e convida o externo via evento do Google Calendar (confirmado, C-Q02). |
| EC-09 | **Edicao que cria conflito:** usuario edita o horario de uma reserva e o novo horario colide com outra reserva ativa | O sistema aplica a mesma validacao anti-double-booking da confirmacao: rejeita a edicao, mantem os dados originais e informa o conflito ao usuario. |
| EC-10 | **Reserva em nome de terceiro ausente:** criacao de reserva em nome de colaborador que nao esta disponivel para confirmar | Qualquer usuario autenticado pode criar reserva em nome de terceiro usando o campo "responsavel" (modelo flat, C-Q04); a reserva e criada com o colaborador indicado como responsavel real; o sistema registra quem operou a criacao. Sem necessidade de perfil admin. |
| EC-11 | **Sistema fora do ar ou sem conectividade:** usuario tenta acessar ou confirmar reserva enquanto o sistema esta indisponivel | Falha segura e visivel: o sistema exibe mensagem de indisponibilidade; nenhuma confirmacao falsa e gerada; o usuario nao deve recorrer ao mural como fallback (canal descontinuado). |
| EC-12 | **Reserva no passado ou fora da janela permitida:** usuario tenta criar reserva para data/hora passada ou alem da antecedencia maxima | O sistema rejeita a criacao com mensagem explicativa; nenhuma reserva e criada. (RN-09/10/11 firmadas, C-Q05.) |
| EC-13 | **Divergencia silenciosa entre Calendar e sistema:** usuario edita evento no Google Calendar sem atualizar o sistema | O sistema permanece como fonte de verdade; a divergencia nao e detectada automaticamente neste release (sync uma via, C-Q02). A UI deve exibir aviso informando que o Calendar e espelho somente de leitura e que alteracoes devem ser feitas no sistema. |

---

## Secao 10: Metricas de sucesso (primaria - secundaria - guardrail)

| Tipo | Metrica | Baseline (campo) | Meta pos-rollout | Prazo | Confianca da projecao |
|---|---|---|---|---|---|
| **Primaria (lagging)** | Conflitos de agendamento (double-bookings) por semana | ~1,8/sem (D003/Q008: 9 conflitos/5sem) | **0** | 4 semanas apos go-live | Alta: baseline de campo confirmado |
| **Primaria (lagging)** | Novos adiamentos de negocios causados por conflito de sala | 9 em 5 semanas (D005/Q012) | **0** | 8 semanas apos go-live | Media: depende de acompanhamento comercial (D02) |
| **Leading** | Adocao do sistema (% de reservas criadas no sistema vs. total) | 0% (100% manual) | **100%** | 2 semanas apos go-live (mural e Forms descontinuados) | Alta: criterio de migracao |
| **Guardrail** | Volume total de reservas realizadas por semana | Baseline a medir na semana pre-go-live | Nao deve cair em relacao ao baseline | Semana 1 pos-go-live | Media: risco de subnotificacao se adocao resistida |
| **Guardrail** | Carga de suporte da secretaria (ocorrencias de remarcar por semana) | Baseline a medir na semana pre-go-live | Nao deve aumentar em relacao ao baseline | 4 semanas apos go-live | Media: proxy de adocao e de falhas no sistema |

**Nota sobre baseline financeiro (referencia):** pipeline ~R$ 700 mil; R$ 111 mil ja perdidos (nao recuperaveis); R$ 90 mil em risco (monitorar junto com D02: lideranca comercial). Recuperacao do pipeline em risco e indicador de resultado de negocio, nao metrica operacional do sistema.

---

## Secao 11: Criterios de sucesso e aceite (do release)

| Dimensao | Criterio | Valor-alvo / Verificacao |
|---|---|---|
| **Negocio** | Zero double-bookings registrados desde o go-live | 0 conflitos nas 4 primeiras semanas pos-rollout; verificado por monitoramento do sistema e ausencia de relatos da secretaria |
| **Negocio** | 100% das reservas centralizadas no sistema | Mural fisico e Google Forms descontinuados em ate 2 semanas; nenhuma reserva fora do sistema; confirmacao da secretaria |
| **Negocio** | Pelo menos uma reuniao comercial previamente travada por conflito de sala remarcada e realizada | Acompanhamento com lideranca comercial (D02) nas 8 semanas pos-rollout |
| **Qualidade** | Sistema retorna conflito em 100% dos cenarios de double-booking testados | Cobertura de teste: todos os cenarios de conflito documentados na Secao 9 (edge cases) retornam erro e impedem a reserva |
| **Qualidade** | Integracao com o Google Calendar reflete reservas em <=2 minutos | Teste funcional de integracao: criar/cancelar reserva e verificar atualizacao no Google Calendar em ate 2 min |
| **UX** | Secretaria confirma que criar uma reserva no novo sistema e mais simples do que preencher o Google Forms | Validacao qualitativa com a secretaria (Persona 4) apos onboarding; criterio: declaracao explicita de preferencia pelo sistema |

---

## Secao 12: Riscos e dependencias (de produto e negocio)

### Riscos

| ID | Risco | Tipo | Probabilidade | Impacto | Mitigacao |
|---|---|---|---|---|---|
| R01 | Baixa adocao / resistencia ao sistema novo: usuarios continuam usando o mural ou o WhatsApp informalmente | Adocao | Alta | Alto | Onboarding ativo; secretaria como agente de mudanca; sistema deve ser mais simples que o Forms (criterio de UX); mural retirado fisicamente apos go-live |
| R02 | Dependencia da secretaria para onboarding e validacao de UX: ausencia ou resistencia dela compromete a migracao | Externo / Adocao | Media | Alto | Envolver a secretaria desde o inicio da Fase B2 (design e teste); incluir como stakeholder formal; planejar sessao de validacao de UX antes do go-live |
| R03 | Retorno ao mural em paralelo: usuarios mantem o processo antigo como "seguranca" mesmo apos o go-live | Adocao | Media-Alta | Alto | Comunicacao formal de descontinuacao do mural; retirada fisica do mural e encerramento do Forms apos 2 semanas; monitorar guardrail de adocao (100% das reservas no sistema) |
| R04 | R$ 90 mil em risco pode nao ser recuperado: o negocio travado nao fecha mesmo apos resolucao dos conflitos | Negocio | Media | Medio | Monitorar junto com D02 (lideranca comercial); resultado de negocio e de responsabilidade comercial, nao do sistema; RP registra como risco residual |
| R05 | Escopo creep de integracao: pressao para adicionar Outlook, SSO ou outras integracoes durante a Fase B2 | Produto / Escopo | Baixa-Media | Medio | Secao 5 (Escopo Excluido) e a referencia formal; qualquer adicao requer aprovacao explicita do PO e reavaliacao do Technical Assessment |

### Dependencias

| ID | Dependencia | Tipo | Dono | Impacto se nao resolvida |
|---|---|---|---|---|
| D01 | Secretaria disponivel para onboarding, validacao de UX e migracao do processo manual | Externo / Adocao | Secretaria / Facilities | Risco R02 e R03 se materializam; criterio de UX da Secao 11 nao verificavel |
| D02 | Lideranca comercial disponivel para acompanhar recuperacao do pipeline (R$ 90k em risco) e confirmar adiamentos | Negocio | Lideranca Comercial | Criterio de negocio da Secao 11 (reuniao comercial remarcada) nao verificavel; R04 nao monitorado |
| D03 | Google Calendar API disponivel e fluxo OAuth de-arriscado pelo Technical Assessment | Tecnico / Externo | CTO / Tech Lead (TA adiado) | Integracao com Google Calendar (uma via: sistema -> Calendar) nao entregavel; escopo de integracao deve ser revisado |

**Nota sobre riscos tecnicos:** riscos tecnicos do fluxo OAuth do Google Calendar migram para o Technical Assessment (Secao 14: Referencia ao Technical Assessment). D03 esta vinculada ao TA adiado.

---

## Secao 13: Avaliacao preliminar de esforco e custo

> **[Estimativa preliminar adiada: disposicao honesta]**
>
> Nenhum dado de prazo ou orcamento foi informado no origination-record nem no intake-record v3. A estimativa preliminar de esforco e custo esta **adiada ao CTO/Tech Lead**: o numero firme vira do Technical Assessment (ver Referencia ao Technical Assessment abaixo). Esta secao **nao bloqueia o freeze** do RP (blocks=false). Ela bloqueia a execucao com compromisso firme de prazo/custo.

[A preencher pelo CTO / Tech Lead no Technical Assessment: estimativa firme de esforco e custo para sequenciamento interno]

---

## Secao 14: Roadmap sugerido

### MVP (este release)

- Sistema digital de reserva de salas de reuniao (CRUD completo).
- Integracao com o Google Calendar, uma via (sistema -> Calendar; sincronizacao em ate 2 min).
- Autenticacao simples (login social).
- Regras automaticas de anti-double-booking.
- Migracao e descontinuacao do processo manual (mural fisico + Google Forms via WhatsApp).

### Fase 2 (backlog futuro)

- Integracao com Outlook / Microsoft 365 (descartada neste release, retorna como demanda futura).
- Analytics e relatorios de ocupacao de salas (dashboards historicos, metricas de uso).
- Lembretes automaticos de reservas.

### Fase 3 (backlog futuro)

- SSO corporativo (autenticacao empresarial).
- Outros recursos fisicos (estacionamento, equipamentos, salas especiais).

---

## Referencia ao Technical Assessment

| Campo | Valor |
|---|---|
| **Escalada requisitada?** | SIM: Technical Assessment LEVE |
| **Status** | requisitado |
| **Veredito** | (pendente) |
| **Link** | (pendente) |
| **Freeze** | PROVISORIO: a tech-assessment skill ainda nao existe; TA pendente, fora do escopo atual de tooling |

### Gatilhos presentes (justificam a escalada LEVE)

1. **Seguranca / autenticacao:** login social / OAuth (NFR-06): o sistema autentica usuarios via login social; o modelo de credencial e os escopos OAuth precisam ser determinados pelo CTO/Tech Lead antes do congelamento tecnico.
2. **Integracao externa com incognitas:** Google Calendar via OAuth, uma via (Escopo §5, Objetivo 4, NFR-02/08, US-06, dependencia D03): a integracao envolve variaveis de configuracao do ambiente real (Workspace, escopos disponiveis, modelo de credencial) que so podem ser confirmadas com acesso ao ambiente da organizacao.

### Gatilhos ausentes (delimitam o escopo do TA como LEVE)

- Sem nova infraestrutura critica.
- Sem multi-tenancy ou isolamento de dados entre organizacoes.
- Sem IA ou runtime experimental.
- Integracao de-arriscada no Discovery (somente Google Calendar, sem Outlook, sem SSO corporativo; login social aceito como premissa confirmada em D003/Q010).

### Contexto de natureza (Hibrido)

O TA deve descobrir o ambiente real antes de confirmar o modelo de integracao: workflow da secretaria, configuracao do Google Workspace da organizacao e escopos OAuth disponiveis para aplicacoes de terceiros. Nao ha premissa greenfield (nova capacidade): o sistema se integra a um ambiente organizacional existente com configuracoes proprias.

### Escopo do TA LEVE (4 pontos)

**(a) Viabilidade do fluxo OAuth Google Calendar:** quais escopos sao necessarios (`calendar.events` ou mais amplo); se o Google Workspace da organizacao permite concessao a aplicacoes de terceiros; qual o modelo de credencial adequado (service account com delegacao de dominio vs. delegacao por usuario autenticado).

**(b) Modelo de sincronizacao (uma via: sistema -> Calendar):** confirmar que a estrategia "sistema = fonte de verdade; Calendar = espelho; alteracoes feitas diretamente no Calendar NAO refletem de volta neste release" e viavel e sustentavel sem webhooks / push que introduzam incognitas adicionais.

**(c) Atomicidade e anti-double-booking sob concorrencia:** confirmar a decisao de arquitetura para garantir a propriedade first-commit-wins (RN-05, EC-01, NFR-01) sob acessos concorrentes; esta e uma decisao de arquitetura, nao de produto.

**(d) Orcamento de latencia de sincronizacao:** confirmar se o SLA de <=2 minutos (NFR-02, Objetivo 4, US-06) e alcancavel com polling ou com push da API do Google Calendar, considerando os limites de quota da API e o ambiente real da organizacao.

### Nota operacional

Quando o TA for executado: atualizar **Status = assinado** e registrar o **Veredito** (viavel / viavel-com-ressalvas / inviavel-como-escopado). A divida esta registrada no `owes` do indice da iniciativa. O TA e LEVE e **nao bloqueia as secoes de produto do RP** (Secoes 1-13), mas o **freeze pleno exige Status = assinado**. O freeze atual e PROVISORIO.

Disposicao autorizada pelo Escalation Flagger. O TA LEVE cobre exclusivamente OAuth Google Calendar (4 pontos acima); nao ha bloqueio as secoes de produto. Quando o TA skill existir e for executado, registrar aqui o veredito e promover Status para assinado, encerrando o freeze provisorio. Origem composta: intake-record v3 (cto-escalation / triage-decision: D003/Q010) + qa-log.md (I011) + disposicao do Escalation Flagger (2026-06-07).

<!-- END OF DOCUMENT -->
