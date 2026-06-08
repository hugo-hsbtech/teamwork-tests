<!--
TECHNICAL ASSESSMENT · room-reservation
Instanciado a partir de: target-template.technical-assessment.md
Linguagem de saída: pt-BR
Fase: Fase 2 — classificar & herdar
-->

# Avaliação Técnica — Sistema de Reserva de Salas de Reunião
<!-- rev: 3 · updated: 2026-06-07 -->

> O Technical Assessment (TA) é o **output do CTO** — e vai **além da arquitetura**:
> estabelece o **terreno técnico** sobre o qual a engenharia decide. Como a camada de
> execução (humana ou agente de IA) **não tem conhecimento implícito do código-fonte**,
> o TA torna explícito o que normalmente fica não-dito: a natureza da demanda (software
> novo vs. existente), o estado atual ou a fundação a ser criada, a base de conhecimento,
> a viabilidade de cada NFR, as alternativas descartadas, a testabilidade e a
> observabilidade. É escrito **sozinho** pelo CTO, **em paralelo** com o Readiness
> Package, e **responde** a ele: o CTO **nunca edita o RP**. O TA não redefine o
> produto — ele pode **vetar** a viabilidade do escopo; nesse caso o PO revisa o escopo
> do RP e re-escala. Veja `personas/03-cto.md`, `personas/02-po.md` §2/§10 e
> `interactions/05-po-to-cto.md` / `interactions/06-cto-to-po.md`.

## Metadados
<!-- origination: id=meta; blocks=false; min-confidence=0; kind=meta -->

| Campo | Valor |
|---|---|
| **ID da Avaliação** | TA-2026-001 |
| **Versão** | v1 |
| **RP Vinculado** | RP-2026-001 v1 |
| **Intake Vinculado** | INT-2026-001 |
| **Responsável** | CTO |
| **Status** | Signed off |
| **Veredito de Viabilidade** | Viável com ressalvas |
| **Data de Aprovação** | 2026-06-07 |
| **Linguagem de saída** | pt-BR |

## Histórico de Revisão
<!-- origination: id=revisions; blocks=false; min-confidence=0; kind=meta -->

| Versão | Data | Autor | Status | Resumo |
|---|---|---|---|---|
| v1 | 2026-06-07 | Doc Updater (Fase 2 — classificar & herdar) | Em andamento | DOC instanciado do template; tech-classification firmada (Híbrido, ambos os caminhos, KB inexistente→Discovery); seções herdadas preenchidas (po-questions, integrations, affected-systems, nfr-feasibility, testability-observability, effort-cost) com Origin: inherited. |
| v2 | 2026-06-07 | Doc Updater (Fase 3 — draft pass) | Em andamento | Draft pass mesclado: tech-foundation, current-state, architectural-impact, alternatives, build-vs-buy, hard-constraints, tech-risks, adrs, effort-cost, discovery-path preenchidos (ai_drafted); nfr-feasibility e integrations com colunas de viabilidade mescladas; testability-observability com estratégia/telemetria/logs. feasibility-verdict pendente. |
| v3 | 2026-06-07 | Doc Updater (Fase 4 — sign-off) | Signed off | Veredito comitado (Viável com ressalvas, conf 86); po-questions respondidas (TA-Q01..Q05); seções do draft pass promovidas a cto_authored; ADR-001..005 aprovados (✓), ADR-006 gated; estimativa firmada; current-state mantido em discovery (gated DISC-001). Status=Signed off. |

---

## Veredito de Viabilidade
<!-- origination: id=feasibility-verdict; blocks=true; min-confidence=85; kind=capture -->
> Rubric: a **decisão de primeira classe do CTO** (`personas/03-cto.md` §3 — *a
> viabilidade é de primeira classe*: cada julgamento carrega `verdict` + `rationale` +
> **`terrain`** + `confidence` + `source` + `generates`). Carrega justificativa —
> nunca carimbo de aprovação — e o **terreno** sobre o qual se apoia: *"a viabilidade
> não pode ser avaliada em terreno desconhecido"* (`03-cto.md` §3, regra de ouro do
> CTO). Se **Inviável como escopado**, o CTO devolve com veto + justificativa; o PO
> revisa o escopo do RP e re-escala. O CTO não redefine o produto. Esta seção se
> resolve apenas com confiança alta (a viabilidade é o julgamento central do CTO).

| Campo | Valor |
|---|---|
| **Veredito** | **Viável com ressalvas** |
| **Justificativa** | Arquitetura bem-compreendida; nenhum NFR é inviável. Capacidades-núcleo mainstream: anti-double-booking first-commit-wins como invariante de dados (exclusão transacional relacional — ADR-001/NFR-01), sync uma-via assíncrona via outbox+worker idempotente folgada para ≤2 min (ADR-002/NFR-02), login social OAuth2/OIDC (ADR-004/NFR-06). NFR-01/03/05/09/10 viáveis sem ressalva. Não é veto (nada torna o escopo inconstruível) nem Discovery-exit (a arquitetura é assessável); as contingências (NFR-02/06/08 e a integração) são de configuração organizacional com caminhos de resolução conhecidos, não bloqueadores de viabilidade. |
| **Terreno** | `tech-landscape-room-reservation.md` — criado neste TA (hsb-landscape-keeper), documentando o terreno conhecido (processo manual + fundação greenfield) e as lacunas Workspace/OAuth ligadas ao spike DISC-001. A assinatura sob ressalvas honra a Discovery. |
| **Ressalvas (se aplicável)** | R1 — admin do Workspace permite grant OAuth a apps de terceiros (`calendar.events`), credencial/quotas confirmados (DISC-001). R2 — first-commit-wins via exclusão transacional no banco (não validação read-then-write de aplicação). R3 — sync estritamente uma-via sistema→Calendar, sem reconciliação reversa neste release. R4 — revisão LGPD Jurídico/DPO antes do release. |
| **Gera** | hard_constraint (5) · adr (ADR-001..005 aprovados; ADR-006 gated) · discovery_spike (DISC-001) · kb_update (criação do tech-landscape) |

**Proveniência**
- **Confiança:** 86
- **Origem:** cto_authored
- **Fonte:** nfr-feasibility (NFR-01/03/05/09/10=Sim; 02/06/08=com ressalvas/gated; 07=Jurídico) + integrations + architectural-impact + tech-risks + hard-constraints + ADRs (RP §8/§12 D03/§14; TA-Q01..Q05)
- **Situação:** respondida
- **Disposição:** decided (assinado sob ressalvas)
- **Observação:** Ressalvas R1 e ADR-006/NFR-02/06/08 re-confirmados no DISC-001 durante a execução inicial; um veto só se materializaria se o admin do Workspace negasse o grant OAuth (gatilho de re-escopo/re-escalada).

---

## Classificação Técnica e Base de Conhecimento
<!-- origination: id=tech-classification; blocks=true; min-confidence=80; kind=capture -->
> Rubric: **a decisão que governa o restante do documento.** Herda a natureza da
> demanda do Intake e a confirma sob a lente técnica. Define qual caminho preencher
> (greenfield vs. brownfield) e ancora o TA na base de conhecimento — o que existe,
> o que está faltando, o que será criado. Se a KB não existir ou for incompleta
> (brownfield), documentar o sistema atual é um **pré-requisito**: registrar como
> spike em *Caminho de Discovery* e produzir/atualizar o `tech-landscape`. Se
> greenfield, os ADRs fundacionais **semeiam** um novo `tech-landscape`.

| Campo | Valor |
|---|---|
| **Natureza (confirmada pelo CTO)** | **Híbrido** — processo informal existente (mural físico + Google Forms via WhatsApp, mantido pela secretária) + software-core novo + integração com Google Calendar. Confirmado sob a lente técnica; sem override da triagem. |
| **Caminho a preencher** | **Ambos** — Technical foundation DEFINE a fundação greenfield do software-core novo; Current state DESCOBRE o terreno: ambiente Google Workspace/OAuth da organização (não documentado) e o processo manual (mural + Forms + WhatsApp) a migrar. |
| **Base de Conhecimento (KB)** | **Não existe → criar (Discovery)** |
| **Referência à KB** | `tech-landscape-room-reservation.md` (a criar pelo hsb-landscape-keeper; semeada pelos ADRs greenfield + populada pelo spike de Discovery) |

**Proveniência**
- **Confiança:** 88
- **Origem:** inherited (triagem D003/Q011) + confirmado (lente técnica, hsb-tech-classifier)
- **Fonte:** intake-record demand-nature + RP §14 tech-assessment-ref ("não há premissa greenfield") + sources-index KB-001
- **Situação:** respondida
- **Disposição:** decided
- **Observação:** current-state é gated no spike de Discovery (terreno Workspace/OAuth); ADRs greenfield semeiam a landscape; gestão de mudança é load-bearing (NFR-04 — o novo sistema deve superar a usabilidade do Forms atual; secretária é stakeholder-chave de migração).

---

## Perguntas do PO Endereçadas
<!-- origination: id=po-questions; blocks=true; min-confidence=70; kind=capture -->
> Rubric: *trace-to-source.* As incógnitas técnicas específicas que o PO escalou —
> e a resposta a cada uma. Mantém a avaliação ancorada ao que foi perguntado
> (herdada do RP / da escalada). Sem ao menos uma pergunta endereçada (ou "nenhuma
> pergunta específica foi escalada"), a seção NÃO está satisfeita.

| # | Pergunta do PO (incógnita técnica escalada) | Resposta do CTO |
|---|---|---|
| TA-Q01 | Viabilidade do fluxo OAuth Google Calendar — quais escopos (`calendar.events` ou mais amplo); se o Workspace da organização permite grant a apps de terceiros; modelo de credencial (service account c/ delegação de domínio vs. delegação por usuário). | Viável. Escopo-alvo `calendar.events`; credencial padrão = delegação por usuário autenticado (OAuth incremental), alternativa = service account com delegação de domínio — a confirmar no DISC-001. Pré-condição: admin do Workspace permitir grant a apps de terceiros (ressalva R1). |
| TA-Q02 | Modelo de sincronização uma-via — confirmar que "sistema = fonte de verdade; Calendar = espelho; alterações no Calendar NÃO refletem de volta neste release" é viável e sustentável sem webhooks/push. | Confirmado viável e sustentável: uma-via via transactional outbox + worker, sem webhooks/push de entrada; o Calendar é espelho read-only (ADR-003). |
| TA-Q03 | Atomicidade e anti-double-booking sob concorrência — confirmar a arquitetura que garante first-commit-wins (RN-05, EC-01, NFR-01). | Confirmado: exclusão transacional no banco relacional garante first-commit-wins (ADR-001, NFR-01); harness de concorrência dedicado é gate de release. |
| TA-Q04 | Orçamento de latência de sync — ≤2 min (NFR-02, Objetivo 4, US-06) é alcançável com polling ou push, dados os limites de quota da Calendar API? | ≤2 min alcançável com worker assíncrono (folga ampla frente à latência típica); confirmar quotas/limites da Calendar API no DISC-001 (ressalva R1). |
| TA-Q05 | Dependência D03 (RP §12) — Google Calendar API disponível + fluxo OAuth de-arriscado: pré-requisito para entregar a integração uma-via. | Dependência D03 reconhecida: a integração uma-via é entregável condicionada ao grant OAuth do Workspace (R1), gated no DISC-001. |

**Proveniência**
- **Confiança:** 80
- **Origem:** cto_authored
- **Fonte:** RP §14 tech-assessment-ref (Escalation Flagger) + RP §12 D03
- **Situação:** respondida
- **Disposição:** answered (itens de credencial/quota contingentes ao DISC-001)
- **Observação:** TA-Q01/Q04/Q05 carregam a ressalva R1 (grant do Workspace).

---

## Caminho BROWNFIELD — Estado Atual / Panorama Técnico
<!-- origination: id=current-state; blocks=true; min-confidence=75; kind=capture -->
> Rubric: **documentar o sistema antes de alterá-lo** (preencher se a demanda
> modifica software existente). No brownfield, a decisão de implementação depende
> do que já existe — padrões, convenções, integrações, débito. Este é o equivalente
> ao *document-project* do BMAD. Quando existe um `tech-landscape` atualizado,
> **referenciá-lo** e registrar aqui apenas o que é específico desta demanda. **Se
> greenfield:** não aplicável — `Disposição: decided`, conteúdo
> "N/A — greenfield (ver Classificação Técnica)".

> Demanda **Híbrida**: o "sistema existente" não é base de código, mas um **processo manual informal** + o **ambiente externo do Google Workspace**. Não há software legado a respeitar; há um processo a substituir e um ambiente de terceiros a integrar. O terreno de configuração Workspace/OAuth **não está documentado** — gated no spike DISC-001.

### Padrões e convenções existentes a respeitar

| Aspecto | Como é hoje | Implicação para esta demanda |
|---|---|---|
| **Processo / "fonte de verdade" atual** | Papel no **mural físico** (fonte de verdade) + **Google Forms** (link via WhatsApp); às vezes só papel. **Secretária** é árbitra de conflitos (D003/Q011). | O sistema substitui a fonte de verdade (mural/Forms descontinuados — RN-04, EC-03). Migração e gestão de mudança são primeira-classe; usabilidade deve superar o Forms (NFR-04). Sem dados legados para portar. |
| **Convenções do ambiente externo (Workspace)** | Organização usa Google Workspace; Calendar é alvo (uma via). Identidades no Workspace; login social/OAuth é o vetor (NFR-06). | Seguir convenções de identidade e Calendar do Workspace. Políticas de OAuth/escopos liberados **a descobrir (spike)** — não assumir. |
| **Modelo de dados / persistência** | Não existe — dados só em papel/Forms; sem esquema, migração ou histórico (RP §2 Limitações). | Esquema novo (greenfield dentro do híbrido) — definir em `tech-foundation`. Sem padrão legado. |
| **Autenticação / autorização** | Não há — qualquer um anota no mural/Forms. | Novo: login social OAuth (NFR-06); modelo flat (RN-06). Provedor/escopos **a descobrir (spike)**. |

### Pontos de integração tocados

| Ponto de integração | Sistema/módulo | Natureza do acoplamento | Risco de mudança |
|---|---|---|---|
| **Google Calendar API** | Google Workspace (externo) | Síncrono na escrita, **uma via** (sistema → Calendar; Calendar é espelho read-only — C-Q02/RN-04) | **Médio** — terceiro fora de controle; quota/disponibilidade afetam o SLA ≤2 min (NFR-02). Quota real **a descobrir (spike)**. |
| **Provedor de login social / OAuth** | Workspace / IdP (externo) | Consumido (delega autenticação) | **Médio-Alto enquanto não descoberto** — depende de o admin do Workspace permitir grant a apps de terceiros; escopos (`calendar.events`) e modelo de credencial **a descobrir (DISC-001)**. |
| **Processo manual (mural+Forms+WhatsApp)** | Processo org. mantido pela secretária | Substituído (não integrado) — sistema sendo aposentado | **Baixo tecnicamente / Alto em adoção** — risco product-owned (RP §12 R01/R03), não de regressão. |

### Dívida técnica e risco de regressão

| Área | Dívida / fragilidade conhecida | Risco de regressão | Cobertura de testes atual |
|---|---|---|---|
| **Processo manual (sendo substituído)** | Processo informal: sem prevenção de conflito, dependente da secretária, não auditável (RP §2). Sem código legado. | Migração/adoção (não regressão técnica) — product-owned (RP §12 R01/R03/R05). | N/A |
| **Sincronização uma via (silent divergence)** | Alterações diretas no Calendar não retroalimentam (C-Q02). Pode haver divergência silenciosa (EC-04/EC-13). | **Médio** — não detectada automaticamente neste release; mitigação de produto: aviso na UI. | N/A — capacidade nova |
| **Terreno Workspace/OAuth (não documentado)** | Ambiente real (políticas OAuth, escopos, credenciais, quota) não documentado — KB a criar. | **Indeterminado até o spike** — viabilidade não afirmável sobre terreno desconhecido. | N/A — a descobrir (DISC-001) |

**Proveniência**
- **Confiança:** 54
- **Origem:** ai_drafted
- **Fonte:** intake demand-nature (D003/Q011) + RP §2 + RP §14 (TA LEVE) + RP §12 D03
- **Situação:** rascunho
- **Disposição:** discovery
- **Observação:** Não atinge min-conf 75 até o hsb-landscape-keeper documentar o terreno Workspace/OAuth (criar tech-landscape-room-reservation.md). Confirmar: (1) o processo manual descrito é a fonte de verdade completa; (2) resolver os itens "a descobrir (spike)" no DISC-001 antes de promover.

---

## Caminho GREENFIELD — Fundação Técnica
<!-- origination: id=tech-foundation; blocks=true; min-confidence=75; kind=capture -->
> Rubric: **decidir a fundação — com critérios, não por reflexo** (preencher se a
> demanda constrói software/módulo novo). No greenfield não há terreno a descobrir:
> o TA o **cria**. Registrar as escolhas base e o *porquê*, para que sustentem ADRs
> e se tornem o ponto de partida do novo `tech-landscape`. **Se puramente
> brownfield:** não aplicável — `Disposição: decided`, conteúdo
> "N/A — brownfield (ver Classificação Técnica)".

### Seleção de stack (com critérios)

| Camada | Escolha | Critério de decisão | Alternativa descartada |
|---|---|---|---|
| **Linguagem / runtime** | TypeScript (Node.js LTS) end-to-end | Linguagem única reduz custo cognitivo de time pequeno; ecossistema maduro para OAuth2/OIDC e cliente Google Calendar; tipagem ajuda na correção das regras temporais (RN-09..RN-12). | Python/Django, Java/Spring — sem ganho frente ao porte (~200 usuários); fragmentariam a stack. |
| **Framework / app** | Backend: NestJS/Express (API REST). Frontend: React (Vite/Next) responsivo/mobile-first | REST cobre o CRUD e a consulta de disponibilidade sem complexidade extra; React atende NFR-05 (mobile ≥360px / tablet ≥768px). | GraphQL — modelo simples não justifica overhead de schema/resolvers; SPA puro sem back — reescreveria validação/auth. |
| **Persistência / dados** | Banco relacional transacional — PostgreSQL | **Âncora em NFR-01/RN-05 (first-commit-wins).** `EXCLUSION constraint` com `tstzrange` + `btree_gist` (ou transação serializável) rejeita no nível do banco qualquer interseção de intervalos para a mesma sala — a regra vira invariante de dados, não lógica de aplicação propensa a corrida (RN-01..RN-03, EC-01). Suporta validação por ocorrência de séries (RN-15). | **NoSQL/documento (MongoDB)** — sem constraint de exclusão multi-linha / transação serializável nativa sobre intervalos; first-commit-wins dependeria de locks aplicacionais frágeis no requisito mais crítico. |
| **Infra / deploy** | Container (Docker) em PaaS gerenciada (Cloud Run/App Service/equiv.) + Postgres gerenciado + worker assíncrono de sync | Porte modesto e ≥99% horário comercial não justificam Kubernetes próprio; PaaS + Postgres gerenciado entregam HA/backup prontos. | Kubernetes auto-gerenciado — overhead desproporcional; FaaS puro para o worker — mantido como opção. |

### Arquitetura-alvo (C4 — Contexto + Container; sync UMA VIA sistema → Calendar)

```text
C4 — CONTEXTO
  [Colaborador] e [Secretária] --HTTPS--> SISTEMA DE RESERVA DE SALAS (novo; fonte de verdade)
       |-- OAuth2/OIDC --> [Provedor de Identidade Social (Google)]
       |-- REST + OAuth2 (uma via -->) --> [Google Calendar API] (espelho de leitura; NÃO retroalimenta — C-Q02)

C4 — CONTAINERS
  Web Frontend (React, responsivo) --REST/JSON--> API/Backend (NestJS/Express)
     - Auth OAuth2/OIDC; validação anti-conflito atômica; regras RN-01..RN-16
  API --SQL (txn)--> PostgreSQL (EXCLUSION constraint anti-overlap; reservas/salas/séries)
  API --enfileira evento--> Worker de Sync Calendar (assíncrono; retry/backoff; EC-02) --REST (uma via -->)--> Google Calendar API
  Direção do sync: SISTEMA --> Google Calendar. O Calendar nunca escreve de volta neste release (NFR-02 ≤2 min).
```

### Estrutura e convenções de repositório

- **Organização de pastas / módulos:** monorepo (workspaces) com `apps/web`, `apps/api`, `packages/shared` (DTOs/enums de status). Backend por domínio (`reservations/`, `availability/`, `auth/`, `calendar-sync/`). Migrações versionadas (a EXCLUSION constraint da NFR-01 nasce em migração explícita e testada).
- **Convenções de nomenclatura / lint / teste:** ESLint + Prettier compartilhados; TS `strict`. Teste unitário para regras temporais (RN-09..12) e séries (RN-15); **teste de integração obrigatório de concorrência** exercitando a constraint (EC-01/NFR-01); e2e dos happy paths das Jornadas A/B/C; nomes espelhando os Given/When/Then da Seção 7.
- **Estratégia de branching / CI:** trunk-based + PR com revisão; `main` sempre deployável. CI: lint → build → unit/integração (incl. teste de concorrência NFR-01) → e2e; deploy contínuo p/ homologação + promoção manual; migrações forward-only.

**Proveniência**
- **Confiança:** 78
- **Origem:** cto_authored
- **Fonte:** RP §6 (RN-01..16, sync uma via) + §8 (NFR-01/02/03/05/06/09/10) + §5 escopo + intake (natureza Híbrida, TA LEVE)
- **Situação:** respondida
- **Disposição:** decided
- **Observação:** CTO confirmou a stack; a âncora de persistência transacional é inegociável; modelo de credencial OAuth do Calendar gated DISC-001.

---

## Sistemas e Componentes Afetados
<!-- origination: id=affected-systems; blocks=true; min-confidence=70; kind=capture -->
> Rubric: o mapa de blast-radius. Cada serviço/módulo tocado e a natureza do
> impacto. Herda os sistemas/integrações que o RP nomeou no escopo.

| Sistema / Componente | Natureza do impacto |
|---|---|
| Novo sistema de reserva de salas (software-core) | Novo — criado neste release (CRUD, anti-double-booking, recorrência, login social) |
| Google Calendar (Workspace da organização) | Consumido apenas (uma via: o sistema escreve eventos; o Calendar não retroalimenta) |
| Processo manual: mural físico | Migrado/descontinuado — retirada física após ≤2 semanas do go-live |
| Processo manual: Google Forms (link via WhatsApp) | Migrado/descontinuado — encerramento formal após ≤2 semanas |
| WhatsApp (canal do Forms) | Descontinuado como canal de reservas — fora do escopo técnico |

**Proveniência**
- **Confiança:** 80
- **Origem:** cto_authored
- **Fonte:** RP §5 scope + intake demand-nature (D003/Q011)
- **Situação:** respondida
- **Disposição:** decided
- **Observação:** CTO confirmou a natureza de impacto para todos os sistemas listados.

---

## Impacto Arquitetural
<!-- origination: id=architectural-impact; blocks=true; min-confidence=75; kind=capture -->
> Rubric: território exclusivo do CTO (migrado do antigo RP §8). Para cada área
> tocada, o impacto e a nota arquitetural (padrão a seguir/evitar). Preencher
> apenas as áreas relevantes — não forçar as irrelevantes.

| Área | Impacto | Nota arquitetural |
|---|---|---|
| **Modelo de dados** | Entidades: sala, reserva (intervalo início/fim), usuário, série recorrente. Elemento de carga: exclusividade — sem sobreposição de intervalos para a mesma sala (RN-01/03, NFR-01 CRÍTICO); sobreposição parcial conta (RN-03). | Modelar reserva como intervalo `[início,fim)`; exclusividade como invariante de dados (`EXCLUDE USING gist` com `tstzrange`), não só validação de aplicação. Recorrência: persistir ocorrências materializadas (cada uma participa da constraint, RN-15). |
| **Eventos / mensageria** | Sync com Calendar = efeito colateral assíncrono e retriável, desacoplado da transação de confirmação (EC-02, RN-04). | **Transactional outbox + worker**: gravar a intenção de sync na mesma txn; worker consome e chama a API com retry/backoff; nunca acoplar a chamada externa ao commit; idempotência por chave da reserva. |
| **Frontend** | UI responsiva/mobile-first (NFR-05); disponibilidade quase real-time (US-03, NFR-03). | Priorizar fluxo de reserva em viewport móvel; re-fetch sob demanda atende o MVP (push/realtime opcional); aviso "Calendar é espelho read-only" (EC-13). |
| **Segurança** | Login social OAuth2/OIDC (NFR-06); credencial/escopo da Calendar API (gated no Discovery); LGPD básico (NFR-07). | Separar OIDC de login (identidade) da credencial de escrita no Calendar (service account c/ delegação de domínio vs por usuário — gated no spike); menor privilégio nos escopos; LGPD: base legal/retenção/exclusão — revisão Jurídico/DPO. |
| **Multi-tenancy** | **N/A** — organização única (gatilho ausente confirmado RP §14). | Não introduzir abstração de tenancy especulativa. |
| **Desempenho / Escalabilidade** | Escala modesta (~200 usuários, pico 10h–16h); o constraint real é a correção sob concorrência na escrita (NFR-01), não volume. Alvos ≤2s/≤3s p95 (NFR-03); ≥99% (NFR-09). | A constraint de exclusão serializa naturalmente confirmações conflitantes; a complexidade vai para a atomicidade do booking, não para escala horizontal. |
| **Observabilidade** | Status/fila de sync, contadores de conflito, latência de propagação ao Calendar (vs ≤2 min). | Instrumentar o worker de outbox (itens pendentes, idade da fila, alerta vs ≤2 min); contador de conflitos (saúde do anti-double-booking); histograma de latência sistema→Calendar. |

**Proveniência**
- **Confiança:** 78
- **Origem:** cto_authored
- **Fonte:** RP §6/§8/§9 + §14 (multi-tenancy ausente; TA LEVE)
- **Situação:** respondida
- **Disposição:** decided
- **Observação:** CTO endossou o impacto arquitetural ao comitar o veredito e aprovar os ADRs; modelo de credencial Calendar gated DISC-001; LGPD requer revisão DPO.

---

## Integrações Necessárias
<!-- origination: id=integrations; blocks=true; min-confidence=70; kind=capture -->
> Rubric: as integrações do RP, agora sob a lente de **viabilidade técnica**
> (migrado do antigo RP §7). Para cada sistema: tipo, protocolo e viabilidade /
> riscos conhecidos. Se a demanda não tiver integrações, registrar "nenhuma" com
> `Disposição: decided`.

> **Contexto:** sync uma via (sistema → Calendar) ≤2 min; alterações no Calendar não retroalimentam (RN-04, NFR-02/08, US-06, EC-02/04/13); login social, SSO/Outlook fora do escopo.

| Sistema | Tipo | Protocolo | Viabilidade / Riscos conhecidos |
|---|---|---|---|
| Google Calendar | Externo / API | OAuth 2.0 / Google Calendar API REST (`calendar.events`) | **Viável com ressalvas.** Tecnologia madura/commoditizada (milhares de apps escrevem eventos via Calendar API com OAuth2); sem risco técnico no padrão uma-via (`calendar.events`, ≤2 min). A ressalva é de **configuração organizacional**: confirmar no spike (DISC-001) se o admin do Workspace permite grant a apps de terceiros, o escopo, o modelo de credencial e as quotas. Risco residual: restrição administrativa do Workspace — mitigável. |
| Login social / Autenticação | Externo / Auth | OAuth 2.0 / OpenID Connect (login social; SSO corporativo fora do escopo) | **Viável.** OAuth2/OIDC padrão; ausência de SSO corporativo neste release reduz a complexidade. Sem ressalva de viabilidade técnica. |

**Proveniência**
- **Confiança:** 76
- **Origem:** cto_authored
- **Fonte:** RP §5/§8 (NFR-02/06/08) + classificação técnica (Workspace/OAuth → Discovery)
- **Situação:** respondida
- **Disposição:** decided
- **Observação:** Google Calendar "viável com ressalvas" gated DISC-001; se o admin negar o grant, escala para risco bloqueante. Login social sem dependência de Discovery.

---

## Build vs. Buy
<!-- origination: id=build-vs-buy; blocks=false; min-confidence=0; kind=capture -->
> Rubric: para cada capacidade não-trivial — construir, comprar/integrar terceiro
> ou reutilizar algo existente? A decisão tem efeito direto em custo, prazo e risco.
> Pular (com `Disposição: decided`, "nenhuma decisão make-or-buy relevante") se não
> houver nenhuma.

| Capacidade | Decisão | Justificativa | Efeito em custo/prazo |
|---|---|---|---|
| Núcleo de reserva + anti-double-booking (CRUD, recorrência, first-commit-wins) | **Construir** | Propriedade central/diferenciadora (NFR-01, RN-05, EC-01); nenhum produto de prateleira garante a regra exata sob concorrência. | Maior parte do esforço; concentra o risco técnico (TA-Q03). |
| Autenticação / login social | **Reutilizar/Comprar** | Provedor OAuth2/OIDC (Google); não construir gestão de credenciais. SSO fora do release. | Reduz esforço e risco de segurança; sem licença adicional. |
| Sincronização de agenda (sistema → Calendar, uma via) | **Reutilizar** | Google Calendar API REST (`calendar.events`); não construir backend de calendário. | Baixo custo, dentro de quota gratuita (~200 usuários); viabilidade depende de TA-Q01/Q02/Q04. |
| Persistência transacional | **Reutilizar** | Banco relacional gerenciado (ACID/concorrência p/ NFR-01) sem reinventar bloqueio. | Custo operacional modesto; acelera a garantia transacional. |

**Proveniência**
- **Confiança:** 68
- **Origem:** ai_drafted
- **Fonte:** RP §5 + §6 (RN-04/05) + §8 (NFR-01/02/06/08/10) + §9 (EC-01) + tech-foundation + classificação
- **Situação:** respondida
- **Disposição:** decided (non-blocking; CTO aceitou as decisões make-or-buy)
- **Observação:** "Reutilizar Calendar API" condicionado a TA-Q01/Q02/Q04 (DISC-001). Seção não-bloqueante.

---

## Alternativas Consideradas
<!-- origination: id=alternatives; blocks=true; min-confidence=70; kind=capture -->
> Rubric: **a justificativa, não apenas a conclusão** (padrão design-doc,
> Google/RFC). Registrar o que foi avaliado e **por que foi descartado** dá ao
> downstream o contexto para decidir sobre a implementação — e impede que a mesma
> alternativa seja reavaliada mais tarde. Uma linha por alternativa significativa.

| Alternativa | Prós | Contras | Por que NÃO foi escolhida |
|---|---|---|---|
| **Sincronização bidirecional (Calendar ↔ sistema)** | Reflete alterações feitas no Calendar; evita divergência silenciosa | Exige webhooks/push + reconciliação; política de conflito; amplia quota/falha; incógnitas não de-arriscadas | Fora do escopo (RP §5; C-Q02/RN-04/NFR-02/08). A uma-via atende o objetivo sem a complexidade de reconciliação; bidirecional fica p/ fase futura (TA-Q02). |
| **Google Calendar como fonte de verdade (sem banco próprio)** | Elimina persistência local; já compartilhado | A Calendar API não oferece exclusividade transacional sobre intervalos; sem garantia de first-commit-wins sob corrida | Não garante NFR-01 (RN-01/05, EC-01). O sistema precisa ser fonte de verdade autoritativa (RN-04) p/ honrar first-commit-wins (TA-Q03). |
| **Persistência NoSQL/documento** | Esquema flexível; escala horizontal | Exclusividade de intervalo exigiria coordenação aplicacional (lock distribuído/otimista), frágil sob corrida | Ajuste impróprio; escala modesta (NFR-10) não justifica trade-offs de NoSQL; relacional resolve first-commit-wins direto e auditável. |
| **Validação otimista sem trava transacional** | Menor contenção; caminho rápido no caso comum | Checagem e gravação não atômicas → janela de corrida sob concorrência | Não garante first-commit-wins (RN-05, EC-01); adota-se txn/serializável que torna checagem-gravação atômicas — única que satisfaz NFR-01. |

**Proveniência**
- **Confiança:** 76
- **Origem:** cto_authored
- **Fonte:** RP §5/§6 (RN-01/02/04/05) + §8 (NFR-01/02/08) + §9 (EC-01/04/13) + TA-Q02/Q03/Q04 + C-Q02
- **Situação:** respondida
- **Disposição:** decided
- **Observação:** CTO endossou as alternativas ao aprovar os ADRs; a alternativa transacional vencedora firmada em ADR-001; sync uma-via via outbox+worker firmada em ADR-002/ADR-003.

---

## Viabilidade dos NFRs  ·  *(mapeado ao RP, Seção 8)*
<!-- origination: id=nfr-feasibility; blocks=true; min-confidence=75; kind=capture -->
> Rubric: **fecha o loop produto ↔ técnica.** O PO declarou requisitos de qualidade
> no RP (Seção 8); aqui o CTO responde, NFR por NFR, se são **viáveis** e **como** —
> os *quality scenarios* do arc42. Um NFR inviável é sinal de veto ou re-escopo,
> não um detalhe. Uma linha por NFR herdado do RP §8.

| NFR (do RP §8) | Requisito de qualidade (PO) | Viável? | Como será atingido / abordagem | Risco / ressalva |
|---|---|---|---|---|
| NFR-01 [CRÍTICO] | O sistema nunca permite duas reservas confirmadas sobrepostas na mesma sala, inclusive sob concorrência de acessos. Propriedade não-negociável. | **Sim** | Exclusão transacional no banco relacional (`EXCLUDE USING gist` sobre (sala, tstzrange) ou txn serializável) → first-commit-wins (RN-05, EC-01); checagem+gravação atômicas; o banco é o árbitro. | Não-negociável — exige teste de concorrência dedicado. Alto risco SE feito só na aplicação (read-then-write). Mapeado a TA-Q03. |
| NFR-02 | Toda reserva confirmada ou cancelada deve refletir no Google Calendar em **≤2 minutos** (sync uma via: sistema → Calendar). | **Com ressalvas** | Worker assíncrono (fila + retry/backoff) propaga ≤2 min (folgado p/ job assíncrono); reserva persiste como fonte de verdade independentemente do sync. | **Gated na Discovery** (TA-Q01/Q04): quotas/rate-limits e modelo de credencial não confirmados. |
| NFR-03 | Consulta de disponibilidade: resposta em **≤2 s** (p95); confirmação de reserva: **≤3 s** (p95). | **Sim** | Índices (sala+intervalo) + consulta simples sobre escala modesta; ≤2s/≤3s p95 confortáveis. | Validar p95 no pico; confirmação inclui a txn anti-conflito — medir junto à NFR-01. |
| NFR-04 [CRÍTICO] | Criar uma reserva no sistema deve ser **mais simples do que preencher o Google Forms atual**; secretária e usuário comum devem conseguir criar uma reserva sem treinamento formal. | **Com ressalvas** | Produto/UX: fluxo mais curto que o Forms; validação qualitativa com a secretária como critério de aceite (RP §11). | Validado por produto, não por arquitetura — o CTO não atesta usabilidade. Risco de adoção se o baseline não for medido. |
| NFR-05 | O sistema deve ser **responsivo e mobile-friendly** (fluxo atual ocorre majoritariamente via WhatsApp/celular). Breakpoints mínimos: mobile ≥ 360px, tablet ≥ 768px. | **Sim** | Front responsivo validado nos breakpoints (≥360px/≥768px). | Risco baixo; testar fluxo crítico em dispositivo móvel real. |
| NFR-06 | Acesso somente via **login social** autenticado; cada reserva é atribuível a um usuário identificado. SSO corporativo está fora deste release. | **Com ressalvas** | Login social OAuth/OIDC (Google); cada reserva atribuída a user_id. | **Gated na Discovery** (TA-Q01): consent screen/escopos/restrição de domínio a confirmar. |
| NFR-07 | Dados de participantes (nome, e-mail, horários de presença) tratados conforme **LGPD básico** — requisito deste release. Base legal a definir (legítimo interesse ou consentimento); política de retenção a estabelecer (ex.: 12 meses após a reunião); mecanismo de exclusão a pedido previsto. | **Com ressalvas** | LGPD básico: criptografia em repouso, retenção (~12 meses), exclusão a pedido. | **Exige revisão Jurídico/DPO** — base legal é decisão legal. Não-bloqueante p/ Fase B2; bloqueante p/ release. |
| NFR-08 | O sistema interopera exclusivamente com a **API do Google Calendar** neste release (uma via: sistema → Calendar); integração com Outlook está fora do escopo. | **Com ressalvas** | Interoperação só com Calendar API, uma via; Outlook fora. Reusa worker/credencial de NFR-02. | **Gated na Discovery** (TA-Q01); risco de scope creep se bidirecional reentrar (R05). |
| NFR-09 | Disponibilidade **≥99%** durante o horário comercial; sem requisito de SLA 24/7. | **Sim** | ≥99% horário comercial com hospedagem gerenciada (managed DB + app stateless), sem HA multi-região; manutenção fora do horário. | Risco baixo; indisponibilidade da Calendar API não derruba o sistema (sync assíncrono/tolerante). |
| NFR-10 | O sistema deve suportar até **~200 usuários**, com pico de carga no horário comercial (10h–16h). | **Sim** | ~200 usuários é carga pequena; 1 instância + DB dimensionado p/ pico. | Risco muito baixo; confirmar em teste de carga. |

**Proveniência**
- **Confiança:** 80
- **Origem:** cto_authored
- **Fonte:** RP §8 (NFR-01..10) + arch-impact + RN-05/EC-01 + TA-Q01/Q03/Q04
- **Situação:** respondida
- **Disposição:** decided
- **Observação:** NFR-01/03/05/09/10 viáveis sem ressalva; NFR-02/06/08 mantêm "com ressalvas" gated DISC-001; NFR-07 revisão DPO. Coluna "Requisito de qualidade" preservada (Origin: inherited).

---

## Testabilidade e Observabilidade
<!-- origination: id=testability-observability; blocks=true; min-confidence=70; kind=capture -->
> Rubric: como **provar** que funciona e como **ver** em produção. Sem isso, os
> critérios de aceite do RP não podem ser verificados e o comportamento não pode
> ser monitorado.

| Dimensão | Abordagem |
|---|---|
| **Estratégia de testes** | Unitários (RN-01..16, foco em validação de sobreposição RN-01/03, parâmetros temporais RN-09/10/11, FCFS RN-13; casos-tabela de fronteira de intervalo); integração (Calendar API mockada/sandbox — criação/remoção, ≤2 min, caminho de falha com retry/backoff EC-02/EC-11; EC-04/EC-13 sem write-back); e2e (Jornadas A/B/C, ALT-1..5, US-01..08); **harness de concorrência dedicado [LOAD-BEARING]** para first-commit-wins (RN-05/EC-01) — N confirmações simultâneas, exatamente uma persiste, gate de release (sem ele o NFR-01 não é demonstrável); regressão: núcleo anti-double-booking, revalidação na edição (EC-09/RN-12), séries (EC-05), DST (EC-06), parâmetros (EC-12). |
| **Dados de teste / ambiente** | O ambiente de testes deve reproduzir os seguintes cenários (edge cases do RP §9): EC-01 — reservas concorrentes (race condition): dois usuários confirmando a mesma sala no mesmo instante; EC-02 — falha da API do Google Calendar no momento da confirmação ou cancelamento; EC-03 — uso paralelo do canal antigo (mural/Forms) durante a transição pós go-live; EC-04 — alteração feita diretamente no Google Calendar sem atuar no sistema; EC-05 — reserva recorrente com uma ou mais ocorrências em conflito com reservas existentes; EC-06 — fuso horário / horário de verão (DST): criação de reserva em horário ambíguo na transição DST (premissa de mono-fuso a confirmar); EC-07 — sala em manutenção: tentativa de criar reserva em sala com estado de manutenção ativo; EC-08 — participante externo sem login tentando criar reserva diretamente; EC-09 — edição de reserva que gera conflito com outra reserva ativa; EC-10 — criação de reserva em nome de terceiro ausente (modelo flat); EC-11 — sistema fora do ar ou sem conectividade no momento da confirmação; EC-12 — tentativa de criar reserva no passado ou fora da janela de antecedência máxima (RN-09/10/11); EC-13 — divergência silenciosa entre Calendar e sistema após edição direta no Calendar. |
| **Telemetria / métricas técnicas** | Contador de conflitos bloqueados (prova viva do NFR-01); latência de propagação ao Calendar (p50/95/99 vs ≤2 min, NFR-02); taxa de falha/retry de sync + profundidade/idade da fila; p95 de consulta (≤2s) e confirmação (≤3s) por horário de pico (NFR-03/10); disponibilidade em horário comercial (≥99%, NFR-09). |
| **Logs / alertas** | Alerta de sync pendente acima do SLA (≤2 min / profundidade da fila — EC-02/EC-13); alerta de falhas OAuth/credencial (TA-Q01 — bloqueia toda a sync); alerta de pico de erro de confirmação (incl. EC-11); log de auditoria de criação/edição/cancelamento (quem operou — relevante ao modelo flat RN-06 e à LGPD NFR-07). |

**Proveniência**
- **Confiança:** 76
- **Origem:** cto_authored
- **Fonte:** RP §9 (EC-01..13) + §11 + §8 (NFR-01/02/03/09/10) + §6 (RN-01..16) + TA-Q01/Q03/Q04
- **Situação:** respondida
- **Disposição:** decided
- **Observação:** CTO endossou a estratégia ao aprovar os ADRs e o veredito; harness de concorrência (EC-01) é gate de release; limiares de alerta (≤2 min, p95) e log de auditoria firmes.

---

## Restrições Rígidas
<!-- origination: id=hard-constraints; blocks=true; min-confidence=75; kind=capture -->
> Rubric: condições não-negociáveis que limitam o espaço de solução. O PO não as
> suaviza nem as reinterpreta — se discordar, escala explicitamente
> (`interactions/06-cto-to-po.md`). Se não houver restrições rígidas, registrar
> "nenhuma" com `Disposição: decided`.

| Restrição | Tipo | Detalhe | Efeito no escopo |
|---|---|---|---|
| **Exclusividade transacional / first-commit-wins** | Técnico | NFR-01 não-negociável: nunca duas reservas confirmadas sobrepostas, mesmo sob concorrência (RN-05, EC-01). | Define a escolha de persistência: store transacional com não-sobreposição. Soluções sem garantia transacional descartadas. |
| **Sincronização uma-via (sistema → Calendar)** | Plataforma/Externo | Firmado C-Q02: sistema é fonte de verdade; Calendar é espelho; não retroalimenta (EC-04/EC-13). | Sem reconciliação bidirecional neste release; sem webhooks de entrada. |
| **Somente Google Calendar; sem Outlook; sem SSO corporativo** | Externo | Escopo firmado (RP §5; NFR-06/08): só Calendar API; só login social. | Login social é o único modelo de identidade; inclusões disparam R05 + reavaliação do TA. |
| **Conformidade LGPD básica** | Segurança/Compliance | Dados de participantes (NFR-07): base legal, retenção e exclusão a pedido. | Revisão Jurídico/DPO obrigatória antes do release; retenção/exclusão como requisitos de aceite. |
| **Dependência da configuração do Google Workspace** | Externo | O grant OAuth a apps de terceiros deve ser permitido pelo admin (RP §14 ponto (a); D03); escopos/credencial dependem do ambiente real. | Gate de Discovery: se o grant for negado, a integração com o Calendar precisa ser re-escopada. |

**Proveniência**
- **Confiança:** 80
- **Origem:** cto_authored
- **Fonte:** RP §5/§6 (RN-01/05; sync uma-via C-Q02) + §8 (NFR-01/06/07/08) + §14 (TA LEVE; D03)
- **Situação:** respondida
- **Disposição:** decided
- **Observação:** CTO confirmou todas as restrições; item Workspace é gate via R1/DISC-001 — se o admin negar o grant, gatilho de re-escopo da integração.

---

## Riscos Técnicos e Mitigações
<!-- origination: id=tech-risks; blocks=true; min-confidence=75; kind=capture -->
> Rubric: riscos **técnicos** aqui (riscos de produto/negócio permanecem no RP §12).
> Cada risco carrega categoria, probabilidade, impacto e mitigação.

| Risco | Categoria | Probabilidade | Impacto | Mitigação |
|---|---|---|---|---|
| Workspace nega/restringe grant OAuth a apps de terceiros (`calendar.events`) | Integração | Média | Alto | Antecipar spike DISC-001 (política do Workspace, escopos) antes do commit de arquitetura; plano B de credencial (service account c/ delegação de domínio vs por usuário — TA-Q01); escalar ao admin cedo. **Gate** da integração (RP §12 D03). |
| Race condition no anti-double-booking sob acesso simultâneo | Técnica | Média | Alto | NFR-01 crítico: gravação atômica via constraint/serializável (RN-05); harness de concorrência dedicado (EC-01, TA-Q03). |
| Quota/latência da Calendar API compromete sync ≤2 min | Integração | Baixa-Média | Médio | Worker assíncrono c/ backoff; ≤2 min tem folga; monitorar quota e alertar antes do teto (TA-Q04). |
| Divergência silenciosa Calendar↔sistema (sync uma-via) | Dados | Média | Médio | Aviso na UI (Calendar é espelho read-only — EC-04/EC-13); sistema é fonte única de verdade (RN-04/C-Q02); sem reconciliação reversa neste release. |
| Tratamento incorreto de fuso/DST | Dados | Baixa | Médio | Timestamps em UTC c/ tz explícito; bloquear/sinalizar intervalos ambíguos (EC-06); confirmar premissa mono-fuso. |
| Falha de sync deixa estado inconsistente | Integração | Baixa | Médio | Outbox + retry idempotente; reserva confirmada localmente independe do sync (EC-02); sinalizar "sincronização pendente". |

**Proveniência**
- **Confiança:** 80
- **Origem:** cto_authored
- **Fonte:** RP §9 (EC-01/02/04/06/13) + §12 D03 + §8 (NFR-01/02) + §6 (RN-04/05) + classificação + TA-Q01/Q03/Q04
- **Situação:** respondida
- **Disposição:** decided
- **Observação:** CTO confirmou probabilidades/impactos. O risco de grant OAuth do Workspace é o gate (DISC-001/TA-Q01) — se bloqueado, gatilho de veto/re-escopo. Riscos de produto/negócio permanecem no RP §12.

---

## Decisões Arquiteturais (ADRs)
<!-- origination: id=adrs; blocks=true; min-confidence=75; kind=capture -->
> Rubric: direção arquitetural no nível do CTO. A IA pode chegar com **ADRs
> sugeridos** (reutilizados da base de conhecimento) — o CTO aprova/ajusta (o
> momento WOW de `03-cto.md` §3/§12). Breakdown fino e ADRs de implementação
> pertencem ao Tech Backlog do Tech Lead. Cada ADR carrega a decisão, a
> justificativa e a aprovação do CTO.

| # | Decisão | Justificativa | Aprovação do CTO |
|---|---|---|---|
| ADR-001 | Persistência relacional transacional com garantia de não-sobreposição (intervalos `[início,fim)` por sala; `EXCLUDE USING gist` com `tstzrange` + `room_id` ou txn serializável), não só validação de aplicação. | NFR-01 [CRÍTICO] não-negociável; a invariante deve viver onde a serialização é garantida (o banco), tornando first-commit-wins consequência da constraint (RN-01/03/05, EC-01); sustenta sobreposição parcial (RN-03). | ✓ |
| ADR-002 | Sincronização uma-via assíncrona via transactional outbox + worker idempotente com retry/backoff. | A reserva é fonte de verdade e confirma independentemente do Calendar (EC-02); desacoplar protege NFR-03 e dá folga ao NFR-02; idempotência evita eventos duplicados em retries. | ✓ |
| ADR-003 | Sistema = fonte de verdade; Calendar = espelho read-only; sem reconciliação de volta neste release. | Firmado em produto (C-Q02, RN-04, NFR-08, EC-04/EC-13); evita complexidade de sync bidirecional; a não-detecção de divergência é consequência explícita do escopo uma-via. | ✓ |
| ADR-004 | Autenticação federada via OAuth2/OIDC (login social Google); sem senha própria e sem SSO neste release. | NFR-06 (acesso autenticado, reserva atribuível); reusa o IdP que os ~200 usuários já têm; minimiza dado sensível (alinha NFR-07); caminho de upgrade p/ SSO sem retrabalho de identidade. | ✓ |
| ADR-005 | Tempo em UTC com fuso explícito; premissa mono-fuso; bloquear/forçar confirmação explícita em intervalos ambíguos de DST. | EC-06 exige horários não-ambíguos; correção de RN-09/10/11 depende de âncora temporal única. Ressalva: premissa mono-fuso a confirmar. | ✓ |
| ADR-006 | Modelo de credencial da Calendar API — **A DECIDIR no spike de Discovery** (service account c/ delegação de domínio vs delegação por usuário). Não settled neste TA. | Depende de terreno desconhecido: config do Workspace e grant a apps de terceiros (TA-Q01/Q05, D03; current-state gated). Decidir agora seria inventar sobre terreno não descoberto. Vincular a DISC-001; reconverter em ADR após o spike. | — (gated DISC-001) |

**Proveniência**
- **Confiança:** 80
- **Origem:** cto_authored
- **Fonte:** RP §6/§8/§9 + §12 D03 + classificação (Híbrido) + TA-Q01..Q05
- **Situação:** respondida
- **Disposição:** decided
- **Observação:** ADR-001..005 aprovados (✓); ADR-006 deliberadamente não-settled (gated DISC-001). ADRs greenfield aprovados semeiam o tech-landscape. Breakdown fino (RFC-5545 recorrência, esquema de tabelas, soft-delete US-05) vai p/ o Tech Backlog.

---

## Avaliação de Esforço e Custo (firme)
<!-- origination: id=effort-cost; blocks=true; min-confidence=70; kind=capture -->
> Rubric: somente uso interno. Estas são as estimativas **firmes** do CTO — elas
> substituem a estimativa preliminar do PO (RP Seção 13). Serão refinadas pelo
> Tech Lead no Tech Backlog. Não é compromisso contratual nem material para cliente.

> **Contexto (insumos de dimensionamento herdados do RP):**
> O RP §13 deferiu a estimativa ao CTO/Tech Lead — não há número preliminar do PO.
> Insumos de dimensionamento do produto:
> - **Escopo do release:** CRUD de reservas + integração Google Calendar uma-via + login social + anti-double-booking + recorrência (séries) + migração e descontinuação do processo manual.
> - **Escala:** ~200 usuários (NFR-10), pico no horário comercial (10h–16h).
> - **SLAs:** disponibilidade ≥99% (horário comercial); latência sync ≤2 min (NFR-02); tempo de resposta ≤2s consulta / ≤3s confirmação (p95, NFR-03).
> - **Complexidade de integração:** OAuth Google Calendar a confirmar (TA-Q01/Q04) — o spike de Discovery pode gerar trabalho adicional antes de fechar a estimativa.

### Esforço de Desenvolvimento (dias-pessoa; time pequeno; ai_drafted)

| Área | Estimativa | Senioridade |
|---|---|---|
| Backend — núcleo de reservas (CRUD, máquina de estados, parâmetros temporais) | 12 dias | Pleno (revisão Sênior) |
| Backend — anti-double-booking + recorrência (txn first-commit-wins; séries por ocorrência) | 8 dias | Sênior |
| Integração / OAuth — Google Calendar + login social (worker async ≤2 min; OIDC) | 10 dias | Sênior |
| Frontend — UI responsiva (disponibilidade, CRUD, terceiro/flat, séries, aviso espelho) | 12 dias | Pleno |
| QA — incl. harness de concorrência (EC-01/NFR-01), 13 ECs, integração de sync, carga p95 | 8 dias | QA |
| LGPD básica + migração/descontinuação (retenção/exclusão; plano de migração mural/Forms) | 4 dias | Pleno |
| **Total (desenvolvimento)** | **~54 dias** | (não inclui o spike de Discovery ~2–4 dias) |

### Impacto em Infraestrutura

Modesto: 1 app host (API+UI) + 1 banco relacional gerenciado + 1 worker async. Sem multi-região, sem multi-tenancy, sem cluster complexo (~200 usuários, NFR-10; ≥99% horário comercial NFR-09).

### Impacto em Custo com Terceiros

Baixo a nulo no MVP: Google Calendar API dentro da quota gratuita no volume previsto (a confirmar no spike, TA-Q04); provedor OAuth/login social (Google) gratuito. Sem licenças pagas. [Depende do spike] config de credencial não-trivial pode gerar custo administrativo, não de licença.

### Impacto em Custo Operacional Recorrente

Baixo: hospedagem (app+worker) + banco gerenciado + observabilidade. Tráfego pequeno; armazenamento/banda marginais.

### Avaliação de TCO

Cria fundação reutilizável (stack + tech-landscape semeado) p/ fases futuras (Outlook Fase 2 reusa o worker/modelo fonte-de-verdade→espelho; SSO Fase 3 sobre a auth; analytics/lembretes Fase 2 sobre o modelo de reservas). Custo recorrente incremental baixo; paga dívida de processo (descontinua o manual). Maior driver de longo prazo é adoção (R01/R02/R03 — fora desta estimativa).

**Proveniência**
- **Confiança:** 72
- **Origem:** cto_authored
- **Fonte:** RP §5/§6/§8/§9 (escopo, RN-01/05, recorrência, EC-01) + classificação (Híbrido, KB→Discovery)
- **Situação:** respondida
- **Disposição:** decided
- **Observação:** Estimativa firmada pelo CTO; linha Integração/OAuth (10 dias) e custo com terceiros a re-firmar após o spike DISC-001 (TA-Q01/Q04).

---

## Caminho de Discovery (se uma incógnita técnica bloqueia a conclusão)
<!-- origination: id=discovery-path; blocks=false; min-confidence=0; kind=capture -->
> Rubric: preencher **apenas** se uma incógnita técnica impede o fechamento da
> avaliação. O CTO define o spike/investigação; o PO determina o time-box. A demanda
> retorna ao Discovery (`interactions/05-po-to-cto.md`). Se nada bloqueia, registrar
> "—" com `Disposição: decided`.

| Incógnita | Spike / Investigação | Responsável | Time-box sugerido |
|---|---|---|---|
| Ambiente Google Workspace / OAuth não documentado (gate de viabilidade) | DISC-001 — documentar: (a) escopos OAuth concedíveis a apps de terceiros e se o admin permite grant; (b) modelo de credencial (service account c/ delegação de domínio vs delegação por usuário); (c) quotas/limites da Calendar API; (d) caracterização final do processo manual (mural+Forms+WhatsApp, secretária). Produz o tech-landscape-room-reservation.md (via hsb-landscape-keeper). | CTO/Tech Lead + TI da organização (acesso ao Workspace); secretária (processo) | ~2–4 dias (acesso ao ambiente real é o gargalo) |

**Proveniência**
- **Confiança:** 80
- **Origem:** ai_drafted
- **Fonte:** classificação técnica (KB inexistente) + RP §14 (TA LEVE pontos (a)/(d)) + RP §12 D03
- **Situação:** rascunho
- **Disposição:** discovery
- **Observação:** DISC-001 destrava current-state (min-conf 75) e os pontos (a)/(d) do TA LEVE; NFR-02/06/08 e ADR-006 são contingentes ao seu fechamento. Owner do time-box: PO; investigação: CTO.

<!-- END OF DOCUMENT -->
