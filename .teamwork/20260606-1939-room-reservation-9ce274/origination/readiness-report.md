<!--
RELATÓRIO DE PRONTIDÃO — room-reservation
Gerado por: Gap Reporter
Documento alvo: target-document.md (rev 2)
Q&A Ledger: qa-log.md (Rev 6)
Data: 2026-06-06
-->

# Relatório de Prontidão — Sistema de Reserva de Salas de Reunião

<!-- rev: 1 · updated: 2026-06-06 -->

## Headline — Estado atual

> **Pontuação de prontidão: 69% · GATE CLEAR** (as-of-rev 2 · 2026-06-06)
>
> Citação canônica do Auditor de Confiança: "GATE CLEAR, readiness = 69%."
>
> Gate liberado por disposição honesta: `impact` (62, abaixo do limiar 70) carregado como **PREMISSA** declarada. Demais seções bloqueantes (`problem` 80, `originator` 72, `reach` 76) atingem seus limiares mínimos.
>
> Triagem rascunhada: **Descoberta (Discovery)** — pendente aprovação humana.

---

## Mapa de seções — visão rápida das lacunas

> Ordenação: bloqueantes primeiro (blocks=true), depois por confiança crescente.

| id | Seção | Bloqueia gate? | Confiança atual | Status | O que elevaria a confiança |
|----|-------|:--------------:|:---------------:|--------|---------------------------|
| impact | Impacto de negócio | Sim | **62** ⚠ (premissa) | Respondida — qualitativa, sem quantificação | Coletar: nº de choques/semana × minutos por evento; exemplos concretos de "negócios adiados" com valor estimado; frequência de reuniões com clientes/diretoria afetadas |
| problem | Problema (a dor) | Sim | **80** | Respondida — atinge limiar | Sem lacuna crítica. Melhoria incremental: quantificar horas perdidas por evento |
| originator | Originador e contexto | Sim | **72** | Respondida — solicitante NÃO identificado nominalmente | Nomear o solicitante que conduziu a sessão; confirmar papel/cargo para firmar peso institucional |
| reach | Quem é impactado (alcance) | Sim | **76** | Respondida | Sem lacuna crítica. Opção C (imagem/relacionamento) não selecionada em Q006 apesar de Q004 citar constrangimento com externos — ver conflito aberto abaixo |
| urgency | Urgência — por que agora | Não | **55** ⚠ (inferida) | Respondida — inferida, sem gatilho direto | Perguntar diretamente: existe prazo, evento externo ou decisão de gestão que justifique "por que agora"? Urgência não foi perguntada na sessão |
| nature-signal | Sinal de natureza (greenfield) | Não | **68** (inferida) | Respondida — inferida da declaração de abertura | PO confirmar se existe planilha, quadro ou calendário compartilhado em uso informal |
| constraints | Restrições | Não | **—** (vazia) | Não explorada | Levantar: orçamento, prazo, integrações com agenda corporativa (Google Calendar / Outlook), requisitos técnicos |
| priority | Prioridade declarada | Não | **—** (não declarada) | Não perguntada | Perguntar ao solicitante: qual a prioridade percebida e o motivo por trás dela |
| meta | Metadados | Não | n/a (meta) | Completa | — |
| revisions | Histórico de revisões | Não | n/a (meta) | Completa | — |
| readiness | Maturidade recebida | Não | n/a (derivada) | Computada | Recomputa automaticamente quando seções de entrada mudam |
| triage | Triagem — decisão de roteamento | Não | ~62 (rascunho IA) | Rascunho — pendente aprovação humana | Aprovação humana do roteamento "Descoberta"; confirmar "Triado por" e data de triagem |
| cto_escalation | Escalação arquitetural | Não | ~60 (inferida) | Inferida — depende de constraints | Levantar restrições (especialmente integração com agenda corporativa) para confirmar ou descartar necessidade de revisão arquitetural |
| assumptions | Premissas | Não | n/a (captura) | 3 premissas abertas | Ver tabela de disposições abertas abaixo |
| discovery | Briefing de descoberta | Não | n/a (condicional) | Incluída (triage.decision==Discovery) | Execução da descoberta fecha as incógnitas; resultados a preencher na coluna "Resultado" |
| handoff | Encaminhamento | Não | n/a (derivada) | Rascunho — pendente aprovação de triagem | Confirmação humana da triagem libera o encaminhamento |

---

## Disposições abertas

### Premissas (a validar — 3 itens)

| # | Premissa | Dono da validação | Caixa-de-tempo |
|---|----------|-------------------|:--------------:|
| P1 | A magnitude do impacto (tempo perdido, reuniões prejudicadas, retrabalho) é estimativa qualitativa, não quantificada | PO + admin/facilities (coletar nº de choques/semana e minutos por evento) | 1 semana |
| P2 | "Negócios adiados" representa custo real de receita/relacionamento — não comprovado | Liderança comercial / diretoria (solicitar exemplos concretos e valor estimado) | 3 dias |
| P3 | Não existe nenhuma ferramenta formal de reserva de salas em uso hoje (greenfield assumido) | PO + admin/facilities (confirmar se há planilha, quadro ou calendário compartilhado) | 2 dias |

### Lacunas fecháveis agora (antes de Discovery)

Estes itens dependem apenas do solicitante e podem ser resolvidos com perguntas diretas na mesma sessão ou em follow-up curto:

| Lacuna | Seção afetada | Ação |
|--------|--------------|------|
| Nome do solicitante não declarado | originator (72 → potencial 85+) | Pedir ao solicitante que se identifique por nome e cargo |
| Urgência não perguntada diretamente | urgency (55 → potencial 70+) | Perguntar: "Existe algum prazo, evento ou decisão que torna isso urgente agora?" |
| Prioridade não declarada | priority (— → qualquer valor) | Perguntar: "Como você priorizaria isso em relação a outros pedidos ativos?" |
| Restrições não exploradas | constraints (— → qualquer valor) | Perguntar sobre orçamento, prazo, integração com agenda corporativa (Google/Outlook) |

### Itens do domínio de Discovery (dono: PO)

Estes itens requerem investigação com partes além do solicitante — pertencem à fase de Descoberta:

| Incógnita | Por que importa | Investigar com | Caixa-de-tempo |
|-----------|----------------|----------------|:--------------:|
| Quantificação do impacto (P1 acima) | Define se o valor justifica priorização imediata | Admin / facilities / recepção | 1 semana |
| "Negócios adiados" como custo real (P2 acima) | Eixo de maior gravidade potencial — não comprovado | Liderança comercial / diretoria | 3 dias |
| Confirmação de greenfield vs. brownfield (P3 acima) | Define escopo e natureza da demanda | PO + admin / facilities | 2 dias |
| Necessidade de integração com agenda corporativa | Possível gatilho de escalação arquitetural | PO + TI | 3 dias |

### Aprovação humana pendente

| Item | Estado |
|------|--------|
| Decisão de triagem: Descoberta (Discovery) | Rascunho de IA — "Triado por" e data de triagem em branco |
| Encaminhamento (handoff) | Derivado da triagem — liberado quando triagem for confirmada |

---

## Conflitos em aberto

| # | Conflito | Seções envolvidas | Estado |
|---|----------|------------------|--------|
| C1 | Eixo de imagem/relacionamento (opção C de Q006) citado como dor em Q004 ("constrangimento e risco de imagem institucional quando visitantes externos estão presentes") mas **não selecionado** em Q006. O solicitante pode ter interpretado que B ("reunião importante prejudicada") ou o item livre "Negócios adiados" cobrem esse eixo, ou pode ter sido uma omissão. | reach (Q004) vs. impact (Q006) | Aguardando Reconciler — sem conflito formal registrado, mas anotado para verificação de sobreposição ou omissão intencional |

---

## O que fecha o gate de forma definitiva

O gate já está CLEAR por disposição honesta. Para elevar a pontuação de 69% para um nível mais firme (meta natural: 75–80%):

1. **Prioridade A — fechar P1 (impact):** quantificar pelo menos um eixo do impacto (ex.: nº de choques/semana × minutos). Isso elevaria `impact` de 62 para ~75, subindo a média geral ~3–4 pontos.
2. **Prioridade B — fechar urgency (55):** uma única pergunta direta sobre gatilho "por que agora" pode elevar urgency de 55 para 70+.
3. **Prioridade C — nomear o solicitante:** resolve a nota pendente de originator (72) e fortalece peso institucional.
4. **Resolução do conflito C1:** confirmar com o Reconciler se o eixo de imagem está implicitamente coberto ou se houve omissão — isso impacta a confiança de reach.

---

<!-- END OF DOCUMENT -->
