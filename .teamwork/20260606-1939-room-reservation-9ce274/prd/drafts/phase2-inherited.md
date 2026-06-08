<!--
PHASE 2 INHERITED CONTENT — fill-ready for hsb-doc-updater to merge into prd.md.
Keyed by section id. Part A = Origin: inherited (RP). Part B = Origin: inherited (TA, escalated).
SUMMARIES at PRD altitude (full RP/TA stay canonical). Verdict carried, never re-decided.
Derived sections (exec-summary, scope-reconciliation, consolidated-risk, inherited-readiness,
handoff-gate) and sign-off are NOT in this file — they are Phase 3/4 work. Language pt-BR.
-->

# ===== SECTION: a-objectives =====
1. **Eliminar o double-booking:** zero novos conflitos nas 4 semanas seguintes ao go-live (monitoramento + ausência de relatos da secretária).
2. **Proteger o pipeline comercial:** zero novos adiamentos de negócios atribuíveis a conflito de sala nas 8 semanas seguintes (acompanhamento com a liderança comercial, D02).
3. **Migrar 100% das reservas para o sistema digital:** mural e Forms descontinuados em até 2 semanas pós go-live; todas as reservas exclusivamente no sistema (observação direta + confirmação da secretária).
4. **Integração em tempo real com o Google Calendar:** toda reserva confirmada/cancelada reflete no Calendar em até 2 minutos (sync uma via) — teste funcional de integração.

Detalhamento: RP §3.

**Provenance** — Confidence 85 · Origin: inherited · Source: RP §3 · Status: herdada · Disposition: inherited · Hint: metas/prazos propostos no RP; outcomes não outputs.

# ===== SECTION: a-scope =====
**Incluído:** CRUD de reservas; integração Google Calendar **uma via** (sistema→Calendar; reflete em ≤2 min; alterações no Calendar não retroalimentam); login social (sem SSO); regras automáticas de anti-double-booking (sobreposição parcial ou total); reservas recorrentes com validação por ocorrência (ocorrências em conflito sinalizadas, série não rejeitada); migração e descontinuação do processo manual (mural + Forms + WhatsApp).
**Excluído:** Outlook/Microsoft 365; SSO corporativo; outros recursos físicos; analytics avançado/relatórios; portal externo para visitantes.
**Adiado:** Outlook (Fase 2); analytics/relatórios (Fase 2); lembretes automáticos (Fase 2); SSO corporativo (Fase 3).
> Nota: escopo carregado do RP (C-Q02 sync uma via; C-Q03 recorrência). A reconciliação final RP×TA é registrada em `scope-reconciliation` (Fase 3) e refletida aqui antes do freeze.

**Provenance** — Confidence 83 · Origin: inherited · Source: RP §5 · Status: herdada · Disposition: inherited · Hint: reconciliação final pendente (scope-reconciliation); qualquer adição ao incluído dispara o risco R05.

# ===== SECTION: a-personas =====
| Persona | Job-to-be-done | Impacto pós-entrega |
|---|---|---|
| Equipes internas (colaboradores) | Reservar sala com antecedência e ter certeza da disponibilidade. | Zero risco de double-booking; disponibilidade em tempo real; confirmação automática. |
| Reuniões com clientes/externos | Conduzir reuniões com visitantes de forma profissional, sem imprevistos. | Reserva confirmada elimina conflito; credibilidade preservada. |
| Liderança e diretoria | Garantir reuniões estratégicas no horário, sem interrupções por conflito. | Visibilidade de ocupação; reservas com confirmação; protegidas por anti-conflito automático. |
| Secretária / Facilities (stakeholder-chave de migração) | Manter o processo ordenado, resolver conflitos, garantir a sala certa. | Sistema assume o papel de árbitro; secretária deixa de ser gargalo. Adesão e validação de usabilidade são necessárias; o sistema deve ser mais simples que o Forms. |

Detalhamento: RP §4.

**Provenance** — Confidence 76 · Origin: inherited · Source: RP §4 · Status: herdada · Disposition: inherited · Hint: conf 76 < 80 — entrevista rápida com a secretária recomendada antes do gate.

# ===== SECTION: a-journey =====
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

**Provenance** — Confidence 80 · Origin: inherited · Source: RP §6.5 · Status: herdada · Disposition: inherited · Hint: ALT-1 (sugestão de alternativas) sem decisão fechada — definir antes da implementação.

# ===== SECTION: a-business-rules =====
Resumo das 16 regras (RN-01..RN-16) em 5 blocos; texto normativo completo em RP §6:
- **Exclusividade / anti-double-booking (RN-01..05):** máx. 1 reserva ativa por sala/intervalo; sobreposição parcial é conflito; validação na confirmação; sistema é fonte de verdade; sob concorrência **first-commit-wins**. (C-Q01)
- **Permissões — modelo flat (RN-06):** qualquer usuário autenticado cria/edita/cancela qualquer reserva (campos "responsável"/"participantes"); sem perfil admin. (C-Q04)
- **Parâmetros temporais (RN-09..12):** janela 08h–19h dias úteis; duração 15 min–8 h; antecedência máx. ~90 dias (valor exato a parametrizar); edição/cancelamento até o início. (C-Q05)
- **Precedência FCFS (RN-13):** first-come, first-served; hierarquia não sobrescreve; realocação facilitada mas não automática. (C-Q01)
- **Recorrentes — MVP (RN-14..16):** séries; validação por ocorrência; conflitos sinalizados; usuário decide. (C-Q03)

Fluxo de estado: Rascunho → Confirmada → Cancelada/Concluída; falha de sync mantém Confirmada (retry/backoff). Sincronização **uma via** (C-Q02): propaga ≤2 min; alterações no Calendar não retroalimentam.

**Provenance** — Confidence 88 · Origin: inherited · Source: RP §6 · Status: herdada · Disposition: inherited · Hint: antecedência máx. (~90 dias) a parametrizar antes da implementação.

# ===== SECTION: a-user-stories =====
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

**Provenance** — Confidence 88 · Origin: inherited · Source: RP §7 · Status: herdada · Disposition: inherited · Hint: US-05 (modelo flat) — considerar confirmação explícita anti-cancelamento acidental antes da implementação.

# ===== SECTION: a-nfrs =====
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

Cada NFR pareia 1:1 com `b-nfr-feasibility` (invariante A.7 ↔ B.4).

**Provenance** — Confidence 82 · Origin: inherited · Source: RP §8 · Status: herdada · Disposition: inherited · Hint: NFR-07 (LGPD) exige revisão Jurídico/DPO antes do release.

# ===== SECTION: a-edge-cases =====
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

**Provenance** — Confidence 80 · Origin: inherited · Source: RP §9 · Status: herdada · Disposition: inherited · Hint: EC-06 (mono-fuso) — confirmar antes da implementação.

# ===== SECTION: success-metrics =====
| Tipo | Métrica | Baseline | Meta pós-rollout | Janela | Confiança |
|---|---|---|---|---|---|
| Primária (lagging) | Double-bookings/semana | ~1,8/sem (9/5sem) | 0 | 4 sem pós go-live | Alta |
| Primária (lagging) | Novos adiamentos de negócios por conflito | 9 em 5 sem | 0 | 8 sem pós go-live | Média (depende de D02) |
| Leading | Adoção (% reservas no sistema) | 0% | 100% | 2 sem pós go-live | Alta |
| Guardrail | Volume total de reservas/semana | a medir pré-go-live | não cair vs baseline | Semana 1 | Média |
| Guardrail | Carga de remarcação da secretária | a medir pré-go-live | não aumentar vs baseline | 4 sem | Média |

Nota financeira (referência, não métrica do sistema): pipeline ~R$700k; R$111k perdidos; R$90k em risco (monitorar com D02).

**Provenance** — Confidence 80 · Origin: inherited · Source: RP §10 · Status: herdada · Disposition: inherited · Hint: guardrails dependem de medição na semana pré-go-live — planejar coleta.

# ===== SECTION: b-feasibility =====
| Campo | Valor |
|---|---|
| **Verdict** | **Viável com ressalvas** |
| **Caveats** | R1 — admin do Workspace permite grant OAuth a apps de terceiros (`calendar.events`) + credencial/quotas (gated DISC-001); R2 — first-commit-wins via exclusão transacional (não read-then-write); R3 — sync estritamente uma-via, sem reconciliação reversa; R4 — revisão LGPD Jurídico/DPO antes do release. |

**Provenance** — Confidence 86 · Origin: inherited · Source: TA-2026-001 §feasibility-verdict (cto_authored) · Status: respondida · Disposition: inherited (decided — assinado sob ressalvas) · Hint: veredito carregado verbatim, nunca re-decidido; um veto só se materializaria se o admin do Workspace negasse o grant (R1).

# ===== SECTION: b-nature-landscape =====
| Campo | Valor |
|---|---|
| **Nature** | Híbrido — processo informal (mural+Forms+WhatsApp, secretária) + software-core novo (greenfield) + integração Google Calendar |
| **Knowledge base** | `tech-landscape-room-reservation.md` — criada neste ciclo (semeada pelos ADRs greenfield + populada por DISC-001) |
| **Current state (brownfield)** | Processo manual (mural = fonte de verdade atual + Forms + WhatsApp); ambiente Workspace/OAuth não documentado (gated DISC-001); sem código legado/dados a migrar; processo será descontinuado. |
| **Foundation (greenfield)** | TypeScript/Node; backend NestJS/Express (REST); frontend React responsivo; PostgreSQL transacional (EXCLUSION constraint anti-overlap); worker async (transactional outbox); monorepo; PaaS gerenciada. |

**Provenance** — Confidence 78 · Origin: inherited · Source: TA §tech-classification + §tech-foundation + §current-state · Status: respondida · Disposition: inherited (discovery para o estado atual/Workspace — DISC-001 aberto) · Hint: confiança limitada pelo current-state (54, gated); terreno Workspace/OAuth não documentado até o spike.

# ===== SECTION: b-arch-impact =====
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

**Provenance** — Confidence 78 · Origin: inherited · Source: TA §affected-systems + §architectural-impact + §integrations · Status: respondida · Disposition: inherited (decided; credencial Calendar gated DISC-001) · Hint: modelo de credencial Calendar não resolvido até DISC-001.

# ===== SECTION: b-nfr-feasibility =====
| NFR (de A.7) | Viável? | Abordagem | Ressalva |
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

**Provenance** — Confidence 80 · Origin: inherited · Source: TA §nfr-feasibility (cto_authored) · Status: respondida · Disposition: inherited (decided; NFR-02/06/08 com ressalvas gated DISC-001; NFR-07 gated DPO) · Hint: NFR-01/03/05/09/10 sem ressalva; NFR-02/06/08 gated; NFR-07 exige Jurídico/DPO.

# ===== SECTION: b-alternatives =====
| Alternativa | Por que NÃO foi escolhida |
|---|---|
| Sincronização bidirecional Calendar↔sistema | Fora do escopo (C-Q02); exige webhooks/reconciliação; uma-via atende sem a complexidade. |
| Google Calendar como fonte de verdade (sem banco) | Calendar API não garante exclusividade transacional/first-commit-wins (TA-Q03); o sistema precisa ser fonte de verdade (RN-04). |
| Persistência NoSQL/documento | Exclusividade de intervalo exigiria coordenação aplicacional frágil; escala modesta não justifica; relacional resolve direto. |
| Validação otimista sem trava transacional | Janela de corrida; não garante first-commit-wins (RN-05, EC-01); transação/serializável é a única que satisfaz NFR-01. |

**Provenance** — Confidence 76 · Origin: inherited · Source: TA §alternatives (cto_authored) · Status: respondida · Disposition: inherited (decided) · Hint: seção não-bloqueante; previne re-litigação downstream.

# ===== SECTION: b-hard-constraints =====
| Restrição | Efeito no escopo |
|---|---|
| Exclusividade transacional / first-commit-wins (NFR-01) | Define a persistência: store transacional com não-sobreposição; sem garantia transacional → descartado. |
| Sincronização uma-via sistema→Calendar | Sem webhooks de entrada, sem bidirecional; Calendar é espelho read-only. |
| Só Google Calendar; sem Outlook; sem SSO | Login social é o único modelo de identidade; inclusões disparam R05 + reavaliação do TA. |
| Conformidade LGPD básica (NFR-07) | Revisão Jurídico/DPO obrigatória antes do release; retenção/exclusão como aceite. |
| Dependência da config do Google Workspace (grant OAuth) | Gate de Discovery (DISC-001); se negado, re-escopar a integração. |

**Provenance** — Confidence 80 · Origin: inherited · Source: TA §hard-constraints (cto_authored) · Status: respondida · Disposition: inherited (decided; Workspace gated DISC-001) · Hint: alimentam scope-reconciliation; a restrição de Workspace é o único gatilho possível de re-escopo.

# ===== SECTION: b-adrs =====
| # | Decisão | Sign-off CTO |
|---|---|---|
| ADR-001 | Persistência relacional transacional com não-sobreposição (intervalos `[início,fim)` por sala; `EXCLUDE USING gist` ou serializável). | ✓ |
| ADR-002 | Sync uma-via assíncrona via transactional outbox + worker idempotente (retry/backoff). | ✓ |
| ADR-003 | Sistema = fonte de verdade; Calendar = espelho read-only; sem reconciliação de volta neste release. | ✓ |
| ADR-004 | Autenticação federada OAuth2/OIDC (login social Google); sem senha própria; sem SSO neste release. | ✓ |
| ADR-005 | Tempo em UTC com fuso explícito; premissa mono-fuso; tratar DST ambíguo (EC-06). | ✓ |
| ADR-006 | Modelo de credencial da Calendar API — A DECIDIR no spike DISC-001 (service account c/ delegação de domínio vs delegação por usuário). | — (gated DISC-001) |

**Provenance** — Confidence 80 · Origin: inherited · Source: TA §adrs (cto_authored) · Status: respondida · Disposition: inherited (decided ADR-001..005 ✓; discovery ADR-006) · Hint: ADR-006 não-settled; breakdown fino vai ao Tech Backlog.

# ===== SECTION: effort-cost =====
| Área | Estimativa | Senioridade |
|---|---|---|
| Backend — núcleo de reservas | 12 dias | Pleno (revisão Sênior) |
| Backend — anti-double-booking + recorrência | 8 dias | Sênior |
| Integração / OAuth — Calendar + login social | 10 dias | Sênior |
| Frontend — UI responsiva | 12 dias | Pleno |
| QA — incl. harness de concorrência | 8 dias | QA |
| LGPD básica + migração/descontinuação | 4 dias | Pleno |
| **Total (desenvolvimento)** | **~54 dias-pessoa** | (+ spike DISC-001 ~2–4 dias, fora do total) |

**Infra / Terceiros / Opex:** infra modesta (1 app host + 1 banco gerenciado + 1 worker; sem multi-região/Kubernetes); terceiros baixo (Calendar API na quota gratuita — confirmar no spike; login social Google gratuito; sem licenças); opex recorrente baixo. TCO cria fundação reutilizável (Outlook Fase 2, SSO Fase 3, analytics Fase 2). Estimativa firme substitui a preliminar do RP §13 (deferida).

**Provenance** — Confidence 72 · Origin: inherited · Source: TA §effort-cost (cto_authored) · Status: respondida · Disposition: inherited (decided; linha OAuth a re-firmar pós-DISC-001) · Hint: uso interno; não é compromisso contratual; o PM trata a linha de integração como sujeita a ajuste pós-spike.

<!-- END OF DOCUMENT -->
