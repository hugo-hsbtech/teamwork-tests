<!--
BROKERED READ-ONLY COPY of the initiative glossary (glossary.md at the initiative root).
Seeded by the orchestrator for the prd/ phase. Canonical writer is hsb-glossary-keeper at
the initiative level. Do not edit here.
-->
# Glossário canônico — room-reservation (cópia brokered — fase prd)

Termos canônicos compartilhados por todas as frentes desta iniciativa.

| Termo | Forma canônica | Definição | Sinônimos a evitar | Notas |
|---|---|---|---|---|
| Conflito de agendamento | conflito de agendamento (double-booking) | Duas ou mais reuniões marcadas para a mesma sala no mesmo horário, gerando confusão quando os grupos aparecem. | "bater sala", "choque de sala" (informais) | Dor central da iniciativa. |
| Sala de reunião | sala de reunião | Espaço físico do escritório reservável para reuniões. | — | Unidade de recurso gerenciada pelo sistema. |
| Negócios adiados | negócios adiados | Reuniões de negócio prejudicadas pelo conflito de salas; custo de receita e relacionamento. | — | Valor R$ quantificado: R$111k perdidos, R$90k em risco, pipeline ~R$700k. |
| Facilities | organização do escritório (facilities) | Admin/recepção/facilities; secretária é stakeholder-chave de migração. | "recepção" isolada | Absorve retrabalho a cada conflito. |
| Greenfield | greenfield (nova capacidade) | Construção de software novo. | — | Natureza FINAL = HÍBRIDA: software-core novo + integração Google Calendar + migração do processo informal. |
| Sync uma-via | sincronização uma-via (sistema → Calendar) | O sistema é a fonte de verdade; o Google Calendar é espelho read-only; alterações no Calendar não retroalimentam o sistema neste release. | "bidirecional", "sync de volta" | Firmado C-Q02 (RP) e ADR-003 (TA). |
| First-commit-wins | first-commit-wins | Sob concorrência, a primeira confirmação persiste; a segunda recebe conflito. | "last-write-wins" | NFR-01 via exclusão transacional (ADR-001). |

<!-- END OF DOCUMENT -->
