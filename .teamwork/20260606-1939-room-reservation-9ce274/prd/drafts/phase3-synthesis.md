<!--
PHASE 3 SYNTHESIS & RECONCILIATION — fill-ready for hsb-doc-updater to merge into prd.md.
Keyed by section id. Derived sections (Origin: synthesized). sign-off stays for Phase 4. Language pt-BR.
-->

# ===== SECTION: scope-reconciliation =====
| Item original (RP) | Alteração pós Avaliação Técnica | Motivo |
|---|---|---|
| CRUD de reservas | Inalterado | Nenhuma restrição/ressalva do TA toca o item. |
| Integração Google Calendar uma via (≤2 min) | Inalterado (entregabilidade **condicionada** ao grant OAuth do Workspace) | Restrições "sync uma-via" e R3 afirmam o item; "dependência da config do Workspace" + R1 são gate de Discovery (DISC-001) sobre a entregabilidade — dependência, não remoção/re-escopo. |
| Login social (sem SSO) | Inalterado | "Só Google; sem Outlook; sem SSO" afirma o item; R1 condiciona apenas consent/escopos. |
| Anti-double-booking (sobreposição parcial/total) | Inalterado | "Exclusividade transacional / first-commit-wins" e R2 especificam o mecanismo (já em NFR-01/ADR-001), não mudam escopo. |
| Reservas recorrentes (validação por ocorrência) | Inalterado | Nenhuma restrição toca o item. |
| Migração/descontinuação do processo manual | Inalterado | Nenhuma restrição toca o item. |
| Excluído: Outlook/M365; SSO; outros recursos; analytics; portal externo | Inalterado | "Só Google; sem Outlook; sem SSO" confirma as exclusões. |
| Adiado: Outlook (F2); analytics (F2); lembretes (F2); SSO (F3) | Inalterado | Nenhuma restrição altera os adiamentos. |
| Conformidade LGPD (NFR-07) | Inalterado | R4 (revisão Jurídico/DPO antes do release) já refletida em NFR-07; bloqueante de release, não mudança de escopo. |

**Síntese:** Escopo do RP **mantido integralmente**. As restrições e ressalvas do TA afirmam ou condicionam itens já escopados, sem adicionar/remover/re-escopar. A entregabilidade da integração Google Calendar fica condicionada ao grant OAuth do Workspace (R1 / gate DISC-001) — dependência registrada em `inherited-readiness` e `consolidated-risk`. Nenhum a-scope reconciliado é necessário; o a-scope atual permanece (resolver a nota pendente para "mantido integralmente").

**Provenance** — Confidence 80 · Origin: synthesized · Source: a-scope (RP §5) + b-feasibility (R1–R4) + b-hard-constraints · Status: respondida · Disposition: decided (escopo mantido integralmente) · Hint: entregabilidade da integração condicionada a R1/DISC-001 (dependência, não remoção); se o grant for negado, re-escopar (gatilho upstream).

# ===== SECTION: a-scope (UPDATE the pending reconciliation note only) =====
> In the a-scope section, REPLACE the inline reconciliation note ("A reconciliação final RP×TA é registrada em scope-reconciliation (Fase 3) e refletida aqui antes do freeze.") with: "Reconciliação RP×TA concluída (ver Scope Reconciliation): **escopo do RP mantido integralmente**; a entregabilidade da integração Google Calendar fica condicionada ao grant OAuth do Workspace (R1 / DISC-001)." Keep all scope items and the rest of the section + Provenance unchanged (Confidence 83, Origin: inherited). Do NOT alter any included/excluded/deferred item.

# ===== SECTION: consolidated-risk =====
| Risco | Origem | Tipo | Probabilidade | Impacto | Mitigação |
|---|---|---|---|---|---|
| Baixa adoção / resistência (usuários voltam ao hábito antigo) | RP | Produto/Adoção | Alta | Alto | NFR-04 [CRÍTICO] — fluxo mais simples que o Forms; validação com a secretária (RP §11); secretária como agente de mudança. |
| Dependência da secretária na migração | RP | Externo/Adoção | Média | Alto | Engajar a secretária como stakeholder-chave (D01); modelo flat reduz dependência de perfil único. |
| Retorno ao mural/Forms em paralelo | RP | Produto/Adoção | Média-Alta | Alto | Descontinuação formal do canal antigo em ≤2 sem (EC-03); reservas fora do sistema inválidas (RN-04). |
| R$90k em risco não recuperado | RP | Negócio | Média | Médio | Acompanhamento com a liderança comercial (D02); zero novos adiamentos em 8 sem. |
| Scope creep de integração (bidirecional/Outlook/SSO) | RP | Produto/Escopo | Baixa-Média | Médio | Escopo fixado (RP §5; restrições B.6); qualquer adição dispara R05 + reavaliação do TA; sync uma-via mantida. |
| Workspace nega/restringe grant OAuth (`calendar.events`) | TA | Externo/Integração | Média | Alto | Antecipar DISC-001; plano B de credencial (TA-Q01); escalar ao admin cedo. **Gate** da integração (D03). |
| Race condition no anti-double-booking | TA | Técnica | Média | Alto | NFR-01: gravação atômica via constraint/serializável (RN-05); harness de concorrência (EC-01, TA-Q03). |
| Quota/latência da Calendar API vs ≤2 min | TA | Integração | Baixa-Média | Médio | Worker async c/ backoff; ≤2 min tem folga; monitorar quota (TA-Q04). |
| Divergência silenciosa Calendar↔sistema | TA | Dados | Média | Médio | Aviso na UI (Calendar é espelho — EC-04/EC-13); sistema é fonte de verdade (RN-04/C-Q02). |
| Fuso/DST | TA | Dados | Baixa | Médio | UTC c/ fuso explícito; bloquear intervalos ambíguos (EC-06); confirmar mono-fuso. |
| Falha de sync deixa estado inconsistente | TA | Integração | Baixa | Médio | Outbox + retry idempotente; reserva confirmada localmente independe do sync (EC-02). |

**Dependências externas conhecidas:** Admin do Google Workspace (grant OAuth / DISC-001 / R1 — único gatilho possível de re-escopo); Secretária/Facilities (onboarding, validação UX/NFR-04, migração — D01); Liderança comercial (recuperação do pipeline R$90k, confirmar adiamentos — D02); Google Calendar API disponível + OAuth de-arriscado (D03, ligado a DISC-001).

**Provenance** — Confidence 78 · Origin: synthesized · Source: RP §12 (R01–R05 + D01–D03) + TA tech-risks (6) · Status: respondida · Disposition: decided (composto; nenhum risco novo inventado) · Hint: o risco de grant OAuth do Workspace (TA) é o único que pode gatilhar re-escopo — escalar via DISC-001/D03.

# ===== SECTION: inherited-readiness =====
| Campo | Valor |
|---|---|
| **Premissas ainda a validar** | Lado-produto: nenhuma OPEN (RP resolvidas em D003+D005). Pontos de atenção ativos para o PM/implementação: (1) EC-06 premissa de mono-fuso (ADR-005); (2) antecedência máxima exata (~90 dias, RN-09..12) a parametrizar; (3) ALT-1 sugestão de alternativas (UX) a definir; (4) US-05 confirmação anti-cancelamento acidental (modelo flat) a definir; (5) Persona 4 (secretária) conf 76 — entrevista recomendada antes do gate. |
| **Incógnitas de Discovery** | RP Discovery RESOLVIDO (D003+D005, 2026-06-06). TA Discovery **DISC-001 EM ABERTO** — ambiente Google Workspace/OAuth não documentado (escopos concedíveis, grant a apps de terceiros, modelo de credencial [ADR-006], quotas Calendar API). Gating: NFR-02/06/08 + ADR-006 + re-firmação da estimativa de integração. |
| **Requisitos delegados (com responsável)** | (1) Avaliação Técnica — antes delegada pelo RP, agora ASSINADA (TA-2026-001, Viável com ressalvas); delegação encerrada. (2) Spike DISC-001 — owner CTO/Tech Lead + TI da organização; ~2 a 4 dias; cobre R1. (3) Revisão LGPD (NFR-07/R4) — owner Jurídico/DPO; bloqueante antes do release. |

**Gatilho de re-triagem (downstream):** se uma premissa carregada se provar falsa na execução (ex.: mono-fuso EC-06, ou grant OAuth do Workspace negado R1/DISC-001), a demanda é re-triada, não corrigida em silêncio.

**Provenance** — Confidence 80 · Origin: synthesized · Source: RP dispositions (D003+D005) + TA discovery-path (R1/R4, current-state, ADR-006) + DISC-001 · Status: respondida · Disposition: discovery (DISC-001 em aberto) · Hint: DISC-001 gate NFR-02/06/08 + ADR-006 + linha de integração; product-side sem premissas OPEN, 5 pontos de atenção ativos.

# ===== SECTION: exec-summary =====
**O problema.** A organização sofre com double-booking crônico de salas: o agendamento se espalha por três canais não-integrados — mural físico, Google Forms e WhatsApp — sem nenhum mecanismo de anti-conflito. O resultado é um ritmo de ~1,8 conflitos por semana (9 em 5 semanas), com impacto comercial já quantificado: R$111 mil em negócios perdidos, R$90 mil em risco e um pipeline de ~R$700 mil de novos negócios exposto a adiamentos por choque de sala. A secretária/facilities atua como árbitro manual e gargalo a cada conflito.

**O que será construído.** Um sistema digital de reserva de salas — natureza Híbrida (software-core novo + integração + migração de um processo informal) — cujo núcleo é o anti-double-booking automático sob a regra first-commit-wins: a primeira confirmação persiste e a segunda recebe conflito, eliminando sobreposições parciais ou totais. Inclui integração uma-via com o Google Calendar (toda reserva confirmada/cancelada reflete em ≤2 minutos, sem retroalimentação reversa), login social, reservas recorrentes com validação por ocorrência, e a migração e descontinuação dos canais manuais (mural + Forms + WhatsApp) em até 2 semanas pós go-live.

**A viabilidade técnica.** O CTO assinou o veredito "Viável com ressalvas" (herdado da Avaliação Técnica, nunca re-decidido aqui). A arquitetura é sólida: a integridade anti-conflito repousa sobre exclusão transacional no banco (não read-then-write), e a sincronização com o Calendar é assíncrona e desacoplada do commit. As ressalvas têm caminhos de resolução conhecidos — o grant OAuth do Google Workspace e o modelo de credencial da Calendar API, mais a revisão LGPD (Jurídico/DPO) — confirmadas no spike DISC-001 no início da execução. Esforço firme ~54 dias-pessoa (+ spike DISC-001 ~2–4 dias, fora do total), com infra e custo recorrente modestos. Não há veto.

**O resultado esperado.** Resultados mensuráveis: zero novos double-bookings em 4 semanas pós go-live, zero novos adiamentos comerciais atribuíveis a conflito de sala em 8 semanas, e 100% das reservas migradas para o sistema digital em 2 semanas — protegendo o pipeline comercial de ~R$700 mil e estancando a perda de receita já observada.

**Provenance** — Confidence 80 · Origin: synthesized · Source: a-objectives + a-scope + b-feasibility + effort-cost + success-metrics · Status: respondida · Disposition: synthesized · Hint: nenhum fato novo; confiança limitada pelo input mais fraco (effort-cost 72) e pela ressalva R1 ainda aberta; sobe quando DISC-001 fecha.

# ===== SECTION: handoff-gate =====
| Checklist de entrega | OK? |
|---|---|
| RP congelado (`freezeReady`) e referenciado | ✓ |
| Avaliação Técnica assinada (ou N/A justificado) | ✓ |
| Reconciliação de escopo registrada | ✓ |
| Riscos e dependências consolidados | ✓ |
| Dependências externas explícitas | ✓ |
| Disposições em aberto visíveis | ✓ |

**Prioridade e contexto de negócio (por que esta demanda, agora):** Double-booking crônico (~1,8 conflitos/semana — 9 em 5 semanas) com impacto comercial quantificado: R$111k já perdidos, R$90k em risco, pipeline ~R$700k acompanhado com a liderança comercial (D02). O custo de esperar cresce a cada semana — cada conflito erode a credibilidade em reuniões com clientes e adia negócios. A integração foi de-arriscada e considerada viável ("Viável com ressalvas", TA-2026-001); o único gatilho possível de re-escopo é a negação do grant OAuth pelo admin do Workspace (R1 / DISC-001). Escala modesta (~200 usuários, janela 08h–19h, organização única); a restrição crítica é corretude sob concorrência (NFR-01), não volume. Migração e descontinuação do processo manual em ≤2 semanas pós go-live.

> Nota de autoridade: o PM tem autoridade explícita para rejeitar o PRD e devolvê-lo com lacunas específicas (não um genérico "precisa de mais detalhes"). A rejeição e o motivo entram no Histórico de Revisões; o PO endereça lacunas de produto, o CTO as técnicas (reabrindo apenas a metade afetada), e a versão é incrementada.

**Provenance** — Confidence 80 · Origin: synthesized · Source: sign-off + scope-reconciliation + consolidated-risk + inherited-readiness (+ meta, b-feasibility) · Status: respondida · Disposition: synthesized · Hint: as 6 caixas são verificáveis a partir das seções correspondentes do documento fundido; a caixa de sign-off fecha quando o dual sign-off for comitado na Fase 4.

<!-- END OF DOCUMENT -->
