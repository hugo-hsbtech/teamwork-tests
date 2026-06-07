<!--
  qa-log.md — Ledger Writer sole output
  Phase : readiness (Act 2)
  Initiative : RP-2026-001 · Sistema de Reserva de Salas
  Rev : 2
  As-of-rev : 1
  Readiness : 74% (handoff score; readiness canônica aguarda nova rodada do Confidence Auditor)
  Gate : OPEN — seção bloqueante: effort-estimate (sem cobertura upstream)
  Blocking sections : effort-estimate
  Non-blocking gaps : roadmap (esqueleto parcial, conf 65)
  Confirmações PO Rev2 : C-Q01–C-Q08 registradas (business-rules, user-journey,
         user-stories, nfrs, edge-cases promovidas de ai_drafted → po_authored)
  END-SENTINEL: END-OF-LOG
-->

# QA Log — readiness · RP-2026-001

## Cabeçalho de Prontidão

| Campo | Valor |
|---|---|
| Iniciativa | RP-2026-001 — Sistema de Reserva de Salas de Reunião |
| Rev | 2 |
| As-of-rev | 1 |
| Readiness | **74%** _(handoff score — Score Canônico aguarda nova rodada do Confidence Auditor)_ |
| Gate | OPEN |
| Seções bloqueantes | `effort-estimate` (sem cobertura upstream; aguarda drafter/PO) |
| Seções não-bloqueantes pendentes | `roadmap` (conf 65, esqueleto derivado) |
| Confirmações PO (Rev 2) | `business-rules`, `user-journey`, `user-stories`, `nfrs`, `edge-cases` — promovidas de ai_drafted → po_authored via C-Q01–C-Q08 |
| Conflitos resolvidos | C2 (premissas product) e C4 (sync one-way) — ver C-Q02 |

---

## Contexto da Iniciativa

- **ID**: RP-2026-001
- **Natureza**: Híbrida (produto interno + processo operacional)
- **Upstream consumido**: origination-record + intake-record v3; triage Product Ready D007
- **Impacto quantificado**: R$ 111k perdidos/ano · R$ 90k em risco
- **Integração confirmada**: somente Google Calendar
- **TA**: Leve — OAuth Google Calendar deferido (dono: CTO/Tech Lead)
- **Premissas abertas**: NENHUMA (todas resolvidas em D003 + D005)
- **Item deferred único**: Technical Assessment leve (OAuth), não-bloqueante para Fase B2

---

## Manifesto de Herança — Entradas Herdadas do Stage Inheritor

> Cada entrada abaixo é um item do índice de herança.
> `Origin: inherited` em todos.
> Seções sem cobertura upstream são marcadas como `status: pending`.

---

### I001 · exec-summary

```
ID            : I001
Section       : exec-summary
Origin        : inherited
Status        : inherited
Confidence    : 80
Source        : origination (problem / reach / impact) + intake (demand-summary / triage / demand-nature / constraints)
Disposition   : inherited — PO confirma parágrafo "o que será construído"
Targets       : exec-summary
Hint          : Conteúdo completo no documento; este índice registra proveniência e conf.
                PO deve validar o parágrafo de síntese antes de publicar.
```

---

### I002 · context-problem

```
ID            : I002
Section       : context-problem
Origin        : inherited
Status        : inherited
Confidence    : 80
Source        : origination (problem / reach / impact) + intake (demand-summary / demand-nature)
Disposition   : inherited — conf ≥ mín 80; subseção "Limitações" inferida estruturalmente
Targets       : context-problem
Hint          : Subseção "Limitações" derivada por inferência estrutural; marcar como INFERRED
                na seção para revisão do PO se necessário.
```

---

### I003 · objectives

```
ID            : I003
Section       : objectives
Origin        : inherited
Status        : inherited
Confidence    : 85
Source        : origination (impact) + intake (demand-summary / constraints / triage)
Disposition   : inherited — metas e prazos propostos; PO confirma
Targets       : objectives
Hint          : Metas e prazos são propostos — requerem confirmação explícita do PO antes
                de promover para status "answered".
```

---

### I004 · personas

```
ID            : I004
Section       : personas
Origin        : inherited
Status        : inherited
Confidence    : 76
Source        : origination (reach) + intake (demand-nature)
Disposition   : inherited — persona secretária/facilities enriquecida; conf abaixo de 80,
                não-bloqueante mas recomenda enriquecimento via entrevista
Targets       : personas
Hint          : conf 76 < 80 — considerar entrevista rápida com secretária/facilities para
                elevar conf antes de user-stories. Não-bloqueante para Fase B2.
```

---

### I005 · scope

```
ID            : I005
Section       : scope
Origin        : inherited
Status        : inherited
Confidence    : 80
Source        : intake (constraints / demand-nature / triage)
Disposition   : inherited — conf ≥ mín 75; PO confirma item a item
Targets       : scope
In-scope      : CRUD reserva · integração Google Calendar · auth simples ·
                migração processo manual · regras anti-double-booking
Out-of-scope  : Outlook · SSO · outros recursos de calendário
Hint          : PO deve validar cada item in/out explicitamente; qualquer adição dispara
                risco R05 (escopo creep).
```

---

### I006 · metrics

```
ID            : I006
Section       : metrics
Origin        : inherited
Status        : inherited
Confidence    : 80
Source        : intake (demand-summary / triage) + origination (impact)
Disposition   : inherited — baseline de campo disponível; metas propostas aguardam PO
Targets       : metrics
Baseline      : 1,8 conflitos/sem · ~3 dias resolução · 9 adiamentos/tri ·
                R$ 700k reuniões/ano · R$ 111k perdidos · R$ 90k em risco
Metas         : propostas (PO confirma)
Hint          : Metas métricas devem ser comprometidas pelo PO; baseline considerado EXTRACTED
                (campo real). Registrar como INFERRED se origem não for auditável.
```

---

### I007 · release-criteria

```
ID            : I007
Section       : release-criteria
Origin        : inherited
Status        : inherited
Confidence    : 75
Source        : intake (triage / demand-summary / constraints / demand-nature)
Disposition   : inherited — conf no mínimo 75; critérios derivados de triage Product Ready D007
Targets       : release-criteria
Hint          : conf 75 = mínimo; Section Drafter deve detalhar critérios de aceite por
                funcionalidade para elevar conf antes de release.
```

---

### I008 · risks

```
ID            : I008
Section       : risks
Origin        : inherited
Status        : inherited
Confidence    : 75
Source        : origination (constraints) + intake (demand-nature / constraints / cto-escalation)
Disposition   : inherited — 5 riscos + 3 dependências registrados
Targets       : risks
Riscos        : R01 adoção · R02 dependência secretária · R03 retorno ao mural ·
                R04 R$90k não recupera · R05 escopo creep
Dependências  : D01 secretária · D02 comercial · D03 Google Calendar
Hint          : R04 vinculado ao impacto R$90k; monitorar junto a metrics (I006).
                D03 vinculada ao TA OAuth deferido.
```

---

### I009 · roadmap

```
ID            : I009
Section       : roadmap
Origin        : inherited
Status        : inherited
Confidence    : 65
Source        : intake (itens "Excluído" — derivação estrutural)
Disposition   : inherited — esqueleto; conf 65 < 75 (mín), não-bloqueante
Targets       : roadmap
Hint          : conf 65 — roadmap é esqueleto derivado dos itens excluídos do intake.
                Section Drafter deve elaborar fases/sprints para elevar conf ≥ 75.
                Classificado como NON-BLOCKING por não impedir Fase B2.
```

---

### I010 · effort-estimate

```
ID            : I010
Section       : effort-estimate
Origin        : inherited
Status        : pending
Confidence    : 0
Source        : — (sem cobertura upstream; prazo/orçamento não informados)
Disposition   : pending — aguarda drafter/PO
Targets       : effort-estimate
Hint          : SEÇÃO BLOQUEANTE para gate final. Nenhum dado de prazo ou orçamento
                disponível no origination-record nem no intake-record v3.
                Ação: PO ou Tech Lead deve fornecer estimativa antes do gate de prontidão.
```

---

### I011 · inherited-readiness (derived)

```
ID            : I011
Section       : inherited-readiness
Origin        : derived (Stage Inheritor)
Status        : answered
Confidence    : 90
Source        : handoff readiness 74% — calculado pelo Stage Inheritor sobre D003+D005
Disposition   : answered
Targets       : header-summary
Readiness     : 74% — HANDOFF SCORE (score de passagem de fase, não o canônico de prontidão)
Premissas     : NENHUMA premissa aberta (todas resolvidas em D003+D005)
Deferred      : Technical Assessment LEVE (OAuth Google Calendar) — dono CTO/Tech Lead;
                não-bloqueante para Fase B2
Hint          : ATENÇÃO (Rev 2): "74%" é o score de handoff do Stage Inheritor, não o score
                canônico de prontidão da fase atual. O score canônico será emitido pelo
                Confidence Auditor após as confirmações C-Q01–C-Q08. Gap Reporter e
                Packager devem rotular este valor como "handoff score" e aguardar nova
                rodada do Auditor para o número canônico desta fase.
```

---

### I012 · seções-nao-cobertas (Fase B2)

```
ID            : I012
Section       : meta-gap
Origin        : inherited
Status        : parcialmente-coberta (Rev 2)
Confidence    : —
Source        : ausência de cobertura no upstream
Disposition   : parcialmente-coberta — PO forneceu confirmações C-Q01–C-Q08 (Rev 2);
                Section Drafter deve incorporar ao rascunho das seções
Targets       : business-rules · user-journey · user-stories · nfrs · edge-cases
Hint          : Rev 2: as seções listadas receberam cobertura PO via loop de confirmação
                (C-Q01–C-Q08). Status promovido de ai_drafted → po_authored para as
                decisões registradas. Section Drafter deve usar C-Q01–C-Q08 como insumo
                primário ao elaborar os rascunhos finais. Seções permanecem bloqueantes
                para gate final até aprovação do Drafter + Auditor.
```

---

---

## Confirmações do PO — Loop de Confirmação (Rev 2)

> Origem: `po_authored` em todos. Status: `answered`. Geradas no confirm loop do Act 2.

---

### C-Q01 · Precedência RN-13 — FCFS e pedido de realocação

```
ID            : C-Q01
Section       : business-rules · user-stories
Origin        : po_authored
Status        : answered
Mode          : open
Targets       : business-rules, user-stories
Answer        : FCFS (primeiro a confirmar vence) é o padrão de precedência de reservas.
                Liderança e diretoria NÃO sobrescrevem automaticamente reservas de outros
                usuários. Caso desejem a sala, podem PEDIR realocação via secretária ou
                sistema (fluxo facilitado, mas não automático nem garantido).
Choice        : —
Disposition   : answered
Confidence    : 95
Source        : PO — confirm loop Act 2
Hint          : Resolve RN-13. Section Drafter deve codificar: (a) regra FCFS como padrão
                explícito; (b) fluxo de "pedido de realocação" como feature facilitadora,
                sem garantia de resultado. Nenhuma hierarquia organizacional confere
                prioridade automática.
```

---

### C-Q02 · Sincronização Google Calendar — uma via

```
ID            : C-Q02
Section       : business-rules · user-journey · edge-cases
Origin        : po_authored
Status        : answered
Mode          : open
Targets       : business-rules, user-journey, edge-cases
Answer        : Sincronização UMA VIA: sistema → Google Calendar. O sistema é a fonte de
                verdade; grava eventos no Calendar. Alterações feitas diretamente no Google
                Calendar NÃO refletem de volta neste release.
Choice        : —
Disposition   : answered
Confidence    : 95
Source        : PO — confirm loop Act 2
Hint          : RESOLVE conflito C4 do Auditor: exec-summary e scope mencionavam
                "bidirecional" — corrigir para "uma via" em ambas as seções.
                Doc Updater: atualizar exec-summary e scope antes de publicar.
                Edge-case: usuário edita no Calendar → divergência silenciosa; seção
                edge-cases deve documentar este cenário e recomendar aviso na UI.
```

---

### C-Q03 · Recorrência — dentro do MVP

```
ID            : C-Q03
Section       : business-rules · user-stories · edge-cases
Origin        : po_authored
Status        : answered
Mode          : open
Targets       : business-rules, user-stories, edge-cases
Answer        : Suporte a séries recorrentes está DENTRO DO MVP. Validação ocorre
                ocorrência a ocorrência; ocorrências em conflito são SINALIZADAS ao usuário
                (não rejeita a série toda). EC-05 entra no escopo do MVP.
Choice        : —
Disposition   : answered
Confidence    : 95
Source        : PO — confirm loop Act 2
Hint          : EC-05 promovido para MVP. Section Drafter deve incluir: (a) regra de
                validação por ocorrência; (b) UX de sinalização de conflito parcial na
                série; (c) decisão do usuário para cada ocorrência conflitante.
                Impacto em scope (I005): adicionar "reservas recorrentes" ao in-scope.
```

---

### C-Q04 · Permissões — todos editam tudo

```
ID            : C-Q04
Section       : business-rules · user-stories
Origin        : po_authored
Status        : answered
Mode          : open
Targets       : business-rules, user-stories
Answer        : Qualquer usuário autenticado pode editar ou cancelar qualquer reserva.
                Não há perfil admin especial para secretária neste release. A secretária
                reserva e edita como qualquer outro usuário, sem permissões diferenciadas.
Choice        : —
Disposition   : answered
Confidence    : 95
Source        : PO — confirm loop Act 2
Hint          : Simplifica RN-07, RN-08 e US-07. Section Drafter: remover distinção de
                perfil admin/secretária das regras de permissão. Registrar como decisão
                explícita de produto — pode ser revisada em release futuro (R05 escopo creep).
                Nota: modelo flat de permissões aumenta risco de cancelamentos acidentais;
                considerar soft-delete ou confirmação de cancelamento na UX.
```

---

### C-Q05 · Parâmetros temporais — aceitos

```
ID            : C-Q05
Section       : business-rules
Origin        : po_authored
Status        : answered
Mode          : open
Targets       : business-rules
Answer        : Parâmetros propostos ACEITOS: janela de reserva 08h–19h dias úteis;
                duração mínima 15 min / máxima 8h; antecedência máxima ~90 dias;
                reservas apenas no futuro (não retroativas).
Choice        : —
Disposition   : answered
Confidence    : 95
Source        : PO — confirm loop Act 2
Hint          : Resolve RN-09, RN-10 e RN-11 — deixam de ser premissa e tornam-se
                regras confirmadas. Section Drafter deve codificar como restrições
                hard no sistema (validação obrigatória). Antecedência "~90 dias" pode
                ser parametrizável — definir valor exato (90 dias corridos ou úteis)
                antes da implementação.
```

---

### C-Q06 · LGPD — patamar básico no release

```
ID            : C-Q06
Section       : nfrs
Origin        : po_authored
Status        : answered
Mode          : open
Targets       : nfrs
Answer        : SIM — patamar básico de LGPD é requisito DESTE release. Dados de
                participantes (nome, e-mail, horários de presença) devem ter base legal
                definida e retenção adequada.
Choice        : —
Disposition   : answered
Confidence    : 95
Source        : PO — confirm loop Act 2
Hint          : Confirma NFR-07. Section Drafter deve detalhar: base legal aplicável
                (legítimo interesse ou consentimento), política de retenção de dados de
                reservas (ex.: 12 meses após a reunião), e mecanismo de exclusão a pedido.
                Jurídico/DPO deve revisar antes do release.
```

---

### C-Q07 · Mobile — responsiva é requisito

```
ID            : C-Q07
Section       : nfrs
Origin        : po_authored
Status        : answered
Mode          : open
Targets       : nfrs
Answer        : SIM — interface responsiva/mobile-friendly é requisito deste release,
                coerente com o hábito de uso via WhatsApp/celular dos usuários.
Choice        : —
Disposition   : answered
Confidence    : 95
Source        : PO — confirm loop Act 2
Hint          : Confirma NFR-05. Section Drafter deve incluir breakpoints mínimos
                (mobile ≥ 360px, tablet ≥ 768px) e testar fluxo crítico de reserva
                em dispositivo móvel antes do release.
```

---

### C-Q08 · Alvos numéricos de performance — aceitos

```
ID            : C-Q08
Section       : nfrs
Origin        : po_authored
Status        : answered
Mode          : open
Targets       : nfrs
Answer        : Alvos ACEITOS: consulta de disponibilidade ≤ 2s (p95); confirmação de
                reserva ≤ 3s (p95); disponibilidade ≥ 99% em horário comercial;
                escala para ~200 usuários simultâneos; sincronização com Google Calendar
                em ≤ 2 min após evento.
Choice        : —
Disposition   : answered
Confidence    : 95
Source        : PO — confirm loop Act 2
Hint          : Confirma NFR-03, NFR-09 e NFR-10 — deixam de ser premissa e tornam-se
                requisitos não-funcionais comprometidos. Section Drafter deve incluir
                estes valores como critérios de aceite mensuráveis no release-criteria
                e nos testes de carga.
```

---

## Nota para Doc Updater — Ações Derivadas das Confirmações (Rev 2)

```
Origem        : Ledger Writer (Rev 2)
Tipo          : nota de ação para Doc Updater
Prioridade    : ALTA

Ações obrigatórias antes de publicar o PRD:

1. exec-summary + scope (I001, I005):
   Corrigir "bidirecional" → "uma via (sistema → Calendar)" em todas as
   ocorrências. Origem: C-Q02 / conflito C4 do Auditor.

2. business-rules:
   - Codificar FCFS como padrão explícito de precedência (C-Q01 / RN-13).
   - Adicionar fluxo de "pedido de realocação" como feature facilitadora (C-Q01).
   - Remover distinção admin/secretária; modelo flat de permissões (C-Q04 / RN-07, RN-08).
   - Incluir regras de janela 08h–19h / mín 15min / máx 8h / antec. ~90 dias (C-Q05 / RN-09–11).
   - Incluir suporte a recorrência com validação por ocorrência (C-Q03 / EC-05).

3. user-stories:
   - US-07: remover permissão diferenciada para secretária (C-Q04).
   - Adicionar US de recorrência com fluxo de sinalização de conflito parcial (C-Q03).

4. nfrs:
   - NFR-05: responsiva/mobile-friendly — requisito confirmado (C-Q07).
   - NFR-07: LGPD patamar básico — requisito confirmado; detalhar base legal e retenção (C-Q06).
   - NFR-03/09/10: alvos numéricos — promover de premissa para requisito (C-Q08).

5. edge-cases:
   - EC-05 (recorrência com conflito parcial): promover para MVP (C-Q03).
   - Novo edge-case: usuário edita evento diretamente no Google Calendar → divergência
     com sistema; documentar e recomendar aviso na UI (C-Q02).

6. scope (I005):
   - Adicionar "reservas recorrentes" ao in-scope (C-Q03).

Conflitos do Auditor resolvidos:
   - C2 (premissas product): resolvidos pelas confirmações C-Q01–C-Q08 (po_authored).
   - C4 (sync one-way vs bidirecional): resolvido por C-Q02 — uma via confirmada pelo PO.

Status de origem pós-Rev 2:
   business-rules, user-journey, user-stories, nfrs, edge-cases:
   ai_drafted → po_authored (para os itens cobertos por C-Q01–C-Q08).
```

---

<!-- END-OF-LOG -->
