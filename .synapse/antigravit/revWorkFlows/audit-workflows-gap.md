# Auditoria de Gaps — Workflows AIOS + AntiGravity

**Data:** 2026-02-26
**Status:** ✅ Concluído (Fase 1 — T1.6)

---

## 1. Gap Matrix: Workflows

| Workflow                 | docs/aios-workflows/ | .aios-core/workflows/ | .antigravity/workflows/ | Status AntiGravity      |
| ------------------------ | :------------------: | :-------------------: | :---------------------: | :---------------------- |
| story-development-cycle  |      ✅ MD 25KB      |      ✅ YAML 8KB      |        ✅ MD 3KB        | OK — Resumido (OK)      |
| brownfield-discovery     |      ✅ MD 26KB      |     ✅ YAML 33KB      |        ✅ MD 4KB        | OK — Resumido (OK)      |
| spec-pipeline            |      ✅ MD 29KB      |     ✅ YAML 24KB      |        ✅ MD 3KB        | OK — Resumido (OK)      |
| create-squad             |          ─           |           ─           |        ✅ MD 4KB        | OK — Exclusivo AntiGrav |
| **greenfield-fullstack** |      ✅ MD 25KB      |     ✅ YAML 16KB      |     ❌ **AUSENTE**      | **CRIAR**               |
| **greenfield-service**   |      ✅ MD 23KB      |     ✅ YAML 11KB      |     ❌ **AUSENTE**      | **CRIAR**               |
| **greenfield-ui**        |      ✅ MD 27KB      |     ✅ YAML 11KB      |     ❌ **AUSENTE**      | **CRIAR**               |
| **brownfield-fullstack** |      ✅ MD 25KB      |     ✅ YAML 13KB      |     ❌ **AUSENTE**      | **CRIAR**               |
| **brownfield-service**   |      ✅ MD 25KB      |      ✅ YAML 9KB      |     ❌ **AUSENTE**      | **CRIAR**               |
| **brownfield-ui**        |      ✅ MD 27KB      |      ✅ YAML 9KB      |     ❌ **AUSENTE**      | **CRIAR**               |
| **qa-loop**              |      ✅ MD 26KB      |     ✅ YAML 19KB      |     ❌ **AUSENTE**      | **CRIAR**               |
| **design-system-build**  |      ✅ MD 20KB      |      ✅ YAML 7KB      |     ❌ **AUSENTE**      | **CRIAR** + Stitch MCP  |
| **auto-worktree**        |      ✅ MD 20KB      |     ✅ YAML 19KB      |     ❌ **AUSENTE**      | **CRIAR** adaptado      |
| **epic-orchestration**   |          ─           |     ✅ YAML 17KB      |     ❌ **AUSENTE**      | **CRIAR/REFERENCIAR**   |
| bob-orchestrator         |      ✅ MD 50KB      |           ─           |            ─            | INVESTIGAR              |
| development-cycle        |          ─           |     ✅ YAML 14KB      |     Coberto por SDC     | OK (via SDC)            |

**Resultado: 10 workflows faltantes no AntiGravity + 1 a investigar (bob-orchestrator)**

---

## 2. Gap Matrix: Skills (.antigravity/skills/)

| Skill            | SKILL.md | Referencia .antigravity/workflows/ | Problema Identificado                                                            |
| ---------------- | :------: | :--------------------------------: | -------------------------------------------------------------------------------- |
| squad            |    ✅    |               ❌ NÃO               | Referencia `squads/squad-creator/workflows/` (interno) mas não `create-squad.md` |
| clone-mind       |    ✅    |               ❌ NÃO               | Pipeline interno completo, sem link para workflow                                |
| enhance-workflow |    ✅    |               ❌ NÃO               | Pipeline próprio sem referência aos workflows AIOS                               |
| architect-first  |    ✅    |               ❌ NÃO               | Menciona "workflow" internamente, não links externos                             |
| checklist-runner |    ✅    |               ❌ NÃO               | Referencia `.aios-core/development/checklists/`                                  |
| synapse          |    ✅    |               ❌ NÃO               | Engine de contexto, sem referência a workflows AIOS                              |

**Resultado: 0 de 6 skills referenciam .antigravity/workflows/ explicitamente**

---

## 3. Gap Matrix: Regras (.antigravity/rules/)

| Arquivo                 | Problema                                                      | Ação                                     |
| ----------------------- | ------------------------------------------------------------- | ---------------------------------------- |
| workflow-execution.md   | Cobre apenas 4 de 14 workflows. Sem guia por tipo de projeto. | **ATUALIZAR** — adicionar 10 workflows   |
| agent-handoff.md        | Cobre handoff entre agentes, não entre workflows.             | **ATUALIZAR** — adicionar handoffs de WF |
| governance.md           | Sem regras para worktrees Git ou design-system.               | **REVISAR** — adicionar contexto         |
| agent-authority.md      | OK                                                            | ─                                        |
| agent-memory-imports.md | OK                                                            | ─                                        |
| ids-principles.md       | OK                                                            | ─                                        |
| story-lifecycle.md      | OK                                                            | ─                                        |
| tool-usage.md           | OK                                                            | ─                                        |

---

## 4. Gap Matrix: ANTIGRAVITY.md

| Seção                 | Status | Problema                                                    |
| --------------------- | ------ | ----------------------------------------------------------- |
| Sistema de Agentes    | ✅     | OK                                                          |
| Workflow de Story     | ⚠️     | Menciona apenas SDC. Sem referência a Greenfield/Brownfield |
| Guia de Seleção       | ❌     | **NÃO EXISTE** — ausência total                             |
| Comandos Frequentes   | ✅     | OK                                                          |
| Governança Automática | ✅     | OK                                                          |

---

## 5. Análise: .claude/commands vs .antigravity/workflows/

| Namespace .claude/commands | Conteúdo Real                    | Equivalente .antigravity/  | Status     |
| -------------------------- | -------------------------------- | -------------------------- | ---------- |
| AIOS/                      | agents/, scripts/, stories/      | Parcialmente em workflows/ | ⚠️ Parcial |
| cohort-squad/              | agents/ (apenas)                 | create-squad.md            | ✅ OK      |
| synapse/                   | manager.md + tasks/ + templates/ | synapse SKILL.md           | ⚠️ Parcial |
| design-system/             | agents/ (apenas)                 | ❌ NÃO EXISTE              | ❌ Gap     |

> **Nota:** Os .claude/commands não contêm arquivos MD de comandos individuais — apenas subpastas de agents/tasks. Os workflows migraram diretamente para .antigravity/workflows/ corretamente.

---

## 6. Observação sobre bob-orchestrator

`docs/aios-workflows/bob-orchestrator-workflow.md` (49KB) é um meta-workflow de orquestração épica. Não tem YAML em `.aios-core`. Investigação necessária para confirmar se requer agente `@bob` específico ou se é puramente documental. Verificar se `.antigravity/agents/` deve ter `bob.md`.

---

## 7. Prioridade de Execução (Fase 2)

| Prioridade | Workflow             | Razão                                 |
| :--------: | -------------------- | ------------------------------------- |
|  🔴 Alta   | greenfield-fullstack | Uso mais comum ao iniciar projetos    |
|  🔴 Alta   | qa-loop              | Complementa SDC (já existente)        |
|  🔴 Alta   | brownfield-fullstack | Uso mais comum em projetos existentes |
|  🟡 Média  | greenfield-service   | Backend-only projects                 |
|  🟡 Média  | brownfield-service   | Backend-only existing                 |
|  🟡 Média  | greenfield-ui        | Frontend-only                         |
|  🟡 Média  | brownfield-ui        | Frontend-only existing                |
|  🟡 Média  | design-system-build  | + Stitch MCP advantage                |
| 🟢 Normal  | auto-worktree        | Git worktree management               |
| 🟢 Normal  | epic-orchestration   | Complemento ao spec-pipeline          |
|  ⚪ Baixa  | bob-orchestrator     | Investigar primeiro                   |
