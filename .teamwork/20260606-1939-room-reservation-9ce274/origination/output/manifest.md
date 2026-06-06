<!--
MANIFESTO DA FASE DE ORIGINAÇÃO · room-reservation
Gerado por: Packager (escritor canônico de output/manifest.md)
Frente: origination
Data de geração: 2026-06-06
-->

# Manifesto — Sistema de Reserva de Salas de Reunião

> Índice completo da frente de originação. Este documento consolida a contagem de artefatos, pontuação de prontidão com citação canônica da auditoria, disposições abertas e proveniência do template. Serve como guia de entrega para o próximo estágio (descoberta direcionada) e registro de trilha para futuras referências.

---

## Artefatos Produzidos

Tabela de todos os arquivos gerados nesta frente, com tipo, linguagem e responsável pela escrita:

| Caminho | O que é | Linguagem | Escrito por |
|---------|---------|-----------|-------------|
| `target-document.md` (rev 5) | Registro de originação preenchido — documento de trabalho canônico que consolida a demanda capturada, seções de captura, derivações, maturidade e triagem | pt-BR | Harmonizer + Synthesizer (iterativo) |
| `output/humanized.md` | Cópia canônica humanizada — transposição limpa e legível de target-document para leitor não técnico; base para herança em frentes a jusante | pt-BR | Humanizer |
| `output/enrichment-plan.md` | Plano de enriquecimento visual — catálogo de 7 visuais propostos (diagramas Mermaid + tabelas); 2 marcados DRAFT (impacto, constraints/CTO) | pt-BR | Visual Enricher (plano) |
| `output/enriched.md` | Cópia enriquecida — humanized.md aumentado com 6 diagramas Mermaid renderizados (flowchart, stakeholder map, cost-benefit conceitual, timeline, readiness radar, triage tree) + 1 tabela de disposições; 1 visual marcado DRAFT | pt-BR | Visual Enricher (render) |
| `final/room-reservation-001.md` | ⭐ **ENTREGÁVEL FINAL IMPRIMÍVEL** — enriquecido limpo, pronto para distribuição, com apêndice "Fontes e Registro de Perguntas" integrando Q&A ledger, links de proveniência canônicos, e versão legível para decisores | pt-BR | Finalizer |
| `qa-log.md` (Rev 9) | Ledger de perguntas e respostas — registro íntegro Q001–Q011 com disposições, confiança, fonte e dicas; carrega a história inteira da captura | pt-BR | Interviewer / Auditor (iterativo) |
| `readiness-report.md` (Rev 3) | Mapa de lacunas e prontidão — síntese do Auditor: score 74%, gate CLEAR, lacunas fecháveis, conflitos resolvidos, disposições abertas | pt-BR | Gap Reporter (Confidence Auditor) |
| `contract.lock.md` | Contrato derivado do template — rubrica de cada seção, bloqueadores, min-confidence, condições e notas sobre fresh-run e gate-sections | pt-BR | Template engine (auto-gerado) |
| `glossary.md` | Glossário de termos canônicos — léxico de domínio (double-booking, negócios adiados, admin/facilities, etc.) para consistência semântica | pt-BR | Harmonizer |

---

## Prontidão — Verdito Final

Citação canônica do Auditor de Confiança (ledger header, qa-log.md):

> **Pontuação: 74% · GATE: CLEAR**  
> *As-of-rev: 9 · 2026-06-06*  
> "Readiness = 74%, pendente reavaliação final. Gate já está CLEAR por disposição honesta (`impact` carregado como PREMISSA qualitativa bem documentada). Seções bloqueantes: `problem` 80 (✓), `originator` 80 (✓), `reach` 76 (✓); único elo abaixo do limiar: `impact` 65 (PREMISSA)."

**Breakdown por seção bloqueante:**
- **Problema** (min-confidence=80): 80 — ✓ **ATENDE** (double-booking crônico semanal confirmado)
- **Originador** (min-confidence=70): 80 — ✓ **ATENDE** (demanda coletiva canalizada, papel de representante estabelecido)
- **Alcance** (min-confidence=70): 76 — ✓ **ATENDE** (quatro perfis confirmados: equipes, clientes/externos, liderança, admin/facilities)
- **Impacto** (min-confidence=70): 65 — ⚠️ **ABAIXO DO LIMIAR, CARREGADO COMO PREMISSA** (quatro eixos de custo qualitativos confirmados; nenhum quantificado)

**Disposições de gate:**
- Nenhuma seção bloqueante permanece aberta — all four resolved (three by confidence, one by honest assumption)
- Impacto é uma premissa declarada, não um defeito: os eixos estão documentados e mapeados para validação na descoberta

---

## Disposições Abertas

### Premissas (a validar — 3 itens)

| # | Premissa | Dono da validação | Caixa-de-tempo | Status |
|---|----------|-------------------|:--------------:|--------|
| **P1** | Magnitude do impacto (tempo perdido, reuniões prejudicadas, retrabalho, negócios adiados) é qualitativa, não quantificada — necessário nº de choques/semana × minutos por evento + exemplos de negócios adiados com valor estimado | PO + admin/facilities + liderança comercial | 1 semana | Aberta — validação em Descoberta |
| **P2** | "Negócios adiados" representa custo real de receita/relacionamento — não comprovado com exemplos concretos | Liderança comercial / diretoria | 3 dias | Aberta — validação em Descoberta |
| **P3** | Inexistência de ferramenta formal de reserva de salas em uso hoje (greenfield assumido) — sem confirmação de planilha, quadro ou calendário compartilhado | PO + admin/facilities | 2 dias | Aberta — validação em Descoberta |

**Nota:** Todas as três premissas foram explicitamente mapeadas no readiness-report.md e no qa-log.md. Nenhuma é oculta; todas carregam critério de validação e proprietário.

### Descoberta Confirmada (D001, D002)

| Item | Descrição | Decisão | Assinado |
|------|-----------|---------|----------|
| **D001** | Triagem — Descoberta direcionada | CONFIRMADO pelo solicitante (Q011, 2026-06-06) | ✓ Solicitante (canalizador) |
| **D002** | Foco da descoberta: (1) quantificar impacto em eixos de custo; (2) viabilidade de integração com agenda corporativa (Google/Outlook) | CONFIRMADO como escopo da descoberta | ✓ Solicitante |

**Implicação:** A triagem deixou de ser rascunho de IA (⚠️ DRAFT) e passou a ser decisão humana confirmada (✅). O handoff está liberado.

### Itens Resolvidos (conflitos, omissões)

| Conflito anterior | Resolução | Evidência |
|------------------|-----------|-----------|
| **C1** — Eixo "imagem/relacionamento" citado em Q004 mas não selecionado em Q006 | Resolvido: imagem/relacionamento está subsumido em "Negócios adiados" (Q010) — não é eixo separado | Q010 answer: "Está embutido em 'negócios adiados'" |
| Urgência não perguntada diretamente | Resolvido: Q008 capturou "pressão contínua" como tipo de urgência | Q008 answer: "Não há gatilho específico, pressão contínua" |
| Nome do solicitante não nominado | Parcialmente resolvido: papel de "canalizador/representante" estabelecido (Q007); nome próprio não coletado (não é bloqueador) | Q007 answer: "Fui eu + outros reclamantes" |

---

## Proveniência

| Campo | Valor |
|-------|-------|
| **Template** | `target-template.origination-record.md` |
| **Versão do template** | v1 |
| **Hash do template** | `6d91450cbf11f615699612c7b47c8c7f6876ba4ce0a85a721196182479f9fe4f` |
| **Linguagem de saída** | pt-BR |
| **Data de geração** | 2026-06-06 |
| **Fase** | origination |
| **Fase-ID** | `/home/ubuntu/hugo/tests/teamwork-tests/.teamwork/20260606-1939-room-reservation-9ce274/origination` |

---

## Próximo Passo — Handoff

**Decisão de triagem confirmada:** DESCOBERTA DIRECIONADA (Q011, assinado pelo solicitante em 2026-06-06)

**Encaminhamento recomendado:**
1. Iniciar fase de Descoberta com prazo de ~1–1,5 semanas
2. Foco A: Quantificar impacto — transformar os quatro eixos de custo qualitativos em estimativas numéricas:
   - Nº de conflitos (double-bookings) por semana
   - Minutos perdidos por evento
   - Frequência e tipo de reuniões com clientes/diretoria afetadas
   - Exemplos concretos de negócios adiados com valor estimado
3. Foco B: Validar viabilidade da integração com agenda corporativa (Google Calendar e/ou Outlook) — consultar TI sobre APIs disponíveis, requisitos de autenticação SSO, e compatibilidade técnica

**Entregáveis da descoberta:**
- Relatório de quantificação de impacto (P1, P2, P3 validadas ou reclassificadas)
- Viabilidade de integração com agenda (restricción arquitetural confirmada ou removida)
- Revisão de escopo inicial com base em insights de descoberta
- Recomendação de roteamento final (escopo, prototipagem, entrega)

---

## Checklist de Finalização

- [x] Artefatos de captura completos (9/9 arquivos)
- [x] Seções bloqueantes atingem limiar ou carregam disposição honesta (problem 80, originator 80, reach 76, impact 65 como PREMISSA)
- [x] Ledger de Q&A fechado (Q001–Q011, Rev 9)
- [x] Conflitos resolvidos (C1, urgência, nome do solicitante)
- [x] Disposições abertas catalogadas (3 premissas, 2 confirmações de descoberta)
- [x] Triagem confirmada por humano (Q011, D001, D002)
- [x] Handoff definido (Descoberta direcionada, 1–1,5 semanas)
- [x] Proveniência registrada (template, hash, data)
- [x] Entregável final imprimível gerado (`final/room-reservation-001.md`)

---

## Sumário para o Tomador de Decisão

O **Sistema de Reserva de Salas de Reunião** entrou em originação com uma declaração de solução ("quero um sistema para reservar salas"). A captura revelou a dor subjacente: **conflito de agendamento (double-booking) que acontece toda semana**, afetando quatro perfis distintos (equipes, reuniões com clientes/externos, liderança, admin/facilities). 

A magnitude do impacto foi capturada em quatro eixos qualitativos — tempo perdido, reuniões prejudicadas, retrabalho operacional, negócios adiados — mas permanece sem quantificação. Essa lacuna coloca a seção `impact` abaixo do limiar de confiança mínimo (65 vs. 70), mas é uma lacuna honesta e mapeada para a fase de Descoberta, não um defeito oculto.

**Pontuação de prontidão: 74%. Gate CLEAR.** O solicitante confirmou que a demanda segue para uma **descoberta direcionada (~1–1,5 semana)** focada em quantificar impacto e validar a viabilidade da integração com agenda corporativa (Google/Outlook), que foi identificada como uma restrição arquitetural que pode exigir escalação para CTO.

**Entregável final para distribuição:** `/home/ubuntu/hugo/tests/teamwork-tests/.teamwork/20260606-1939-room-reservation-9ce274/origination/final/room-reservation-001.md` — pronto para impressão, com apêndice de fontes e registro de perguntas.

<!-- END OF DOCUMENT -->
