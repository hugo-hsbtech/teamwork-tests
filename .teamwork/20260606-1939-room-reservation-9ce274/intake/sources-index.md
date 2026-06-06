# Índice de fontes — fase Intake (Triagem)
<!-- Initiative: room-reservation · Phase: intake · Indexed: 2026-06-06 -->

## Resumo de indexação
**Total indexado:** 2 fontes · **Status:** 2 indexed, 0 unresolved

---

## Tabela de fontes

| ID | Arquivo | Tipo | Conteúdo | Status |
|---|---|---|---|---|
| S001 | humanized.md | Registro de originação (formato humanizado, pt-BR) | Artefato formal de originação da demanda (INT-2026-001): problema (conflito de agendamento / double-booking), originador (demanda coletiva bottom-up), alcance (4 perfis: equipes, clientes/externos, liderança, facilities), impacto (4 eixos qualitativos não quantificados), urgência (pressão contínua), restrições técnicas (integração com Google Calendar/Outlook), decisão de triagem (Descoberta direcionada, confiança 95%, confirmada pelo solicitante em 2026-06-06). Inclui histórico de 4 revisões, maturidade (~74%), premissas (3 a validar), briefing de descoberta (4 incógnitas), encaminhamento para PO/CTO/facilities/liderança comercial. Versão v1, gerada a partir de template de originação-brainstorm. | indexed |
| S002 | room-reservation-001-final.md | Registro de originação (versão final imprimível, pt-BR) | Mesma demanda INT-2026-001 em formato compilado final: estrutura idêntica a S001 (metadados, revisões, maturidade, demanda consolidada, triagem, escalação, premissas, restrições, briefing de descoberta, encaminhamento), com inclusão de diagramas Mermaid (flowchart e radar) ilustrando conflito de agendamento, perfis impactados, eixos de custo, decisão de triagem. Versão destinada a apresentação/documento executivo. Inclui seção "Fontes e registro de perguntas" com 11 respostas do solicitante (Q001–Q011) com confiança e proveniência, e referência a 2 decisões da iniciativa (D001/D002). | indexed |

---

## Proveniência e rastreamento

### Origem dos arquivos
- **Caminho de origem:** `/home/ubuntu/hugo/tests/teamwork-tests/.teamwork/20260606-1939-room-reservation-9ce274/origination/output/` (humanized.md) e `/origination/final/` (room-reservation-001.md)
- **Data de indexação:** 2026-06-06
- **Fase:** intake (triagem de originação)
- **Linguagem de saída:** pt-BR

### Identificação do artefato primário
Ambas as fontes documentam a mesma demanda (INT-2026-001). A fonte **S001 (humanized.md)** é o registro de originação canônico, com anotações detalhadas de metadados estruturais (blocks, kind, inputs). A fonte **S002 (room-reservation-001-final.md)** é versão compilada derivada, com inclusão de visualizações (diagramas Mermaid) e apresentação formatada para audência executiva, mantendo integridade de conteúdo.

### Matriz de confiança e disposição
Demanda: confiança geral ~74% (maturidade), triagem confirmada com confiança 95% (Q011, solicitante, 2026-06-06).
- Problem: 80 (respondida)
- Originator: 80 (respondida)
- Reach: 76 (respondida)
- Urgency: 70 (respondida)
- Impact: 65 (premissa — único elo abaixo do limiar)
- Constraints: 72 (respondida)
- Triage decision: 95 (confirmada)
- CTO escalation: ~75 (inferida)

### Incógnitas abertas na descoberta (4)
1. Magnitude quantificada do impacto (nº choques/semana × min/evento) — prazo: 1 semana
2. "Negócios adiados" como custo real de receita/relacionamento — prazo: 3 dias (CRÍTICA)
3. Viabilidade da integração com agenda corporativa (Google/Outlook, plataformas, APIs, SSO, sincronização) — prazo: 1 semana (CRÍTICA, gatilho de escalação ao CTO)
4. Existe ferramenta/processo informal hoje? (greenfield vs. brownfield) — prazo: 2 dias

Prazo total sugerido: ~1 a 1,5 semana.

### Decisões vinculadas
- **D001** (2026-06-06, ativa): Triagem roteada para DESCOBERTA DIRECIONADA (aprovada, substitui rascunho de IA)
- **D002** (2026-06-06, ativa): Escalação arquitetural ao CTO obrigatória (viabilidade da integração com agenda corporativa)

---

## Anotações para o Evidence Extractor

Ambas as fontes documentam o mesmo artefato primário (registro de originação INT-2026-001) em duas presentações:
- **S001 (humanized.md):** canônica, estruturada, com anotações de metadados
- **S002 (room-reservation-001-final.md):** executiva, ilustrada com diagramas

Nenhuma fonte de referência adicional (arquivos, planilhas, entrevistas transcritas) foi fornecida. A demanda foi capturada exclusivamente por entrevista com o solicitante em 2026-06-06, com 11 respostas (Q001–Q011) documentadas em ambas as fontes.

Todos os dados necessários para triagem estão presentes. Validação de premissas (impacto quantificado, negócios adiados, greenfield/brownfield) e de viabilidade técnica (integração com agenda corporativa) será realizada na fase de Descoberta.

---

<!-- END OF DOCUMENT -->
