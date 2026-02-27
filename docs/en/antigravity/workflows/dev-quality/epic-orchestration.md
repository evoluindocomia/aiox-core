# Workflow: Epic Orchestration

**Native source file:** `.antigravity/workflows/epic-orchestration.md`

The **Epic Orchestration** process coordinates the parallelism and lifetime health of an entire Epic. It works as a traffic controller when there are 5+ Stories that need to be built with cross-dependencies (e.g., Story A's database needs to exist before Story B's Screen B can start).

---

## 1. Usage Trigger (When to invoke)

Use this workflow to:

- Start massive operation after finishing the `spec-pipeline` workflow (when the backlog is clean and documented).
- Control the mathematical sequence of what developers/agents will pick up first.

## 2. The Operational Journey (Phases)

### Phase 1: Tactical Planning (@po)

No code is written until `@po` creates the dependency matrix inside `docs/epics/{epic-slug}-execution-plan.md`. It maps if the Authentication system must necessarily finish so the Statement Page can begin.

### Phase 2: The Waves Concept (Execution Waves)

Stories are not thrown into a single cauldron. They are sliced into **Waves**:

- **Wave 1:** Root stories, without parents (e.g., JWT Setup).
- **Wave 2:** Stories that claim existence from Wave 1.

### Phase 3: Construction Looping

For each Story inside the current Wave, the `story-development-cycle` Workflow is invoked independently for the AIs to code under the scrutiny of the `qa-loop`.
When Wave 1 strikes the hammer (100% Done) and is committed, the agents open the floodgates for Wave 2.

### Phase 4: Progress Bureaucracy

The consolidated status of the epic runs natively in memory at `.aios/epic-status-{epic-slug}.json`. The `@sm` supervises if agents choked on a Story Blocked for more than 2 days and demands intervention in the communication channel (escalation).

### Phase 5: Final Closure (@po & @devops)

The `@po` validates all Acceptance Criteria of the Epic's sum. If approved, `@devops` pushes to remote and generates a Release tag.

## 3. Deliverables Matrix

- Dependency Mapping Report shielding dangerous initial couplings.
- Epic linearly built through _Waves_ grouping without branch delay.
- Tagged release nailed in Github/Gitlab.
