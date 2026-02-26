# Getting Started with Antigravity

> **Version:** 2.0 | **Updated:** 2026-02-26

Complete guide to start using AIOS on Antigravity (Gemini IDE) — from zero to your first development cycle.

---

## Prerequisites

- **Node.js** 18+ and **npm** 8+
- **Git** installed
- **Antigravity** IDE (Google Gemini Code Assist or Gemini IDE)
- AIOS installed in the project (see installation below)

---

## 1. Installing AIOS

### New Project

```bash
# Creates the full project structure with AIOS
npx aios-core init my-project
cd my-project
```

The `init` command automatically creates:

- `.antigravity/` — Antigravity configuration (agents, rules, skills, workflows)
- `.aios-core/` — Core framework (tasks, templates, checklists)
- `docs/` — Documentation structure
- `squads/` — Specialized agent packs

### Existing Project

```bash
# Adds AIOS to an existing project
cd existing-project
npx aios-core install
```

### Verify Installation

```bash
npx aios-core doctor    # Full diagnostic
npx aios-core info      # Version and status
```

---

## 2. Understanding the Master Document

Every Antigravity session begins with `ANTIGRAVITY.md` being read automatically. It defines:

- **Constitution** — 6 core principles (CLI First, Agent Authority, etc.)
- **Default language** — PT-BR (configurable)
- **Agent system** — who does what
- **Workflow selection guide** — which workflow to use in each situation
- **Governance** — mandatory checks before critical operations

> File: [`.antigravity/ANTIGRAVITY.md`](../../../../.antigravity/ANTIGRAVITY.md)

---

## 3. Choosing the Right Workflow

Before invoking an agent, identify the right workflow for your situation:

### New project

```
"I want to build a fullstack application from scratch"
  → Antigravity uses: greenfield-fullstack.md
  → Sequence: @analyst → @pm → @ux → @architect → @po → @dev → @qa → @devops
```

```
"I need only a backend/API"
  → greenfield-service.md

"I need only a frontend/landing page"
  → greenfield-ui.md  (+ Stitch MCP for UI generation)
```

### Existing project

```
"I've never worked on this project — I need to understand it first"
  → brownfield-discovery.md
  → @architect maps → @data-engineer audits DB → @ux audits frontend

"I know the project — I want to add a fullstack feature"
  → brownfield-fullstack.md

"I want to add an endpoint to the existing backend"
  → brownfield-service.md

"I want to add a page/component to the existing frontend"
  → brownfield-ui.md
```

### During development

```
"I have an idea → I want a complete backlog"
  → spec-pipeline.md

"I have a ready epic → I want to run all stories"
  → epic-orchestration.md

"I have a story → I want to implement it"
  → story-development-cycle.md (SDC)

"QA failed → I need to fix and re-validate"
  → qa-loop.md  (max 5 iterations, automatic escalation)
```

> **Full index:** [`.antigravity/workflows/README.md`](../../../../.antigravity/workflows/README.md)

---

## 4. Activating Agents

Use the `@` prefix to invoke any agent:

```
@dev           → Dex, lead developer
@qa            → Quinn, quality & testing
@architect     → Aria, system architecture
@pm            → Kai, product management
@po            → Nova, product owner & stories
@sm            → River, scrum master
@analyst       → Zara, research & analysis
@data-engineer → Dara, database & schema
@ux            → Uma, UX/UI design
@devops        → Gage, CI/CD and git push
@brad-frost    → Brad Frost, Design System (Atomic Design)
@squad-chief   → Squad Architect 🎨
```

**Examples:**

```
@architect create the architecture for the payments service
```

```
@dev implement the authentication endpoint per story 3.2
```

---

## 5. Agent Commands (`*`)

Within an agent context, use `*` to trigger specific actions:

| Command              | What It Does                          |
| -------------------- | ------------------------------------- |
| `*help`              | List all available commands           |
| `*create-story`      | Create a new development story        |
| `*task {name}`       | Run a specific task                   |
| `*qa-loop {storyId}` | Start a QA correction iteration cycle |
| `*push`              | (@devops exclusive) — push to remote  |
| `*status`            | Show epic or workflow progress        |
| `*exit`              | Exit agent mode                       |

---

## 6. Full Development Cycle (SDC)

The **Story Development Cycle** is the standard flow for implementing any feature:

```
1. @sm *draft         → Outlines the story with epic context
2. @po *validate      → Validates acceptance criteria (GO / NO-GO)
3. @dev *develop      → Implements (Interactive or YOLO mode)
4. @qa *qa-gate       → Quality gate — PASS / CONCERNS / FAIL
5. @devops *push      → Push to remote (exclusive authority)
```

**If QA fails** → `qa-loop.md` takes over (max 5 iterations, then auto-escalation).

> ⚠️ **Non-negotiable rule:** Only `@devops` can run `git push`. All other agents must delegate.

---

## 7. Automatic Governance

Antigravity proactively verifies before each critical operation:

| Operation                      | Mandatory Check                      |
| ------------------------------ | ------------------------------------ |
| Write to `supabase/functions/` | Architecture documentation approved? |
| Create `squads/*/agents/*.md`  | DNA extracted for mind-clones?       |
| Run SQL DDL                    | Using `supabase migration` CLI?      |
| `git push`                     | Active agent is `@devops`?           |
| `git worktree add/remove`      | Active agent is `@devops`?           |
| Use `mcp_stitch_*`             | UI/Design System workflow context?   |
| Slugs/IDs                      | Valid `snake_case` format?           |

Details: [`.antigravity/rules/governance.md`](../../../../.antigravity/rules/governance.md)

---

## 8. Exclusive Antigravity Tools

Capabilities that Claude Code **does not have**:

### Image Generation

```
@ux create a mockup for the product login screen
→ Uses: generate_image() — returns a real image
```

### UI Design with Stitch MCP

```
@ux generate the main dashboard screens based on the front-end-spec
→ Uses: mcp_stitch_generate_screen_from_text()
→ Creates high-fidelity wireframes without external tools
```

### Browser Automation

```
@qa visually validate the login component in a browser
→ Uses: browser_subagent()
→ Automatically records a WebP video of the tested flow
```

---

## 9. Creating a Specialized Squad

```
@squad-chief I want a digital marketing squad
```

`@squad-chief` will:

1. Research elite minds in the domain
2. Extract behavioral and thinking DNA from each expert
3. Create agents based on real expert personalities
4. Generate the full squad structure in `squads/`

> Workflow: [`.antigravity/workflows/create-squad.md`](../../../../.antigravity/workflows/create-squad.md)

---

## 10. Worktrees — Parallel Development

To work on multiple features simultaneously:

```
@devops, create a worktree for the payments feature
→ Workflow: auto-worktree.md
→ Creates isolated branch: feat/payments
→ Development occurs without affecting main
```

---

## Next Steps

- [Agent System](./agents/overview.md) — Full hierarchy of 28+ agents
- [Rules & Governance](./rules/overview.md) — Behavioral rules and safety checkpoints
- [Workflows](./workflows/overview.md) — All 14 workflows and when to use each
- [Tool Mapping](./tools/tool-mapping.md) — All available tools
- [Templates](./templates/overview.md) — 16 ready-to-use templates
- [Migration from Claude](./migration/from-claude.md) — Differences and adaptations

---

_Synkra AIOS — Antigravity Getting Started v2.0_
_Updated 2026-02-26_
