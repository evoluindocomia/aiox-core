# Workflow: Greenfield UI

**Native source file:** `.antigravity/workflows/greenfield-ui.md`

The **Greenfield UI** process is a visual construction track focused 100% on the human user. It's the production line for Landing Pages, decoupled Dashboards, and complex interactivity systems without depending on complex business logic integrations in the Backend in its initial setup.

> **Important:** This workflow triggers the true exclusive power of the _Antigravity MCP (Stitch)_ model with images, direct generation of interactive wireframes from spoken language to code.

---

## 1. Usage Trigger (When to invoke)

Use this workflow exclusively for:

- SPAs in Next/React consuming APIs that are already live or mocked.
- Heavy construction of Token-oriented Design-Systems.
- Front-heavy MVPs (Heavy focus on retention via visually rich Interface).

## 2. The Operational Journey (Phases)

### Phase 1: Research, Design Spec, and the Magic Interface

The orchestration escapes the data engineer's bureaucracy and enters the era of pure atomic design:

1. `@ux` Starts with deep User Research of personas and pain points.
2. `@pm` formats this into the PRD focusing on journeys and navigation flows.
3. Back to `@ux`, who instigates the base **Front-End Spec**: Corporate colors, fonts, global CSS breakpoints, and essential brand components.
4. **Magic:** `@ux` initiates the typing bypass and pulls the Stitch lever (`generate-ui-screens` with `mcp_stitch_generate_screen_from_text`), generating buttons and skeletal forms in _visual runtime_.
5. `@architect` takes on the purely Front architecture (How Pinia/Redux will operate the injected data in memory).
6. `@po` inspects the files under the checklist.

### Phase 2: Atomic System Bootstrap (Atomic Design)

If necessary, `@brad-frost` extracts all the specification from the previous step's files and initiates the repository nailing the UI component library in isolation. He creates atoms and consolidates native color tokens before the dev gets hurt with generic CSS.

### Phase 3: Component Refinement (The Story Loop)

- `@sm` creates the story focused purely on responsiveness and design binding.
- `@dev` enters developing the refined CSS or calling again the raw screen extracted by `@ux`.
- Surprisingly, `@qa` triggers an automatic audit of **APCA Accessibility** and native contrast via the `browser_subagent` engine, which takes WebP prints and videos for blind scanning by aesthetic visual error detection algorithms.

## 3. Deliverables Matrix

- Initialized UI environment, often with isolated design Tokens folders ready and shielded to prevent Devs from mistyping HEX Colors in future pull requests.
- Accessible Features approved under native WCAG in each Sprint evaluated by the visual Q&A bot.
