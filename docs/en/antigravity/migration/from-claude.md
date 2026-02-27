# From Claude to Antigravit

Technical guide on what was migrated, what changed, and what is exclusive to Antigravity.

> **Migration Date:** 2026-02-25  
> **Status:** ✅ COMPLETED (Parts 1-5)  
> **Full Walkthrough:** `.synapse/antigravity/walkthrough-migracao-claude.md`

---

## What was Migrated

The legacy `.claude/` environment had **8 layers** that were mapped to the new `.antigravity/` structure:

| Claude Layer  | Files                               | Antigravit Destination                   |
| ------------- | ----------------------------------- | ---------------------------------------- |
| Configuration | `CLAUDE.md` (379L), `settings.json` | `ANTIGRAVITY.md` (17KB)                  |
| Rules         | 10 `.md` files                      | `.antigravity/rules/` (8 files)          |
| Hooks         | 12 files (6 Python scripts)         | `governance.md` (instructional)          |
| Agents        | 29 `.md` files                      | `.antigravity/agents/` (28 files)        |
| Skills        | 12 skills + subfolders              | `.antigravity/skills/` (6 skills)        |
| Commands      | 4 slash command namespaces          | `.antigravity/workflows/` (14 workflows) |
| Templates     | 18 YAML/MD templates                | `.antigravity/templates/` (16 templates) |
| Agent Memory  | 8 subfolders with `MEMORY.md`       | `.antigravity/agent-memory/` (7 agents)  |

---

## Critical Changes

### 1. Hooks → Governance (Main Difference)

**In Claude Code:**
Automatic `PreToolUse` hooks blocked operations via exit codes (exit 2 = blocked).

**In Antigravit:**
Instructional checklists in `governance.md`. The agent proactively verifies rules before each operation. This relies on agent autonomy and covers ~95% of use cases.

| Original Python Hook            | Antigravit Governance Equivalent                |
| ------------------------------- | ----------------------------------------------- |
| `enforce-architecture-first.py` | 🔴 "Before WRITING to protected paths"          |
| `mind-clone-governance.py`      | 🔴 "Before CREATING agent in squads/\*/agents/" |
| `sql-governance.py`             | 🔴 "Before EXECUTING SQL DDL"                   |
| `enforce-git-push-authority.sh` | 🔴 "Before GIT PUSH"                            |
| `write-path-validation.py`      | 🟡 "Before SAVING documents"                    |

---

### 2. Inline Persona vs. External Files

Antigravit agents have their persona **INLINE** within the agent file (e.g., `.antigravity/agents/aios-dev.md`). No more external file dependencies, making agents more portable and specific.

### 3. Slash Commands → Workflows

Antigravity now has **full parity** with Claude Code slash commands, plus additional workflows with exclusive capabilities:

| Claude Command         | Antigravity Workflow          | Status        |
| ---------------------- | ----------------------------- | ------------- |
| `/AIOS:story`          | `story-development-cycle.md`  | ✅ Migrated   |
| `/AIOS:spec-pipeline`  | `spec-pipeline.md`            | ✅ Migrated   |
| `/cohort-squad:create` | `create-squad.md` (via packs) | ✅ Migrated   |
| `/cohort-squad:sync`   | `sync-squads.md` (via packs)  | ✅ Migrated   |
| Analysis commands      | `brownfield-discovery.md`     | ✅ Migrated   |
| _(did not exist)_      | `greenfield-fullstack.md`     | ✅ **NEW**    |
| _(did not exist)_      | `greenfield-service.md`       | ✅ **NEW**    |
| _(did not exist)_      | `greenfield-ui.md`            | ✅ **NEW** ⭐ |
| _(did not exist)_      | `brownfield-fullstack.md`     | ✅ **NEW**    |
| _(did not exist)_      | `brownfield-service.md`       | ✅ **NEW**    |
| _(did not exist)_      | `brownfield-ui.md`            | ✅ **NEW**    |
| _(did not exist)_      | `epic-orchestration.md`       | ✅ **NEW**    |
| _(did not exist)_      | `qa-loop.md`                  | ✅ **NEW**    |
| _(did not exist)_      | `design-system-build.md`      | ✅ **NEW** ⭐ |
| _(did not exist)_      | `auto-worktree.md`            | ✅ **NEW**    |

> ⭐ Workflows with exclusive Antigravity capabilities (Stitch MCP, browser_subagent, generate_image)

---

## What Does NOT Exist in Antigravity (Limitations)

| Claude Resource            | Antigravity Status | Workaround                             |
| -------------------------- | ------------------ | -------------------------------------- |
| Automatic PreToolUse Hooks | ❌ N/A             | Instructional `governance.md`          |
| `/synapse:save` command    | ❌ N/A             | Manual save to `.synapse/sessions/`    |
| Checklists of Chiefs       | ⚠️ Not created     | Medium priority for future improvement |
