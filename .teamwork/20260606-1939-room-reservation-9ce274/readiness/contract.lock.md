---
template: target-template.readiness-package.md
template_hash: 343566f7940e5c2cc8344853178fcc2a09aed59fd7518e76aefb90891c5a1dbd
template_version: v1
default_min_confidence: 70
generated: 2026-06-07
notes: Fresh run — no prior contract. Template Validator passed. 19 sections derived.
---

# Contract

| id | section | kind | blocks | min-confidence | rubric (one line) |
|----|---------|------|--------|----------------|-------------------|
| meta | Metadados | meta | false | 0 | Campos de identificação do pacote: ID, versão, origination vinculado, responsável, natureza, base de conhecimento, escalada, status, freeze, idioma. |
| revisions | Histórico de Revisão | meta | false | 0 | Tabela de revisões com versão, data, autor, status e resumo da alteração. |
| inherited-readiness | Prontidão herdada e dispositions em aberto | derived | false | 0 | Resumo do que o Origination entregou: readiness score, premissas a validar, incógnitas de Discovery abertas e requisitos delegados com dono. Inputs: exec-summary, context-problem, objectives, personas, scope, metrics, release-criteria, risks. |
| exec-summary | Seção 1 — Resumo Executivo | capture | true | 70 | 2–4 parágrafos curtos cobrindo problema, o que será construído e resultado esperado de negócio; legível por qualquer stakeholder sem contexto adicional. |
| context-problem | Seção 2 — Contexto e Problema | capture | true | 80 | Cenário atual, limitações, dor do cliente e impacto de negócio — descreve o problema, nunca a solução; subseções Cenário Atual, Limitações, Dor do Cliente, Impacto de Negócio preenchidas. |
| objectives | Seção 3 — Objetivos e Resultado Esperado | capture | true | 70 | Mínimo dois objetivos numerados e observáveis, cada um verificável (mensurável ou observável) após o release. |
| personas | Seção 4 — Personas Impactadas / Jobs-to-be-done | capture | true | 70 | Para cada persona: job-to-be-done e como é impactada por esta entrega; sem persona definida, scope e critérios de aceite perdem âncora. |
| scope | Seção 5 — Escopo Incluído e Excluído | capture | true | 75 | Lista explícita do que está DENTRO e do que está FORA; sem "excluído" preenchido a seção não está satisfeita; itens adiados alimentam Seção 14. |
| business-rules | Seção 6 — Regras de Negócio e Fluxos | capture | true | 80 | Regras verificáveis e atômicas + fluxo de transição de estado cobrindo caminhos de erro, não apenas o caminho feliz. |
| user-journey | Seção 6.5 — Jornada(s) do Usuário (ponta-a-ponta) | capture | true | 70 | Happy path completo em tabela de passos (gatilho → resultado → touchpoint → pré-condição) + caminhos alternativos; sem ao menos o happy path a seção não está satisfeita. |
| user-stories | Seção 7 — User Stories + Critérios de Aceite | capture | true | 80 | Uma história por bloco de valor em formato "Como [persona], quero [ação], para [benefício]" com critérios Given/When/Then verificáveis por não-dev; derivam dos passos da Jornada (Seção 6.5). |
| nfrs | Seção 8 — Requisitos Não-Funcionais (NFRs) | capture | true | 70 | Ao menos uma dimensão aplicável do checklist ISO/IEC 25010 preenchida com requisito de qualidade do PO; viabilidade e "como" são do Technical Assessment. |
| edge-cases | Seção 9 — Edge Cases e Modos de Falha | capture | true | 70 | Estados de erro, timeouts, permissões, concorrência — cada item descreve o comportamento esperado do sistema, não apenas o que pode dar errado; primeira classe, não rodapé. |
| metrics | Seção 10 — Métricas de Sucesso | capture | true | 70 | Valores projetados com indicadores leading e lagging e ao menos um guardrail (métrica que não pode piorar); baseline para confronto pós-rollout. |
| release-criteria | Seção 11 — Critérios de Sucesso e Aceite (do release) | capture | true | 70 | Indicadores de alto nível definindo "concluído e valioso" cobrindo ao menos Negócio, Qualidade e UX; critérios genéricos sem valor-alvo mensurável não estão satisfeitos. |
| risks | Seção 12 — Riscos e Dependências | capture | true | 70 | Riscos de produto, negócio, adoção, externos e compliance com probabilidade, impacto e mitigação; dependências de produto/negócio listadas separadamente dos riscos técnicos. |
| effort-estimate | Seção 13 — Avaliação Preliminar de Esforço e Custo | capture | false | 0 | Estimativa interna do PO para sequenciamento (não é compromisso); confiança esperada baixa (ai_drafted ou po_authored sem dados firmes). |
| roadmap | Seção 14 — Roadmap Sugerido | capture | false | 0 | Sequenciamento de valor além deste release: MVP (este release), Fase 2 e Fase 3 (backlog futuro); alimentado por itens adiados da Seção 5; não é compromisso de entrega. |
| tech-assessment-ref | Referência ao Technical Assessment | derived | false | 0 | Ponte para o artefato do CTO: status, veredito e link — NÃO conteúdo técnico; congela com Disposition=deferred (TA pendente) ou Status=Assinado quando existir. Inputs: scope, business-rules, nfrs, risks. |

## Derived sections — inputs

| id | inputs |
|----|--------|
| inherited-readiness | exec-summary, context-problem, objectives, personas, scope, metrics, release-criteria, risks |
| tech-assessment-ref | scope, business-rules, nfrs, risks |

## Gate summary

Blocking sections (blocks=true): exec-summary, context-problem, objectives, personas, scope, business-rules, user-journey, user-stories, nfrs, edge-cases, metrics, release-criteria, risks — **13 sections gate the pipeline.**

Non-blocking sections (blocks=false): meta, revisions, inherited-readiness, effort-estimate, roadmap, tech-assessment-ref — **6 sections.**

Default threshold: **70%**. Sections above default: context-problem (80), business-rules (80), scope (75), user-stories (80).

<!-- END OF DOCUMENT -->
