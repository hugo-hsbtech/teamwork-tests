<!--
READINESS PACKAGE · room-reservation
Gerado a partir de: target-template.readiness-package.md
Linguagem de saída: pt-BR
Fase: Act 2: Ato 2 do PO
-->

# Readiness Package: Sistema de Reserva de Salas de Reunião
<!-- rev: 4 · updated: 2026-06-07 -->

> O Readiness Package (RP) é a **definição de pronto de produto**: o output do PO.
> Ele é auto-suficiente: visão, problema, escopo, regras, jornadas de usuário, histórias, NFRs,
> edge cases, critérios e métricas. O RP **não** contém seções de autoria do CTO; a
> avaliação técnica vive no Technical Assessment (referenciado abaixo). O RP herda
> a camada de confiança do Origination vinculado; o que entrou como premissa ou incógnita
> é resolvido ou carregado explicitamente na seção "Prontidão herdada".

## Metadados
<!-- origination: id=meta; blocks=false; min-confidence=0; kind=meta -->

| Campo | Valor |
|---|---|
| **ID do Pacote** | RP-2026-001 |
| **Versão** | v1 |
| **Origination vinculado** | INT-2026-001 |
| **Responsável** | PO (Ato 2) |
| **Natureza da demanda** | HÍBRIDO: processo informal existente (mural físico + Google Forms via WhatsApp, mantido pela secretária) + software-core novo + integração com Google Calendar |
| **Base de conhecimento** | `tech-landscape-room-reservation.md` · A criar (não existe) |
| **Escalada ao CTO** | SIM: LEVE (Technical Assessment OAuth Google Calendar, adiada) |
| **Status** | Rascunho |
| **Data de congelamento (freeze)** | (pendente) |
| **Idioma de saída** | pt-BR |

## Histórico de Revisão
<!-- origination: id=revisions; blocks=false; min-confidence=0; kind=meta -->

| Versão | Data | Autor | Status | Resumo |
|---|---|---|---|---|
| v1 | 2026-06-07 | Doc Updater (Stage Inheritor) | Rascunho | Criação do RP a partir do template; seções herdadas preenchidas (I001-I011); seções de produto deixadas como placeholders para Fase B2. |
| v2 | 2026-06-07 | Doc Updater (Fase B2) | Rascunho | Cinco seções de produto preenchidas com rascunho IA do Section Drafter: regras de negócio (Seção 6), jornada do usuário (Seção 6.5), user stories (Seção 7), NFRs (Seção 8), edge cases (Seção 9). Todas abaixo do limiar de confiança; loop de confirmação do PO pendente. |
| v3 | 2026-06-07 | Doc Updater (Escalation Flagger) | Rascunho | Seção tech-assessment-ref refinada com disposição autoritativa do Escalation Flagger: gatilhos presentes e ausentes detalhados, escopo do TA LEVE (4 pontos), contexto Híbrido, nota operacional de freeze provisório. Status=requisitado · Disposição=adiada · Freeze=PROVISÓRIO. |
| v4 | 2026-06-07 | Doc Updater (Act 2: confirm loop) | Rascunho | 5 seções de produto promovidas de rascunho IA para po_authored com confirmações C-Q01..C-Q08 do PO: regras de negócio (conf 88), jornada do usuário (conf 80), user stories (conf 88), NFRs (conf 82), edge cases (conf 80). Conflitos C4 (sync uma via), C1 (rótulo readiness 74%) e C2 (premissas product) corrigidos. Estimativa de esforço mantida como adiada honesta (não-bloqueante). |

---

## Prontidão herdada e disposições em aberto
<!-- origination: id=inherited-readiness; blocks=false; min-confidence=0; kind=derived; inputs=exec-summary,context-problem,objectives,personas,scope,metrics,release-criteria,risks -->

> Resumo do que o Origination entregou e do que continua em aberto na entrada da execução.
> Premissas, incógnitas de Discovery e respostas delegadas que sobreviveram à
> racionalização precisam estar visíveis, não enterradas nas seções. Se uma
> premissa carregada aqui se provar falsa durante a execução, a demanda deve ser
> reavaliada (o mesmo gatilho de retriage do origination se aplica downstream).

| Campo | Valor |
|---|---|
| **Readiness Score no handoff do origination (não é o score atual do RP)** | ~74%: score de passagem de fase calculado pelo Stage Inheritor; o score canônico atual virá da próxima rodada do Confidence Auditor |
| **Premissas ainda a validar** | NENHUMA: todas as 3 premissas do origination resolvidas em D003 + D005: (1) impacto quantificado operacional e em R$ [D003/Q008 + D005/Q012]; (2) "negócios adiados" confirmado com valor firme [D005/Q012]; (3) natureza greenfield rejeitada, demanda Híbrida confirmada [D003/Q011]. |
| **Incógnitas de Discovery** | RESOLVIDAS: Discovery totalmente encerrado (D003 + D005, 2026-06-06): impacto operacional quantificado, viabilidade de integração de-arriscada (somente Google Calendar), processo informal caracterizado, valor R$ dos negócios adiados firmado. |
| **Premissas de Discovery/origination** | NENHUMA aberta (resolvidas em D003+D005); as decisões de produto do RP foram confirmadas pelo PO no confirm loop (C-Q01..C-Q08). |
| **Requisitos delegados (com dono)** | Technical Assessment LEVE (OAuth Google Calendar): dono CTO/Tech Lead; adiado, não-bloqueante para Fase B2. |

**Proveniência**
- **Confiança:** 90
- **Origem:** derivado (Stage Inheritor): I011
- **Fonte:** Handoff readiness 74% calculado pelo Stage Inheritor sobre D003 + D005; origination-record + intake-record v3
- **Situação:** respondida
- **Disposição:** respondida
- **Observação:** O valor "74%" é o score de handoff do origination, não o score canônico de prontidão desta fase. Não recomputar sem nova rodada do Confidence Auditor. As decisões de produto foram confirmadas pelo PO no confirm loop (C-Q01..C-Q08); premissas de Discovery/origination encerradas (D003+D005). O único item adiado (Technical Assessment OAuth) é não-bloqueante para a Fase B2.

---

## Seção 1: Resumo executivo
<!-- origination: id=exec-summary; blocks=true; min-confidence=70; kind=capture -->
> Rubric: 2-4 parágrafos curtos. Qual é o problema, o que será construído e qual é
> o resultado esperado de negócio. Deve ser legível por qualquer stakeholder sem
> contexto adicional. Herdado e expandido do origination quando possível.

A empresa tem um problema crônico de **conflito de agendamento** (double-booking) em suas salas de reunião. Toda semana, sem parar, dois grupos chegam à mesma sala no mesmo horário e "vira confusão": nenhum mecanismo impede o duplo agendamento, e o processo atual de reserva, que mistura anotação manual no mural físico e um Google Forms enviado por WhatsApp gerenciado pela secretária, não consegue garantir exclusividade de horário nem alertar sobre conflitos em tempo real.

O impacto foi quantificado em campo: cerca de 9 conflitos em 5 semanas (média de 1,8 por semana), com atraso médio de ~3 dias por conflito para reencontrar agenda comum. Desses conflitos, 9 reuniões de negócio foram adiadas, envolvendo um pipeline total de aproximadamente **R$ 700 mil** em prospecção de novos negócios. Do total afetado, **R$ 111 mil já foram perdidos** (dois negócios que não fecham mais) e **R$ 90 mil estão em risco** (um negócio ainda em aberto, travado pelo conflito). A dor atinge quatro perfis: equipes internas que disputam o espaço, reuniões com clientes e externos (risco de imagem), liderança e diretoria, e a própria secretária/facilities, que absorve o retrabalho de remarcar.

Será construído um **sistema digital de reserva de salas** integrado ao Google Calendar, de natureza Híbrida: migra o processo manual atual (mural + Forms + WhatsApp) para um fluxo digital com regras automáticas de anti-conflito. A secretária é o stakeholder-chave da migração; o sistema precisa ser mais simples de usar do que o Google Forms atual para vencer a inércia de adoção. A integração com o Google Calendar é **uma via (sistema → Calendar; o sistema é a fonte de verdade)**: reservas criadas ou canceladas no sistema refletem automaticamente no Calendar em até 2 minutos; alterações feitas diretamente no Google Calendar não retroalimentam o sistema neste release. A autenticação será simples (login social); SSO corporativo e integração com Outlook estão fora do escopo deste release.

O resultado esperado é a **eliminação dos conflitos de agendamento** e a **proteção do pipeline comercial**: zero novos double-bookings após o rollout, 100% das reservas centralizadas no sistema (mural e Forms descontinuados) e, no horizonte de 8 semanas, zero novos adiamentos de negócios causados por conflito de sala. O critério executivo de sucesso é direto: nenhum novo double-booking ocorre após o go-live.

**Proveniência**
- **Confiança:** 82
- **Origem:** po_authored: C-Q02 (sync uma via confirmada)
- **Fonte:** origination-record (problem / reach / impact: Q001, Q003, Q004, Q006, Q010) + intake-record v3 (demand-summary / triage-decision / demand-nature: D003/Q008/Q010/Q011 + D005/Q012) + confirmação PO C-Q02 (sync uma via)
- **Situação:** respondida
- **Disposição:** po_authored: conflito C4 resolvido; parágrafo de integração corrigido para "uma via (sistema → Calendar)"
- **Observação:** Conteúdo expandido e consolidado das fontes upstream; impacto totalmente quantificado (D003 + D005). Parágrafo de integração atualizado per C-Q02: "bidirecional" substituído por "uma via (sistema → Calendar; o sistema é a fonte de verdade)".

---

## Seção 2: Contexto e problema (a dor, não a solução)
<!-- origination: id=context-problem; blocks=true; min-confidence=80; kind=capture -->
> Rubric: cenário atual, limitações, dor do cliente e impacto de negócio: o
> problema, nunca a solução. Se descreve uma solução ("construir X"), NÃO está
> satisfeita: reformule para a dor subjacente. Herdada do origination quando possível.

### Cenário atual

O processo de reserva de salas de reunião é inteiramente manual e informal. A **fonte de verdade** é um **mural físico** onde as reservas são anotadas em papel. Para solicitar uma reserva, os usuários preenchem um **Google Forms** cujo link circula via **WhatsApp**, ou simplesmente anotam diretamente no papel. A **secretária** atua como árbitro e gestora desse processo: ela valida os conflitos, remarca reuniões e mantém a coerência do mural. Não há sistema digital, regra automática, notificação em tempo real ou integração com a agenda digital dos participantes. O processo existe, funciona de forma informal, e tem a secretária como elo central.

### Limitações

O processo manual tem quatro limitações estruturais que o tornam incapaz de prevenir conflitos:

1. **Não previne double-booking automaticamente.** Duas reservas para o mesmo horário e sala podem ser feitas sem qualquer alerta; o conflito só é descoberto quando os grupos aparecem fisicamente na sala.
2. **Depende de uma pessoa-chave.** A secretária é o único ponto de controle; na ausência dela, o processo fica sem árbitro e os conflitos não têm resolução definida.
3. **Não é auditável nem rastreável.** Não há registro histórico consultável de reservas, cancelamentos ou conflitos. Cada ocorrência começa do zero.
4. **Não integra com a agenda digital.** As reservas no mural não aparecem automaticamente no Google Calendar dos participantes, criando desconexão entre o espaço físico e a agenda pessoal.

### Dor do cliente

O conflito de agendamento (double-booking) acontece **toda semana, sem parar**: dor crônica e recorrente, não exceção isolada. Quando dois grupos chegam à mesma sala no mesmo horário, "vira confusão"; não há protocolo claro de resolução e a situação se repete. Quatro perfis são diretamente afetados:

- **Equipes internas que disputam a sala:** transtorno imediato para quem encontrou o espaço já ocupado; a reunião atrasa ou não acontece no horário.
- **Reuniões com clientes e externos:** constrangimento institucional quando visitantes estão presentes; risco de imagem e de relacionamento comercial.
- **Liderança e diretoria:** suas próprias reuniões estão sujeitas ao mesmo conflito, sem tratamento preferencial pelo processo atual.
- **Secretária/facilities:** absorve o retrabalho de remarcar, negociar e resolver cada ocorrência; é o único ponto de controle do processo e stakeholder-chave de qualquer migração.

### Impacto de negócio

O impacto foi **totalmente quantificado** em campo (Discovery D003 + D005, 2026-06-06):

- **Frequência:** ~9 conflitos em 5 semanas, equivalente a **1,8 conflitos por semana**, concentrados em dias úteis, pico entre 10h e 16h.
- **Atraso por conflito:** atraso médio de **~3 dias** para reencontrar agenda comum após um conflito.
- **Negócios afetados:** 9 reuniões de negócios adiadas, envolvendo um **pipeline total de ~R$ 700 mil** em prospecção de novos negócios (receita nova, não recorrente).
- **Perdas confirmadas:** **R$ 111 mil já perdidos**, dois negócios que não fecham mais por conta dos adiamentos encadeados.
- **Valor em risco:** **R$ 90 mil em risco**, um negócio ainda em aberto e travado.

O eixo de maior gravidade é o de negócios adiados: o custo de imagem e de relacionamento com clientes externos está subsumido neste eixo (confirmado em D003/Q010). O impacto operacional (tempo perdido, retrabalho da secretária) é real, mas secundário frente à exposição de receita.

**Proveniência**
- **Confiança:** 80
- **Origem:** herdada: I002
- **Fonte:** origination-record (problem / reach / impact: Q001, Q003, Q004, Q006, Q010) + intake-record v3 (demand-summary / demand-nature: D003/Q008/Q011 + D005/Q012)
- **Situação:** herdada
- **Disposição:** herdada: conf >= mínimo 80; subseção "Limitações" derivada por inferência estrutural
- **Observação:** Subseção "Limitações" derivada por inferência estrutural a partir das características do processo manual descrito; marcar como INFERIDA para revisão do PO se necessário. Impacto totalmente quantificado; reconciliação D003 vs. D005 (7 vs. 9 adiamentos): adotado 9 como valor mais recente (D005, não-bloqueante).

---

## Seção 3: Objetivos e resultado esperado
<!-- origination: id=objectives; blocks=true; min-confidence=70; kind=capture -->
> Rubric: objetivos numerados e observáveis que esta entrega deve alcançar após o
> release. Cada objetivo deve ser verificável: se não pode ser medido ou observado,
> não está satisfeito. Mínimo dois objetivos.

1. **Eliminar o conflito de agendamento (double-booking):** zero novos double-bookings registrados nas 4 semanas seguintes ao rollout. Verificável por monitoramento de conflitos no próprio sistema e por ausência de relatos presenciais da secretária e dos usuários.

2. **Interromper novos adiamentos comerciais causados por conflito de sala:** zero novos adiamentos de negócios atribuíveis a conflito de sala nas 8 semanas seguintes ao rollout. Verificável por acompanhamento com a liderança comercial (D02).

3. **Migrar 100% das reservas para o sistema digital:** mural físico e Google Forms descontinuados em até 2 semanas após o go-live; todas as reservas criadas, consultadas e canceladas exclusivamente pelo novo sistema. Verificável por observação direta e confirmação da secretária.

4. **Integrar com o Google Calendar em tempo real:** toda reserva criada ou cancelada no sistema deve refletir automaticamente no Google Calendar dos participantes em até 2 minutos. Verificável por teste funcional de integração.

**Proveniência**
- **Confiança:** 85
- **Origem:** herdada: I003
- **Fonte:** origination-record (impact / urgency) + intake-record v3 (demand-summary / constraints / triage-decision: D003/Q010 + D005/Q012)
- **Situação:** herdada
- **Disposição:** herdada: metas e prazos propostos; PO deve confirmar antes de promover para "respondida"
- **Observação:** Metas e prazos (4 sem, 8 sem, 2 sem, <=2 min) são propostos com base nos dados de campo do Discovery; requerem confirmação explícita do PO antes do gate de prontidão.

---

## Seção 4: Personas impactadas / jobs-to-be-done
<!-- origination: id=personas; blocks=true; min-confidence=70; kind=capture -->
> Rubric: para cada persona, o job-to-be-done (o que está tentando realizar) e como
> é impactada por esta entrega. Sem persona definida, escopo e critérios de aceite
> não têm âncora. Herdado do origination (campo reach) quando possível.

### Persona 1: equipes internas que disputam a sala

**Job-to-be-done:** reservar uma sala de reunião com antecedência e ter a certeza de que ela estará disponível no horário marcado, sem surpresas.

**Impacto hoje:** chegam à sala e encontram outro grupo já ocupando o espaço; a reunião atrasa ou não acontece. Não há visibilidade prévia de disponibilidade; a reserva no mural não garante exclusividade.

**Impacto pós-entrega:** conseguem verificar disponibilidade em tempo real, criar a reserva pelo sistema e receber confirmação; conflito de agendamento deixa de existir como risco operacional.

---

### Persona 2: reuniões com clientes e externos

**Job-to-be-done:** conduzir reuniões com visitantes externos de forma profissional, em um ambiente preparado e reservado, sem imprevistos.

**Impacto hoje:** um conflito de agendamento em reunião com clientes gera constrangimento institucional e risco de imagem; o processo atual não tem proteção especial para reuniões com externos.

**Impacto pós-entrega:** a reserva confirmada pelo sistema elimina o risco de double-booking e protege a credibilidade da empresa perante clientes e parceiros.

---

### Persona 3: liderança e diretoria

**Job-to-be-done:** garantir que reuniões estratégicas e de alta prioridade aconteçam no horário planejado, sem interrupções causadas por conflito de espaço.

**Impacto hoje:** as reuniões da liderança não têm tratamento diferenciado no processo atual; estão sujeitas ao mesmo double-booking que qualquer outro grupo.

**Impacto pós-entrega:** visibilidade de ocupação em tempo real; possibilidade de reservar com antecedência e com confirmação; reuniões estratégicas protegidas por regra automática de anti-conflito.

---

### Persona 4: secretária / facilities (stakeholder-chave de migração)

**Job-to-be-done:** manter o processo de reservas funcionando de forma ordenada, resolver conflitos quando ocorrem e garantir que a sala certa esteja disponível para cada reunião.

**Impacto hoje:** é o único ponto de controle do processo; absorve todo o retrabalho de remarcar e negociar a cada conflito; o processo depende de sua presença e disponibilidade.

**Impacto pós-entrega:** o sistema assume a função de árbitro de conflitos automaticamente; a secretária deixa de ser o gargalo operacional do processo. É o stakeholder-chave da migração: sua adesão e validação de usabilidade são necessárias para o sucesso do rollout. O sistema deve ser mais simples de operar do que o Google Forms atual.

**Proveniência**
- **Confiança:** 76
- **Origem:** herdada: I004
- **Fonte:** origination-record (reach: Q004) + intake-record v3 (demand-nature: D003/Q011)
- **Situação:** herdada
- **Disposição:** herdada: persona secretária/facilities enriquecida com contexto de migração (D003/Q011); conf 76, abaixo de 80
- **Observação:** conf 76 < 80; considerar entrevista rápida com a secretária/facilities para elevar confiança antes de redigir as user stories (Fase B2). Não-bloqueante para início da Fase B2, mas recomendado antes do gate de prontidão.

---

## Seção 5: Escopo incluído e excluído
<!-- origination: id=scope; blocks=true; min-confidence=75; kind=capture -->
> Rubric: protege o downstream de escopo creep. Deve listar explicitamente o que
> está FORA, não apenas o que está dentro. Itens adiados alimentam o Roadmap
> (Seção 14). Sem "excluído" preenchido, a seção NÃO está satisfeita.

### Incluído

- **CRUD de reservas:** criar, consultar, editar e cancelar reservas de salas de reunião.
- **Integração com o Google Calendar (uma via: sistema → Calendar; o sistema é a fonte de verdade):** toda reserva criada ou cancelada no sistema reflete automaticamente no Google Calendar dos participantes em até 2 min; alterações feitas diretamente no Google Calendar não retroalimentam o sistema neste release.
- **Autenticação simples (login social):** acesso ao sistema via autenticação simplificada; sem SSO corporativo.
- **Regras automáticas de anti-double-booking:** o sistema impede a criação de reservas conflitantes (mesma sala, mesmo horário) automaticamente, sem intervenção humana.
- **Reservas recorrentes (séries):** o sistema suporta criação de séries recorrentes; a validação de conflito ocorre ocorrência a ocorrência; ocorrências em conflito são sinalizadas (a série não é rejeitada integralmente).
- **Migração do processo manual:** substituição e descontinuação do mural físico e do Google Forms como instrumentos de reserva; o novo sistema é o único canal de reservas após o rollout.

### Excluído

- **Integração com Outlook / Microsoft 365:** fora do escopo deste release (Outlook descartado em D003/Q010); pode entrar em fase futura.
- **SSO corporativo:** autenticação simples/login social é suficiente; SSO é escopo futuro.
- **Outros recursos físicos:** o sistema reserva exclusivamente salas de reunião; outros recursos (estacionamento, equipamentos, etc.) estão fora do escopo.
- **Analytics avançado e relatórios de uso:** sem dashboards de utilização ou relatórios históricos neste release.
- **Portal externo para visitantes:** agendamento por clientes ou externos diretamente no sistema está fora do escopo.

### Adiado (fases futuras)

- **Integração com Outlook:** fase futura, após estabilização com Google Calendar.
- **Analytics e relatórios de ocupação:** dashboards de uso de salas, histórico de conflitos, métricas operacionais; Fase 2.
- **Lembretes automáticos:** notificações de lembrete antes da reserva; Fase 2.
- **SSO corporativo:** autenticação empresarial; Fase 3.

**Proveniência**
- **Confiança:** 83
- **Origem:** po_authored: C-Q02 (sync uma via), C-Q03 (recorrência no escopo)
- **Fonte:** intake-record v3 (constraints / demand-nature / triage-decision: D003/Q010/Q011) + confirmações PO C-Q02 e C-Q03
- **Situação:** respondida
- **Disposição:** po_authored: escopo atualizado; integração corrigida para "uma via (sistema → Calendar)"; reservas recorrentes adicionadas ao no escopo (C-Q03)
- **Observação:** Qualquer adição ao escopo incluído ativa o risco R05 (escopo creep de integração). Item "bidirecional" corrigido per C-Q02. Reservas recorrentes incluídas per C-Q03.

---

## Seção 6: Regras de negócio e fluxos
<!-- origination: id=business-rules; blocks=true; min-confidence=80; kind=capture -->
> Rubric: regras, validações e transições de estado que governam a funcionalidade.
> Cada regra deve ser verificável e atômica. Fluxos de transição de estado devem
> cobrir caminhos de erro, não apenas o caminho feliz.

### Bloco 1: exclusividade e anti-double-booking

- **RN-01:** Uma sala em um determinado intervalo de tempo pode ter no máximo uma reserva ativa; sobreposição de reservas é proibida.
- **RN-02:** A validação de conflito ocorre no momento da **confirmação** da reserva; tentativas de confirmar uma reserva que sobreponha outra ativa são recusadas pelo sistema.
- **RN-03:** O sistema considera **sobreposição parcial**, não apenas horários idênticos, para fins de conflito; qualquer interseção de intervalos configura conflito. (Decisão firmada: C-Q01.)
- **RN-04:** O **sistema é a fonte de verdade** de disponibilidade; mural físico e Google Forms são descontinuados após o go-live e não geram reservas válidas.
- **RN-05:** Sob criação concorrente (dois usuários confirmando a mesma sala no mesmo instante), o sistema adota a política **first-commit-wins**: a primeira confirmação persiste; a segunda recebe conflito.

### Bloco 2: permissões (modelo flat)

- **RN-06:** Qualquer usuário autenticado via login social pode criar, consultar, editar e cancelar **qualquer** reserva no sistema, inclusive reservas criadas por outros usuários. Não existe perfil admin especial. (Decisão firmada: C-Q04.)
- **RN-07:** ~~[premissa]~~ **Removido**: distinção de perfil secretária/admin eliminada. A secretária opera como qualquer usuário autenticado; cria reservas em nome de terceiros usando os campos "responsável" e "participantes" disponíveis a todos. (C-Q04.)
- **RN-08:** ~~[premissa]~~ **Removido**: sem perfil admin diferenciado neste release. (C-Q04.)

### Bloco 3: parâmetros temporais (firmados)

- **RN-09:** O sistema aceita reservas dentro da janela de **08h às 19h em dias úteis**. (Firmado: C-Q05; validação obrigatória no sistema.)
- **RN-10:** A duração mínima de uma reserva é de **15 minutos**; a duração máxima é de **8 horas**. (Firmado: C-Q05.)
- **RN-11:** Reservas devem ser criadas para datas **futuras**; a antecedência máxima permitida é de aproximadamente **90 dias** corridos. (Firmado: C-Q05. Valor exato a parametrizar antes da implementação.)
- **RN-12:** Edição e cancelamento de uma reserva são permitidos até o **momento de início** da reserva; edição revalida o conflito contra as demais reservas ativas.

### Bloco 4: precedência e desempate (FCFS firmado)

- **RN-13:** A política de precedência é **FCFS (first-come, first-served)**: a primeira confirmação vence, independentemente de hierarquia ou perfil. Liderança e diretoria **não** sobrescrevem automaticamente reservas já confirmadas. Caso desejem a sala, podem **solicitar realocação** via secretária ou sistema: fluxo facilitado, mas não automático nem garantido. (Decisão firmada pelo PO: C-Q01.)

### Bloco 5: reservas recorrentes (MVP)

- **RN-14:** O sistema suporta criação de **séries recorrentes** de reservas. (Decisão firmada: C-Q03.)
- **RN-15:** A validação de conflito de uma série recorrente ocorre **ocorrência a ocorrência**; ocorrências em conflito são **sinalizadas** ao usuário; o sistema não rejeita a série inteira por causa de uma ocorrência em conflito.
- **RN-16:** O usuário decide individualmente o que fazer com as ocorrências sinalizadas como conflitantes (aceitar as sem conflito, remover as em conflito, ou cancelar a série).

### Fluxo de transição de estado da reserva

```
Rascunho → Confirmada → Cancelada
                     ↘ Concluída
```

- **Rascunho → Confirmada:** o sistema executa a validação anti-conflito; se não houver interseção com reserva ativa na mesma sala, confirma e dispara a sincronização com o Google Calendar.
- **Confirmada → Cancelada:** libera o slot; remove o evento no Google Calendar; notifica participantes. A liberação do slot ocorre imediatamente no sistema (fonte de verdade), independentemente do status da sincronização.
- **Confirmada → Concluída:** transição automática após o término do intervalo reservado.
- **Falha de sincronização:** a reserva permanece **Confirmada** como fonte de verdade; o sistema sinaliza sincronização pendente e realiza retry com backoff.

### Fluxo de conflito

1. Usuário seleciona sala e intervalo.
2. Sistema consulta reservas ativas para a sala no intervalo solicitado.
3. Se houver interseção: bloqueia a confirmação e informa o conflito (e, se aplicável, sugere alternativas).
4. Se não houver interseção: confirma a reserva (sob concorrência, a checagem e a gravação são atômicas).

### Sincronização com o Google Calendar (uma via, firmada)

- Toda transição **Confirmada** ou **Cancelada** propaga para o Google Calendar em até **<=2 minutos**. (Firmado: C-Q08.)
- O sistema é a **fonte de verdade**; o Google Calendar é espelho de leitura.
- Alterações feitas diretamente no Google Calendar **não refletem** de volta no sistema neste release: sincronização é **uma via** (sistema → Calendar). (Decisão firmada pelo PO: C-Q02. Remove premissa anterior.)

**Proveniência**
- **Confiança:** 88
- **Origem:** po_authored: C-Q01, C-Q02, C-Q03, C-Q04, C-Q05
- **Fonte:** contexto herdado das Seções 1-5 deste RP + confirmações PO (C-Q01: FCFS; C-Q02: sync uma via; C-Q03: recorrência MVP; C-Q04: modelo flat de permissões; C-Q05: parâmetros temporais firmados)
- **Situação:** respondida
- **Disposição:** po_authored: conf 88 >= mínimo 80; todas as premissas críticas resolvidas pelo PO no confirm loop
- **Observação:** RN-03 firmada (sobreposição parcial). RN-07/08 removidas (modelo flat). RN-09/10/11 firmadas (sem premissa). RN-13 firmada (FCFS + pedido de realocação facilitado). RN-14/15/16 adicionadas (recorrência MVP). Sync uma via firmada (C-Q02). Valor exato de antecedência (~90 dias) a parametrizar antes da implementação.

---

## Seção 6.5: Jornadas do usuário (ponta a ponta)
<!-- origination: id=user-journey; blocks=true; min-confidence=70; kind=capture -->
> Rubric: a peça entre "o que" e "as histórias". A definição precisa de uma noção do
> que o usuário faz **de ponta a ponta**: o caminho completo, não fragmentos. As
> user stories (Seção 7) **derivam** dos passos desta jornada. Território do PO
> (produto, não UX detalhado de tela). Padrão: user journey map (caminho principal +
> caminhos alternativos) e, quando há bastidor relevante, blueprint de serviço
> (opcional). Compressão: melhoria pequena = jornada de 3-5 passos do caminho principal,
> sem blueprint. Sem ao menos o caminho principal da jornada principal, NÃO está satisfeita.

### Jornada A: colaborador (caminho principal)

| # | Gatilho / Ação do usuário | Resultado esperado | Touchpoint / Tela | Pré-condição |
|---|---|---|---|---|
| A1 | Usuário acessa o sistema e realiza login social | Usuário autenticado; acesso ao sistema liberado | Tela de login | Conta Google/social válida |
| A2 | Consulta disponibilidade de salas em tempo real | Sistema exibe salas disponíveis no intervalo selecionado | Tela de disponibilidade | Usuário autenticado |
| A3 | Escolhe sala e horário; preenche dados da reserva (título, participantes etc.) | Formulário de reserva preenchido; dados validados | Formulário de reserva | Sala e intervalo selecionados |
| A4 | Confirma a reserva | Sistema executa validação anti-conflito; reserva criada e confirmada | Tela de confirmação | Sem sobreposição com reservas ativas |
| A5 | (ação do sistema) | Sincronização automática com o Google Calendar em <=2 minutos | Bastidores: API Google Calendar | Reserva confirmada; credenciais OAuth válidas |
| A6 | (ação do sistema) | Participantes recebem convite do Google Calendar | E-mail / Google Calendar | Sincronização A5 concluída |

### Jornada B: secretária reservando em nome de terceiro (modelo flat)

| # | Gatilho / Ação | Resultado esperado | Touchpoint / Tela | Pré-condição |
|---|---|---|---|---|
| B1 | Secretária recebe pedido de reserva (presencial ou via WhatsApp) e acessa o sistema | Secretária autenticada como usuário comum (sem perfil admin especial) | Tela de login | Conta Google/social válida |
| B2 | Cria reserva preenchendo o campo "responsável" com o nome do solicitante e adicionando os participantes | Reserva registrada com o solicitante como responsável; secretária como criadora operacional | Formulário de reserva: campos "responsável" e "participantes" disponíveis a qualquer usuário | Usuário autenticado |
| B3 | Confirma a reserva | Sistema valida anti-conflito; confirma; dispara sync com Google Calendar; solicitante recebe convite | Tela de confirmação | Sem conflito no intervalo |

Esta jornada **substitui o papel de árbitro manual** que a secretária exerce hoje no mural e no Forms. Não exige perfil diferenciado; qualquer usuário autenticado pode criar reservas em nome de terceiros. (C-Q04.)

### Jornada C: reserva recorrente (série)

| # | Gatilho / Ação do usuário | Resultado esperado | Touchpoint / Tela | Pré-condição |
|---|---|---|---|---|
| C1 | Usuário autenticado seleciona "reserva recorrente" | Sistema apresenta opções de recorrência (diária, semanal, etc.) e período da série | Formulário de reserva: seção recorrência | Usuário autenticado |
| C2 | Preenche dados da série (sala, horário, frequência, data de fim) e confirma | Sistema valida cada ocorrência individualmente | Formulário de reserva | Sala e intervalo selecionados |
| C3 | Sistema apresenta resultado da validação | Ocorrências sem conflito: confirmadas. Ocorrências em conflito: sinalizadas. Série não é rejeitada integralmente | Tela de resultado da série | Validação concluída |
| C4 | Usuário decide individualmente sobre as ocorrências sinalizadas | Ocorrências confirmadas seguem para sync no Google Calendar; ocorrências rejeitadas ficam pendentes ou são removidas pelo usuário | Tela de gestão da série | Resultado C3 apresentado |

### Caminhos alternativos e de saída

- **ALT-1: sala indisponível / conflito na confirmação:** sistema bloqueia a confirmação e informa o conflito; [premissa] sugere alternativas de sala ou horário disponíveis.
- **ALT-2: cancelamento:** usuário cancela reserva confirmada; o sistema libera o slot imediatamente, remove o evento no Google Calendar e notifica participantes.
- **ALT-3: edição de reserva:** usuário edita dados ou horário; o sistema revalida conflito e, se aprovado, re-sincroniza com o Calendar.
- **ALT-4: falha de sincronização com o Google Calendar:** a reserva permanece confirmada no sistema (fonte de verdade: sync uma via confirmada, C-Q02); sistema sinaliza "sincronização pendente" e realiza retry com backoff. Alterações feitas diretamente no Google Calendar não retroalimentam o sistema (ver Seção 9, EC-02 e EC-04).
- **ALT-5: hábito antigo (mural / Forms):** canal descontinuado após até 2 semanas do go-live; reservas no canal antigo não são reconhecidas como válidas pelo sistema.

### Blueprint de serviço parcial

| Camada | Elementos |
|---|---|
| **Frente (visível ao usuário)** | Tela de disponibilidade em tempo real; formulário de criação/edição; confirmação de reserva; convite enviado ao Google Calendar dos participantes |
| **Bastidores (sistema)** | Cálculo de disponibilidade; validação anti-double-booking (atômica); chamada à API Google Calendar via OAuth; retry em caso de falha de sync |
| **Suporte / Pessoas** | Secretária: deixa de manter o mural físico e passa a usar o sistema para reservas em nome de terceiros; Technical Assessment OAuth Google Calendar: adiado (não-bloqueante para Fase B2) |

**Proveniência**
- **Confiança:** 80
- **Origem:** po_authored: C-Q02, C-Q03, C-Q04
- **Fonte:** contexto herdado das Seções 1-5 deste RP + confirmações PO (C-Q02: sync uma via; C-Q03: recorrência MVP + Jornada C adicionada; C-Q04: modelo flat: Jornada B simplificada sem perfil admin)
- **Situação:** respondida
- **Disposição:** po_authored: conf 80 >= mínimo 70; decisões de produto incorporadas
- **Observação:** Jornada B simplificada: sem perfil admin (C-Q04); secretária opera como qualquer usuário. Jornada C adicionada para reserva recorrente (C-Q03). ALT-4 confirmada como sync uma via (C-Q02). Notificação via convite do Google Calendar (confirmado). Sugestão de alternativas (ALT-1) permanece sem decisão fechada; definir antes da implementação.

---

## Seção 7: User stories + critérios de aceite
<!-- origination: id=user-stories; blocks=true; min-confidence=80; kind=capture -->
> Rubric: uma história por bloco de valor, "Como [persona], quero [ação], para
> [benefício]"; critérios de aceite em Given/When/Then, verificáveis por não-dev,
> com limites específicos. **Derivam dos passos da Jornada (Seção 6.5)**: cada
> passo do caminho principal gera ou valida uma história. origin=rascunho IA no fase de rascunho;
> o PO confirma.

> Nota: estas histórias derivam 1:1 dos passos da Jornada (Seção 6.5).

---

### US-01: autenticação via login social

**Como** qualquer colaborador da empresa,
**quero** acessar o sistema de reservas usando minha conta Google (login social),
**para** não precisar criar e memorizar uma nova senha.

**Critérios de aceite:**

- **Dado** que sou um colaborador com conta Google válida,
  **quando** acesso o sistema e escolho "Entrar com Google",
  **então** sou autenticado e redirecionado para a tela principal do sistema sem etapas adicionais de cadastro.

- **Dado** que não possuo conta Google ou o login social falha,
  **quando** tento acessar o sistema,
  **então** recebo mensagem de erro clara e não acesso o sistema.

---

### US-02: bloqueio de conflito (anti-double-booking) [CENTRAL]

**Como** qualquer usuário autenticado,
**quero** que o sistema impeça automaticamente a criação de reservas sobrepostas para a mesma sala,
**para** ter a garantia de que a sala estará disponível no horário reservado.

**Critérios de aceite:**

- **Dado** que a Sala A está confirmada das 14h às 15h,
  **quando** tento confirmar uma nova reserva para a Sala A das 14h30 às 15h30 (sobreposição parcial),
  **então** o sistema bloqueia a confirmação, exibe mensagem de conflito e não cria a reserva.

- **Dado** que a Sala A está confirmada das 14h às 15h,
  **quando** confirmo uma reserva para a Sala A das 15h às 16h (adjacente, sem sobreposição),
  **então** o sistema aceita e confirma a reserva normalmente.

- **Dado** que dois usuários tentam confirmar a mesma sala no mesmo instante (concorrência),
  **quando** as duas confirmações chegam simultaneamente,
  **então** a primeira é confirmada e a segunda recebe mensagem de conflito (first-commit-wins).

---

### US-03: consultar disponibilidade de salas

**Como** qualquer usuário autenticado,
**quero** consultar a disponibilidade de salas em tempo real,
**para** escolher sala e horário antes de criar uma reserva.

**Critérios de aceite:**

- **Dado** que estou autenticado,
  **quando** seleciono uma data e um intervalo de horário,
  **então** o sistema exibe quais salas estão disponíveis e quais estão ocupadas naquele intervalo.

- **Dado** que uma reserva é confirmada por outro usuário,
  **quando** consulto a disponibilidade em seguida,
  **então** a sala recém-reservada aparece como indisponível no intervalo correspondente.

---

### US-04: criar reserva

**Como** qualquer usuário autenticado,
**quero** criar uma reserva de sala informando os dados necessários (sala, data, horário de início e fim, título e participantes),
**para** garantir o uso exclusivo da sala no período escolhido.

**Critérios de aceite:**

- **Dado** que estou autenticado e a sala está disponível no intervalo,
  **quando** preencho todos os campos obrigatórios e confirmo,
  **então** a reserva é criada com status "Confirmada" e aparece imediatamente na consulta de disponibilidade.

- **Dado** que não preencho um campo obrigatório,
  **quando** tento confirmar,
  **então** o sistema exibe erro de validação e não cria a reserva.

---

### US-05: editar ou cancelar reserva (modelo flat)

**Como** qualquer usuário autenticado,
**quero** editar ou cancelar qualquer reserva existente antes do seu início,
**para** liberar ou ajustar o slot sem depender de perfil especial ou intervenção de terceiros.

**Critérios de aceite:**

- **Dado** que sou um usuário autenticado e há uma reserva confirmada que ainda não iniciou,
  **quando** edito o horário e confirmo a edição,
  **então** o sistema revalida o conflito; se não houver sobreposição, a reserva é atualizada e re-sincronizada com o Google Calendar.

- **Dado** que edito o horário e há conflito com outra reserva ativa,
  **quando** confirmo a edição,
  **então** o sistema rejeita a edição, mantém os dados originais e informa o conflito.

- **Dado** que sou um usuário autenticado e há uma reserva confirmada,
  **quando** cancelo a reserva,
  **então** o slot é liberado imediatamente, o evento é removido do Google Calendar e os participantes são notificados.

> **Nota de produto (C-Q04):** o modelo flat de permissões aumenta o risco de cancelamentos acidentais. Considerar confirmação explícita antes de cancelar (exclusão lógica ou diálogo de confirmação de dois passos): decisão de UX a definir antes da implementação.

---

### US-06: sincronização com o Google Calendar

**Como** participante de uma reunião reservada no sistema,
**quero** que a reserva e seu cancelamento reflitam automaticamente no meu Google Calendar,
**para** não precisar inserir os compromissos manualmente na agenda.

**Critérios de aceite:**

- **Dado** que uma reserva é confirmada com minha participação,
  **quando** a confirmação ocorre,
  **então** em até 2 minutos recebo convite de evento no Google Calendar com os dados da reserva.

- **Dado** que uma reserva confirmada é cancelada,
  **quando** o cancelamento ocorre,
  **então** em até 2 minutos o evento é removido do meu Google Calendar.

- **Dado** que a API do Google Calendar está indisponível no momento da confirmação,
  **quando** a confirmação ocorre,
  **então** a reserva é confirmada no sistema (fonte de verdade) e sinaliza "sincronização pendente"; o sistema realiza retry até concluir a sincronização (ver Seção 9, EC-02).

---

### US-07: reserva em nome de terceiro (modelo flat)

**Como** qualquer usuário autenticado (incluindo a secretária),
**quero** criar uma reserva informando outro colaborador como responsável e adicionando participantes,
**para** atender pedidos recebidos por WhatsApp ou pessoalmente sem que o solicitante precise acessar o sistema diretamente e sem necessitar de perfil especial.

**Critérios de aceite:**

- **Dado** que estou autenticado,
  **quando** crio uma reserva preenchendo o campo "responsável" com outro colaborador e confirmo,
  **então** a reserva é criada vinculada ao responsável indicado e o processo é ao menos tão simples quanto preencher o Google Forms atual.

- **Dado** que a reserva é criada em nome de terceiro,
  **quando** a confirmação ocorre,
  **então** o responsável indicado (e os participantes) recebem o convite do Google Calendar; o responsável aparece como dono da reserva.

---

### US-08: reserva recorrente (série)

**Como** qualquer usuário autenticado,
**quero** criar uma série de reservas recorrentes (ex.: reunião semanal toda terça-feira às 10h),
**para** não precisar criar manualmente cada ocorrência individualmente.

**Critérios de aceite:**

- **Dado** que estou autenticado,
  **quando** crio uma reserva recorrente informando frequência, horário e data de fim da série,
  **então** o sistema cria todas as ocorrências da série e valida cada uma individualmente quanto a conflitos.

- **Dado** que algumas ocorrências da série estão em conflito com reservas existentes,
  **quando** o sistema conclui a validação,
  **então** as ocorrências sem conflito são confirmadas; as ocorrências em conflito são sinalizadas (não rejeitadas); a série não é descartada integralmente.

- **Dado** que ocorrências foram sinalizadas como conflitantes,
  **quando** visualizo o resultado da criação da série,
  **então** o sistema apresenta quais ocorrências estão em conflito e me permite decidir individualmente (manter, remover ou resolver cada ocorrência).

---

**Proveniência**
- **Confiança:** 88
- **Origem:** po_authored: C-Q01, C-Q03, C-Q04
- **Fonte:** derivado dos passos da Jornada (Seção 6.5) e das Regras de Negócio (Seção 6) + confirmações PO (C-Q01: FCFS firmado; C-Q03: recorrência MVP, US-08 adicionada; C-Q04: modelo flat, US-05 e US-07 atualizadas)
- **Situação:** respondida
- **Disposição:** po_authored: conf 88 >= mínimo 80; decisões de produto incorporadas
- **Observação:** US-02 confirmada como história central (anti-double-booking). US-05 atualizada: qualquer usuário autenticado pode editar/cancelar qualquer reserva (modelo flat, C-Q04). US-07 simplificada: sem perfil admin; secretária opera como usuário comum (C-Q04). US-08 adicionada para reserva recorrente com validação por ocorrência (C-Q03). Participantes são campo disponível no formulário de criação (todos os usuários).

---

## Seção 8: Requisitos não-funcionais (NFRs)
<!-- origination: id=nfrs; blocks=true; min-confidence=70; kind=capture -->
> Rubric: preencher apenas as dimensões aplicáveis (checklist ISO/IEC 25010: não
> forçar as irrelevantes). O PO descreve o requisito de qualidade; viabilidade e
> "como" são do Technical Assessment. Sem ao menos uma dimensão preenchida,
> a seção NÃO está satisfeita.

> Dimensões ISO/IEC 25010 aplicáveis a este release. Todos os itens abaixo foram confirmados pelo PO no confirm loop (C-Q06..C-Q08). Viabilidade e "como" são do Technical Assessment, não descritos aqui.

| ID | Dimensão ISO/IEC 25010 | Requisito de qualidade | Observação |
|---|---|---|---|
| NFR-01 | **Confiabilidade / Integridade** [CRÍTICO] | O sistema nunca permite duas reservas confirmadas sobrepostas na mesma sala, inclusive sob concorrência de acessos. Propriedade não-negociável. | Verificável por teste de concorrência; implementação atômica (TA) |
| NFR-02 | **Desempenho / Sincronização** | Toda reserva confirmada ou cancelada deve refletir no Google Calendar em **<=2 minutos** (sync uma via: sistema → Calendar). | Âncora: Objetivo 4 deste RP; viabilidade é do TA; firmado C-Q08 |
| NFR-03 | **Desempenho / Tempo de resposta** | Consulta de disponibilidade: resposta em **<=2 s** (p95); confirmação de reserva: **<=3 s** (p95). | Requisito firmado pelo PO: C-Q08. Critério de aceite mensurável nos testes de carga |
| NFR-04 | **Usabilidade / Adoção** [CRÍTICO] | Criar uma reserva no sistema deve ser **mais simples do que preencher o Google Forms atual**; secretária e usuário comum devem conseguir criar uma reserva sem treinamento formal. | Verificável por validação qualitativa com a secretária (critério de aceite da Seção 11) |
| NFR-05 | **Usabilidade / Responsividade** | O sistema deve ser **responsivo e adaptado para dispositivos móveis** (fluxo atual ocorre majoritariamente via WhatsApp/celular). Breakpoints mínimos: mobile >= 360px, tablet >= 768px. | Requisito firmado pelo PO: C-Q07. Fluxo crítico de reserva testado em dispositivo móvel antes do release |
| NFR-06 | **Segurança / Autenticação** | Acesso somente via **login social** autenticado; cada reserva é atribuível a um usuário identificado. SSO corporativo está fora deste release. | Alinhado ao escopo da Seção 5 |
| NFR-07 | **Segurança / Privacidade** | Dados de participantes (nome, e-mail, horários de presença) tratados conforme **LGPD** básico: requisito deste release. Base legal a definir (legítimo interesse ou consentimento); política de retenção a estabelecer (ex.: 12 meses após a reunião); mecanismo de exclusão a pedido previsto. | Requisito firmado pelo PO: C-Q06. Revisão obrigatória com Jurídico/DPO antes do release |
| NFR-08 | **Compatibilidade / Interoperabilidade** | O sistema interopera exclusivamente com a **API do Google Calendar** neste release (uma via: sistema → Calendar); integração com Outlook está fora do escopo. | Alinhado ao escopo da Seção 5; TA OAuth adiado |
| NFR-09 | **Confiabilidade / Disponibilidade** | Disponibilidade **>=99%** durante o horário comercial; sem requisito de SLA 24/7. | Requisito firmado pelo PO: C-Q08. Critério de aceite mensurável nos testes de disponibilidade |
| NFR-10 | **Eficiência / Escala** | O sistema deve suportar até **~200 usuários**, com pico de carga no horário comercial (10h-16h). | Requisito firmado pelo PO: C-Q08. Dimensionamento baseado no perfil da empresa |

**Dimensões não aplicáveis neste release:** Manutenibilidade e Portabilidade são tratadas no nível do Technical Assessment (TA), não do RP de produto.

**Proveniência**
- **Confiança:** 82
- **Origem:** po_authored: C-Q06, C-Q07, C-Q08
- **Fonte:** contexto herdado das Seções 1-5 deste RP + confirmações PO (C-Q06: LGPD básico firmado; C-Q07: mobile responsiva firmada; C-Q08: alvos numéricos NFR-03/09/10 firmados)
- **Situação:** respondida
- **Disposição:** po_authored: conf 82 >= mínimo 70; todos os marcadores [premissa] removidos dos itens confirmados
- **Observação:** NFR-03 firmado (<=2s consulta / <=3s confirmação p95). NFR-05 firmado (mobile responsiva). NFR-07 firmado (LGPD básico: revisão com Jurídico/DPO obrigatória antes do release). NFR-09 firmado (>=99% horário comercial). NFR-10 firmado (~200 usuários). NFR-01, NFR-02, NFR-04, NFR-06, NFR-08 mantidos. Manutenibilidade/Portabilidade: N/A para RP de produto (TA). Viabilidade dos alvos numéricos é do Technical Assessment.

---

## Seção 9: Edge cases e modos de falha
<!-- origination: id=edge-cases; blocks=true; min-confidence=70; kind=capture -->
> Rubric: estados de erro, timeouts, permissões, concorrência. Para features de IA:
> comportamento do modelo e baixa confiança. Primeira classe, não rodapé. Cada
> item descreve o comportamento esperado do sistema (não apenas o que pode dar errado).

| ID | Cenário | Comportamento esperado do sistema |
|---|---|---|
| EC-01 | **Reservas concorrentes (condição de corrida):** dois usuários confirmam a mesma sala no mesmo instante | Exclusividade transacional: first-commit-wins (firmado, C-Q01). A primeira gravação persiste; a segunda recebe resposta de conflito e mensagem com alternativa de horário/sala. |
| EC-02 | **Falha da API do Google Calendar:** a API está indisponível no momento da confirmação ou cancelamento | A reserva é confirmada (ou cancelada) **localmente no sistema** (fonte de verdade); o sistema sinaliza status "sincronização pendente" e executa retry com backoff até concluir a sincronização. Nenhuma ação é revertida por falha de sync. (C-Q02.) |
| EC-03 | **Dupla fonte durante a transição:** mural físico ou Google Forms usados em paralelo ao sistema no período pós go-live | Canal antigo descontinuado formalmente após até 2 semanas do go-live; reservas feitas fora do sistema não são reconhecidas como válidas. Retirada física do mural e encerramento do Forms são passos do plano de migração. |
| EC-04 | **Alteração feita diretamente no Google Calendar:** usuário edita ou cancela o evento no Calendar sem atuar no sistema | O sistema é a fonte de verdade (sync uma via, C-Q02): alterações feitas no Google Calendar **não retroalimentam** o sistema neste release. O slot permanece ocupado no sistema mesmo que o evento tenha sido editado no Calendar. Recomendar aviso na UI alertando que o Calendar é espelho (somente leitura). |
| EC-05 | **Reserva recorrente com ocorrência em conflito:** uma das ocorrências de uma reserva recorrente colide com reserva existente | Dentro do MVP (firmado, C-Q03: RN-14/15/16): o sistema valida cada ocorrência individualmente e sinaliza quais estão em conflito; as demais são confirmadas. O usuário decide individualmente sobre as ocorrências conflitantes. |
| EC-06 | **Fuso horário / horário de verão (DST):** usuário cria reserva em horário ambíguo (transição DST) | O sistema exibe e armazena horários de forma não-ambígua, com indicação do fuso local. Reservas não devem ser criadas em intervalos ambíguos sem confirmação explícita. (Premissa de mono-fuso: confirmar antes da implementação.) |
| EC-07 | **Sala em manutenção:** sala indisponível por manutenção ou bloqueio administrativo | Estado de manutenção bloqueia criação de novas reservas para a sala; reservas existentes devem ser realocadas manualmente (requer notificação aos responsáveis). |
| EC-08 | **Participante externo sem login:** cliente ou visitante externo tenta criar reserva no sistema | Externos **não reservam** salas diretamente (portal externo está fora do escopo deste release). O organizador interno cria a reserva e convida o externo via evento do Google Calendar (confirmado, C-Q02). |
| EC-09 | **Edição que cria conflito:** usuário edita o horário de uma reserva e o novo horário colide com outra reserva ativa | O sistema aplica a mesma validação anti-double-booking da confirmação: rejeita a edição, mantém os dados originais e informa o conflito ao usuário. |
| EC-10 | **Reserva em nome de terceiro ausente:** criação de reserva em nome de colaborador que não está disponível para confirmar | Qualquer usuário autenticado pode criar reserva em nome de terceiro usando o campo "responsável" (modelo flat, C-Q04); a reserva é criada com o colaborador indicado como responsável real; o sistema registra quem operou a criação. Sem necessidade de perfil admin. |
| EC-11 | **Sistema fora do ar ou sem conectividade:** usuário tenta acessar ou confirmar reserva enquanto o sistema está indisponível | Falha segura e visível: o sistema exibe mensagem de indisponibilidade; nenhuma confirmação falsa é gerada; o usuário não deve recorrer ao mural como fallback (canal descontinuado). |
| EC-12 | **Reserva no passado ou fora da janela permitida:** usuário tenta criar reserva para data/hora passada ou além da antecedência máxima | O sistema rejeita a criação com mensagem explicativa; nenhuma reserva é criada. (RN-09/10/11 firmadas, C-Q05.) |
| EC-13 | **Divergência silenciosa entre Calendar e sistema:** usuário edita evento no Google Calendar sem atualizar o sistema | O sistema permanece como fonte de verdade; a divergência não é detectada automaticamente neste release (sync uma via, C-Q02). A UI deve exibir aviso informando que o Calendar é espelho somente de leitura e que alterações devem ser feitas no sistema. |

**Proveniência**
- **Confiança:** 80
- **Origem:** po_authored: C-Q01, C-Q02, C-Q03, C-Q04, C-Q05
- **Fonte:** derivado das Regras de Negócio (Seção 6) e da Jornada (Seção 6.5) + confirmações PO (C-Q01: EC-01 first-commit-wins firmado; C-Q02: EC-04 sync uma via + EC-13 adicionado; C-Q03: EC-05 recorrência promovida para MVP; C-Q04: EC-10 modelo flat; C-Q05: EC-12 parâmetros temporais firmados)
- **Situação:** respondida
- **Disposição:** po_authored: conf 80 >= mínimo 70; decisões de produto incorporadas
- **Observação:** EC-01 firmado (first-commit-wins). EC-04 corrigido (sync uma via: sem reconciliação de volta do Calendar). EC-05 promovido para MVP (recorrência IN, validação por ocorrência). EC-08 confirmado (externos via convite do Calendar). EC-10 simplificado (modelo flat, sem admin). EC-13 adicionado (divergência silenciosa Calendar: aviso na UI). EC-06 (mono-fuso) permanece como ponto de atenção; confirmar antes da implementação.

---

## Seção 10: Métricas de sucesso (primária · secundária · guardrail)
<!-- origination: id=metrics; blocks=true; min-confidence=70; kind=capture -->
> Rubric: valores projetados: o baseline que metrics.md confronta com o medido
> pós-rollout. Inclua indicadores leading e lagging e ao menos um guardrail (a
> métrica que não pode piorar). Cada meta carrega a confiança da projeção.

| Tipo | Métrica | Baseline (campo) | Meta pós-rollout | Prazo | Confiança da projeção |
|---|---|---|---|---|---|
| **Primária (lagging)** | Conflitos de agendamento (double-bookings) por semana | ~1,8/sem (D003/Q008: 9 conflitos/5sem) | **0** | 4 semanas após go-live | Alta: baseline de campo confirmado |
| **Primária (lagging)** | Novos adiamentos de negócios causados por conflito de sala | 9 em 5 semanas (D005/Q012) | **0** | 8 semanas após go-live | Média: depende de acompanhamento comercial (D02) |
| **Leading** | Adoção do sistema (% de reservas criadas no sistema vs. total) | 0% (100% manual) | **100%** | 2 semanas após go-live (mural e Forms descontinuados) | Alta: critério de migração |
| **Guardrail** | Volume total de reservas realizadas por semana | Baseline a medir na semana pré-go-live | Não deve cair em relação ao baseline | Semana 1 pós-go-live | Média: risco de subnotificação se adoção resistida |
| **Guardrail** | Carga de suporte da secretária (ocorrências de remarcar por semana) | Baseline a medir na semana pré-go-live | Não deve aumentar em relação ao baseline | 4 semanas após go-live | Média: proxy de adoção e de falhas no sistema |

**Nota sobre baseline financeiro (referência):** pipeline ~R$ 700 mil; R$ 111 mil já perdidos (não recuperáveis); R$ 90 mil em risco (monitorar junto com D02: liderança comercial). Recuperação do pipeline em risco é indicador de resultado de negócio, não métrica operacional do sistema.

**Proveniência**
- **Confiança:** 80
- **Origem:** herdada: I006
- **Fonte:** intake-record v3 (demand-summary / triage-criteria: D003/Q008 + D005/Q012) + origination-record (impact: Q006/Q010)
- **Situação:** herdada
- **Disposição:** herdada: baseline de campo disponível; metas propostas aguardam confirmação do PO
- **Observação:** Metas métricas devem ser comprometidas pelo PO. Baseline considerado EXTRAÍDO (campo real: D003 + D005). Guardrails de volume e carga de secretária dependem de medição na semana pré-go-live. Monitorar R$ 90 mil em risco junto com D02 (liderança comercial).

---

## Seção 11: Critérios de sucesso e aceite (do release)
<!-- origination: id=release-criteria; blocks=true; min-confidence=70; kind=capture -->
> Rubric: indicadores de alto nível que definem "concluído e valioso" para este
> release: distintos das métricas contínuas da Seção 10. Deve cobrir ao menos
> as dimensões Negócio, Qualidade e UX. Critérios genéricos ("funciona bem") NÃO
> estão satisfeitos: exija valor-alvo mensurável.

| Dimensão | Critério | Valor-alvo / Verificação |
|---|---|---|
| **Negócio** | Zero double-bookings registrados desde o go-live | 0 conflitos nas 4 primeiras semanas pós-rollout; verificado por monitoramento do sistema e ausência de relatos da secretária |
| **Negócio** | 100% das reservas centralizadas no sistema | Mural físico e Google Forms descontinuados em até 2 semanas; nenhuma reserva fora do sistema; confirmação da secretária |
| **Negócio** | Pelo menos uma reunião comercial previamente travada por conflito de sala remarcada e realizada | Acompanhamento com liderança comercial (D02) nas 8 semanas pós-rollout |
| **Qualidade** | Sistema retorna conflito em 100% dos cenários de double-booking testados | Cobertura de teste: todos os cenários de conflito documentados na Seção 9 (edge cases) retornam erro e impedem a reserva |
| **Qualidade** | Integração com o Google Calendar reflete reservas em <=2 minutos | Teste funcional de integração: criar/cancelar reserva e verificar atualização no Google Calendar em até 2 min |
| **UX** | Secretária confirma que criar uma reserva no novo sistema é mais simples do que preencher o Google Forms | Validação qualitativa com a secretária (Persona 4) após onboarding; critério: declaração explícita de preferência pelo sistema |

**Proveniência**
- **Confiança:** 75
- **Origem:** herdada: I007
- **Fonte:** intake-record v3 (triage-decision / demand-summary / constraints / demand-nature: D003/Q010/Q011 + D005/Q012)
- **Situação:** herdada
- **Disposição:** herdada: conf no mínimo 75; critérios derivados de triage Product Ready D007
- **Observação:** conf 75 = mínimo aceito. Section Drafter deve detalhar critérios de aceite por funcionalidade (Seção 7) para elevar conf antes do release. Critério de UX depende de onboarding da secretária; planejar sessão de validação.

---

## Seção 12: Riscos e dependências (de produto e negócio)
<!-- origination: id=risks; blocks=true; min-confidence=70; kind=capture -->
> Rubric: riscos de produto, negócio, adoção, externos e compliance. Riscos
> técnicos migram para o Technical Assessment. Cada risco tem probabilidade,
> impacto e mitigação. Dependências de produto/negócio listadas separadamente.

### Riscos

| ID | Risco | Tipo | Probabilidade | Impacto | Mitigação |
|---|---|---|---|---|---|
| R01 | Baixa adoção / resistência ao sistema novo: usuários continuam usando o mural ou o WhatsApp informalmente | Adoção | Alta | Alto | Onboarding ativo; secretária como agente de mudança; sistema deve ser mais simples que o Forms (critério de UX); mural retirado fisicamente após go-live |
| R02 | Dependência da secretária para onboarding e validação de UX: ausência ou resistência dela compromete a migração | Externo / Adoção | Média | Alto | Envolver a secretária desde o início da Fase B2 (design e teste); incluir como stakeholder formal; planejar sessão de validação de UX antes do go-live |
| R03 | Retorno ao mural em paralelo: usuários mantêm o processo antigo como "segurança" mesmo após o go-live | Adoção | Média-Alta | Alto | Comunicação formal de descontinuação do mural; retirada física do mural e encerramento do Forms após 2 semanas; monitorar guardrail de adoção (100% das reservas no sistema) |
| R04 | R$ 90 mil em risco pode não ser recuperado: o negócio travado não fecha mesmo após resolução dos conflitos | Negócio | Média | Médio | Monitorar junto com D02 (liderança comercial); resultado de negócio é de responsabilidade comercial, não do sistema; RP registra como risco residual |
| R05 | Escopo creep de integração: pressão para adicionar Outlook, SSO ou outras integrações durante a Fase B2 | Produto / Escopo | Baixa-Média | Médio | Seção 5 (Escopo Excluído) é a referência formal; qualquer adição requer aprovação explícita do PO e reavaliação do Technical Assessment |

### Dependências

| ID | Dependência | Tipo | Dono | Impacto se não resolvida |
|---|---|---|---|---|
| D01 | Secretária disponível para onboarding, validação de UX e migração do processo manual | Externo / Adoção | Secretária / Facilities | Risco R02 e R03 se materializam; critério de UX da Seção 11 não verificável |
| D02 | Liderança comercial disponível para acompanhar recuperação do pipeline (R$ 90k em risco) e confirmar adiamentos | Negócio | Liderança Comercial | Critério de negócio da Seção 11 (reunião comercial remarcada) não verificável; R04 não monitorado |
| D03 | Google Calendar API disponível e fluxo OAuth de-arriscado pelo Technical Assessment | Técnico / Externo | CTO / Tech Lead (TA adiado) | Integração com Google Calendar (uma via: sistema → Calendar) não entregável; escopo de integração deve ser revisado |

**Nota sobre riscos técnicos:** riscos técnicos do fluxo OAuth do Google Calendar migram para o Technical Assessment (Seção 14: Referência ao Technical Assessment). D03 está vinculada ao TA adiado.

**Proveniência**
- **Confiança:** 75
- **Origem:** herdada: I008
- **Fonte:** origination-record (constraints: Q009) + intake-record v3 (demand-nature / constraints / cto-escalation: D003/Q010/Q011)
- **Situação:** herdada
- **Disposição:** herdada: 5 riscos e 3 dependências registrados
- **Observação:** R04 vinculado ao impacto R$ 90 mil; monitorar junto às métricas (I006). D03 vinculada ao TA OAuth adiado. Riscos técnicos do OAuth migram para o Technical Assessment.

---

## Seção 13: Avaliação preliminar de esforço e custo
<!-- origination: id=effort-estimate; blocks=false; min-confidence=0; kind=capture -->
> Rubric: somente uso interno: o chute do PO para sustentar sequenciamento. O
> número firme vem do CTO no Technical Assessment. Não é compromisso contratual
> nem material para cliente. Confiança esperada: baixa (rascunho IA ou po_authored
> sem dados firmes).

> **[Estimativa preliminar adiada: disposição honesta]**
>
> Nenhum dado de prazo ou orçamento foi informado no origination-record nem no intake-record v3. A estimativa preliminar de esforço e custo está **adiada ao CTO/Tech Lead**: o número firme virá do Technical Assessment (ver Referência ao Technical Assessment abaixo). Esta seção **não bloqueia o freeze** do RP (blocks=false). Ela bloqueia a execução com compromisso firme de prazo/custo.

[A preencher pelo CTO / Tech Lead no Technical Assessment: estimativa firme de esforço e custo para sequenciamento interno]

**Proveniência**
- **Confiança:** 0
- **Origem:** adiada: I010
- **Fonte:** ausência de cobertura upstream (prazo/orçamento não informados no origination-record nem no intake-record v3)
- **Situação:** adiada: aguarda CTO/Tech Lead (Technical Assessment)
- **Disposição:** adiada: estimativa firme é do Technical Assessment; esta seção não bloqueia o freeze do RP (blocks=false)
- **Observação:** Disposição honesta per instrução do confirm loop: "Estimativa preliminar adiada ao CTO/Tech Lead (sem dado de prazo/orçamento no upstream); a estimativa firme é do Technical Assessment." Não-bloqueante para gate do RP.

---

## Seção 14: Roadmap sugerido
<!-- origination: id=roadmap; blocks=false; min-confidence=0; kind=capture -->
> Rubric: visão de sequenciamento de valor além deste release. Items adiados da
> Seção 5 alimentam fases futuras. MVP é este release; Fase 2 e Fase 3 são
> backlog futuro. Não é compromisso de entrega.

### MVP (este release)

- Sistema digital de reserva de salas de reunião (CRUD completo).
- Integração com o Google Calendar, uma via (sistema → Calendar; sincronização em até 2 min).
- Autenticação simples (login social).
- Regras automáticas de anti-double-booking.
- Migração e descontinuação do processo manual (mural físico + Google Forms via WhatsApp).

### Fase 2 (backlog futuro)

- Integração com Outlook / Microsoft 365 (descartada neste release, retorna como demanda futura).
- Analytics e relatórios de ocupação de salas (dashboards históricos, métricas de uso).
- Lembretes automáticos de reservas.

### Fase 3 (backlog futuro)

- SSO corporativo (autenticação empresarial).
- Outros recursos físicos (estacionamento, equipamentos, salas especiais).

**Proveniência**
- **Confiança:** 65
- **Origem:** herdada: I009
- **Fonte:** intake-record v3 (itens "Excluído": derivação estrutural)
- **Situação:** herdada
- **Disposição:** herdada: esqueleto derivado; conf 65, não-bloqueante
- **Observação:** conf 65: roadmap é esqueleto derivado dos itens excluídos do intake. Section Drafter deve elaborar fases com detalhamento de prioridade e critérios de entrada para elevar conf >= 75. Não-bloqueante para Fase B2.

---

## Referência ao Technical Assessment
<!-- origination: id=tech-assessment-ref; blocks=false; min-confidence=0; kind=derived; inputs=scope,business-rules,nfrs,risks -->
> Rubric: ponte para o artefato do CTO: status + veredito + link, NÃO conteúdo.
> Se a escalada for requisitada, congela só com Disposition=adiada (TA pendente,
> fora do escopo desta ferramenta) ou Status=Assinado quando o TA existir.

| Campo | Valor |
|---|---|
| **Escalada requisitada?** | SIM: Technical Assessment LEVE |
| **Status** | requisitado |
| **Veredito** | (pendente) |
| **Link** | (pendente) |
| **Freeze** | PROVISÓRIO: a tech-assessment skill ainda não existe; TA pendente, fora do escopo atual de tooling |

### Gatilhos presentes (justificam a escalada LEVE)

1. **Segurança / autenticação:** login social / OAuth (NFR-06): o sistema autentica usuários via login social; o modelo de credencial e os escopos OAuth precisam ser determinados pelo CTO/Tech Lead antes do congelamento técnico.
2. **Integração externa com incógnitas:** Google Calendar via OAuth, uma via (Escopo §5, Objetivo 4, NFR-02/08, US-06, dependência D03): a integração envolve variáveis de configuração do ambiente real (Workspace, escopos disponíveis, modelo de credencial) que só podem ser confirmadas com acesso ao ambiente da organização.

### Gatilhos ausentes (delimitam o escopo do TA como LEVE)

- Sem nova infraestrutura crítica.
- Sem multi-tenancy ou isolamento de dados entre organizações.
- Sem IA ou runtime experimental.
- Integração de-arriscada no Discovery (somente Google Calendar, sem Outlook, sem SSO corporativo; login social aceito como premissa confirmada em D003/Q010).

### Contexto de natureza (Híbrido)

O TA deve descobrir o ambiente real antes de confirmar o modelo de integração: workflow da secretária, configuração do Google Workspace da organização e escopos OAuth disponíveis para aplicações de terceiros. Não há premissa greenfield (nova capacidade): o sistema se integra a um ambiente organizacional existente com configurações próprias.

### Escopo do TA LEVE (4 pontos)

**(a) Viabilidade do fluxo OAuth Google Calendar:** quais escopos são necessários (`calendar.events` ou mais amplo); se o Google Workspace da organização permite concessão a aplicações de terceiros; qual o modelo de credencial adequado (service account com delegação de domínio vs. delegação por usuário autenticado).

**(b) Modelo de sincronização (uma via: sistema → Calendar):** confirmar que a estratégia "sistema = fonte de verdade; Calendar = espelho; alterações feitas diretamente no Calendar NÃO refletem de volta neste release" é viável e sustentável sem webhooks / push que introduzam incógnitas adicionais.

**(c) Atomicidade e anti-double-booking sob concorrência:** confirmar a decisão de arquitetura para garantir a propriedade first-commit-wins (RN-05, EC-01, NFR-01) sob acessos concorrentes; esta é uma decisão de arquitetura, não de produto.

**(d) Orçamento de latência de sincronização:** confirmar se o SLA de <=2 minutos (NFR-02, Objetivo 4, US-06) é alcançável com polling ou com push da API do Google Calendar, considerando os limites de quota da API e o ambiente real da organização.

### Nota operacional

Quando o TA for executado: atualizar **Status = assinado** e registrar o **Veredito** (viável / viável-com-ressalvas / inviável-como-escopado). A dívida está registrada no `owes` do índice da iniciativa. O TA é LEVE e **não bloqueia as seções de produto do RP** (Seções 1-13), mas o **freeze pleno exige Status = assinado**. O freeze atual é PROVISÓRIO.

**Proveniência**

**Confiança · Disposição:** 85 · adiada (freeze provisório: TA pendente, fora do escopo atual de tooling)

Disposição autorizada pelo Escalation Flagger. O TA LEVE cobre exclusivamente OAuth Google Calendar (4 pontos acima); não há bloqueio às seções de produto. Quando o TA skill existir e for executado, registrar aqui o veredito e promover Status para assinado, encerrando o freeze provisório. Origem composta: intake-record v3 (cto-escalation / triage-decision: D003/Q010) + qa-log.md (I011) + disposição do Escalation Flagger (2026-06-07).

<!-- END OF DOCUMENT -->
