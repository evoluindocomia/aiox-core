# Task: Revisão e Integração Completa dos Workflows AIOS + AntiGravity

**Referência PRD:** [prd-workflow-review.md](./prd-workflow-review.md)
**Data:** 2026-02-26
**Prioridade:** Alta

---

## Fase 1 — Auditoria e Diagnóstico

- [x] **T1.1** Auditar os 4 workflows em `.antigravity/workflows/` e comparar com os 14 de `docs/aios-workflows/`
- [x] **T1.2** Auditar os 15 YAMLs de `.aios-core/development/workflows/` e verificar quais são referenciados por `.antigravity/rules/workflow-execution.md`
- [x] **T1.3** Mapear os 4 namespaces de `.claude/commands/` (AIOS, synapse, cohort-squad, design-system) e verificar quais foram convertidos em workflows AntiGravity
- [x] **T1.4** Verificar `.antigravity/ANTIGRAVITY.md` seção "Workflow de Story" — só menciona ciclo SDC, nenhuma referência a outros 13 workflows
- [x] **T1.5** Auditar `.antigravity/rules/workflow-execution.md` — menciona 4 workflows primários (SDC, QA Loop, Spec Pipeline, Brownfield Discovery), mas não menciona: Greenfield-\*, Auto-worktree, Design System Build, Create-Squad
- [x] **T1.6** Criar tabela de gap completa → `.synapse/antigravity/revWorkFlows/audit-workflows-gap.md` ✅

---

## Fase 2 — Reconciliação: Workflows Faltantes no AntiGravity

_Criar ou expandir os arquivos em `.antigravity/workflows/` para cobrir TODOS os 14 workflows documentados._

### 2A — Workflows Greenfield (3 workflows faltantes)

- [x] **T2A.1** Criar `.antigravity/workflows/greenfield-fullstack.md` ✅
- [x] **T2A.2** Criar `.antigravity/workflows/greenfield-service.md` ✅
- [x] **T2A.3** Criar `.antigravity/workflows/greenfield-ui.md` (+ Stitch MCP) ✅

### 2B — Workflows Brownfield Expansão (3 workflows faltantes)

- [x] **T2B.1** Criar `.antigravity/workflows/brownfield-fullstack.md` ✅
- [x] **T2B.2** Criar `.antigravity/workflows/brownfield-service.md` ✅
- [x] **T2B.3** Criar `.antigravity/workflows/brownfield-ui.md` ✅

### 2C — Workflows de Processo (2 workflows faltantes)

- [x] **T2C.1** Criar `.antigravity/workflows/qa-loop.md` ✅
- [x] **T2C.2** Criar `.antigravity/workflows/design-system-build.md` (+ Stitch MCP) ✅

### 2D — Workflows Especiais (2 workflows faltantes)

- [x] **T2D.1** Criar `.antigravity/workflows/auto-worktree.md` (adaptado sem hooks) ✅
- [x] **T2D.2** Criar `.antigravity/workflows/epic-orchestration.md` ✅

---

## Fase 3 — Integração de Skills com Workflows

- [x] **T3.1** Skill `squad` — SKILL.md atualizado com link para `create-squad.md` ✅
- [x] **T3.2** Skill `enhance-workflow` — SKILL.md atualizado com links para workflows greenfield/brownfield/spec-pipeline ✅
- [x] **T3.3** Skill `architect-first` — SKILL.md atualizado com tabela de workflows onde se aplica ✅
- [x] **T3.4** Skill `checklist-runner` — OK, já referencia `.aios-core/checklists/` (não precisa de link de workflow) ✅
- [x] **T3.5** Skill `synapse` — OK, engine de contexto, não referencia workflows de desenvolvimento ✅
- [x] **T3.6** Skill `clone-mind` — pipeline interno completo, sem necessidade de link para workflow externo ✅

---

## Fase 4 — Atualização das Regras e ANTIGRAVITY.md

- [x] **T4.1** Atualizar `.antigravity/rules/workflow-execution.md` — tabela completa dos 14 workflows adicionada ✅
- [x] **T4.2** Atualizar `.antigravity/ANTIGRAVITY.md` seção "Story-Driven Development" — guia de seleção completo incluído ✅
- [x] **T4.3** Seção "Guia de Seleção de Workflow" criada em `ANTIGRAVITY.md` ✅
- [x] **T4.4** `agent-handoff.md` atualizado — tabela de encadeamento de workflows adicionada ✅
- [x] **T4.5** `governance.md` atualizado — seções de worktree Git e Stitch MCP adicionadas ✅

---

## Fase 5 — Alinhamento com `.aios-core`

- [x] **T5.1** `brownfield-discovery.yaml` — alinhado com `.antigravity/workflows/brownfield-discovery.md` ✅
- [x] **T5.2** `development-cycle.yaml` — coberto pelo SDC do AntiGravity (`story-development-cycle.md`) ✅
- [x] **T5.3** `qa-loop.yaml` — alinhado com `qa-loop.md` (max 5 iterações, verdicts APPROVE/REJECT/BLOCKED, `qa/loop-status.json`) ✅
- [x] **T5.4** `epic-orchestration.yaml` — criado `epic-orchestration.md` no AntiGravity ✅
- [x] **T5.5** Divergência `ux-design-expert` (YAML) vs `@ux` (AntiGravity) — alias intencional, ambos apontam para `aios-ux.md` — ACEITÁVEL ✅

---

## Fase 6 — Validação e Teste de Execução

- [x] **T6.1** Smoke test agentes — 12 agentes verificados, todos presentes em `.antigravity/agents/` ✅
- [x] **T6.2** Smoke test qa-loop — max 5 iterações, verdicts e `qa/loop-status.json` documentados ✅
- [x] **T6.3** Smoke test design-system-build — Stitch MCP e @brad-frost/@design-chief referenciados corretamente ✅
- [x] **T6.4** `@bob` investigado — bob-orchestrator é meta-workflow documental sem agente específico; não requer migração para AntiGravity neste ciclo ✅
- [x] **T6.5** Templates verificados — todos os templates referenciados existem em `.antigravity/templates/` ✅

---

## Fase 7 — Documentação Final

- [x] **T7.1** Criar `.antigravity/workflows/README.md` — índice + guia de seleção completo ✅
- [x] **T7.2** Atualizar `.synapse/antigravity/walkthrough-migracao-claude.md` — pendente revisit
- [~] **T7.3** KI de Governança de Workflows — **ADIADO** por decisão consciente (2026-02-26). `ANTIGRAVITY.md` já cobre o contexto necessário. Revisitar se o agente não encontrar workflows em sessões futuras.

---

## Dependências

```
T1.* (Auditoria) → T2.* (Criação) → T3.* (Skills) → T4.* (Regras) → T5.* (Core) → T6.* (Testes) → T7.* (Docs)
```

## Critério de Conclusão (DoD)

- [ ] Todos os 14 workflows de `docs/aios-workflows/` têm correspondência em `.antigravity/workflows/`
- [ ] Todos os agentes invocados pelos workflows existem em `.antigravity/agents/`
- [ ] `.antigravity/rules/workflow-execution.md` cobre todos os workflows
- [ ] `ANTIGRAVITY.md` inclui guia de seleção de workflow completo
- [ ] `.antigravity/workflows/README.md` existe e serve como ponto de entrada
- [ ] Nenhum workflow referencia template que não existe em `.antigravity/templates/`
