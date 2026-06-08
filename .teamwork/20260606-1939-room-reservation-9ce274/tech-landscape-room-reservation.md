<!--
TECH LANDSCAPE · Sistema de Reserva de Salas de Reunião
Criado por: hsb-landscape-keeper (Landscape Keeper)
Originado de: TA-2026-001 · 2026-06-07
Natureza: Híbrido
Status KB: inicial/semeada (fundação greenfield confirmada) + parcial (terreno Workspace/OAuth pendente de DISC-001)
rev: 1 · updated: 2026-06-07
-->

# Tech Landscape — Sistema de Reserva de Salas de Reunião

> **KB criada pelo Technical Assessment TA-2026-001 (2026-06-07).**
> Status: inicial/semeada (greenfield) + parcial (terreno Workspace/OAuth pendente de DISC-001).
> Esta é a base de conhecimento técnico persistente do sistema — lida por todo futuro Technical
> Assessment, Tech Backlog e engenheiro. Não é o TA por demanda; este documento sobrevive à demanda
> e documenta o terreno sobre o qual a viabilidade ("Viável com ressalvas") se apoia.
> Mantenedor exclusivo: `hsb-landscape-keeper`.

---

## 1. Contexto do Produto

| Campo | Valor |
|---|---|
| **Sistema** | Sistema de Reserva de Salas de Reunião |
| **Natureza da demanda que originou este KB** | Híbrido — software-core novo + integração Google Calendar uma-via + migração do processo manual (mural físico + Google Forms via WhatsApp) |
| **Escala de usuários** | ~200 usuários; pico de carga 10h–16h (horário comercial) |
| **Objetivo de negócio central** | Eliminar o double-booking e proteger o pipeline comercial da organização; substituir o processo informal (mural + Forms + WhatsApp, arbitrado pela secretária) por uma fonte de verdade digital e auditável |
| **Veredito de viabilidade** | Viável com ressalvas (TA-2026-001, conf 86) |
| **Ressalvas ativas** | R1 — grant OAuth do Workspace a apps de terceiros + credencial/quotas (gated DISC-001); R2 — first-commit-wins via exclusão transacional (não validação read-then-write); R3 — sync estritamente uma-via neste release; R4 — revisão LGPD Jurídico/DPO antes do release |
| **Decisão técnica pendente** | ADR-006 (modelo de credencial Calendar API) gated em DISC-001 |

### Sistemas substituídos / descontinuados

| Sistema | Status |
|---|---|
| Mural físico (fonte de verdade atual) | Migrado/descontinuado — retirada física ≤2 semanas após go-live |
| Google Forms (link via WhatsApp) | Migrado/descontinuado — encerramento formal ≤2 semanas após go-live |
| WhatsApp (canal do Forms) | Descontinuado como canal de reservas — fora do escopo técnico |

### Processo manual documentado (terreno existente a substituir)

O "sistema legado" é um **processo informal**, não uma base de código:

- **Fonte de verdade atual:** papel no mural físico, com reservas anotadas manualmente.
- **Fluxo de solicitação:** Google Forms cujo link é distribuído via WhatsApp.
- **Árbitro de conflitos:** secretária da organização (papel humano insubstituível no processo atual).
- **Limitações documentadas:** sem prevenção de conflito automatizada, dependente de uma pessoa, não auditável, sem histórico digital estruturado.
- **Dados legados:** não existem — sem esquema, migração ou histórico a portar. O novo sistema começa do zero.
- **Risco de migração:** não é regressão técnica, é risco de adoção (RP §12 R01/R03/R05) — product-owned. A usabilidade do novo sistema deve superar o Forms (NFR-04); a secretária é stakeholder-chave de migração.

---

## 2. Stack Tecnológica

> Fundação greenfield confirmada pelo CTO (TA-2026-001, cto_authored, conf 78). A âncora de
> persistência transacional é inegociável; o modelo de credencial OAuth do Calendar é gated DISC-001.

### 2.1 Tabela de Stack

| Camada | Escolha | Critério de decisão | Alternativa descartada |
|---|---|---|---|
| **Linguagem / runtime** | TypeScript (Node.js LTS) end-to-end | Linguagem única reduz custo cognitivo para time pequeno; ecossistema maduro para OAuth2/OIDC e cliente Google Calendar; tipagem apoia correção das regras temporais (RN-09..RN-12) | Python/Django, Java/Spring — sem ganho frente ao porte (~200 usuários); fragmentariam a stack |
| **Framework / app** | Backend: NestJS/Express (API REST). Frontend: React (Vite/Next) responsivo/mobile-first | REST cobre o CRUD e a consulta de disponibilidade sem complexidade extra; React atende NFR-05 (mobile ≥360px / tablet ≥768px) | GraphQL — modelo simples não justifica overhead de schema/resolvers; SPA puro sem back — reescreveria validação/auth |
| **Persistência / dados** | PostgreSQL — banco relacional transacional | Âncora em NFR-01/RN-05 (first-commit-wins): `EXCLUSION constraint` com `tstzrange` + `btree_gist` (ou transação serializável) rejeita no nível do banco qualquer interseção de intervalos para a mesma sala — a regra vira invariante de dados, não lógica de aplicação propensa a corrida (RN-01..RN-03, EC-01). Suporta validação de séries recorrentes (RN-15). | NoSQL/documento (MongoDB) — sem constraint de exclusão multi-linha / transação serializável nativa sobre intervalos; first-commit-wins dependeria de locks aplicacionais frágeis no requisito mais crítico |
| **Infra / deploy** | Container (Docker) em PaaS gerenciada (Cloud Run/App Service/equiv.) + PostgreSQL gerenciado + worker assíncrono de sync | Porte modesto e ≥99% horário comercial não justificam Kubernetes próprio; PaaS + Postgres gerenciado entregam HA/backup prontos | Kubernetes auto-gerenciado — overhead desproporcional; FaaS puro para o worker — mantido como opção futura |

### 2.2 Decisões Make-or-Buy

| Capacidade | Decisão | Justificativa |
|---|---|---|
| Núcleo de reserva + anti-double-booking (CRUD, recorrência, first-commit-wins) | **Construir** | Propriedade central/diferenciadora; nenhum produto de prateleira garante a regra exata sob concorrência |
| Autenticação / login social | **Reutilizar/Comprar** | Provedor OAuth2/OIDC (Google); não construir gestão de credenciais; sem licença adicional |
| Sincronização de agenda (sistema → Calendar, uma via) | **Reutilizar** | Google Calendar API REST (`calendar.events`); dentro de quota gratuita (~200 usuários) |
| Persistência transacional | **Reutilizar** | Banco relacional gerenciado (ACID/concorrência para NFR-01) |

---

## 3. Arquitetura-Alvo

> Padrão confirmado pelo CTO (TA-2026-001, ADR-001..005). Sync **estritamente uma-via**
> (sistema → Calendar). Calendar = espelho read-only neste release (ADR-003).

```text
C4 — CONTEXTO
  [Colaborador] e [Secretária] --HTTPS--> SISTEMA DE RESERVA DE SALAS (novo; fonte de verdade)
       |-- OAuth2/OIDC --> [Provedor de Identidade Social (Google)]
       |-- REST + OAuth2 (uma via -->) --> [Google Calendar API] (espelho de leitura; NÃO retroalimenta)

C4 — CONTAINERS
  Web Frontend (React, responsivo/mobile-first)
       --REST/JSON-->
  API / Backend (NestJS/Express)
       - Auth OAuth2/OIDC; validação anti-conflito atômica; regras RN-01..RN-16
       --SQL (transação atômica)-->
  PostgreSQL
       - EXCLUSION constraint anti-overlap: EXCLUDE USING gist (room_id WITH =, tstzrange WITH &&)
       - Reservas / Salas / Séries recorrentes (ocorrências materializadas)
       --enfileira evento (transactional outbox)-->
  Worker de Sync Calendar
       - Assíncrono; retry/backoff; idempotente por chave de reserva
       --REST OAuth2 (uma via) -->
  Google Calendar API (espelho; nunca escreve de volta neste release)

INVARIANTE DE DADOS: first-commit-wins é consequência da constraint PostgreSQL, não da aplicação.
DIREÇÃO DO SYNC: SISTEMA --> Google Calendar. O Calendar nunca escreve de volta neste release.
```

### Padrão arquitetural chave: Transactional Outbox

- A intenção de sync é gravada na **mesma transação** que confirma a reserva.
- O worker consome a fila de outbox e chama a Calendar API com retry/backoff.
- A chamada externa **nunca é acoplada ao commit** da reserva.
- Idempotência garantida por chave da reserva.
- A reserva é confirmada localmente independentemente do estado do sync (EC-02).

---

## 4. Estrutura e Convenções do Repositório

> Convenções confirmadas pelo CTO (TA-2026-001, tech-foundation, cto_authored).

### 4.1 Organização de Pastas

```
monorepo/
├── apps/
│   ├── web/          # Frontend React (Vite/Next) responsivo/mobile-first
│   └── api/          # Backend NestJS/Express (API REST)
├── packages/
│   └── shared/       # DTOs compartilhados, enums de status, tipos comuns
```

**Backend por domínio (`apps/api/`):**

```
api/
├── reservations/     # Núcleo: CRUD, máquina de estados, séries recorrentes
├── availability/     # Consulta de disponibilidade (sala + intervalo)
├── auth/             # OAuth2/OIDC, identidade, atribuição de reserva
└── calendar-sync/    # Worker transactional outbox + integração Calendar API
```

**Migrações:** versionadas e forward-only. A EXCLUSION constraint do NFR-01 nasce em migração explícita e testada — é a primeira migração load-bearing do projeto.

### 4.2 Convenções de Código e Lint

| Aspecto | Convenção |
|---|---|
| Linting | ESLint + Prettier compartilhados (monorepo) |
| TypeScript | `strict: true` em todos os pacotes |
| Testes unitários | Foco em regras temporais (RN-09..12), validação de sobreposição (RN-01/03), FCFS (RN-13); casos-tabela de fronteira de intervalo |
| Testes de integração | Calendar API mockada/sandbox (criação/remoção, ≤2 min, caminho de falha com retry/backoff); sem write-back (EC-04/EC-13) |
| Testes e2e | Jornadas A/B/C, ALT-1..5, US-01..08 |
| **Harness de concorrência [LOAD-BEARING]** | N confirmações simultâneas para a mesma sala+horário; exatamente uma persiste; **gate de release** para NFR-01 — sem ele o anti-double-booking não é demonstrável |
| Nomes de teste | Espelham os Given/When/Then da seção de Critérios de Aceite do RP |

### 4.3 Estratégia de Branching e CI

| Aspecto | Convenção |
|---|---|
| Branching | Trunk-based + PR com revisão obrigatória; `main` sempre deployável |
| Pipeline CI | lint → build → unit/integração (incl. harness de concorrência NFR-01) → e2e |
| Deploy | Contínuo para homologação + promoção manual para produção |
| Migrações | Forward-only (nunca reverter em produção; cada migração é testada antes do merge) |

---

## 5. Pontos de Integração

> Integrações confirmadas pelo CTO (TA-2026-001, integrations + architectural-impact, cto_authored).

### 5.1 Google Calendar API (sistema → Calendar, uma via)

| Aspecto | Detalhe |
|---|---|
| **Direção** | Sistema → Calendar (uma via, sem retroalimentação neste release — ADR-003) |
| **Protocolo** | REST / Google Calendar API v3 |
| **Escopo OAuth alvo** | `calendar.events` |
| **Modelo de credencial** | A DECIDIR no spike DISC-001 — service account com delegação de domínio vs. delegação por usuário autenticado (ADR-006 gated) |
| **SLA de propagação** | ≤2 minutos (NFR-02) — alcançável com worker assíncrono (folga ampla frente à latência típica) |
| **Padrão de resiliência** | Transactional outbox + worker idempotente com retry/backoff; reserva confirmada localmente independe do sync |
| **Riscos conhecidos** | Grant OAuth do Workspace a apps de terceiros; quotas/limites reais da API; modelo de credencial — todos **não documentados, gated DISC-001** |
| **Risco de scope creep** | Sync bidirecional NÃO está no escopo deste release (C-Q02, NFR-08); inclusão dispara reavaliação do TA (R05 RP §12) |

### 5.2 Provedor de Identidade / Login Social (OAuth2/OIDC)

| Aspecto | Detalhe |
|---|---|
| **Protocolo** | OAuth2 / OpenID Connect (OIDC) |
| **Provedor** | Login social Google |
| **Modelo** | Flat — cada reserva atribuída a um user_id; sem senha própria; sem SSO corporativo neste release |
| **Escopos de identidade** | A confirmar (consent screen, restrição de domínio — items de configuração, não bloqueadores técnicos) |
| **Outlook / SSO corporativo** | Fora do escopo deste release (NFR-06/08); upgrade para SSO Fase 3 sem retrabalho de identidade (reutiliza ADR-004) |

---

## 6. Decisões Arquiteturais (ADRs) — Aprovadas

> ADR-001..005 aprovados pelo CTO (✓). ADR-006 deliberadamente não-settled (gated DISC-001).
> Fonte: TA-2026-001, seção adrs, cto_authored.

| # | Decisão | Justificativa | Status |
|---|---|---|---|
| **ADR-001** | Persistência relacional transacional com garantia de não-sobreposição (`EXCLUDE USING gist` com `tstzrange` + `room_id` ou txn serializável) — a invariante vive no banco, não na aplicação. | NFR-01 [CRÍTICO] inegociável; o banco é o árbitro de first-commit-wins (RN-01/03/05, EC-01); sustenta sobreposição parcial (RN-03) e ocorrências de séries (RN-15). | Aprovado ✓ |
| **ADR-002** | Sincronização uma-via assíncrona via transactional outbox + worker idempotente com retry/backoff. | A reserva confirma independentemente do Calendar (EC-02); desacopla protegendo NFR-03; idempotência evita eventos duplicados em retries. | Aprovado ✓ |
| **ADR-003** | Sistema = fonte de verdade; Calendar = espelho read-only; sem reconciliação reversa neste release. | Firmado em produto (C-Q02, RN-04, NFR-08, EC-04/EC-13); evita complexidade de sync bidirecional; a divergência silenciosa é consequência explícita e comunicada (aviso na UI). | Aprovado ✓ |
| **ADR-004** | Autenticação federada via OAuth2/OIDC (login social Google); sem senha própria; sem SSO neste release. | NFR-06 (acesso autenticado, reserva atribuível); reutiliza o IdP existente dos ~200 usuários; minimiza dado sensível (alinha NFR-07); caminho de upgrade para SSO sem retrabalho de identidade. | Aprovado ✓ |
| **ADR-005** | Tempo em UTC com fuso explícito; premissa mono-fuso; bloquear/forçar confirmação explícita em intervalos ambíguos de DST. | EC-06 exige horários não-ambíguos; correção de RN-09/10/11 depende de âncora temporal única. Ressalva: premissa mono-fuso a confirmar no DISC-001. | Aprovado ✓ |
| **ADR-006** | Modelo de credencial da Calendar API — **A DECIDIR no spike DISC-001** (service account com delegação de domínio vs. delegação por usuário autenticado). | Depende de terreno não documentado: config do Workspace e grant OAuth a apps de terceiros (TA-Q01/Q05, D03). Decidir agora seria inventar sobre terreno desconhecido. Reconverter em ADR após o spike. | **Gated — DISC-001** |

---

## 7. NFRs e Requisitos de Qualidade

> Mapeamento de viabilidade confirmado pelo CTO (TA-2026-001, nfr-feasibility, cto_authored, conf 80).

| NFR | Requisito | Viabilidade | Abordagem / Gate |
|---|---|---|---|
| **NFR-01 [CRÍTICO]** | Nunca duas reservas confirmadas sobrepostas na mesma sala, inclusive sob concorrência. | Sim | EXCLUSION constraint PostgreSQL (ADR-001); harness de concorrência é gate de release. |
| **NFR-02** | Sync sistema → Calendar em ≤2 min. | Com ressalvas | Worker assíncrono (ADR-002); gated DISC-001 (quotas/credencial). |
| **NFR-03** | Consulta ≤2s p95; confirmação ≤3s p95. | Sim | Índices (sala+intervalo); escala modesta; medir junto à txn anti-conflito. |
| **NFR-04 [CRÍTICO]** | Criar reserva mais simples do que o Forms atual; sem treinamento formal. | Com ressalvas | Produto/UX — validado com a secretária (critério de aceite RP §11); não atestável por arquitetura. |
| **NFR-05** | Responsivo/mobile-first; breakpoints ≥360px (mobile) e ≥768px (tablet). | Sim | React responsivo; testar fluxo crítico em dispositivo real. |
| **NFR-06** | Acesso somente via login social autenticado; reserva atribuível. | Com ressalvas | OAuth2/OIDC (ADR-004); consent screen/escopos a confirmar (DISC-001). |
| **NFR-07** | Dados de participantes conformes à LGPD básica (base legal, retenção, exclusão a pedido). | Com ressalvas | Criptografia em repouso, retenção ~12 meses, exclusão a pedido; **exige revisão Jurídico/DPO** antes do release. |
| **NFR-08** | Interoperação exclusivamente com Google Calendar neste release (sem Outlook). | Com ressalvas | Gated DISC-001; risco de scope creep se sync bidirecional reentrar (R05). |
| **NFR-09** | Disponibilidade ≥99% no horário comercial. | Sim | PaaS gerenciada + Postgres gerenciado; manutenção fora do horário; sync assíncrono não derruba o sistema. |
| **NFR-10** | Suporte a ~200 usuários com pico 10h–16h. | Sim | 1 instância + DB dimensionado para pico; confirmar em teste de carga. |

---

## 8. Observabilidade e Testabilidade

> Estratégia confirmada pelo CTO (TA-2026-001, testability-observability, cto_authored, conf 76).

### 8.1 Métricas Técnicas Chave

| Métrica | Target | NFR |
|---|---|---|
| Contador de conflitos bloqueados | Prova viva do anti-double-booking | NFR-01 |
| Latência de propagação ao Calendar (p50/95/99) | ≤2 min | NFR-02 |
| Taxa de falha/retry de sync + profundidade/idade da fila de outbox | Monitorar | NFR-02 |
| Latência de consulta de disponibilidade (p95) | ≤2s | NFR-03 |
| Latência de confirmação de reserva (p95) | ≤3s | NFR-03 |
| Disponibilidade em horário comercial | ≥99% | NFR-09 |

### 8.2 Alertas Operacionais

| Alerta | Gatilho |
|---|---|
| Sync pendente acima do SLA | Itens na fila de outbox com idade > 2 min (EC-02/EC-13) |
| Falhas OAuth/credencial | Qualquer erro de autenticação na Calendar API — bloqueia toda a sync (TA-Q01) |
| Pico de erro de confirmação | Taxa de erro acima do threshold (incl. EC-11) |

### 8.3 Logs de Auditoria

| Log | Relevância |
|---|---|
| Criação/edição/cancelamento de reserva (quem operou) | Modelo flat RN-06 + LGPD NFR-07 |
| Eventos de sync Calendar (sucesso/falha/retry por reserva) | Rastreabilidade da integração |

### 8.4 Edge Cases Load-Bearing para Testes

| EC | Cenário | Abordagem |
|---|---|---|
| EC-01 | Reservas concorrentes (race condition) — dois usuários confirmando a mesma sala no mesmo instante | Harness de concorrência dedicado [GATE DE RELEASE]; N threads simultâneas; exatamente uma persiste |
| EC-02 | Falha da Calendar API no momento da confirmação ou cancelamento | Retry/backoff no worker; reserva confirmada localmente |
| EC-04 | Alteração feita diretamente no Google Calendar sem atuar no sistema | Aviso na UI; sem write-back (ADR-003) |
| EC-05 | Reserva recorrente com ocorrências em conflito com reservas existentes | Cada ocorrência participa da constraint (RN-15) |
| EC-06 | Fuso/DST — criação em horário ambíguo na transição | UTC + bloqueio/confirmação explícita (ADR-005) |
| EC-09 | Edição de reserva que gera conflito com outra reserva ativa | Revalidação via constraint na edição (RN-12) |
| EC-13 | Divergência silenciosa Calendar↔sistema após edição direta no Calendar | Aviso na UI; sistema é fonte de verdade (ADR-003) |

---

## 9. Dívida Técnica e Lacunas Conhecidas

> Lacunas documentadas na criação desta KB. Atualizar após o spike DISC-001.

### 9.1 Lacunas Abertas (DISC-001 — ~2–4 dias)

As seguintes incógnitas são **abertas** e devem ser resolvidas no spike DISC-001 antes de qualquer commit de implementação que dependa da integração Calendar:

| Lacuna | Detalhe | Owner |
|---|---|---|
| **Grant OAuth do Workspace a apps de terceiros** | O admin do Workspace da organização permite grant de escopos (`calendar.events`) a apps de terceiros? Se negado, a integração com o Calendar precisa ser re-escopada (gatilho de veto parcial). | CTO/Tech Lead + TI da organização |
| **Modelo de credencial da Calendar API** | Service account com delegação de domínio vs. delegação por usuário autenticado — ADR-006 gated até esta decisão. | CTO/Tech Lead + TI da organização |
| **Quotas e limites da Calendar API** | Quotas/rate-limits reais para o volume previsto (~200 usuários); confirmar viabilidade do SLA ≤2 min (NFR-02, TA-Q04). | CTO/Tech Lead |
| **Consent screen e restrição de domínio** | Escopos de identidade concedíveis; restrição de domínio no OAuth do Workspace (NFR-06, TA-Q01). | CTO/Tech Lead + TI da organização |
| **Premissa mono-fuso (EC-06)** | Confirmar que a organização opera em fuso único (premissa de ADR-005). | CTO/Tech Lead + stakeholders |

### 9.2 Premissas a Confirmar (não bloqueantes para início, mas load-bearing para release)

| Premissa | Ação requerida |
|---|---|
| **LGPD — base legal e política de retenção** | Revisão Jurídico/DPO obrigatória antes do release (NFR-07); base legal (legítimo interesse vs. consentimento) e retenção (~12 meses) são decisões legais, não técnicas. |
| **NFR-04 — usabilidade superior ao Forms** | Validação qualitativa com a secretária como critério de aceite (RP §11); medição do baseline atual. |

### 9.3 Dívida de Processo (herdada — sem código legado)

| Área | Situação |
|---|---|
| Processo manual (mural+Forms+WhatsApp) | Sendo substituído — dívida de processo, não técnica. Risco de adoção (RP §12 R01/R03/R05), product-owned. Secretária é stakeholder-chave de migração. |
| Divergência silenciosa Calendar↔sistema | Não detectada automaticamente neste release (ADR-003, EC-04/EC-13); mitigação de produto: aviso na UI. |

### 9.4 Riscos Técnicos Residuais

| Risco | Probabilidade | Impacto | Mitigação |
|---|---|---|---|
| Workspace nega/restringe grant OAuth | Média | Alto | Spike DISC-001 antes do commit de arquitetura; plano B de credencial; escalar ao admin cedo |
| Race condition no anti-double-booking | Média | Alto | ADR-001 (constraint PostgreSQL); harness de concorrência [gate de release] |
| Quota/latência Calendar API compromete sync ≤2 min | Baixa-Média | Médio | Worker assíncrono com backoff; monitorar quota; alertar antes do teto |
| Divergência silenciosa Calendar↔sistema | Média | Médio | Aviso na UI; sistema é fonte única de verdade (ADR-003) |
| Tratamento incorreto de fuso/DST | Baixa | Médio | Timestamps UTC; bloqueio de intervalos ambíguos (ADR-005); confirmar mono-fuso |
| Falha de sync deixa estado inconsistente | Baixa | Médio | Outbox + retry idempotente; reserva confirma localmente (EC-02) |

---

## 10. Restrições Rígidas (não-negociáveis)

> Confirmadas pelo CTO (TA-2026-001, hard-constraints, cto_authored, conf 80).

| Restrição | Tipo | Efeito no escopo |
|---|---|---|
| Exclusividade transacional / first-commit-wins | Técnico — NFR-01 inegociável | Define a escolha de persistência: PostgreSQL com EXCLUSION constraint. Soluções sem garantia transacional descartadas. |
| Sincronização uma-via (sistema → Calendar) | Plataforma/Externo | Sem reconciliação bidirecional neste release; sem webhooks de entrada. |
| Somente Google Calendar; sem Outlook; sem SSO corporativo | Externo | Login social é o único modelo de identidade neste release; inclusões disparam reavaliação do TA (R05). |
| Conformidade LGPD básica | Segurança/Compliance | Revisão Jurídico/DPO obrigatória antes do release. |
| Dependência da configuração do Google Workspace | Externo | Gate de Discovery (DISC-001): se o grant for negado, a integração com o Calendar precisa ser re-escopada. |

---

## 11. Histórico de Atualizações desta KB

| Versão | Data | Evento | Seções afetadas |
|---|---|---|---|
| v1 | 2026-06-07 | Criação — semeada pelo TA-2026-001 (Híbrido; fundação greenfield confirmada; terreno Workspace/OAuth parcial, gated DISC-001) | Todas — criação inicial |

> **Próxima atualização esperada:** após o fechamento do spike DISC-001, o Landscape Keeper deverá atualizar as seções 5 (Pontos de Integração), 6 (ADR-006), 7 (NFR-02/06/08) e 9 (Lacunas Abertas) com o terreno descoberto, e promover o status da KB de "parcial" para "completa".

<!-- END OF DOCUMENT -->
