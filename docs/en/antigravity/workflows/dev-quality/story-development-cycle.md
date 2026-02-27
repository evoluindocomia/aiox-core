# Workflow: Story Development Cycle (SDC)

**Native source file:** `.antigravity/workflows/story-development-cycle.md`

The **Story Development Cycle (SDC)** is the highest turnover workflow within an Antigravity studio. It focuses fundamentally on the isolated routine of a strict programming block aimed at the merciless fulfillment of the documented obligations (Acceptance Criteria) of an already validated Ticket.

---

## 1. Usage Trigger (When to invoke)

Use this workflow exclusively when:

- Green light has been signaled for the Sprint.
- You want to process a single _Story_ whose document rests comfortably in the `docs/stories/` directory under the `Ready` status tag.
- **MUST NOT** be used if the general architecture changes; this deals only with brick by brick.

## 2. The Operational Journey (Phases)

### Phase 1: Cold Pre-Read

Hard initial check of premises via local prompt: Does the Story exist? Are the evaluative points and Criteria formatted? If not, it falls out of the flow prematurely.

### Phase 2: Seismic Jolts Test (@architect)

The `@architect` is temporarily triggered (`analyze-impact`) with the mission of a microscopic sweep: Reads what the ticket claims and deduces "which `src/` files break and will bleed trying to do this" based on `impact-analysis.md`. A lock closes if he identifies collapses in the current foundations.

### Phase 3: The Raw Implementation Operation (@dev / @ui-builder)

The heavy lifting starts following the natural bifurcation of the task:

- Being a routine logic and generic systemic: Delegated to the root dev (`@dev`).
- Having an immense appeal towards front-end governed by `ui-guidelines`: Unavoidable redirection to the visual architect (`@ui-builder`).
  In this sub-loop, the system forces agents to force local linting and atomic code typing (no pushing castigated TypeScript).

### Phase 4: Definitive Audit (@qa)

Code done, iterative verification is awakened (`review-story`). The `@qa` bot crosses the codes VS the Acceptance. Rejecting, he doesn't sweep it under the rug and demands focused surgery, returning to DEV to arrest the Criteria gaps via iterations flow (`qa-loop`). If severely punctured, he screams for Human Intervention (Escalation).

### Phase 5: Launch Shelf (@devops)

Passed smooth by the court (QA Approved), `@devops` commits associating strictly linked messages under _Conventional Commits_ and stamps the metamorphosis of the Story to _Done_. NO PUSH IS EFFECTUATED; the mature delivery waits resting locally for macro repo approvals (`push`).

## 3. Deliverables Matrix

- Formatted code without severe typing/linter warnings.
- Impact Report of modifications for base history.
- Ticket formally set as _Done_ on the dead panel and saved isolated commits.
