# Skills — Skills System

The **7 skills** in `.antigravity/skills/` are specialized capabilities that any agent can invoke. Each skill resides in a subfolder with a mandatory `SKILL.md` file.

---

## What is a Skill?

A skill is a specific competency module. Unlike agents (which have an identity and persona), skills are **functional instructions** that enrich what an agent can do when called upon.

**Mandatory Format:**

```
.antigravity/skills/
└── {skill-name}/
    └── SKILL.md    ← YAML frontmatter + markdown instructions
```

**Frontmatter:**

```yaml
---
name: skill-name
description: 'When to use this skill and why.'
---
```

---

## Skills Catalog

| Skill              | Origin   | Description                                        |
| ------------------ | -------- | -------------------------------------------------- |
| `clone-mind`       | Migrated | DNA extraction and cloning of real experts         |
| `architect-first`  | Migrated | Architectural check before implementation          |
| `enhance-workflow` | Migrated | Improve existing workflows                         |
| `checklist-runner` | Migrated | Execute structured quality checklists              |
| `governance`       | **NEW**  | AIOS Governance Pipeline: blocks ops without rules |
| `squad`            | Migrated | Squad creation and management                      |
| `synapse`          | **NEW**  | Integration with the `.synapse/` context engine    |

---

## Skill Profiles

### `clone-mind`

**Location:** `.antigravity/skills/clone-mind/SKILL.md`

DNA extraction from real experts to create mind clones.

**When to use:**

- When creating an agent based on a real person
- When you need to verify the fidelity of an existing mind clone
- To extract thought patterns from documented sources

**Pipeline:**

```
*collect-sources      → Collect books, talks, posts
*extract-voice-dna    → Communication patterns
*extract-thinking-dna → Frameworks and heuristics
```

**Output:** `mind_dna_complete.yaml` with voice DNA + thinking DNA.

---

### `architect-first`

**Location:** `.antigravity/skills/architect-first/SKILL.md`

Mandatory architectural check before touching infrastructure code.

**When to use:**

- Before implementing in `supabase/functions/`
- Before creating database migrations
- When there is no architecture documentation for a feature

**Flow:**

```
1. Check docs/architecture/{feature}.md
2. If it doesn't exist: create it first, get approval
3. Then implement the code
```

Implements the **Architecture First** constitutional rule of governance.

---

### `enhance-workflow`

**Location:** `.antigravity/skills/enhance-workflow/SKILL.md`

Optimization and improvement of existing workflows.

**When to use:**

- When reviewing a workflow that is causing friction
- To add quality gates to an existing process
- When handoffs between agents are breaking

**Typical analysis:**

```
→ Map current steps
→ Identify failure points
→ Propose improvements
→ Validate with @pedro-valerio (if available)
```

---

### `checklist-runner`

**Location:** `.antigravity/skills/checklist-runner/SKILL.md`

Structured execution of quality checklists.

**When to use:**

- QA gates before push
- Agent structure validation (SC_AGT_001, SC_AGT_002)
- Reviews of PRDs, stories, and documentation

**Execution format:**

```
[✅] Item 1 — PASSED
[✅] Item 2 — PASSED
[❌] Item 3 — FAILED: {reason}
→ Result: X/Y (threshold: Y/Y)
```

---

### `squad`

**Location:** `.antigravity/skills/squad/SKILL.md`

Complete squad creation and management. In Antigravit, this skill delegates heavy orchestration to the **`squads/squad-creator/`** pack.

**When to use:**

- Create a new squad for a specific domain
- Add an agent to an existing squad
- Generate the squad's directory structure

**Generated structure:**

```
squads/{squad-name}/
├── agents/          ← Squad agents
├── tasks/           ← Specialized tasks
├── workflows/       ← Squad workflows
├── data/            ← Data and registry
│   └── minds/       ← Expert DNA
└── README.md        ← Squad documentation
```

---

### `synapse` ← NEW (exclusive to Antigravit)

**Location:** `.antigravity/skills/synapse/SKILL.md`

Management of the **SYNAPSE Context Engine** — the unified context engine of AIOS.

**When to use:**

- To understand the current state of the context engine
- When configuring new rule domains
- To debug context injection issues
- When creating new star-commands (`*`)

**SYNAPSE is:**

> **Synkra Adaptive Processing & State Engine** — organizes rules by domain in `.synapse/` and loads them by context (8 layers: L0 Constitution → L7 Star-Commands).

**Skill commands:**

| Command            | What it does                |
| ------------------ | --------------------------- |
| `*synapse status`  | Current state of the engine |
| `*synapse domains` | List registered domains     |
| `*synapse debug`   | Detailed debug info         |
| `*synapse create`  | Create a new domain         |
| `*synapse add`     | Add a rule to a domain      |
| `*synapse toggle`  | Enable/Disable a domain     |

**8-Layer Pipeline:**

| Layer | Name          | Description                  |
| ----- | ------------- | ---------------------------- |
| L0    | Constitution  | Immutable foundational rules |
| L1    | Global        | Global project context       |
| L2    | Agent-Scoped  | Agent-specific rules         |
| L3    | Workflow      | Active workflow context      |
| L4    | Task          | Current task context         |
| L5    | Squad         | Active squad context         |
| L6    | Session       | Session state                |
| L7    | Star-Commands | Special `*` commands         |

**Context Brackets** (adaptive injection volume):

| Bracket  | Context Usage | Active Layers |
| -------- | ------------- | ------------- |
| FRESH    | < 30%         | All (L0-L7)   |
| MODERATE | 30-60%        | L0-L5         |
| DEPLETED | 60-80%        | L0-L3         |
| CRITICAL | > 80%         | L0 only       |

---

## How to Invoke a Skill

Skills are invoked when an agent needs a specific capability. The agent reads the `SKILL.md` file of the skill before executing:

```
"Use the clone-mind skill to extract Seth Godin's DNA"
→ Agent reads .antigravity/skills/clone-mind/SKILL.md
→ Follows the documented instructions
```

---

## Related Documentation

- [SYNAPSE skill (source code)](../../../../.antigravity/skills/synapse/SKILL.md)
- [Workflows](../workflows/overview.md)
- [Mind Clones](../agents/mind-clones.md)
