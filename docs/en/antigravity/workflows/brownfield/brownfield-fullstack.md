# Workflow: Brownfield Fullstack

**Native source file:** `.antigravity/workflows/brownfield-fullstack.md`

The **Brownfield Fullstack** process governs how to build new features or deeply refactor legacy systems without breaking everything in production.

---

## 1. Usage Trigger (When to invoke)

Use this workflow to:

- Add massive features (Backend and Frontend) to a project that already generates revenue or has active users.
- When your PRD crosses boundaries and hits N layers of an old monolithic code.

> **Golden Rule:** Only invoke this IF `brownfield-discovery` was run at some point in the last few months and the architecture (`.aios/gotchas.json`) is fresh.

## 2. The Operational Journey (Phases)

### Phase 1: Context and Respectful Planning

1. `@pm` raises the **Brownfield PRD** focused on the Current State (As-Is) before the Future State (To-Be).
2. The `@architect` submits this PRD to a stress test against the `docs/architecture/` folder. He needs to validate if the proposed feature explodes current standards. If approved, he dictates the integration strategy.

### Phase 2: Sliced Spec (DB & Visual)

- If the interface changes, `@ux` adapts the wireframe trying to **reuse the base system** without forcing Tailwind injection into a strictly Bootstrap project.
- If the DB changes, `@data-engineer` traces a blind migration (which never involves DROP commands on active client data), running a stress KISS-gate.

### Phase 3: Epics and Stories

The construction slices go to the `@sm`'s panel.

### Phase 4: The Heart of Development (The R.A.C Law)

During the executions of the Interactive `@dev`, the Legacy Code Law (**REUSE > ADAPT > CREATE**) is natively injected:

- REUSE: Does it exist in legacy? Pull it and don't create new.
- ADAPT: Is it 80% similar to the legacy one? Adapt without breaking current panels.
- CREATE: Totally new? Isolate in a new cohesive folder and write the "Why".
  Upon finishing the code, `@qa` tests iteratively before the final commit.

## 3. Deliverables Matrix

- New Epic modularly fitted into the monolithic block without causing Visual or Rest service Regression.
- Packaged commits ensuring that gotchas from `.aios/gotchas.json` were avoided.
