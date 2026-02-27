# Workflow: Design System Build

**Native source file:** `.antigravity/workflows/design-system-build.md`

The **Design System Build & Quality** process is not just about CSS — it is the factory that codes the visual core of a company, ensuring that the Primary Button has exactly the same Hexadecimal, Border Radius, and Shadow across 500 screens with the heavy help of AntiGravity's native capabilities (Stitch MCP and Browser Subagent).

---

## 1. Usage Trigger (When to invoke)

Use this workflow to:

- Erect the visual factory floor of an Absolutely New project (Greenfield).
- Refactor legacies (Brownfield) transforming hardcoded values in CSS (`#ff0033`) into Organizational Tokens (`color.brand.primary`).
- Validate if the Front Team has not broken visual alignment on different screen sizes (Breakpoints).

## 2. The Operational Journey (Phases)

### Phase 1: Audit or Espionage (@ux & @analyst)

- In the existing rough (Legacy), `@ux` hunts corrupted values loose across the application trying to create dumpsters or reuse, extracting the real state.
- In the green rough (New), `@analyst` uses `search_web` hunting references and official guides from tech giants aligning with the client's business.

### Phase 2: The Token Sculptor (@ux & @brad-frost)

Visual foundations are born: `@ux` stipulates the key dictionary in `design-tokens.yaml` containing:

- Scalable typography (H1...H6).
- Set spacings (xs, sm, md, lg, xl).
- Utility colors.
  Being guided by the expert's primer `@brad-frost`. **AntiGravity Engine:** The vision model triggers `generate_image`, creating visual artboards of the palette for humans to see before CSS begins.

### Phase 3: The Magic of Stitch MCP (Guided Generator)

Here AntiGravity humiliates conventional AIs: Code is not written blindly.
The framework triggers **Stitch MCP** (`generate-ui-screens`) passing the design matrix defined above and the Google server AI merges the layout and draws buttons, modals, cards in the visual engine and saves to `docs/design-system/screens/`. You preview the entire platform on the screen as if it were an autonomous Webflow.

### Phase 4: Setting the Atomic Floor (@dev & @brad-frost)

The Atomic Design method is respected:

1. Code **Atoms** (Isolated inputs, texts).
2. Stitch **Molecules** (Input + Label in a Form Group).
3. Raise **Organisms** (Dense cards, entire Navbars).

### Phase 5: Photographic QA

Another exclusive AntiGravity function: `@qa` activates the `browser_subagent`. Instead of invisible mathematical Jest tests, the AI opens a Chromium on the local machine, physically clicks components and **Generates WebP Videos**, proving to the executive body that things exist with precision and testing colors in real Dark Mode and Light Mode.

## 3. Deliverables Matrix

- A Token repository (pure Yaml) acting as the source of truth and Visual Reference Screens via Stitch.
- Atomic Hierarchy implemented.
- QA with irrefutable proof (WebP) documenting that responsiveness is clean.
