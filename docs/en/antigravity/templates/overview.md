# Templates — Complete Catalog

The **16 templates** in `.antigravity/templates/` are standardized model documents used by AIOS agents to generate consistent artifacts.

---

## How to Use Templates

Agents access templates via `view_file`:

```
@pm use the PRD template to start the document for product X
→ @pm view_file('.antigravity/templates/prd-tmpl.yaml')
→ fills the fields and saves in docs/
```

No template should be edited directly — they reside in `.antigravity/templates/` as an immutable reference.

---

## Template Catalog

### Product Templates

| Template                   | Size  | Primary Agent | Path                                              |
| -------------------------- | ----- | ------------- | ------------------------------------------------- |
| `prd-tmpl.yaml`            | 6.4KB | `@pm`         | `.antigravity/templates/prd-tmpl.yaml`            |
| `project-brief-tmpl.yaml`  | 7.1KB | `@pm`         | `.antigravity/templates/project-brief-tmpl.yaml`  |
| `brownfield-prd-tmpl.yaml` | 7.4KB | `@architect`  | `.antigravity/templates/brownfield-prd-tmpl.yaml` |
| `story-tmpl.yaml`          | 4.4KB | `@po`         | `.antigravity/templates/story-tmpl.yaml`          |

### Architecture Templates

| Template                           | Size   | Primary Agent       | Path                                                      |
| ---------------------------------- | ------ | ------------------- | --------------------------------------------------------- |
| `fullstack-architecture-tmpl.yaml` | 13.8KB | `@architect`        | `.antigravity/templates/fullstack-architecture-tmpl.yaml` |
| `front-end-architecture-tmpl.yaml` | 6.7KB  | `@architect`        | `.antigravity/templates/front-end-architecture-tmpl.yaml` |
| `front-end-spec-tmpl.yaml`         | 7.9KB  | `@ux-design-expert` | `.antigravity/templates/front-end-spec-tmpl.yaml`         |

### Database Templates

| Template                          | Size  | Primary Agent    | Path                                                     |
| --------------------------------- | ----- | ---------------- | -------------------------------------------------------- |
| `database-schema-request-full.md` | 9.7KB | `@data-engineer` | `.antigravity/templates/database-schema-request-full.md` |
| `database-schema-request-lite.md` | 5.6KB | `@data-engineer` | `.antigravity/templates/database-schema-request-lite.md` |

### Research and Analysis Templates

| Template                         | Size  | Primary Agent | Path                                                    |
| -------------------------------- | ----- | ------------- | ------------------------------------------------------- |
| `market-research-tmpl.yaml`      | 7.9KB | `@analyst`    | `.antigravity/templates/market-research-tmpl.yaml`      |
| `competitor-analysis-tmpl.yaml`  | 7.7KB | `@analyst`    | `.antigravity/templates/competitor-analysis-tmpl.yaml`  |
| `brainstorming-output-tmpl.yaml` | 5.1KB | `@analyst`    | `.antigravity/templates/brainstorming-output-tmpl.yaml` |

### Quality Templates

| Template            | Size  | Primary Agent | Path                                       |
| ------------------- | ----- | ------------- | ------------------------------------------ |
| `qa-gate-tmpl.yaml` | 2.4KB | `@qa`         | `.antigravity/templates/qa-gate-tmpl.yaml` |

### System Templates (Meta-templates)

| Template                 | Size  | Used By        | Path                                            |
| ------------------------ | ----- | -------------- | ----------------------------------------------- |
| `agent-template.yaml`    | 1.7KB | `@squad-chief` | `.antigravity/templates/agent-template.yaml`    |
| `workflow-template.yaml` | 3.1KB | `@squad-chief` | `.antigravity/templates/workflow-template.yaml` |
| `task-template.md`       | 1.5KB | `@squad-chief` | `.antigravity/templates/task-template.md`       |

---

## Template Details

### `prd-tmpl.yaml` — Product Requirements Document

**Used by:** `@pm`  
**When:** Starting product specification or a major feature

**Covered sections:**

- Executive Summary
- Problem Statement and User Pain Points
- Goals and Success Metrics
- User Personas
- Feature Requirements (MoSCoW)
- Non-functional Requirements
- Timeline and Milestones

---

### `story-tmpl.yaml` — Development Story

**Used by:** `@po`  
**When:** `@po *create-story`

**Covered sections:**

- Story ID and title
- As a [persona], I want [feature] so that [benefit]
- Acceptance Criteria (BDD: Given/When/Then)
- Definition of Done
- File List (change tracking)
- Progress checkboxes

---

### `fullstack-architecture-tmpl.yaml` — Full-Stack Architecture

**Used by:** `@architect`  
**When:** Before implementing in `supabase/functions/` (Architecture First)

**Covered sections:**

- System Overview and Context Diagram
- Technology Stack decisions (ADRs)
- Frontend Architecture
- Backend Architecture
- Database Schema overview
- Security Considerations
- Deployment Strategy

---

### `database-schema-request-full.md` vs `lite.md`

**Used by:** `@data-engineer`

| Version           | When to Use                               |
| ----------------- | ----------------------------------------- |
| `full.md` (9.7KB) | Complex new schema, multi-table, with RLS |
| `lite.md` (5.6KB) | Simple table or field addition            |

---

### `agent-template.yaml` — Agent Template

**Used by:** `@squad-chief`  
**When:** Creating a new agent in a squad

**Generated structure:**

```yaml
agent:
  name: ...
  id: ...
  title: ...
persona:
  role: ...
  style: ...
  voice_dna: []
commands: []
quality_gates: {}
```

---

### `workflow-template.yaml` — Workflow Template

**Used by:** `@squad-chief`  
**When:** Creating a new workflow for a squad

**Sections:**

- `description` — What it does
- `trigger` — When to execute
- `steps` — Numbered steps
- `output` — Generated artifacts

---

## Output Locations

After filling out a template, save the file in the correct path:

| Template                           | Output Path                           |
| ---------------------------------- | ------------------------------------- |
| `prd-tmpl.yaml`                    | `docs/architecture/{project}-prd.md`  |
| `story-tmpl.yaml`                  | `docs/stories/active/{id}-{title}.md` |
| `market-research-tmpl.yaml`        | `docs/research/{topic}.md`            |
| `fullstack-architecture-tmpl.yaml` | `docs/architecture/{feature}.md`      |
| `qa-gate-tmpl.yaml`                | `docs/qa/{story-id}-qa-report.md`     |

---

## Templates `README.md`

The `.antigravity/templates/README.md` file contains additional guidance and the complete index:

```
view_file('.antigravity/templates/README.md')
```
