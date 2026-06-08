<!-- 
Índice de Fontes — Technical Assessment: Sistema de Reserva de Salas de Reunião
Fase: Technical Assessment (CTO)
Linguagem: pt-BR
Gerado: 2026-06-07 (Source Indexer)
-->

# Índice de Fontes · Technical Assessment

**Escopo:** Consolidação dos artefatos de entrada para a fase de Avaliação Técnica (TA) do CTO.  
**Fase:** Technical Assessment (Ato 3 do Teamwork)  
**Demanda:** Sistema de Reserva de Salas de Reunião (room-reservation)  
**Output Language:** pt-BR

---

## Tabela de Fontes Indexadas

| ID | Arquivo | Tipo | Descrição sumária | Linguagem | Alimenta (TA concerns) | Status |
|---|---|---|---|---|---|---|
| **RP-001** | `readiness-document.md` | Readiness Package (RP) — documento de trabalho com proveniência | Definição completa de pronto de produto (vision, problema, escopo, regras de negócio, jornadas, histórias, NFRs, edge cases, critérios de sucesso, métricas, riscos); inclui seções de produto (Seções 1–12) com confiança e disposição; referência ao TA e premissas técnicas deferred (Seção 14). | pt-BR | Escopo §5 (integração Google Calendar uma via, OAuth) → integrations · NFRs §8 (desempenho ≤2min sync, ≤2s consulta, ≤3s confirmação, ~200 usuários, ≥99% availability, mobile-responsivo, LGPD) → nfr-feasibility · Regras de Negócio §6 (anti-double-booking, first-commit-wins, FCFS, modelo flat) → consistency-concurrency · Edge Cases §9 (race conditions, sync failures, alterações no Google Calendar) → edge-case-analysis · Riscos §12 (integração OAuth, adoção, processo manual) → risk-context · Esforço deferred §13 → effort-cost-context | indexed |
| **IR-001** | `intake-record.md` | Intake Record (Triagem) — artefato do Ato 1 do PO | Consolidação da decisão de roteamento do PO: triagem Product Ready. Inclui demand-summary quantificado (impacto operacional + financeiro: R$111k perdidos, R$90k risco, ~R$700k pipeline), natureza HÍBRIDA confirmada (mural + Forms + WhatsApp → novo sistema), base de conhecimento a criar, escalação CTO flagged como LEVE (Google Calendar somente), premissas validadas (3 resolvidas via D003 + D005). | pt-BR | Demand-nature (Híbrido: mural + Forms + WhatsApp) → tech-classification · Escalação CTO (Google Calendar, OAuth deferred) → cto-flag · Impacto R$ quantificado (9 conflitos/5sem, R$111k+R$90k) → business-impact-context · Constraints (Google only, no Outlook/SSO) → scope-constraints · Premissas resolvidas (3 de 3 validadas) → assumptions-resolved | indexed |
| **KB-001** | tech-landscape-room-reservation.md | Base de Conhecimento (KB) técnica — **não existe** | A ser criada. Referência: intake-record (demand-nature §135–178) especifica: processo informal existente (mural físico, Google Forms via WhatsApp, secretária como árbitro), natureza HÍBRIDA. KB deve documentar a landscape técnica atual: dependências do Google Workspace da organização, escopos OAuth disponíveis, integração com Google Calendar (configuração, quotas, fluxos). **PRIMEIRA TAREFA DE DISCOVERY TÉCNICO do TA.** | pt-BR (quando criado) | Ambiente real da organização (Google Workspace config, OAuth scopes, integração Google Calendar) → discovery-prerequisites · Artefatos herdados (mural + Forms + WhatsApp) → brownfield-context · Stakeholder-chave (secretária) → people-discovery | unresolved — Does not exist · To be created (Discovery) |
| **RP-DERIV-1** | readiness/output/humanized.md | Readiness Package (RP) — cópia humanizada (referência) | Cópia limpa/humanizada do readiness-document.md, sem seções de meta/proveniência. Referência apenas — a versão com proveniência é RP-001. | pt-BR | (derivativa — usa RP-001) | indexed (derivative) |
| **RP-DERIV-2** | readiness/final/room-reservation-001.md | Readiness Package (RP) — cópia final/impressão (referência) | Cópia formatada para entrega final/impressão (sem markup de meta). Referência apenas — a versão com proveniência é RP-001. | pt-BR | (derivativa — usa RP-001) | indexed (derivative) |

---

## Sumário de Status

| Categoria | Total | Indexed | Unresolved | Notas |
|---|---|---|---|---|
| **Fontes primárias (bloqueantes)** | 2 | 2 | 0 | Readiness Package + Intake Record ambos presentes e indexados |
| **Base de Conhecimento** | 1 | 0 | 1 | **Does not exist** · tech-landscape-room-reservation.md · Primeira tarefa de Discovery do TA |
| **Derivativas (referência)** | 2 | 2 | 0 | Cópias humanizada + final do RP (não-bloqueantes) |
| **TOTAL** | 5 | 4 | 1 | |

---

## Mapeamento: Fontes → TA Concerns

### Integrations (Google Calendar OAuth)
- **Fonte primária:** RP-001 (Seção 5, §231–262; Seção 8, NFR-08, §605; Seção 14, §799–848)
- **Fonte primária:** IR-001 (Demand-nature, §146–178; CTO escalation, §181–192)
- **Dependência de discovery:** KB-001 (não existe — mapear Google Workspace config da organização)

### NFR Feasibility (Desempenho, Usabilidade, Segurança, Compatibilidade)
- **Fonte primária:** RP-001 (Seção 8, §587–618)
  - NFR-02: Sync ≤2 min (Google Calendar)
  - NFR-03: Consulta ≤2s p95; confirmação ≤3s p95
  - NFR-04: Usabilidade > Google Forms atual
  - NFR-05: Mobile-responsivo (360px+, 768px+)
  - NFR-06: Login social autenticado
  - NFR-07: LGPD básico
  - NFR-09: Disponibilidade ≥99% horário comercial
  - NFR-10: Suporte ~200 usuários

### Consistency & Concurrency
- **Fonte primária:** RP-001 (Seção 6, §265–334; Seção 9, EC-01, EC-02, §629–631)
  - RN-01, RN-02, RN-03: Exclusividade e anti-double-booking
  - RN-05: First-commit-wins sob concorrência
  - EC-01: Race condition — first-commit-wins firmado
  - EC-02: Falha de API Google Calendar — sys local com retry

### Edge Case Analysis
- **Fonte primária:** RP-001 (Seção 9, §621–650)
  - 13 edge cases documentados: race conditions, sync failures, alterações no Google Calendar sem retorno, séries recorrentes com conflitos, fuso horário, sala em manutenção, etc.

### Risk Context
- **Fonte primária:** RP-001 (Seção 12, §705–738)
  - R01–R05: Riscos de produto/negócio (adoção, dependência secretária, escopo creep, R$ em risco, integração)
  - D01–D03: Dependências (secretária, liderança comercial, Google Calendar API)

### Business Impact Context
- **Fonte primária:** IR-001 (Demand-summary, §66–80; Validated Assumptions, §202–206)
  - Impacto quantificado: 9 conflitos/5sem (~1,8/sem), R$111k perdidos, R$90k em risco, ~R$700k pipeline

### Effort & Cost Context
- **Fonte primária:** RP-001 (Seção 13, §741–761)
  - Estimativa deferida ao CTO/Tech Lead (sem dados de prazo/orçamento no origination)

### Tech Classification
- **Fonte primária:** IR-001 (Demand-nature, §146–178)
  - **Híbrido confirmado:** novo software-core + integração Google Calendar + migração processo manual (mural + Forms + WhatsApp)
  - **Base de Conhecimento:** tech-landscape-room-reservation.md (não existe — criar)

---

## Observações Operacionais

### 1. Readiness Package (RP-001) — Documento Primário
O arquivo `readiness-document.md` é o **documento de trabalho autorizado** com proveniência completa (confiança, origem, disposição, observações). Inclui:
- **Seções de produto confirmadas pelo PO** (1–12, conf ≥75): vision, problema, escopo, regras, jornadas, histórias, NFRs, edge cases, métricas, critérios de aceite, riscos.
- **Seção de Technical Assessment** (§14, §799–848): referência ao TA com 4 gatilhos presentes (OAuth, integração, atomicidade, latência) e disposição **deferred** (TA pending).

### 2. Intake Record (IR-001) — Contrato de Triagem
O arquivo `intake-record.md` consolida a decisão do PO:
- **Status:** Product Ready (Ato 2 aberto)
- **Discovery encerrada:** D003 + D005 (2026-06-06) — 4/4 incógnitas resolvidas
- **Impacto ALTO quantificado em R$:** pipeline ~R$700k, R$111k perdidos, R$90k em risco
- **CTO flag LEVE:** Google Calendar somente (Outlook, SSO descartados); OAuth deferred

### 3. Base de Conhecimento (KB-001) — **NÃO EXISTE**
A KB `tech-landscape-room-reservation.md` não foi encontrada. Conforme IR-001 (§146–151):
> "Base de conhecimento existe? **Não** → exige discovery de documentação"
> "Referência da Base de Conhecimento — (futura: tech-landscape-room-reservation.md)"

**Ação recomendada:** A primeira tarefa de Discovery técnico do TA é **criar** a KB, documentando:
- Google Workspace da organização (versão, configuração de OAuth, escopos disponíveis)
- Processo manual existente em detalhe (mural, Forms, WhatsApp, secretária)
- Integrações existentes (ou ausentes) com Google Calendar
- Stakeholders técnicos e de mudança (secretária, TI, liderança comercial)

### 4. Confiança & Disposição nas Fontes
- **RP-001:** Confiança ≥75 (seções 1–12 respondidas pelo PO); disposição po_authored com confirmações C-Q01..C-Q08
- **IR-001:** Confiança ~90 (todos 5 critérios de triagem answered; impacto R$ quantificado)
- **KB-001:** Confiança 0 (não existe); disposição: a criar (Discovery)

### 5. Dependência Explícita: RP §14 (tech-assessment-ref)
A Seção 14 do RP especifica o escopo do TA LEVE em 4 pontos:
1. Viabilidade do fluxo OAuth Google Calendar (escopos, credenciais, delegação)
2. Modelo de sincronização bidirecional (sync uma via viável?)
3. Atomicidade e anti-double-booking sob concorrência (arquitetura)
4. Orçamento de latência (≤2 min com polling/push?)

O TA **deve completar** estes 4 pontos antes de assinar o escopo técnico.

---

## Linguagem & Proveniência

- **Output Language da TA:** pt-BR (conforme especificação do Readiness Package)
- **Todas as fontes índexadas:** pt-BR
- **Proveniência dos documentos primários:**
  - RP-001: Readiness Package gerado 2026-06-07; herdado do origination-record INT-2026-001
  - IR-001: Intake Record v3, triado 2026-06-06; contém decisão PO Product Ready + Discovery D003 + D005

---

## Próximos Passos Recomendados (fora do escopo do Source Indexer)

1. **[Evidence Extractor]** Ler as fontes indexadas (RP-001, IR-001, KB-001 status) e extrair evidências de:
   - Requisitos técnicos (NFRs, regras, edge cases)
   - Contexto de negócio (impacto R$, personas, riscos)
   - Constraints de arquitetura (integração Google, auth, sync)
   - Pressupostos e premissas (HÍBRIDO, stakeholder secretária, processo manual)

2. **[TA Agent — Discovery da KB]** Criar `tech-landscape-room-reservation.md`:
   - Mapear Google Workspace da organização
   - Documentar processo manual existente (mural + Forms + WhatsApp)
   - Confirmar escopos OAuth disponíveis

3. **[TA Agent — Avaliação Técnica]** Responder aos 4 pontos do Escopo TA LEVE (RP §829–837)

---

<!-- END OF DOCUMENT -->
