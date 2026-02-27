# Workflow: Brownfield UI

**Native source file:** `.antigravity/workflows/brownfield-ui.md`

The **Brownfield UI** process treats visual alterations of a Client-Side code (Next/Svelte/Vue) with a scalpel, ensuring it doesn't lose the corporate harmony deployed months before. Absolute focus on intelligent reuse of Design Tokens and shielding from CSS Visual Regression.

---

## 1. Usage Trigger (When to invoke)

Use this workflow to:

- Fit new routes/pages into Dashboards and Apps using Lego blocks created from the Design System.
- Retouch animations and reactions of static components maintaining raw React/Vue Behavior.

## 2. The Operational Journey (Phases)

Front-End engineering does not act isolated from the brand's past, requiring the strictly cohesive UX-DEV-QA triad:

### Phase 1: Surgical Audit and the New Visual Spec (@ux)

`@ux` enters hunting in the codebase: Components with buttons similar to the desired feature and extracts all official Hexadecimals from `front-end-spec.md`. Unlike trying to randomly pull new heavy NPM libraries, he lists which blocks to reuse from the previous screen.
In case of a severe change (Rebranding), the **Antigravity MCP Stitch** is invoked, the AI connected in the web viewport, which takes pre-built screenshots to show management even before billing developer hours on the ticket.

### Phase 2: The Dev/Visual Pipeline (@sm / @dev)

When coding, there is a vital `grep` execution rule that the agent silently triggers: _"Where is this InputTextX component used today in the system?"_ — Before the DEV tries to refactor it.
Visual changes go down in the severe prioritization of the **Mobile First** format.

### Phase 3: Quality Containment Barrier (Visual Review)

Here resides an Antigravity superpower: Before `@qa` codes unit tests, the `browser_subagent` script is activated. It takes automated WebPs of the raw DOM render and analyzes to hunt blocks out of place due to clumsy CSS refactoring that leaked from the parent div, avoiding malformed deploys for the final human.

## 3. Deliverables Matrix

- Enriched interfaces strictly tied to corporate tokens.
- Visual regressions and Breakpoint blowouts (badly formatted Mobile screens) shielded by the Visual QA machine.
