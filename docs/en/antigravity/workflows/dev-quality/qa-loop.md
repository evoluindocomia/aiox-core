# Workflow: QA Loop

**Native source file:** `.antigravity/workflows/qa-loop.md`

The **QA Loop** is Antigravity's iterative hammer for Software Quality. It is the hellish back-and-forth circle between the Quality Bot (`@qa`) and the Developer Bot (`@dev`). It is invoked not for the first friendly review, but **when the implementation breaks and needs multiple automatic correction cycles**.

---

## 1. Usage Trigger (When to invoke)

Use this workflow exclusively when:

- `@qa` gives a big red `REJECT` on a delivered Story and returns a list of bugs.
- To turn on automation without needing to intercede humanly every time asking the dev to fix the PR.

## 2. The Loop Engineering (Phases)

### Phase 1: Persistence Tracking

To avoid "Circular Hallucination" that occurs in loose basic LLMs, the state-machine file in `qa/loop-status.json` is immediately created. The system notes that it is on Iteration N of a maximum of 5 allowed.

### Phase 2: The Code Tribunal (@qa)

`@qa` sets down the Acceptance Criteria rules and strictly checks the found issues.
It processes the status with limited outputs:

- `APPROVE`: Gives the final blessing and ends the loop.
- `REJECT`: Thickens the infraction list and sends it to the operating table.
- `BLOCKED`: Accuses an unresolvable technical block at the moment and locks everything.

### Phase 3: The Cold Surgery (@dev)

Upon receiving the `REJECT`, the Dev doesn't redo the task; it **only** processes the QA's fix list. The central framework rule blocks the AI's intention to inflate the code with improvements that were not requested on top of the repair scope.

### Phase 4: The Limiting "If"

At the end of the repair, N is incremented. If the intelligences get stuck in this back-and-forth fight and pass `Iteration 5`, the QA Bot no longer returns it to the Dev: it locks (Trigger: `max_iterations_reached`) and cries for Human Intervention via a formal notice with the summary of the technical fight in `escalation-report.md`.

## 3. Deliverables Matrix

- Isolated fixes documented in the status file validating persistence of why the code was breaking at iteration N.
- Final code sanctioned ONLY after a sweep by the @qa Bot.
- Or: Hard stop point proving in a report why the bots couldn't resolve the ticket's instruction.
