# Workflow: Greenfield Fullstack

**Native source file:** `.antigravity/workflows/greenfield-fullstack.md`

The **Greenfield Fullstack** process is Antigravity's end-to-end production track, designed to start an entire ecosystem from scratch, covering both backend and frontend simultaneously.

---

## 1. Usage Trigger (When to invoke)

Use this workflow for:

- New MVPs and Web/SaaS applications started from scratch.
- Projects where visual and logical layers will coexist.
- When there is no previous code. If there is already a repository with code, use `brownfield-fullstack`.

## 2. The Operational Journey (Phases)

Antigravity prescribes 4 strictly chronological major phases for this cycle:

### Phase 0: Environment Bootstrap

The raw repository configuration commanded by `@devops` happens here.

- He checks via `.aios/environment-report.json` if CLIs and Git are running.
- Configures the GitHub repository and prepares the folder.

### Phase 1: Chain Discovery and Planning

Not a single line of React/Python code is written here. Intelligence is passed from hand to hand:

1. `@analyst` writes the **Project Brief** (Vision and Market Pain).
2. `@pm` consolidates this into the **PRD (Product Requirements Document)**.
3. `@ux` extracts the **Front-End Spec** from the PRD (being able to generate visual drafts in Stitch MCP).
4. `@architect` takes over and nails down the **Fullstack Architecture**.
5. Finally, `@po` acts as an Auditor (Quality Gate), reading all generated files against the `po-master-checklist`. If it fails, the pipeline rolls back.

### Phase 2: Sharding (Tactical Fragmentation)

With everything approved, `@po` fragments (shards) the long PRD into guidelines consumable by the IDE (tech-stack, coding-standards, and the source-tree hierarchy), preparing the practical ground.

### Phase 3: The Development Cycle (Looping)

The heart of engineering, guided Story by Story (Ticket):

- `@sm` pulls the requirements into the sprint.
- `@dev` takes the ticket in YOLO or Interactive mode, spitting out code.
- `@qa` wakes up to run linters, test-coverage, and TypeScript typing. If it breaks, the code does not commit and returns to `@dev`.
- Approved locally, `@devops` finalizes the commit in the repository.

## 3. Deliverables Matrix

Upon finishing this workflow, the system panels should contain:

- Provisioned GitHub/Node environment.
- Core documents initialed: Brief, PRD, UX Spec, and Architecture.
- All code tested, linked via JEST/Typescript without severe warnings, and Committed to remote pipelines.
