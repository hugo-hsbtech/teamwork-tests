<!--
TECHNICAL ASSESSMENT · room-reservation
Instanciado a partir de: target-template.technical-assessment.md
Linguagem de saída: pt-BR
Fase: Fase 2 - classificar & herdar
-->

# Avaliação técnica: sistema de reserva de salas de reunião
<!-- rev: 3 · updated: 2026-06-07 -->

> O Technical Assessment (TA) é o **output do CTO**. Vai **além da arquitetura**:
> estabelece o **terreno técnico** sobre o qual a engenharia decide. Como a camada de
> execução (humana ou agente de IA) **não tem conhecimento implícito do código-fonte**,
> o TA torna explícito o que normalmente fica não-dito: a natureza da demanda (software
> novo vs. existente), o estado atual ou a fundação a ser criada, a base de conhecimento,
> a viabilidade de cada NFR, as alternativas descartadas, a testabilidade e a
> observabilidade. É escrito **sozinho** pelo CTO, **em paralelo** com o Readiness
> Package, e **responde** a ele: o CTO **nunca edita o RP**. O TA não redefine o
> produto; pode **vetar** a viabilidade do escopo, e nesse caso o PO revisa o escopo
> do RP e re-escala. Veja `personas/03-cto.md`, `personas/02-po.md` §2/§10 e
> `interactions/05-po-to-cto.md` / `interactions/06-cto-to-po.md`.

## Metadados
<!-- origination: id=meta; blocks=false; min-confidence=0; kind=meta -->

| Campo | Valor |
|---|---|
| **ID da avaliacao** | TA-2026-001 |
| **Versao** | v1 |
| **RP vinculado** | RP-2026-001 v1 |
| **Intake vinculado** | INT-2026-001 |
| **Responsavel** | CTO |
| **Situação** | Assinado |
| **Veredito de viabilidade** | Viavel com ressalvas |
| **Data de aprovacao** | 2026-06-07 |
| **Linguagem de saida** | pt-BR |

## Historico de revisao
<!-- origination: id=revisions; blocks=false; min-confidence=0; kind=meta -->

| Versao | Data | Autor | Situação | Resumo |
|---|---|---|---|---|
| v1 | 2026-06-07 | Doc Updater (Fase 2 - classificar & herdar) | Em andamento | DOC instanciado do template; tech-classification firmada (Hibrido, ambos os caminhos, KB inexistente→Discovery); secoes herdadas preenchidas (po-questions, integrations, affected-systems, nfr-feasibility, testability-observability, effort-cost) com Origin: inherited. |
| v2 | 2026-06-07 | Doc Updater (Fase 3 - draft pass) | Em andamento | Draft pass mesclado: tech-foundation, current-state, architectural-impact, alternatives, build-vs-buy, hard-constraints, tech-risks, adrs, effort-cost, discovery-path preenchidos (ai_drafted); nfr-feasibility e integrations com colunas de viabilidade mescladas; testability-observability com estrategia/telemetria/logs. feasibility-verdict pendente. |
| v3 | 2026-06-07 | Doc Updater (Fase 4 - sign-off) | Assinado | Veredito comitado (Viavel com ressalvas, conf 86); po-questions respondidas (TA-Q01..Q05); secoes do draft pass promovidas a cto_authored; ADR-001..005 aprovados (✓), ADR-006 gated; estimativa firmada; current-state mantido em discovery (gated DISC-001). Situação=Assinado. |

---

## Veredito de viabilidade
<!-- origination: id=feasibility-verdict; blocks=true; min-confidence=85; kind=capture -->
> Rubric: a **decisao de primeira classe do CTO** (`personas/03-cto.md` §3, *a
> viabilidade e de primeira classe*: cada julgamento carrega `verdict` + `rationale` +
> **`terrain`** + `confidence` + `source` + `generates`). Carrega justificativa (nunca
> carimbo de aprovacao) e o **terreno** sobre o qual se apoia: *"a viabilidade
> nao pode ser avaliada em terreno desconhecido"* (`03-cto.md` §3, regra de ouro do
> CTO). Se **Inviavel como escopado**, o CTO devolve com veto + justificativa; o PO
> revisa o escopo do RP e re-escala. O CTO nao redefine o produto. Esta secao se
> resolve apenas com confianca alta (a viabilidade e o julgamento central do CTO).

| Campo | Valor |
|---|---|
| **Veredito** | **Viavel com ressalvas** |
| **Justificativa** | Arquitetura bem-compreendida; nenhum NFR e inviavel. Capacidades-nucleo sao corriqueiras: anti-double-booking first-commit-wins como invariante de dados (exclusao transacional relacional, ADR-001/NFR-01), sync uma-via assincrona via outbox+worker idempotente folgada para ≤2 min (ADR-002/NFR-02), login social OAuth2/OIDC (ADR-004/NFR-06). NFR-01/03/05/09/10 sao viaveis sem ressalva. Nao e veto (nada torna o escopo inconstruivel) nem Discovery-exit (a arquitetura e assessavel); as contingencias (NFR-02/06/08 e a integracao) sao de configuracao organizacional com caminhos de resolucao conhecidos, nao bloqueadores de viabilidade. |
| **Terreno** | `tech-landscape-room-reservation.md`, criado neste TA (hsb-landscape-keeper), documentando o terreno conhecido (processo manual + fundacao greenfield) e as lacunas Workspace/OAuth ligadas ao spike DISC-001. A assinatura sob ressalvas honra a Discovery. |
| **Ressalvas (se aplicavel)** | R1: admin do Workspace permite grant OAuth a apps de terceiros (`calendar.events`), credencial/quotas confirmados (DISC-001). R2: first-commit-wins via exclusao transacional no banco (nao validacao read-then-write de aplicacao). R3: sync estritamente uma-via sistema→Calendar, sem reconciliacao reversa neste release. R4: revisao LGPD Juridico/DPO antes do release. |
| **Gera** | hard_constraint (5) · adr (ADR-001..005 aprovados; ADR-006 gated) · discovery_spike (DISC-001) · kb_update (criacao do tech-landscape) |

**Provenencia**
- **Confianca:** 86
- **Origem:** cto_authored
- **Fonte:** nfr-feasibility (NFR-01/03/05/09/10=Sim; 02/06/08=com ressalvas/gated; 07=Juridico) + integrations + architectural-impact + tech-risks + hard-constraints + ADRs (RP §8/§12 D03/§14; TA-Q01..Q05)
- **Situacao:** respondida
- **Disposicao:** decided (assinado sob ressalvas)
- **Observacao:** Ressalvas R1 e ADR-006/NFR-02/06/08 re-confirmados no DISC-001 durante a execucao inicial; um veto so se materializaria se o admin do Workspace negasse o grant OAuth (gatilho de re-escopo/re-escalada).

---

## Classificacao tecnica e base de conhecimento
<!-- origination: id=tech-classification; blocks=true; min-confidence=80; kind=capture -->
> Rubric: **a decisao que governa o restante do documento.** Herda a natureza da
> demanda do Intake e a confirma sob a lente tecnica. Define qual caminho preencher
> (greenfield vs. brownfield) e ancora o TA na base de conhecimento: o que existe,
> o que esta faltando, o que sera criado. Se a KB nao existir ou for incompleta
> (brownfield), documentar o sistema atual e um **pre-requisito**: registrar como
> spike em *Caminho de Discovery* e produzir/atualizar o `tech-landscape`. Se
> greenfield, os ADRs fundacionais **semeiam** um novo `tech-landscape`.

| Campo | Valor |
|---|---|
| **Natureza (confirmada pelo CTO)** | **Hibrido**: processo informal existente (mural fisico + Google Forms via WhatsApp, mantido pela secretaria) + software-core novo + integracao com Google Calendar. Confirmado sob a lente tecnica; sem override da triagem. |
| **Caminho a preencher** | **Ambos**: Technical foundation DEFINE a fundacao greenfield do software-core novo; Current state DESCOBRE o terreno: ambiente Google Workspace/OAuth da organizacao (nao documentado) e o processo manual (mural + Forms + WhatsApp) a migrar. |
| **Base de Conhecimento (KB)** | **Nao existe → criar (Discovery)** |
| **Referencia a KB** | `tech-landscape-room-reservation.md` (a criar pelo hsb-landscape-keeper; semeada pelos ADRs greenfield + populada pelo spike de Discovery) |

**Provenencia**
- **Confianca:** 88
- **Origem:** inherited (triagem D003/Q011) + confirmado (lente tecnica, hsb-tech-classifier)
- **Fonte:** intake-record demand-nature + RP §14 tech-assessment-ref ("nao ha premissa greenfield") + sources-index KB-001
- **Situacao:** respondida
- **Disposicao:** decided
- **Observacao:** current-state e gated no spike de Discovery (terreno Workspace/OAuth); ADRs greenfield semeiam a landscape; gestao de mudanca e load-bearing (NFR-04: o novo sistema deve superar a usabilidade do Forms atual; secretaria e stakeholder-chave de migracao).

---

## Perguntas do PO endereçadas
<!-- origination: id=po-questions; blocks=true; min-confidence=70; kind=capture -->
> Rubric: *trace-to-source.* As incognitas tecnicas especificas que o PO escalou,
> com a resposta a cada uma. Mantem a avaliacao ancorada ao que foi perguntado
> (herdada do RP / da escalada). Sem ao menos uma pergunta endereçada (ou "nenhuma
> pergunta especifica foi escalada"), a secao nao esta satisfeita.

| # | Pergunta do PO (incognita tecnica escalada) | Resposta do CTO |
|---|---|---|
| TA-Q01 | Viabilidade do fluxo OAuth Google Calendar: quais escopos (`calendar.events` ou mais amplo); se o Workspace da organizacao permite grant a apps de terceiros; modelo de credencial (service account c/ delegacao de dominio vs. delegacao por usuario). | Viavel. Escopo-alvo `calendar.events`; credencial padrao = delegacao por usuario autenticado (OAuth incremental), alternativa = service account com delegacao de dominio, a confirmar no DISC-001. Pre-condicao: admin do Workspace permitir grant a apps de terceiros (ressalva R1). |
| TA-Q02 | Modelo de sincronizacao uma-via: confirmar que "sistema = fonte de verdade; Calendar = espelho; alteracoes no Calendar NAO refletem de volta neste release" e viavel e sustentavel sem webhooks/push. | Confirmado viavel e sustentavel: uma-via via transactional outbox + worker, sem webhooks/push de entrada; o Calendar e espelho read-only (ADR-003). |
| TA-Q03 | Atomicidade e anti-double-booking sob concorrencia: confirmar a arquitetura que garante first-commit-wins (RN-05, EC-01, NFR-01). | Confirmado: exclusao transacional no banco relacional garante first-commit-wins (ADR-001, NFR-01); harness de concorrencia dedicado e gate de release. |
| TA-Q04 | Orcamento de latencia de sync: ≤2 min (NFR-02, Objetivo 4, US-06) e alcancavel com polling ou push, dados os limites de quota da Calendar API? | ≤2 min alcancavel com worker assincrono (folga ampla frente a latencia tipica); confirmar quotas/limites da Calendar API no DISC-001 (ressalva R1). |
| TA-Q05 | Dependencia D03 (RP §12): Google Calendar API disponivel + fluxo OAuth de-arriscado; pre-requisito para entregar a integracao uma-via. | Dependencia D03 reconhecida: a integracao uma-via e entregavel condicionada ao grant OAuth do Workspace (R1), gated no DISC-001. |

**Provenencia**
- **Confianca:** 80
- **Origem:** cto_authored
- **Fonte:** RP §14 tech-assessment-ref (Escalation Flagger) + RP §12 D03
- **Situacao:** respondida
- **Disposicao:** answered (itens de credencial/quota contingentes ao DISC-001)
- **Observacao:** TA-Q01/Q04/Q05 carregam a ressalva R1 (grant do Workspace).

---

## Caminho BROWNFIELD: estado atual / panorama tecnico
<!-- origination: id=current-state; blocks=true; min-confidence=75; kind=capture -->
> Rubric: **documentar o sistema antes de altera-lo** (preencher se a demanda
> modifica software existente). No brownfield, a decisao de implementacao depende
> do que ja existe: padroes, convencoes, integracoes, debito. Este e o equivalente
> ao *document-project* do BMAD. Quando existe um `tech-landscape` atualizado,
> **referencia-lo** e registrar aqui apenas o que e especifico desta demanda. **Se
> greenfield:** nao aplicavel. `Disposicao: decided`, conteudo
> "N/A (greenfield, ver Classificacao Tecnica)".

> Demanda **Hibrida**: o "sistema existente" nao e base de codigo, mas um **processo manual informal** + o **ambiente externo do Google Workspace**. Nao ha software legado a respeitar; ha um processo a substituir e um ambiente de terceiros a integrar. O terreno de configuracao Workspace/OAuth **nao esta documentado** (gated no spike DISC-001).

### Padroes e convencoes existentes a respeitar

| Aspecto | Como e hoje | Implicacao para esta demanda |
|---|---|---|
| **Processo / "fonte de verdade" atual** | Papel no **mural fisico** (fonte de verdade) + **Google Forms** (link via WhatsApp); as vezes so papel. **Secretaria** e arbitra de conflitos (D003/Q011). | O sistema substitui a fonte de verdade (mural/Forms descontinuados per RN-04, EC-03). Migracao e gestao de mudanca sao primeira-classe; usabilidade deve superar o Forms (NFR-04). Sem dados legados para portar. |
| **Convencoes do ambiente externo (Workspace)** | Organizacao usa Google Workspace; Calendar e alvo (uma via). Identidades no Workspace; login social/OAuth e o vetor (NFR-06). | Seguir convencoes de identidade e Calendar do Workspace. Politicas de OAuth/escopos liberados **a descobrir (spike)**; nao assumir. |
| **Modelo de dados / persistencia** | Nao existe. Dados so em papel/Forms; sem esquema, migracao ou historico (RP §2 Limitacoes). | Esquema novo (greenfield dentro do hibrido), a definir em `tech-foundation`. Sem padrao legado. |
| **Autenticacao / autorizacao** | Nao ha: qualquer um anota no mural/Forms. | Novo: login social OAuth (NFR-06); modelo flat (RN-06). Provedor/escopos **a descobrir (spike)**. |

### Pontos de integracao tocados

| Ponto de integracao | Sistema/modulo | Natureza do acoplamento | Risco de mudanca |
|---|---|---|---|
| **Google Calendar API** | Google Workspace (externo) | Sincrono na escrita, **uma via** (sistema → Calendar; Calendar e espelho read-only per C-Q02/RN-04) | **Medio**: terceiro fora de controle; quota/disponibilidade afetam o SLA ≤2 min (NFR-02). Quota real **a descobrir (spike)**. |
| **Provedor de login social / OAuth** | Workspace / IdP (externo) | Consumido (delega autenticacao) | **Medio-Alto enquanto nao descoberto**: depende de o admin do Workspace permitir grant a apps de terceiros; escopos (`calendar.events`) e modelo de credencial **a descobrir (DISC-001)**. |
| **Processo manual (mural+Forms+WhatsApp)** | Processo org. mantido pela secretaria | Substituido, nao integrado (sistema sendo aposentado) | **Baixo tecnicamente / Alto em adocao**: risco product-owned (RP §12 R01/R03), nao de regressao. |

### Divida tecnica e risco de regressao

| Area | Divida / fragilidade conhecida | Risco de regressao | Cobertura de testes atual |
|---|---|---|---|
| **Processo manual (sendo substituido)** | Processo informal: sem prevencao de conflito, dependente da secretaria, nao auditavel (RP §2). Sem codigo legado. | Migracao/adocao (nao regressao tecnica), product-owned (RP §12 R01/R03/R05). | N/A |
| **Sincronizacao uma via (silent divergence)** | Alteracoes diretas no Calendar nao retroalimentam (C-Q02). Pode haver divergencia silenciosa (EC-04/EC-13). | **Medio**: nao detectada automaticamente neste release; mitigacao de produto: aviso na UI. | N/A (capacidade nova) |
| **Terreno Workspace/OAuth (nao documentado)** | Ambiente real (politicas OAuth, escopos, credenciais, quota) nao documentado. KB a criar. | **Indeterminado ate o spike**: viabilidade nao afirmavel sobre terreno desconhecido. | N/A (a descobrir no DISC-001) |

**Provenencia**
- **Confianca:** 54
- **Origem:** ai_drafted
- **Fonte:** intake demand-nature (D003/Q011) + RP §2 + RP §14 (TA LEVE) + RP §12 D03
- **Situacao:** rascunho
- **Disposicao:** discovery
- **Observacao:** Nao atinge min-conf 75 ate o hsb-landscape-keeper documentar o terreno Workspace/OAuth (criar tech-landscape-room-reservation.md). Confirmar: (1) o processo manual descrito e a fonte de verdade completa; (2) resolver os itens "a descobrir (spike)" no DISC-001 antes de promover.

---

## Caminho GREENFIELD: fundacao tecnica
<!-- origination: id=tech-foundation; blocks=true; min-confidence=75; kind=capture -->
> Rubric: **decidir a fundacao com criterios, nao por reflexo** (preencher se a
> demanda constroi software/modulo novo). No greenfield nao ha terreno a descobrir:
> o TA o **cria**. Registrar as escolhas base e o *porque*, para que sustentem ADRs
> e se tornem o ponto de partida do novo `tech-landscape`. **Se puramente
> brownfield:** nao aplicavel. `Disposicao: decided`, conteudo
> "N/A (brownfield, ver Classificacao Tecnica)".

### Selecao de stack (com criterios)

| Camada | Escolha | Criterio de decisao | Alternativa descartada |
|---|---|---|---|
| **Linguagem / runtime** | TypeScript (Node.js LTS) end-to-end | Linguagem unica reduz custo cognitivo de time pequeno; ecossistema maduro para OAuth2/OIDC e cliente Google Calendar; tipagem ajuda na correcao das regras temporais (RN-09..RN-12). | Python/Django, Java/Spring: sem ganho frente ao porte (~200 usuarios); fragmentariam a stack. |
| **Framework / app** | Backend: NestJS/Express (API REST). Frontend: React (Vite/Next) responsivo/mobile-first | REST cobre o CRUD e a consulta de disponibilidade sem complexidade extra; React atende NFR-05 (mobile ≥360px / tablet ≥768px). | GraphQL: modelo simples nao justifica overhead de schema/resolvers; SPA puro sem back reescreveria validacao/auth. |
| **Persistencia / dados** | Banco relacional transacional: PostgreSQL | **Ancora em NFR-01/RN-05 (first-commit-wins).** `EXCLUSION constraint` com `tstzrange` + `btree_gist` (ou transacao serializavel) rejeita no nivel do banco qualquer intersecao de intervalos para a mesma sala. A regra vira invariante de dados, nao logica de aplicacao propensa a corrida (RN-01..RN-03, EC-01). Suporta validacao por ocorrencia de series (RN-15). | **NoSQL/documento (MongoDB)**: sem constraint de exclusao multi-linha / transacao serializavel nativa sobre intervalos; first-commit-wins dependeria de locks aplicacionais frageis no requisito mais critico. |
| **Infra / deploy** | Container (Docker) em PaaS gerenciada (Cloud Run/App Service/equiv.) + Postgres gerenciado + worker assincrono de sync | Porte modesto e ≥99% horario comercial nao justificam Kubernetes proprio; PaaS + Postgres gerenciado entregam HA/backup prontos. | Kubernetes auto-gerenciado: overhead desproporcional; FaaS puro para o worker, mantido como opcao. |

### Arquitetura-alvo (C4: Contexto + Container; sync UMA VIA sistema → Calendar)

```text
C4 - CONTEXTO
  [Colaborador] e [Secretaria] --HTTPS--> SISTEMA DE RESERVA DE SALAS (novo; fonte de verdade)
       |-- OAuth2/OIDC --> [Provedor de Identidade Social (Google)]
       |-- REST + OAuth2 (uma via -->) --> [Google Calendar API] (espelho de leitura; NAO retroalimenta per C-Q02)

C4 - CONTAINERS
  Web Frontend (React, responsivo) --REST/JSON--> API/Backend (NestJS/Express)
     - Auth OAuth2/OIDC; validacao anti-conflito atomica; regras RN-01..RN-16
  API --SQL (txn)--> PostgreSQL (EXCLUSION constraint anti-overlap; reservas/salas/series)
  API --enfileira evento--> Worker de Sync Calendar (assincrono; retry/backoff; EC-02) --REST (uma via -->)--> Google Calendar API
  Direcao do sync: SISTEMA --> Google Calendar. O Calendar nunca escreve de volta neste release (NFR-02 ≤2 min).
```

### Estrutura e convencoes de repositorio

- **Organizacao de pastas / modulos:** monorepo (workspaces) com `apps/web`, `apps/api`, `packages/shared` (DTOs/enums de status). Backend por dominio (`reservations/`, `availability/`, `auth/`, `calendar-sync/`). Migracoes versionadas (a EXCLUSION constraint da NFR-01 nasce em migracao explicita e testada).
- **Convencoes de nomenclatura / lint / teste:** ESLint + Prettier compartilhados; TS `strict`. Teste unitario para regras temporais (RN-09..12) e series (RN-15); **teste de integracao obrigatorio de concorrencia** exercitando a constraint (EC-01/NFR-01); e2e dos happy paths das Jornadas A/B/C; nomes espelhando os Given/When/Then da Secao 7.
- **Estrategia de branching / CI:** trunk-based + PR com revisao; `main` sempre deployavel. CI: lint → build → unit/integracao (incl. teste de concorrencia NFR-01) → e2e; deploy continuo p/ homologacao + promocao manual; migracoes forward-only.

**Provenencia**
- **Confianca:** 78
- **Origem:** cto_authored
- **Fonte:** RP §6 (RN-01..16, sync uma via) + §8 (NFR-01/02/03/05/06/09/10) + §5 escopo + intake (natureza Hibrida, TA LEVE)
- **Situacao:** respondida
- **Disposicao:** decided
- **Observacao:** CTO confirmou a stack; a ancora de persistencia transacional e inegociavel; modelo de credencial OAuth do Calendar gated DISC-001.

---

## Sistemas e componentes afetados
<!-- origination: id=affected-systems; blocks=true; min-confidence=70; kind=capture -->
> Rubric: o mapa de blast-radius. Cada servico/modulo tocado e a natureza do
> impacto. Herda os sistemas/integracoes que o RP nomeou no escopo.

| Sistema / Componente | Natureza do impacto |
|---|---|
| Novo sistema de reserva de salas (software-core) | Novo, criado neste release (CRUD, anti-double-booking, recorrencia, login social) |
| Google Calendar (Workspace da organizacao) | Consumido apenas (uma via: o sistema escreve eventos; o Calendar nao retroalimenta) |
| Processo manual: mural fisico | Migrado/descontinuado. Retirada fisica apos ≤2 semanas do go-live |
| Processo manual: Google Forms (link via WhatsApp) | Migrado/descontinuado. Encerramento formal apos ≤2 semanas |
| WhatsApp (canal do Forms) | Descontinuado como canal de reservas. Fora do escopo tecnico |

**Provenencia**
- **Confianca:** 80
- **Origem:** cto_authored
- **Fonte:** RP §5 scope + intake demand-nature (D003/Q011)
- **Situacao:** respondida
- **Disposicao:** decided
- **Observacao:** CTO confirmou a natureza de impacto para todos os sistemas listados.

---

## Impacto arquitetural
<!-- origination: id=architectural-impact; blocks=true; min-confidence=75; kind=capture -->
> Rubric: territorio exclusivo do CTO (migrado do antigo RP §8). Para cada area
> tocada, o impacto e a nota arquitetural (padrao a seguir/evitar). Preencher
> apenas as areas relevantes; nao forcar as irrelevantes.

| Area | Impacto | Nota arquitetural |
|---|---|---|
| **Modelo de dados** | Entidades: sala, reserva (intervalo inicio/fim), usuario, serie recorrente. Elemento de carga: exclusividade (sem sobreposicao de intervalos para a mesma sala, RN-01/03, NFR-01 CRITICO); sobreposicao parcial conta (RN-03). | Modelar reserva como intervalo `[inicio,fim)`; exclusividade como invariante de dados (`EXCLUDE USING gist` com `tstzrange`), nao so validacao de aplicacao. Recorrencia: persistir ocorrencias materializadas (cada uma participa da constraint, RN-15). |
| **Eventos / mensageria** | Sync com Calendar = efeito colateral assincrono e retriavel, desacoplado da transacao de confirmacao (EC-02, RN-04). | **Transactional outbox + worker**: gravar a intencao de sync na mesma txn; worker consome e chama a API com retry/backoff; nunca acoplar a chamada externa ao commit; idempotencia por chave da reserva. |
| **Frontend** | UI responsiva/mobile-first (NFR-05); disponibilidade quase real-time (US-03, NFR-03). | Priorizar fluxo de reserva em viewport movel; re-fetch sob demanda atende o MVP (push/realtime opcional); aviso "Calendar e espelho read-only" (EC-13). |
| **Seguranca** | Login social OAuth2/OIDC (NFR-06); credencial/escopo da Calendar API (gated no Discovery); LGPD basico (NFR-07). | Separar OIDC de login (identidade) da credencial de escrita no Calendar (service account c/ delegacao de dominio vs por usuario, gated no spike); menor privilegio nos escopos; LGPD: base legal/retencao/exclusao, revisao Juridico/DPO. |
| **Multi-tenancy** | **N/A** (organizacao unica, gatilho ausente confirmado RP §14). | Nao introduzir abstracao de tenancy especulativa. |
| **Desempenho / Escalabilidade** | Escala modesta (~200 usuarios, pico 10h-16h); o constraint real e a correcao sob concorrencia na escrita (NFR-01), nao volume. Alvos ≤2s/≤3s p95 (NFR-03); ≥99% (NFR-09). | A constraint de exclusao serializa naturalmente confirmacoes conflitantes; a complexidade vai para a atomicidade do booking, nao para escala horizontal. |
| **Observabilidade** | Status/fila de sync, contadores de conflito, latencia de propagacao ao Calendar (vs ≤2 min). | Instrumentar o worker de outbox (itens pendentes, idade da fila, alerta vs ≤2 min); contador de conflitos (saude do anti-double-booking); histograma de latencia sistema→Calendar. |

**Provenencia**
- **Confianca:** 78
- **Origem:** cto_authored
- **Fonte:** RP §6/§8/§9 + §14 (multi-tenancy ausente; TA LEVE)
- **Situacao:** respondida
- **Disposicao:** decided
- **Observacao:** CTO endossou o impacto arquitetural ao comitar o veredito e aprovar os ADRs; modelo de credencial Calendar gated DISC-001; LGPD requer revisao DPO.

---

## Integracoes necessarias
<!-- origination: id=integrations; blocks=true; min-confidence=70; kind=capture -->
> Rubric: as integracoes do RP, agora sob a lente de **viabilidade tecnica**
> (migrado do antigo RP §7). Para cada sistema: tipo, protocolo e viabilidade /
> riscos conhecidos. Se a demanda nao tiver integracoes, registrar "nenhuma" com
> `Disposicao: decided`.

> **Contexto:** sync uma via (sistema → Calendar) ≤2 min; alteracoes no Calendar nao retroalimentam (RN-04, NFR-02/08, US-06, EC-02/04/13); login social, SSO/Outlook fora do escopo.

| Sistema | Tipo | Protocolo | Viabilidade / Riscos conhecidos |
|---|---|---|---|
| Google Calendar | Externo / API | OAuth 2.0 / Google Calendar API REST (`calendar.events`) | **Viavel com ressalvas.** A tecnologia e madura (muitos sistemas escrevem eventos via Calendar API com OAuth2); nao ha risco tecnico no padrao uma-via (`calendar.events`, ≤2 min). A ressalva e de **configuracao organizacional**: confirmar no spike (DISC-001) se o admin do Workspace permite grant a apps de terceiros, o escopo, o modelo de credencial e as quotas. Risco residual: restricao administrativa do Workspace, mitigavel. |
| Login social / Autenticacao | Externo / Auth | OAuth 2.0 / OpenID Connect (login social; SSO corporativo fora do escopo) | **Viavel.** OAuth2/OIDC padrao; ausencia de SSO corporativo neste release reduz a complexidade. Sem ressalva de viabilidade tecnica. |

**Provenencia**
- **Confianca:** 76
- **Origem:** cto_authored
- **Fonte:** RP §5/§8 (NFR-02/06/08) + classificacao tecnica (Workspace/OAuth → Discovery)
- **Situacao:** respondida
- **Disposicao:** decided
- **Observacao:** Google Calendar "viavel com ressalvas" gated DISC-001; se o admin negar o grant, escala para risco bloqueante. Login social sem dependencia de Discovery.

---

## Build vs. buy
<!-- origination: id=build-vs-buy; blocks=false; min-confidence=0; kind=capture -->
> Rubric: para cada capacidade nao-trivial: construir, comprar/integrar terceiro
> ou reutilizar algo existente? A decisao tem efeito direto em custo, prazo e risco.
> Pular (com `Disposicao: decided`, "nenhuma decisao make-or-buy relevante") se nao
> houver nenhuma.

| Capacidade | Decisao | Justificativa | Efeito em custo/prazo |
|---|---|---|---|
| Nucleo de reserva + anti-double-booking (CRUD, recorrencia, first-commit-wins) | **Construir** | Propriedade central/diferenciadora (NFR-01, RN-05, EC-01); nenhum produto de prateleira garante a regra exata sob concorrencia. | Maior parte do esforco; concentra o risco tecnico (TA-Q03). |
| Autenticacao / login social | **Reutilizar/Comprar** | Provedor OAuth2/OIDC (Google); nao construir gestao de credenciais. SSO fora do release. | Reduz esforco e risco de seguranca; sem licenca adicional. |
| Sincronizacao de agenda (sistema → Calendar, uma via) | **Reutilizar** | Google Calendar API REST (`calendar.events`); nao construir backend de calendario. | Baixo custo, dentro de quota gratuita (~200 usuarios); viabilidade depende de TA-Q01/Q02/Q04. |
| Persistencia transacional | **Reutilizar** | Banco relacional gerenciado (ACID/concorrencia p/ NFR-01) sem reinventar bloqueio. | Custo operacional modesto; acelera a garantia transacional. |

**Provenencia**
- **Confianca:** 68
- **Origem:** ai_drafted
- **Fonte:** RP §5 + §6 (RN-04/05) + §8 (NFR-01/02/06/08/10) + §9 (EC-01) + tech-foundation + classificacao
- **Situacao:** respondida
- **Disposicao:** decided (não bloqueante; CTO aceitou as decisoes make-or-buy)
- **Observacao:** "Reutilizar Calendar API" condicionado a TA-Q01/Q02/Q04 (DISC-001). Secao não bloqueante.

---

## Alternativas consideradas
<!-- origination: id=alternatives; blocks=true; min-confidence=70; kind=capture -->
> Rubric: **a justificativa, nao apenas a conclusao** (padrao design-doc,
> Google/RFC). Registrar o que foi avaliado e **por que foi descartado** da ao
> downstream o contexto para decidir sobre a implementacao, e impede que a mesma
> alternativa seja reavaliada mais tarde. Uma linha por alternativa significativa.

| Alternativa | Pros | Contras | Por que NAO foi escolhida |
|---|---|---|---|
| **Sincronizacao bidirecional (Calendar ↔ sistema)** | Reflete alteracoes feitas no Calendar; evita divergencia silenciosa | Exige webhooks/push + reconciliacao; politica de conflito; amplia quota/falha; incognitas nao de-arriscadas | Fora do escopo (RP §5; C-Q02/RN-04/NFR-02/08). A uma-via atende o objetivo sem a complexidade de reconciliacao; bidirecional fica p/ fase futura (TA-Q02). |
| **Google Calendar como fonte de verdade (sem banco proprio)** | Elimina persistencia local; ja compartilhado | A Calendar API nao oferece exclusividade transacional sobre intervalos; sem garantia de first-commit-wins sob corrida | Nao garante NFR-01 (RN-01/05, EC-01). O sistema precisa ser fonte de verdade autoritativa (RN-04) p/ honrar first-commit-wins (TA-Q03). |
| **Persistencia NoSQL/documento** | Esquema flexivel; escala horizontal | Exclusividade de intervalo exigiria coordenacao aplicacional (lock distribuido/otimista), fragil sob corrida | Ajuste improprio; escala modesta (NFR-10) nao justifica trade-offs de NoSQL; relacional resolve first-commit-wins direto e auditavel. |
| **Validacao otimista sem trava transacional** | Menor contencao; caminho rapido no caso comum | Checagem e gravacao nao atomicas → janela de corrida sob concorrencia | Nao garante first-commit-wins (RN-05, EC-01); adota-se txn/serializavel que torna checagem-gravacao atomicas, unica abordagem que satisfaz NFR-01. |

**Provenencia**
- **Confianca:** 76
- **Origem:** cto_authored
- **Fonte:** RP §5/§6 (RN-01/02/04/05) + §8 (NFR-01/02/08) + §9 (EC-01/04/13) + TA-Q02/Q03/Q04 + C-Q02
- **Situacao:** respondida
- **Disposicao:** decided
- **Observacao:** CTO endossou as alternativas ao aprovar os ADRs; a alternativa transacional vencedora firmada em ADR-001; sync uma-via via outbox+worker firmada em ADR-002/ADR-003.

---

## Viabilidade dos NFRs · *(mapeado ao RP, Secao 8)*
<!-- origination: id=nfr-feasibility; blocks=true; min-confidence=75; kind=capture -->
> Rubric: **fecha o loop produto ↔ tecnica.** O PO declarou requisitos de qualidade
> no RP (Secao 8); aqui o CTO responde, NFR por NFR, se sao **viaveis** e **como**
> (os *quality scenarios* do arc42). Um NFR inviavel e sinal de veto ou re-escopo,
> nao um detalhe. Uma linha por NFR herdado do RP §8.

| NFR (do RP §8) | Requisito de qualidade (PO) | Viavel? | Como sera atingido / abordagem | Risco / ressalva |
|---|---|---|---|---|
| NFR-01 [CRITICO] | O sistema nunca permite duas reservas confirmadas sobrepostas na mesma sala, inclusive sob concorrencia de acessos. Propriedade nao-negociavel. | **Sim** | Exclusao transacional no banco relacional (`EXCLUDE USING gist` sobre (sala, tstzrange) ou txn serializavel) → first-commit-wins (RN-05, EC-01); checagem+gravacao atomicas; o banco e o arbitro. | Nao-negociavel: exige teste de concorrencia dedicado. Alto risco se feito so na aplicacao (read-then-write). Mapeado a TA-Q03. |
| NFR-02 | Toda reserva confirmada ou cancelada deve refletir no Google Calendar em **≤2 minutos** (sync uma via: sistema → Calendar). | **Com ressalvas** | Worker assincrono (fila + retry/backoff) propaga ≤2 min (folgado p/ job assincrono); reserva persiste como fonte de verdade independentemente do sync. | **Gated na Discovery** (TA-Q01/Q04): quotas/rate-limits e modelo de credencial nao confirmados. |
| NFR-03 | Consulta de disponibilidade: resposta em **≤2 s** (p95); confirmacao de reserva: **≤3 s** (p95). | **Sim** | Indices (sala+intervalo) + consulta simples sobre escala modesta; ≤2s/≤3s p95 confortaveis. | Validar p95 no pico; confirmacao inclui a txn anti-conflito, medir junto a NFR-01. |
| NFR-04 [CRITICO] | Criar uma reserva no sistema deve ser **mais simples do que preencher o Google Forms atual**; secretaria e usuario comum devem conseguir criar uma reserva sem treinamento formal. | **Com ressalvas** | Produto/UX: fluxo mais curto que o Forms; validacao qualitativa com a secretaria como criterio de aceite (RP §11). | Validado por produto, nao por arquitetura. O CTO nao atesta usabilidade. Risco de adocao se o baseline nao for medido. |
| NFR-05 | O sistema deve ser **responsivo e mobile-friendly** (fluxo atual ocorre majoritariamente via WhatsApp/celular). Breakpoints minimos: mobile ≥ 360px, tablet ≥ 768px. | **Sim** | Front responsivo validado nos breakpoints (≥360px/≥768px). | Risco baixo; testar fluxo critico em dispositivo movel real. |
| NFR-06 | Acesso somente via **login social** autenticado; cada reserva e atribuivel a um usuario identificado. SSO corporativo esta fora deste release. | **Com ressalvas** | Login social OAuth/OIDC (Google); cada reserva atribuida a user_id. | **Gated na Discovery** (TA-Q01): consent screen/escopos/restricao de dominio a confirmar. |
| NFR-07 | Dados de participantes (nome, e-mail, horarios de presenca) tratados conforme **LGPD basico** (requisito deste release). Base legal a definir (legitimo interesse ou consentimento); politica de retencao a estabelecer (ex.: 12 meses apos a reuniao); mecanismo de exclusao a pedido previsto. | **Com ressalvas** | LGPD basico: criptografia em repouso, retencao (~12 meses), exclusao a pedido. | **Exige revisao Juridico/DPO**: base legal e decisao legal. Nao-bloqueante p/ Fase B2; bloqueante p/ release. |
| NFR-08 | O sistema interopera exclusivamente com a **API do Google Calendar** neste release (uma via: sistema → Calendar); integracao com Outlook esta fora do escopo. | **Com ressalvas** | Interoperacao so com Calendar API, uma via; Outlook fora. Reusa worker/credencial de NFR-02. | **Gated na Discovery** (TA-Q01); risco de scope creep se bidirecional reentrar (R05). |
| NFR-09 | Disponibilidade **≥99%** durante o horario comercial; sem requisito de SLA 24/7. | **Sim** | ≥99% horario comercial com hospedagem gerenciada (managed DB + app stateless), sem HA multi-regiao; manutencao fora do horario. | Risco baixo; indisponibilidade da Calendar API nao derruba o sistema (sync assincrono/tolerante). |
| NFR-10 | O sistema deve suportar ate **~200 usuarios**, com pico de carga no horario comercial (10h-16h). | **Sim** | ~200 usuarios e carga pequena; 1 instancia + DB dimensionado p/ pico. | Risco muito baixo; confirmar em teste de carga. |

**Provenencia**
- **Confianca:** 80
- **Origem:** cto_authored
- **Fonte:** RP §8 (NFR-01..10) + arch-impact + RN-05/EC-01 + TA-Q01/Q03/Q04
- **Situacao:** respondida
- **Disposicao:** decided
- **Observacao:** NFR-01/03/05/09/10 viaveis sem ressalva; NFR-02/06/08 mantem "com ressalvas" gated DISC-001; NFR-07 revisao DPO. Coluna "Requisito de qualidade" preservada (Origin: inherited).

---

## Testabilidade e observabilidade
<!-- origination: id=testability-observability; blocks=true; min-confidence=70; kind=capture -->
> Rubric: como **provar** que funciona e como **ver** em producao. Sem isso, os
> criterios de aceite do RP nao podem ser verificados e o comportamento nao pode
> ser monitorado.

| Dimensao | Abordagem |
|---|---|
| **Estrategia de testes** | Unitarios (RN-01..16, foco em validacao de sobreposicao RN-01/03, parametros temporais RN-09/10/11, FCFS RN-13; casos-tabela de fronteira de intervalo); integracao (Calendar API mockada/sandbox: criacao/remocao, ≤2 min, caminho de falha com retry/backoff EC-02/EC-11; EC-04/EC-13 sem write-back); e2e (Jornadas A/B/C, ALT-1..5, US-01..08); **harness de concorrencia dedicado [LOAD-BEARING]** para first-commit-wins (RN-05/EC-01), N confirmacoes simultaneas, exatamente uma persiste, gate de release (sem ele o NFR-01 nao e demonstravel); regressao: nucleo anti-double-booking, revalidacao na edicao (EC-09/RN-12), series (EC-05), DST (EC-06), parametros (EC-12). |
| **Dados de teste / ambiente** | O ambiente de testes deve reproduzir os seguintes cenarios (edge cases do RP §9): EC-01: reservas concorrentes (race condition), dois usuarios confirmando a mesma sala no mesmo instante; EC-02: falha da API do Google Calendar no momento da confirmacao ou cancelamento; EC-03: uso paralelo do canal antigo (mural/Forms) durante a transicao pos go-live; EC-04: alteracao feita diretamente no Google Calendar sem atuar no sistema; EC-05: reserva recorrente com uma ou mais ocorrencias em conflito com reservas existentes; EC-06: fuso horario / horario de verao (DST), criacao de reserva em horario ambiguo na transicao DST (premissa de mono-fuso a confirmar); EC-07: sala em manutencao, tentativa de criar reserva em sala com estado de manutencao ativo; EC-08: participante externo sem login tentando criar reserva diretamente; EC-09: edicao de reserva que gera conflito com outra reserva ativa; EC-10: criacao de reserva em nome de terceiro ausente (modelo flat); EC-11: sistema fora do ar ou sem conectividade no momento da confirmacao; EC-12: tentativa de criar reserva no passado ou fora da janela de antecedencia maxima (RN-09/10/11); EC-13: divergencia silenciosa entre Calendar e sistema apos edicao direta no Calendar. |
| **Telemetria / metricas tecnicas** | Contador de conflitos bloqueados (prova viva do NFR-01); latencia de propagacao ao Calendar (p50/95/99 vs ≤2 min, NFR-02); taxa de falha/retry de sync + profundidade/idade da fila; p95 de consulta (≤2s) e confirmacao (≤3s) por horario de pico (NFR-03/10); disponibilidade em horario comercial (≥99%, NFR-09). |
| **Logs / alertas** | Alerta de sync pendente acima do SLA (≤2 min / profundidade da fila, EC-02/EC-13); alerta de falhas OAuth/credencial (TA-Q01, bloqueia toda a sync); alerta de pico de erro de confirmacao (incl. EC-11); log de auditoria de criacao/edicao/cancelamento (quem operou, relevante ao modelo flat RN-06 e a LGPD NFR-07). |

**Provenencia**
- **Confianca:** 76
- **Origem:** cto_authored
- **Fonte:** RP §9 (EC-01..13) + §11 + §8 (NFR-01/02/03/09/10) + §6 (RN-01..16) + TA-Q01/Q03/Q04
- **Situacao:** respondida
- **Disposicao:** decided
- **Observacao:** CTO endossou a estrategia ao aprovar os ADRs e o veredito; harness de concorrencia (EC-01) e gate de release; limiares de alerta (≤2 min, p95) e log de auditoria firmes.

---

## Restricoes rigidas
<!-- origination: id=hard-constraints; blocks=true; min-confidence=75; kind=capture -->
> Rubric: condicoes nao-negociaveis que limitam o espaco de solucao. O PO nao as
> suaviza nem as reinterpreta. Se discordar, escala explicitamente
> (`interactions/06-cto-to-po.md`). Se nao houver restricoes rigidas, registrar
> "nenhuma" com `Disposicao: decided`.

| Restricao | Tipo | Detalhe | Efeito no escopo |
|---|---|---|---|
| **Exclusividade transacional / first-commit-wins** | Tecnico | NFR-01 nao-negociavel: nunca duas reservas confirmadas sobrepostas, mesmo sob concorrencia (RN-05, EC-01). | Define a escolha de persistencia: store transacional com nao-sobreposicao. Solucoes sem garantia transacional descartadas. |
| **Sincronizacao uma-via (sistema → Calendar)** | Plataforma/Externo | Firmado C-Q02: sistema e fonte de verdade; Calendar e espelho; nao retroalimenta (EC-04/EC-13). | Sem reconciliacao bidirecional neste release; sem webhooks de entrada. |
| **Somente Google Calendar; sem Outlook; sem SSO corporativo** | Externo | Escopo firmado (RP §5; NFR-06/08): so Calendar API; so login social. | Login social e o unico modelo de identidade; inclusoes disparam R05 + reavaliacao do TA. |
| **Conformidade LGPD basica** | Seguranca/Compliance | Dados de participantes (NFR-07): base legal, retencao e exclusao a pedido. | Revisao Juridico/DPO obrigatoria antes do release; retencao/exclusao como requisitos de aceite. |
| **Dependencia da configuracao do Google Workspace** | Externo | O grant OAuth a apps de terceiros deve ser permitido pelo admin (RP §14 ponto (a); D03); escopos/credencial dependem do ambiente real. | Gate de Discovery: se o grant for negado, a integracao com o Calendar precisa ser re-escopada. |

**Provenencia**
- **Confianca:** 80
- **Origem:** cto_authored
- **Fonte:** RP §5/§6 (RN-01/05; sync uma-via C-Q02) + §8 (NFR-01/06/07/08) + §14 (TA LEVE; D03)
- **Situacao:** respondida
- **Disposicao:** decided
- **Observacao:** CTO confirmou todas as restricoes; item Workspace e gate via R1/DISC-001. Se o admin negar o grant, gatilho de re-escopo da integracao.

---

## Riscos tecnicos e mitigacoes
<!-- origination: id=tech-risks; blocks=true; min-confidence=75; kind=capture -->
> Rubric: riscos **tecnicos** aqui (riscos de produto/negocio permanecem no RP §12).
> Cada risco carrega categoria, probabilidade, impacto e mitigacao.

| Risco | Categoria | Probabilidade | Impacto | Mitigacao |
|---|---|---|---|---|
| Workspace nega/restringe grant OAuth a apps de terceiros (`calendar.events`) | Integracao | Media | Alto | Antecipar spike DISC-001 (politica do Workspace, escopos) antes do commit de arquitetura; plano B de credencial (service account c/ delegacao de dominio vs por usuario, TA-Q01); escalar ao admin cedo. **Gate** da integracao (RP §12 D03). |
| Race condition no anti-double-booking sob acesso simultaneo | Tecnica | Media | Alto | NFR-01 critico: gravacao atomica via constraint/serializavel (RN-05); harness de concorrencia dedicado (EC-01, TA-Q03). |
| Quota/latencia da Calendar API compromete sync ≤2 min | Integracao | Baixa-Media | Medio | Worker assincrono c/ backoff; ≤2 min tem folga; monitorar quota e alertar antes do teto (TA-Q04). |
| Divergencia silenciosa Calendar ↔ sistema (sync uma-via) | Dados | Media | Medio | Aviso na UI (Calendar e espelho read-only, EC-04/EC-13); sistema e fonte unica de verdade (RN-04/C-Q02); sem reconciliacao reversa neste release. |
| Tratamento incorreto de fuso/DST | Dados | Baixa | Medio | Timestamps em UTC c/ tz explicito; bloquear/sinalizar intervalos ambiguos (EC-06); confirmar premissa mono-fuso. |
| Falha de sync deixa estado inconsistente | Integracao | Baixa | Medio | Outbox + retry idempotente; reserva confirmada localmente independe do sync (EC-02); sinalizar "sincronizacao pendente". |

**Provenencia**
- **Confianca:** 80
- **Origem:** cto_authored
- **Fonte:** RP §9 (EC-01/02/04/06/13) + §12 D03 + §8 (NFR-01/02) + §6 (RN-04/05) + classificacao + TA-Q01/Q03/Q04
- **Situacao:** respondida
- **Disposicao:** decided
- **Observacao:** CTO confirmou probabilidades/impactos. O risco de grant OAuth do Workspace e o gate (DISC-001/TA-Q01). Se bloqueado, gatilho de veto/re-escopo. Riscos de produto/negocio permanecem no RP §12.

---

## Decisoes arquiteturais (ADRs)
<!-- origination: id=adrs; blocks=true; min-confidence=75; kind=capture -->
> Rubric: direcao arquitetural no nivel do CTO. A IA pode chegar com **ADRs
> sugeridos** (reutilizados da base de conhecimento); o CTO aprova/ajusta (o
> momento WOW de `03-cto.md` §3/§12). Breakdown fino e ADRs de implementacao
> pertencem ao Tech Backlog do Tech Lead. Cada ADR carrega a decisao, a
> justificativa e a aprovacao do CTO.

| # | Decisao | Justificativa | Aprovacao do CTO |
|---|---|---|---|
| ADR-001 | Persistencia relacional transacional com garantia de nao-sobreposicao (intervalos `[inicio,fim)` por sala; `EXCLUDE USING gist` com `tstzrange` + `room_id` ou txn serializavel), nao so validacao de aplicacao. | NFR-01 [CRITICO] nao-negociavel; a invariante deve viver onde a serializacao e garantida (o banco), tornando first-commit-wins consequencia da constraint (RN-01/03/05, EC-01); sustenta sobreposicao parcial (RN-03). | ✓ |
| ADR-002 | Sincronizacao uma-via assincrona via transactional outbox + worker idempotente com retry/backoff. | A reserva e fonte de verdade e confirma independentemente do Calendar (EC-02); desacoplar protege NFR-03 e da folga ao NFR-02; idempotencia evita eventos duplicados em retries. | ✓ |
| ADR-003 | Sistema = fonte de verdade; Calendar = espelho read-only; sem reconciliacao de volta neste release. | Firmado em produto (C-Q02, RN-04, NFR-08, EC-04/EC-13); evita complexidade de sync bidirecional; a nao-deteccao de divergencia e consequencia explicita do escopo uma-via. | ✓ |
| ADR-004 | Autenticacao federada via OAuth2/OIDC (login social Google); sem senha propria e sem SSO neste release. | NFR-06 (acesso autenticado, reserva atribuivel); reusa o IdP que os ~200 usuarios ja tem; minimiza dado sensivel (alinha NFR-07); caminho de upgrade p/ SSO sem retrabalho de identidade. | ✓ |
| ADR-005 | Tempo em UTC com fuso explicito; premissa mono-fuso; bloquear/forcar confirmacao explicita em intervalos ambiguos de DST. | EC-06 exige horarios nao-ambiguos; correcao de RN-09/10/11 depende de ancora temporal unica. Ressalva: premissa mono-fuso a confirmar. | ✓ |
| ADR-006 | Modelo de credencial da Calendar API: **A DECIDIR no spike de Discovery** (service account c/ delegacao de dominio vs delegacao por usuario). Nao definido neste TA. | Depende de terreno desconhecido: config do Workspace e grant a apps de terceiros (TA-Q01/Q05, D03; current-state gated). Decidir agora seria inventar sobre terreno nao descoberto. Vincular a DISC-001; reconverter em ADR apos o spike. | (gated DISC-001) |

**Provenencia**
- **Confianca:** 80
- **Origem:** cto_authored
- **Fonte:** RP §6/§8/§9 + §12 D03 + classificacao (Hibrido) + TA-Q01..Q05
- **Situacao:** respondida
- **Disposicao:** decided
- **Observacao:** ADR-001..005 aprovados (✓); ADR-006 deliberadamente nao definido (gated DISC-001). ADRs greenfield aprovados semeiam o tech-landscape. Breakdown fino (RFC-5545 recorrencia, esquema de tabelas, soft-delete US-05) vai p/ o Tech Backlog.

---

## Avaliacao de esforco e custo (firme)
<!-- origination: id=effort-cost; blocks=true; min-confidence=70; kind=capture -->
> Rubric: somente uso interno. Estas sao as estimativas **firmes** do CTO;
> substituem a estimativa preliminar do PO (RP Secao 13). Serao refinadas pelo
> Tech Lead no Tech Backlog. Nao e compromisso contratual nem material para cliente.

> **Contexto (insumos de dimensionamento herdados do RP):**
> O RP §13 deferiu a estimativa ao CTO/Tech Lead. Nao ha numero preliminar do PO.
> Insumos de dimensionamento do produto:
> - **Escopo do release:** CRUD de reservas + integracao Google Calendar uma-via + login social + anti-double-booking + recorrencia (series) + migracao e descontinuacao do processo manual.
> - **Escala:** ~200 usuarios (NFR-10), pico no horario comercial (10h-16h).
> - **SLAs:** disponibilidade ≥99% (horario comercial); latencia sync ≤2 min (NFR-02); tempo de resposta ≤2s consulta / ≤3s confirmacao (p95, NFR-03).
> - **Complexidade de integracao:** OAuth Google Calendar a confirmar (TA-Q01/Q04). O spike de Discovery pode gerar trabalho adicional antes de fechar a estimativa.

### Esforco de desenvolvimento (dias-pessoa; time pequeno; ai_drafted)

| Area | Estimativa | Senioridade |
|---|---|---|
| Backend: nucleo de reservas (CRUD, maquina de estados, parametros temporais) | 12 dias | Pleno (revisao Senior) |
| Backend: anti-double-booking + recorrencia (txn first-commit-wins; series por ocorrencia) | 8 dias | Senior |
| Integracao / OAuth: Google Calendar + login social (worker async ≤2 min; OIDC) | 10 dias | Senior |
| Frontend: UI responsiva (disponibilidade, CRUD, terceiro/flat, series, aviso espelho) | 12 dias | Pleno |
| QA: incl. harness de concorrencia (EC-01/NFR-01), 13 ECs, integracao de sync, carga p95 | 8 dias | QA |
| LGPD basica + migracao/descontinuacao (retencao/exclusao; plano de migracao mural/Forms) | 4 dias | Pleno |
| **Total (desenvolvimento)** | **~54 dias** | (nao inclui o spike de Discovery, ~2 a 4 dias) |

### Impacto em infraestrutura

Modesto: 1 app host (API+UI) + 1 banco relacional gerenciado + 1 worker async. Sem multi-regiao, sem multi-tenancy, sem cluster complexo (~200 usuarios, NFR-10; ≥99% horario comercial NFR-09).

### Impacto em custo com terceiros

Baixo a nulo no MVP: Google Calendar API dentro da quota gratuita no volume previsto (a confirmar no spike, TA-Q04); provedor OAuth/login social (Google) gratuito. Sem licencas pagas. Dependendo do spike, a configuracao de credencial pode gerar custo administrativo, nao de licenca.

### Impacto em custo operacional recorrente

Baixo: hospedagem (app+worker) + banco gerenciado + observabilidade. Trafego pequeno; armazenamento/banda marginais.

### Avaliacao de TCO

O release cria uma fundacao reutilizavel (stack + tech-landscape semeado) para fases futuras: Outlook na Fase 2 reusa o worker e o modelo fonte-de-verdade→espelho; SSO na Fase 3 se apoia na camada de auth existente; analytics e lembretes na Fase 2 usam o modelo de reservas. O custo recorrente incremental e baixo; o release elimina o processo manual como divida operacional. O maior driver de longo prazo e adocao (R01/R02/R03, fora desta estimativa).

**Provenencia**
- **Confianca:** 72
- **Origem:** cto_authored
- **Fonte:** RP §5/§6/§8/§9 (escopo, RN-01/05, recorrencia, EC-01) + classificacao (Hibrido, KB→Discovery)
- **Situacao:** respondida
- **Disposicao:** decided
- **Observacao:** Estimativa firmada pelo CTO; linha Integracao/OAuth (10 dias) e custo com terceiros a re-firmar apos o spike DISC-001 (TA-Q01/Q04).

---

## Caminho de Discovery (se uma incognita tecnica bloqueia a conclusao)
<!-- origination: id=discovery-path; blocks=false; min-confidence=0; kind=capture -->
> Rubric: preencher **apenas** se uma incognita tecnica impede o fechamento da
> avaliacao. O CTO define o spike/investigacao; o PO determina o prazo fechado. A demanda
> retorna ao Discovery (`interactions/05-po-to-cto.md`). Se nada bloqueia, registrar
> "-" com `Disposicao: decided`.

| Incognita | Spike / Investigacao | Responsavel | Prazo fechado sugerido |
|---|---|---|---|
| Ambiente Google Workspace / OAuth nao documentado (gate de viabilidade) | DISC-001: documentar: (a) escopos OAuth concediaveis a apps de terceiros e se o admin permite grant; (b) modelo de credencial (service account c/ delegacao de dominio vs delegacao por usuario); (c) quotas/limites da Calendar API; (d) caracterizacao final do processo manual (mural+Forms+WhatsApp, secretaria). Produz o tech-landscape-room-reservation.md (via hsb-landscape-keeper). | CTO/Tech Lead + TI da organizacao (acesso ao Workspace); secretaria (processo) | ~2 a 4 dias (acesso ao ambiente real e o gargalo) |

**Provenencia**
- **Confianca:** 80
- **Origem:** ai_drafted
- **Fonte:** classificacao tecnica (KB inexistente) + RP §14 (TA LEVE pontos (a)/(d)) + RP §12 D03
- **Situacao:** rascunho
- **Disposicao:** discovery
- **Observacao:** DISC-001 destrava current-state (min-conf 75) e os pontos (a)/(d) do TA LEVE; NFR-02/06/08 e ADR-006 sao contingentes ao seu fechamento. Responsável pelo prazo fechado: PO; investigacao: CTO.

<!-- END OF DOCUMENT -->
