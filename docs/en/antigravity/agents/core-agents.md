# Core AIOS Agents

The 11 fundamental agents of Synkra AIOS, all available in any project with the `.antigravity/` environment.

---

## Quick Reference Table

| Agent                   | Persona            | Scope                           | Key Tools                                     |
| ----------------------- | ------------------ | ------------------------------- | --------------------------------------------- |
| `@dev`                  | Dex                | Code Implementation             | `write_to_file`, `run_command`, `grep_search` |
| `@qa`                   | Quinn              | Quality & Testing               | `run_command` (test), `find_by_name`          |
| `@architect`            | Aria               | Architecture & Design           | `search_web`, `read_url_content`, `view_file` |
| `@pm`                   | Kai                | Product Management              | `view_file` (templates), `write_to_file`      |
| `@po`                   | Nova               | Product Owner, Stories/Epics    | `view_file` (templates), `write_to_file`      |
| `@sm`                   | River              | Scrum Master                    | `view_file`, model: `gemini-2.0-flash`        |
| `@analyst`              | Zara               | Research & Intelligence         | `search_web`, `read_url_content`              |
| `@data-engineer`        | Dara               | Database Design                 | `run_command` (supabase), SQL governance      |
| `@ux`                   | Uma                | UX/UI Design                    | `generate_image`, `mcp_stitch_*`              |
| `@devops`               | Gage               | CI/CD, Git push (**EXCLUSIVE**) | `run_command` (git), `.github/`               |
| `@brad-frost`           | Brad Frost         | Design System & Atomic Design   | `mcp_stitch_*`, `generate_image`              |
| `@squad-chief`          | Squad Architect 🎨 | Squad & Mind Creation           | `search_web`, `write_to_file`                 |
| `@research-specialists` | Research Team 🔍   | Deep Research & Frameworks      | `search_web`, `read_url_content`              |

---

## Detailed Profiles

### `@dev` — Dex (Developer)

**File:** `.antigravity/agents/aios-dev.md`

Dex is responsible for all code implementation. He follows the **REUSE > ADAPT > CREATE** principle: always looking for existing code before creating new ones.

**Scope:**

- `packages/`, `.aios-core/core/`, `bin/`
- Feature implementation from validated Stories.
- Refactoring and maintenance.

---

### `@qa` — Quinn (QA)

**File:** `.antigravity/agents/aios-qa.md`

Quinn handles quality gates. She executes tests and validates acceptance criteria before any push.

**Quality Gates:**

```bash
npm run lint        # ESLint
npm run typecheck   # TypeScript
npm test            # Jest
```

---

### `@squad-chief` — Squad Architect 🎨

**File:** `.antigravity/agents/squad-chief.md`

The orchestrator of the **MINDS FIRST** philosophy. He creates complete squads with mind clones of real-world experts.

**Squad Creation Flow:**

1. Domesticates the domain request.
2. **IMMEDIATELY** researches elite minds (no questions asked first).
3. Presents curated experts with documented frameworks.
4. Extracts DNA (`*clone-mind`) and creates agents.

**Delegated Subagents (Packs):**

- `@oalanicolas` — Mind Cloning Architect (DNA extraction)
- `@pedro-valerio` — Process Absolutist (workflow validation)
- `@research-specialists` — Research Specialists (Consolidated team)

> Implementation location: `squads/squad-creator/agents/`

---

### `@ux` — Uma (UX/UI)

**File:** `.antigravity/agents/aios-ux.md`

Uma is highly enriched in the Antigravity migration, featuring native access to image generation and professional UI design tools via Stitch MCP.

**Exclusive Tools:**

- `generate_image` (Assets/Mockups)
- `mcp_stitch_*` (Professional Screen Generation)

**Works with:** `@brad-frost` for Atomic Design System workflows.

---

### `@brad-frost` — Brad Frost (Design System)

**File:** `.antigravity/agents/brad-frost.md`

Mind clone of Brad Frost — creator of Atomic Design methodology. Used in `design-system-build.md` workflow.

**Exclusive Tools:**

- `mcp_stitch_*` (UI design and screen variants)
- `generate_image` (Visual assets)
