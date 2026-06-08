<!--
PHASE 3 DRAFT PASS — fill-ready content for hsb-doc-updater to merge into technical-assessment.md.
Each block is keyed by its section id. Origin: ai_drafted (partial confidence) unless noted.
The doc-updater is the SOLE writer of the DOC; this is orchestrator-routed proposer output.
For nfr-feasibility and integrations: MERGE the analysis columns into the EXISTING inherited rows
(keep the inherited "Requisito de qualidade" / system+protocol cells). For testability-observability:
replace only the three [a definir pelo CTO] dimensions; keep the inherited EC test-data row.
Language: pt-BR.
-->

# ===== SECTION: tech-foundation =====

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
- **Organização:** monorepo (workspaces) com `apps/web`, `apps/api`, `packages/shared` (DTOs/enums de status). Backend por domínio (`reservations/`, `availability/`, `auth/`, `calendar-sync/`). Migrações versionadas (a EXCLUSION constraint da NFR-01 nasce em migração explícita e testada).
- **Convenções:** ESLint + Prettier compartilhados; TS `strict`. Teste unitário para regras temporais (RN-09..12) e séries (RN-15); **teste de integração obrigatório de concorrência** exercitando a constraint (EC-01/NFR-01); e2e dos happy paths das Jornadas A/B/C; nomes espelhando os Given/When/Then da Seção 7.
- **Branching/CI:** trunk-based + PR com revisão; `main` sempre deployável. CI: lint → build → unit/integração (incl. teste de concorrência NFR-01) → e2e; deploy contínuo p/ homologação + promoção manual; migrações forward-only.

**Provenance**
- **Confidence:** 64
- **Origin:** ai_drafted
- **Source:** RP §6 (RN-01..16, sync uma via) + §8 (NFR-01/02/03/05/06/09/10) + §5 escopo + intake (natureza Híbrida, TA LEVE)
- **Status:** rascunho
- **Disposition:** ai_drafted
- **Hint:** CTO confirma: stack final (substituível desde que a persistência preserve a garantia atômica de não-sobreposição — ponto inegociável); mecanismo concreto de anti-overlap (EXCLUDE vs serializável vs lock); modelo de credencial OAuth do Calendar (gated no spike DISC-001); monorepo vs repos + PaaS específica (afeta effort/infra).

# ===== SECTION: current-state =====

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

**Provenance**
- **Confidence:** 54
- **Origin:** ai_drafted
- **Source:** intake demand-nature (D003/Q011) + RP §2 + RP §14 (TA LEVE) + RP §12 D03
- **Status:** rascunho
- **Disposition:** discovery
- **Hint:** Não atinge min-conf 75 até o hsb-landscape-keeper documentar o terreno Workspace/OAuth (criar tech-landscape-room-reservation.md). Confirmar: (1) o processo manual descrito é a fonte de verdade completa; (2) resolver os itens "a descobrir (spike)" no DISC-001 antes de promover.

# ===== SECTION: architectural-impact =====

| Área | Impacto | Nota arquitetural |
|---|---|---|
| **Modelo de dados** | Entidades: sala, reserva (intervalo início/fim), usuário, série recorrente. Elemento de carga: exclusividade — sem sobreposição de intervalos para a mesma sala (RN-01/03, NFR-01 CRÍTICO); sobreposição parcial conta (RN-03). | Modelar reserva como intervalo `[início,fim)`; exclusividade como invariante de dados (`EXCLUDE USING gist` com `tstzrange`), não só validação de aplicação. Recorrência: persistir ocorrências materializadas (cada uma participa da constraint, RN-15). |
| **Eventos / mensageria** | Sync com Calendar = efeito colateral assíncrono e retriável, desacoplado da transação de confirmação (EC-02, RN-04). | **Transactional outbox + worker**: gravar a intenção de sync na mesma txn; worker consome e chama a API com retry/backoff; nunca acoplar a chamada externa ao commit; idempotência por chave da reserva. |
| **Frontend** | UI responsiva/mobile-first (NFR-05); disponibilidade quase real-time (US-03, NFR-03). | Priorizar fluxo de reserva em viewport móvel; re-fetch sob demanda atende o MVP (push/realtime opcional); aviso "Calendar é espelho read-only" (EC-13). |
| **Segurança** | Login social OAuth2/OIDC (NFR-06); credencial/escopo da Calendar API (gated no Discovery); LGPD básico (NFR-07). | Separar OIDC de login (identidade) da credencial de escrita no Calendar (service account c/ delegação de domínio vs por usuário — gated no spike); menor privilégio nos escopos; LGPD: base legal/retenção/exclusão — revisão Jurídico/DPO. |
| **Multi-tenancy** | **N/A** — organização única (gatilho ausente confirmado RP §14). | Não introduzir abstração de tenancy especulativa. |
| **Desempenho / Escalabilidade** | Escala modesta (~200 usuários, pico 10h–16h); o constraint real é a correção sob concorrência na escrita (NFR-01), não volume. Alvos ≤2s/≤3s p95 (NFR-03); ≥99% (NFR-09). | A constraint de exclusão serializa naturalmente confirmações conflitantes; a complexidade vai para a atomicidade do booking, não para escala horizontal. |
| **Observabilidade** | Status/fila de sync, contadores de conflito, latência de propagação ao Calendar (vs ≤2 min). | Instrumentar o worker de outbox (itens pendentes, idade da fila, alerta vs ≤2 min); contador de conflitos (saúde do anti-double-booking); histograma de latência sistema→Calendar. |

**Provenance**
- **Confidence:** 64
- **Origin:** ai_drafted
- **Source:** RP §6/§8/§9 + §14 (multi-tenancy ausente; TA LEVE)
- **Status:** rascunho
- **Disposition:** ai_drafted
- **Hint:** CTO confirma: modelo de credencial Calendar (gated DISC-001); mecanismo de overlap (liga a tech-foundation/alternatives/NFR-01); estratégia de sync (outbox+worker; polling vs push ≤2 min); realtime no front; LGPD (revisão DPO).

# ===== SECTION: nfr-feasibility (MERGE analysis columns into existing NFR-01..10 rows) =====

| NFR | Viável? | Como será atingido / abordagem | Risco / ressalva |
|---|---|---|---|
| **NFR-01** [CRÍTICO] | **Sim** | Exclusão transacional no banco relacional (`EXCLUDE USING gist` sobre (sala, tstzrange) ou txn serializável) → first-commit-wins (RN-05, EC-01); checagem+gravação atômicas; o banco é o árbitro. | Não-negociável — exige teste de concorrência dedicado. Alto risco SE feito só na aplicação (read-then-write). Mapeado a TA-Q03. |
| **NFR-02** | **Com ressalvas** | Worker assíncrono (fila + retry/backoff) propaga ≤2 min (folgado p/ job assíncrono); reserva persiste como fonte de verdade independentemente do sync. | **Gated na Discovery** (TA-Q01/Q04): quotas/rate-limits e modelo de credencial não confirmados. |
| **NFR-03** | **Sim** | Índices (sala+intervalo) + consulta simples sobre escala modesta; ≤2s/≤3s p95 confortáveis. | Validar p95 no pico; confirmação inclui a txn anti-conflito — medir junto à NFR-01. |
| **NFR-04** [CRÍTICO] | **Com ressalvas** | Produto/UX: fluxo mais curto que o Forms; validação qualitativa com a secretária como critério de aceite (RP §11). | Validado por produto, não por arquitetura — o CTO não atesta usabilidade. Risco de adoção se o baseline não for medido. |
| **NFR-05** | **Sim** | Front responsivo validado nos breakpoints (≥360px/≥768px). | Risco baixo; testar fluxo crítico em dispositivo móvel real. |
| **NFR-06** | **Com ressalvas** | Login social OAuth/OIDC (Google); cada reserva atribuída a user_id. | **Gated na Discovery** (TA-Q01): consent screen/escopos/restrição de domínio a confirmar. |
| **NFR-07** | **Com ressalvas** | LGPD básico: criptografia em repouso, retenção (~12 meses), exclusão a pedido. | **Exige revisão Jurídico/DPO** — base legal é decisão legal. Não-bloqueante p/ Fase B2; bloqueante p/ release. |
| **NFR-08** | **Com ressalvas** | Interoperação só com Calendar API, uma via; Outlook fora. Reusa worker/credencial de NFR-02. | **Gated na Discovery** (TA-Q01); risco de scope creep se bidirecional reentrar (R05). |
| **NFR-09** | **Sim** | ≥99% horário comercial com hospedagem gerenciada (managed DB + app stateless), sem HA multi-região; manutenção fora do horário. | Risco baixo; indisponibilidade da Calendar API não derruba o sistema (sync assíncrono/tolerante). |
| **NFR-10** | **Sim** | ~200 usuários é carga pequena; 1 instância + DB dimensionado p/ pico. | Risco muito baixo; confirmar em teste de carga. |

**Provenance**
- **Confidence:** 68
- **Origin:** ai_drafted
- **Source:** RP §8 (NFR-01..10) + arch-impact + RN-05/EC-01 + TA-Q01/Q03/Q04
- **Status:** rascunho
- **Disposition:** ai_drafted
- **Hint:** CTO confirma cada linha. NFR-01/NFR-04 são os CRÍTICOS. NFR-02/06/08 contingentes ao spike OAuth/Workspace. NFR-07 depende de revisão Jurídico/DPO.

# ===== SECTION: integrations (MERGE viability column into existing 2 rows) =====

- **Google Calendar** → Viabilidade: **Viável com ressalvas.** Tecnologia madura/commoditizada (milhares de apps escrevem eventos via Calendar API com OAuth2); sem risco técnico no padrão uma-via (`calendar.events`, ≤2 min). A ressalva é de **configuração organizacional**: confirmar no spike (DISC-001) se o admin do Workspace permite grant a apps de terceiros, o escopo, o modelo de credencial e as quotas. Risco residual: restrição administrativa do Workspace — mitigável.
- **Login social / Autenticação** → Viabilidade: **Viável.** OAuth2/OIDC padrão; ausência de SSO corporativo neste release reduz a complexidade. Sem ressalva de viabilidade técnica.

**Provenance**
- **Confidence:** 68
- **Origin:** ai_drafted
- **Source:** RP §5/§8 (NFR-02/06/08) + classificação técnica (Workspace/OAuth → Discovery)
- **Status:** rascunho
- **Disposition:** ai_drafted
- **Hint:** Google Calendar é "com ressalvas" porque contingente à Discovery do Workspace (DISC-001/TA-Q01); se o admin negar o grant, escala para risco bloqueante. Login social sem dependência de Discovery.

# ===== SECTION: testability-observability (replace the 3 [a definir] dimensions; keep inherited EC test-data row) =====

- **Estratégia de testes:** unitários (RN-01..16, foco em validação de sobreposição RN-01/03, parâmetros temporais RN-09/10/11, FCFS RN-13; casos-tabela de fronteira de intervalo); integração (Calendar API mockada/sandbox — criação/remoção, ≤2 min, caminho de falha com retry/backoff EC-02/EC-11; EC-04/EC-13 sem write-back); e2e (Jornadas A/B/C, ALT-1..5, US-01..08); **harness de concorrência dedicado [LOAD-BEARING]** para first-commit-wins (RN-05/EC-01) — N confirmações simultâneas, exatamente uma persiste, gate de release (sem ele o NFR-01 não é demonstrável); regressão: núcleo anti-double-booking, revalidação na edição (EC-09/RN-12), séries (EC-05), DST (EC-06), parâmetros (EC-12).
- **Telemetria / métricas técnicas:** contador de conflitos bloqueados (prova viva do NFR-01); latência de propagação ao Calendar (p50/95/99 vs ≤2 min, NFR-02); taxa de falha/retry de sync + profundidade/idade da fila; p95 de consulta (≤2s) e confirmação (≤3s) por horário de pico (NFR-03/10); disponibilidade em horário comercial (≥99%, NFR-09).
- **Logs / alertas:** alerta de sync pendente acima do SLA (≤2 min / profundidade da fila — EC-02/EC-13); alerta de falhas OAuth/credencial (TA-Q01 — bloqueia toda a sync); alerta de pico de erro de confirmação (incl. EC-11); log de auditoria de criação/edição/cancelamento (quem operou — relevante ao modelo flat RN-06 e à LGPD NFR-07).

**Provenance**
- **Confidence:** 66
- **Origin:** ai_drafted
- **Source:** RP §9 (EC-01..13) + §11 + §8 (NFR-01/02/03/09/10) + §6 (RN-01..16) + TA-Q01/Q03/Q04
- **Status:** rascunho
- **Disposition:** ai_drafted
- **Hint:** CTO confirma — o harness de concorrência (first-commit-wins, EC-01) é o teste mais crítico; validar limiares de alerta (≤2 min, p95) e granularidade do log de auditoria face à LGPD.

# ===== SECTION: alternatives =====

| Alternativa | Prós | Contras | Por que NÃO foi escolhida |
|---|---|---|---|
| **Sincronização bidirecional (Calendar ↔ sistema)** | Reflete alterações feitas no Calendar; evita divergência silenciosa | Exige webhooks/push + reconciliação; política de conflito; amplia quota/falha; incógnitas não de-arriscadas | Fora do escopo (RP §5; C-Q02/RN-04/NFR-02/08). A uma-via atende o objetivo sem a complexidade de reconciliação; bidirecional fica p/ fase futura (TA-Q02). |
| **Google Calendar como fonte de verdade (sem banco próprio)** | Elimina persistência local; já compartilhado | A Calendar API não oferece exclusividade transacional sobre intervalos; sem garantia de first-commit-wins sob corrida | Não garante NFR-01 (RN-01/05, EC-01). O sistema precisa ser fonte de verdade autoritativa (RN-04) p/ honrar first-commit-wins (TA-Q03). |
| **Persistência NoSQL/documento** | Esquema flexível; escala horizontal | Exclusividade de intervalo exigiria coordenação aplicacional (lock distribuído/otimista), frágil sob corrida | Ajuste impróprio; escala modesta (NFR-10) não justifica trade-offs de NoSQL; relacional resolve first-commit-wins direto e auditável. |
| **Validação otimista sem trava transacional** | Menor contenção; caminho rápido no caso comum | Checagem e gravação não atômicas → janela de corrida sob concorrência | Não garante first-commit-wins (RN-05, EC-01); adota-se txn/serializável que torna checagem-gravação atômicas — única que satisfaz NFR-01. |

**Provenance**
- **Confidence:** 68
- **Origin:** ai_drafted
- **Source:** RP §5/§6 (RN-01/02/04/05) + §8 (NFR-01/02/08) + §9 (EC-01/04/13) + TA-Q02/Q03/Q04 + C-Q02
- **Status:** rascunho
- **Disposition:** ai_drafted
- **Hint:** CTO confirma/enriquece: a alternativa transacional vencedora (EXCLUDE vs serializable vs lock pessimista) pertence a tech-foundation/ADR; avaliar polling vs push/webhook p/ a sync uma-via (TA-Q04).

# ===== SECTION: hard-constraints =====

| Restrição | Tipo | Detalhe | Efeito no escopo |
|---|---|---|---|
| **Exclusividade transacional / first-commit-wins** | Técnico | NFR-01 não-negociável: nunca duas reservas confirmadas sobrepostas, mesmo sob concorrência (RN-05, EC-01). | Define a escolha de persistência: store transacional com não-sobreposição. Soluções sem garantia transacional descartadas. |
| **Sincronização uma-via (sistema → Calendar)** | Plataforma/Externo | Firmado C-Q02: sistema é fonte de verdade; Calendar é espelho; não retroalimenta (EC-04/EC-13). | Sem reconciliação bidirecional neste release; sem webhooks de entrada. |
| **Somente Google Calendar; sem Outlook; sem SSO corporativo** | Externo | Escopo firmado (RP §5; NFR-06/08): só Calendar API; só login social. | Login social é o único modelo de identidade; inclusões disparam R05 + reavaliação do TA. |
| **Conformidade LGPD básica** | Segurança/Compliance | Dados de participantes (NFR-07): base legal, retenção e exclusão a pedido. | Revisão Jurídico/DPO obrigatória antes do release; retenção/exclusão como requisitos de aceite. |
| **Dependência da configuração do Google Workspace** | Externo | O grant OAuth a apps de terceiros deve ser permitido pelo admin (RP §14 ponto (a); D03); escopos/credencial dependem do ambiente real. | Gate de Discovery: se o grant for negado, a integração com o Calendar precisa ser re-escopada. |

**Provenance**
- **Confidence:** 68
- **Origin:** ai_drafted
- **Source:** RP §5/§6 (RN-01/05; sync uma-via C-Q02) + §8 (NFR-01/06/07/08) + §14 (TA LEVE; D03)
- **Status:** rascunho
- **Disposition:** ai_drafted
- **Hint:** CTO confirma cada restrição. O item Workspace é gated no spike — se o admin não autorizar grant, vira gatilho de re-escopo da integração (sinal ao Feasibility Assessor).

# ===== SECTION: tech-risks =====

| Risco | Categoria | Probabilidade | Impacto | Mitigação |
|---|---|---|---|---|
| Workspace nega/restringe grant OAuth a apps de terceiros (`calendar.events`) | Integração | Média | Alto | Antecipar spike DISC-001 (política do Workspace, escopos) antes do commit de arquitetura; plano B de credencial (service account c/ delegação de domínio vs por usuário — TA-Q01); escalar ao admin cedo. **Gate** da integração (RP §12 D03). |
| Race condition no anti-double-booking sob acesso simultâneo | Técnica | Média | Alto | NFR-01 crítico: gravação atômica via constraint/serializável (RN-05); harness de concorrência dedicado (EC-01, TA-Q03). |
| Quota/latência da Calendar API compromete sync ≤2 min | Integração | Baixa-Média | Médio | Worker assíncrono c/ backoff; ≤2 min tem folga; monitorar quota e alertar antes do teto (TA-Q04). |
| Divergência silenciosa Calendar↔sistema (sync uma-via) | Dados | Média | Médio | Aviso na UI (Calendar é espelho read-only — EC-04/EC-13); sistema é fonte única de verdade (RN-04/C-Q02); sem reconciliação reversa neste release. |
| Tratamento incorreto de fuso/DST | Dados | Baixa | Médio | Timestamps em UTC c/ tz explícito; bloquear/sinalizar intervalos ambíguos (EC-06); confirmar premissa mono-fuso. |
| Falha de sync deixa estado inconsistente | Integração | Baixa | Médio | Outbox + retry idempotente; reserva confirmada localmente independe do sync (EC-02); sinalizar "sincronização pendente". |

**Provenance**
- **Confidence:** 68
- **Origin:** ai_drafted
- **Source:** RP §9 (EC-01/02/04/06/13) + §12 D03 + §8 (NFR-01/02) + §6 (RN-04/05) + classificação + TA-Q01/Q03/Q04
- **Status:** rascunho
- **Disposition:** ai_drafted
- **Hint:** CTO confirma/prioriza prob/impacto. O risco de grant OAuth do Workspace é o gate (DISC-001/TA-Q01) — se bloqueado, é sinal de veto/re-escopo, não detalhe. Riscos de produto/negócio ficam no RP §12.

# ===== SECTION: build-vs-buy =====

| Capacidade | Decisão | Justificativa | Efeito em custo/prazo |
|---|---|---|---|
| Núcleo de reserva + anti-double-booking (CRUD, recorrência, first-commit-wins) | **Construir** | Propriedade central/diferenciadora (NFR-01, RN-05, EC-01); nenhum produto de prateleira garante a regra exata sob concorrência. | Maior parte do esforço; concentra o risco técnico (TA-Q03). |
| Autenticação / login social | **Reutilizar/Comprar** | Provedor OAuth2/OIDC (Google); não construir gestão de credenciais. SSO fora do release. | Reduz esforço e risco de segurança; sem licença adicional. |
| Sincronização de agenda (sistema → Calendar, uma via) | **Reutilizar** | Google Calendar API REST (`calendar.events`); não construir backend de calendário. | Baixo custo, dentro de quota gratuita (~200 usuários); viabilidade depende de TA-Q01/Q02/Q04. |
| Persistência transacional | **Reutilizar** | Banco relacional gerenciado (ACID/concorrência p/ NFR-01) sem reinventar bloqueio. | Custo operacional modesto; acelera a garantia transacional. |

**Provenance**
- **Confidence:** 65
- **Origin:** ai_drafted
- **Source:** RP §5 + §6 (RN-04/05) + §8 (NFR-01/02/06/08/10) + §9 (EC-01) + tech-foundation + classificação
- **Status:** rascunho
- **Disposition:** ai_drafted
- **Hint:** CTO confirma make-or-buy; o banco gerenciado específico depende de tech-foundation; "Reutilizar Calendar API" condicionado a TA-Q01/Q02/Q04. Seção não-bloqueante.

# ===== SECTION: adrs =====

| # | Decisão | Justificativa | Aprovação do CTO |
|---|---|---|---|
| ADR-001 | Persistência relacional transacional com garantia de não-sobreposição (intervalos `[início,fim)` por sala; `EXCLUDE USING gist` com `tstzrange` + `room_id` ou txn serializável), não só validação de aplicação. | NFR-01 [CRÍTICO] não-negociável; a invariante deve viver onde a serialização é garantida (o banco), tornando first-commit-wins consequência da constraint (RN-01/03/05, EC-01); sustenta sobreposição parcial (RN-03). | — (pendente) |
| ADR-002 | Sincronização uma-via assíncrona via transactional outbox + worker idempotente com retry/backoff. | A reserva é fonte de verdade e confirma independentemente do Calendar (EC-02); desacoplar protege NFR-03 e dá folga ao NFR-02; idempotência evita eventos duplicados em retries. | — (pendente) |
| ADR-003 | Sistema = fonte de verdade; Calendar = espelho read-only; sem reconciliação de volta neste release. | Firmado em produto (C-Q02, RN-04, NFR-08, EC-04/EC-13); evita complexidade de sync bidirecional; a não-detecção de divergência é consequência explícita do escopo uma-via. | — (pendente) |
| ADR-004 | Autenticação federada via OAuth2/OIDC (login social Google); sem senha própria e sem SSO neste release. | NFR-06 (acesso autenticado, reserva atribuível); reusa o IdP que os ~200 usuários já têm; minimiza dado sensível (alinha NFR-07); caminho de upgrade p/ SSO sem retrabalho de identidade. | — (pendente) |
| ADR-005 | Tempo em UTC com fuso explícito; premissa mono-fuso; bloquear/forçar confirmação explícita em intervalos ambíguos de DST. | EC-06 exige horários não-ambíguos; correção de RN-09/10/11 depende de âncora temporal única. Ressalva: premissa mono-fuso a confirmar. | — (pendente) |
| ADR-006 | Modelo de credencial da Calendar API — **A DECIDIR no spike de Discovery** (service account c/ delegação de domínio vs delegação por usuário). Não settled neste TA. | Depende de terreno desconhecido: config do Workspace e grant a apps de terceiros (TA-Q01/Q05, D03; current-state gated). Decidir agora seria inventar sobre terreno não descoberto. Vincular a DISC-001; reconverter em ADR após o spike. | — (gated no spike — não aprovar até DISC-001) |

**Provenance**
- **Confidence:** 66
- **Origin:** ai_drafted (KB inexistente — nenhuma reused_from_KB)
- **Source:** RP §6/§8/§9 + §12 D03 + classificação (Híbrido) + TA-Q01..Q05
- **Status:** rascunho
- **Disposition:** ai_drafted
- **Hint:** CTO aprova/ajusta cada linha (✓ → cto_authored). ADR-001..005 defensáveis; ADR-006 deliberadamente não-settled (gated DISC-001). ADRs greenfield aprovados semeiam o tech-landscape. Breakdown fino (RFC-5545 recorrência, esquema de tabelas, soft-delete US-05) vai p/ o Tech Backlog.

# ===== SECTION: effort-cost =====

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

**Provenance**
- **Confidence:** 58
- **Origin:** ai_drafted
- **Source:** RP §5/§6/§8/§9 (escopo, RN-01/05, recorrência, EC-01) + classificação (Híbrido, KB→Discovery)
- **Status:** rascunho
- **Disposition:** ai_drafted
- **Hint:** CTO firma os números. A estimativa de Integração/OAuth (10 dias) e o custo com terceiros dependem do spike (TA-Q01/Q04) — re-firmar após o spike. Se o veredito for Inviável, re-dispor a "N/A — vetado".

# ===== SECTION: discovery-path =====

| Incógnita | Spike / Investigação | Quem | Time-box sugerido |
|---|---|---|---|
| Ambiente Google Workspace / OAuth não documentado (gate de viabilidade) | DISC-001 — documentar: (a) escopos OAuth concedíveis a apps de terceiros e se o admin permite grant; (b) modelo de credencial (service account c/ delegação de domínio vs delegação por usuário); (c) quotas/limites da Calendar API; (d) caracterização final do processo manual (mural+Forms+WhatsApp, secretária). Produz o tech-landscape-room-reservation.md (via hsb-landscape-keeper). | CTO/Tech Lead + TI da organização (acesso ao Workspace); secretária (processo) | ~2–4 dias (acesso ao ambiente real é o gargalo) |

**Provenance**
- **Confidence:** 80
- **Origin:** ai_drafted
- **Source:** classificação técnica (KB inexistente) + RP §14 (TA LEVE pontos (a)/(d)) + RP §12 D03
- **Status:** rascunho
- **Disposition:** discovery
- **Hint:** DISC-001 destrava current-state (min-conf 75) e os pontos (a)/(d) do TA LEVE; NFR-02/06/08 e ADR-006 são contingentes ao seu fechamento. Owner do time-box: PO; investigação: CTO.

<!-- END OF DOCUMENT -->
