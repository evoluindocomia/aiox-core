# Antigravity Environment

> **Version:** 2.0 | **Language:** EN | **Updated:** 2026-02-26 | **Status:** ✅ Production

**Antigravity** is the native configuration and agent orchestration environment for Synkra AIOS, built for the **Google Gemini** IDE. It replaces the legacy `.claude/` environment with a richer, workflow-complete structure.

> In simple terms: `.antigravity/` is to Antigravity what `.claude/` is to Claude Code — the system's brain. But with capabilities Claude Code doesn't have.

---

## What is `.antigravity/`?

```
.antigravity/
├── ANTIGRAVITY.md          ← Master document (constitution + agent guide)
├── agents/                 ← 28+ agents (core, chiefs, mind clones, specials)
├── rules/                  ← Behavioral rules and governance
├── skills/                 ← 6 modular skills (SKILL.md)
├── workflows/              ← 14 workflows + selection README
├── templates/              ← 16 document templates
└── agent-memory/           ← Persistent agent memory
```

---

## Why Antigravity?

| Dimension            | Claude Code                   | Antigravity                            |
| -------------------- | ----------------------------- | -------------------------------------- |
| AI Engine            | Claude (Anthropic)            | Gemini (Google DeepMind)               |
| Master file          | `.claude/CLAUDE.md`           | `.antigravity/ANTIGRAVITY.md`          |
| Automatic hooks      | 6 Python scripts (PreToolUse) | Instructional `governance.md`          |
| Image generation     | ❌ N/A                        | ✅ `generate_image`                    |
| UI Design            | ❌ N/A                        | ✅ `mcp_stitch_*` (Stitch MCP)         |
| Browser automation   | ❌ N/A                        | ✅ `browser_subagent` (WebP recording) |
| Cross-session memory | MEMORY.md per agent           | KI System + MEMORY.md                  |
| Available Workflows  | 14 workflows via `.claude/`   | ✅ 14 workflows in `.antigravity/`     |

---

## Quick Start — Choose Your Entry Point

### New Project?

| Project Type              | Tell Antigravity                     | Workflow Activated        |
| ------------------------- | ------------------------------------ | ------------------------- |
| Full-Stack (front + back) | "Create a new fullstack application" | `greenfield-fullstack.md` |
| Backend / API only        | "Create a new service/API"           | `greenfield-service.md`   |
| Frontend / UI only        | "Create a new frontend/landing page" | `greenfield-ui.md`        |

### Existing Project?

| Situation              | Tell Antigravity                      | Workflow Activated        |
| ---------------------- | ------------------------------------- | ------------------------- |
| Don't know the project | "Run discovery on existing project"   | `brownfield-discovery.md` |
| Add full-stack feature | "Evolve the existing application"     | `brownfield-fullstack.md` |
| Add backend feature    | "Add endpoint/service to the project" | `brownfield-service.md`   |
| Add frontend feature   | "Add page/component to the project"   | `brownfield-ui.md`        |

### During Development?

| Situation                     | Flow                              | Workflow Activated           |
| ----------------------------- | --------------------------------- | ---------------------------- |
| Idea → full backlog           | "Create spec for feature X"       | `spec-pipeline.md`           |
| Run a full epic               | "Execute all stories in the epic" | `epic-orchestration.md`      |
| Implement a story             | Full SDC cycle                    | `story-development-cycle.md` |
| QA failed → fix loop          | "QA loop for story X"             | `qa-loop.md`                 |
| Create/refactor design system | "Build design system"             | `design-system-build.md`     |
| Create specialist squad       | "Create squad for [domain]"       | `create-squad.md`            |
| Parallel feature work         | "Create worktree for feature X"   | `auto-worktree.md`           |

> **Full Reference:** [`.antigravity/workflows/README.md`](../../../.antigravity/workflows/README.md)

---

## Documentation Index

### [1. Getting Started](./getting-started.md)

Installation, workflow selection, agent activation, and the full development cycle.

### [2. Agents System](./agents/overview.md)

All 28+ agents — Core AIOS roles, Chiefs, Mind Clones, and Special agents.

### [3. Rules & Governance](./rules/overview.md)

How Antigravity ensures quality and security: SQL, git push, worktrees, Stitch MCP.

### [4. Skills & Capabilities](./skills/overview.md)

Modular powers: `clone-mind`, `architect-first`, `enhance-workflow`, `synapse`.

### [5. Squads & Scalability](./squads/overview.md)

The Packs model and the `squad-creator` orchestrator.

### [6. Native Workflows](./workflows/overview.md)

All 14 workflows — when to use each and how they chain together.

### [7. Tool Mapping](./tools/tool-mapping.md)

Full translation from Claude Code tools to Antigravity native tools.

### [8. Migration Guide](./migration/from-claude.md)

Lessons learned and technical mapping for teams transitioning from Claude.

---

## Core Principles

- **CLI First**: All implementations start from the terminal. UI is never a prerequisite.
- **Minds First**: Real frameworks from real experts > generic bot instructions.
- **Story Driven**: All code must originate from a validated Story.
- **Governance Inline**: Safety checks are built into agent instructions.
- **Reuse > Adapt > Create**: Always search for existing solutions before building new.

---

## Quick Reference

### Agent activation

```
@dev          → Dex (Development)
@qa           → Quinn (Quality)
@architect    → Aria (Architecture)
@pm           → Kai (Product Manager)
@po           → Nova (Product Owner)
@sm           → River (Scrum Master)
@analyst      → Zara (Research & Analysis)
@data-engineer → Dara (Database)
@ux           → Uma (UX/UI Design)
@devops       → Gage (DevOps + exclusive git push)
@brad-frost   → Brad Frost (Design System)
@squad-chief  → Squad Architect 🎨
```

### Full development cycle (SDC)

```
@sm *draft → @po *validate → @dev *develop → @qa *qa-gate → @devops *push
```

### Exclusive Antigravity tools

```typescript
generate_image()         // Generate images, mockups, and design palettes
browser_subagent()       // Browser automation with automatic WebP recording
mcp_stitch_*()           // UI design — wireframes and full screens
```

---

_Synkra AIOS — Antigravity Environment v2.0_
_Updated 2026-02-26 — 14 workflows integrated_
