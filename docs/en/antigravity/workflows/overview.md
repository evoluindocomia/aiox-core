# Workflows — The 14 Native Workflows

> **Updated:** 2026-02-26 | **Total:** 14 workflows + selection README

The **14 workflows** in `.antigravity/workflows/` are equivalent to Claude Code's slash commands and sequences, translated and enriched for the native Antigravity format.

---

## What are Workflows in Antigravity?

In Claude Code, workflows were slash commands like `/AIOS:story`, `/cohort-squad:create`. In Antigravity, they are `.md` files in `.antigravity/workflows/` that agents execute as structured sequences of steps.

**Format:**

```yaml
---
description: brief workflow description
---
## Steps
1. ...
2. ...
```

> **Complete index with selection guide:** [`.antigravity/workflows/README.md`](../../../../.antigravity/workflows/README.md)

---

## Complete Workflows Table

### Greenfield — New Projects

| Workflow                                                     | When to Use                            | Responsible                                                      |
| ------------------------------------------------------------ | -------------------------------------- | ---------------------------------------------------------------- |
| [`greenfield-fullstack`](greenfield/greenfield-fullstack.md) | New full-stack app from scratch        | `@analyst → @pm → @ux → @architect → @po → @dev → @qa → @devops` |
| [`greenfield-service`](greenfield/greenfield-service.md)     | New backend/API from scratch           | `@architect → @data-engineer → @dev → @qa`                       |
| [`greenfield-ui`](greenfield/greenfield-ui.md)               | New frontend/landing page from scratch | `@ux → @ui-builder → @qa` (+ Stitch MCP)                         |

### Brownfield — Existing Projects

| Workflow                                                     | When to Use                                | Responsible                                    |
| ------------------------------------------------------------ | ------------------------------------------ | ---------------------------------------------- |
| [`brownfield-discovery`](brownfield/brownfield-discovery.md) | New to the project — need to understand it | `@architect → @analyst → @data-engineer → @ux` |
| [`brownfield-fullstack`](brownfield/brownfield-fullstack.md) | Add a full-stack feature                   | `@architect → @dev → @qa → @devops`            |
| [`brownfield-service`](brownfield/brownfield-service.md)     | Add endpoint/service                       | `@data-engineer → @dev → @qa`                  |
| [`brownfield-ui`](brownfield/brownfield-ui.md)               | Add page/component                         | `@ux → @ui-builder → @qa` (+ browser_subagent) |

### Development and Quality

| Workflow                                                            | When to Use                       | Responsible                                        |
| ------------------------------------------------------------------- | --------------------------------- | -------------------------------------------------- |
| [`story-development-cycle`](dev-quality/story-development-cycle.md) | Implement a story                 | `@sm → @po → @dev`/`@ui-builder` `→ @qa → @devops` |
| [`spec-pipeline`](dev-quality/spec-pipeline.md)                     | Idea → complete backlog           | `@pm → @analyst → @architect → @po → @dev`         |
| [`epic-orchestration`](dev-quality/epic-orchestration.md)           | Execute a complete epic           | `@po → @sm → @dev → @qa → @devops`                 |
| [`qa-loop`](dev-quality/qa-loop.md)                                 | QA rejected → fix and re-validate | `@qa → @dev → @qa` (max 5 iterations)              |

### Specials

| Workflow                                                 | When to Use                            | Responsible                      |
| -------------------------------------------------------- | -------------------------------------- | -------------------------------- |
| [`design-system-build`](specials/design-system-build.md) | Create or refactor a design system     | `@ux → @brad-frost → @dev → @qa` |
| [`stitch-ui-workflow`](stitch-ui-workflow.md)            | Mandatory pipeline to generate screens | `@ui-builder` orchestrating MCP  |
| [`create-squad`](specials/create-squad.md)               | Create an expert squad                 | `@squad-chief → @oalanicolas`    |
| [`auto-worktree`](specials/auto-worktree.md)             | Parallel feature development           | `@devops`                        |

### Match with Claude Code

| Claude Slash Command   | Antigravity Workflow                            |
| ---------------------- | ----------------------------------------------- |
| `/AIOS:story`          | `story-development-cycle.md`                    |
| `/AIOS:spec-pipeline`  | `spec-pipeline.md`                              |
| `/cohort-squad:create` | `create-squad.md`                               |
| `/cohort-squad:sync`   | `auto-worktree.md` (partial)                    |
| Analysis commands      | `brownfield-discovery.md`                       |
| _(did not exist)_      | `greenfield-fullstack.md` (new)                 |
| _(did not exist)_      | `greenfield-ui.md` + Stitch MCP **(exclusive)** |
| _(did not exist)_      | `design-system-build.md` **(exclusive)**        |
| _(did not exist)_      | `epic-orchestration.md` (new)                   |
| _(did not exist)_      | `qa-loop.md` (new)                              |

---

## Main Workflows Details

### `story-development-cycle` — Complete Story Cycle

**File:** `.antigravity/workflows/story-development-cycle.md`

The most used workflow — governs the full development cycle of a feature.

**Sequence:**

```
@sm *draft
  ↓
@po *validate
  ↓
@dev *develop (Logical/backend sides) OR @ui-builder (Screens and frontend via Stitch MCP)
  ↓
@qa *qa-gate
  ↓
@devops *push
```

| Step     | Agent                | Artifact                       | Exit Criteria                     |
| -------- | -------------------- | ------------------------------ | --------------------------------- |
| Draft    | `@sm`                | Story in `docs/stories/`       | Story with initial criteria       |
| Validate | `@po`                | Story with acceptance criteria | Measurable and complete ACs       |
| Develop  | `@dev`/`@ui-builder` | Implemented code               | All ACs covered                   |
| QA Gate  | `@qa`                | Quality report                 | lint ✅ + typecheck ✅ + tests ✅ |
| Push     | `@devops`            | PR created / branch pushed     | Remote updated                    |

---

### `greenfield-fullstack` — Full-Stack Project from Scratch

**File:** `.antigravity/workflows/greenfield-fullstack.md`

Complete workflow to build full-stack apps from scratch. Includes 4 phases:

```
Phase 0: Environment bootstrap
Phase 1: Discovery & Planning (@analyst → @pm → @ux → @architect → @po)
Phase 2: Document fragmentation
Phase 3: Development cycle (SDC repeated for each story)
```

---

### `qa-loop` — QA Fix Iterative Cycle

**File:** `.antigravity/workflows/qa-loop.md`

Activated when `@qa` issues a `REJECT` verdict. Operates with a maximum of **5 iterations**:

```
@qa review → REJECT verdict
  ↓
@qa create-fix-request
  ↓
@dev apply-fixes
  ↓
Increment iteration — back to review
  ↓ (if iteration ≥ 5 or BLOCKED)
ESCALATION to human
```

**Verdicts:** `APPROVE` / `REJECT` / `BLOCKED`

---

### `design-system-build` — Design System with Stitch MCP

**File:** `.antigravity/workflows/design-system-build.md`

> ⭐ Exclusive Antigravity workflow — utilizes tools that Claude Code does not have.

```
@ux audit → @brad-frost atomic design review
→ mcp_stitch_* (wireframes and screens)
→ generate_image (visual assets)
→ @dev implements tokens and components
→ @qa visual validation with browser_subagent
```

---

### `create-squad` — Squad Creation

**File:** `.antigravity/workflows/create-squad.md`

```
@squad-chief receives request
→ Research elite minds (search_web)
→ Curated list of real experts with frameworks
→ DNA extraction by @oalanicolas
→ Generate agents
→ Squad structure at squads/
```

---

## Natural Workflow Chaining

Some workflows naturally chain after the completion of another:

| Completed Workflow        | Suggested Next                    | Condition                      |
| ------------------------- | --------------------------------- | ------------------------------ |
| `brownfield-discovery`    | `brownfield-fullstack/service/ui` | Based on the evolution type    |
| `spec-pipeline`           | `epic-orchestration`              | After epics are generated      |
| `epic-orchestration`      | `story-development-cycle`         | For each story                 |
| `story-development-cycle` | `qa-loop`                         | If QA issues a REJECT          |
| `greenfield-ui`           | `design-system-build`             | When a design system is needed |

---

## Related Documentation

- [Workflows Index](../../../../.antigravity/workflows/README.md) — Complete quick selection
- [Core Agents](../agents/core-agents.md) — Agents that execute the workflows
- [Templates](../templates/overview.md) — Templates used in workflows
- [Skills](../skills/overview.md) — Skills called during workflows
