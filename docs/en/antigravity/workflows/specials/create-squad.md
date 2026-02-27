# Workflow: Create Squad

**Native source file:** `.antigravity/workflows/create-squad.md`

The **Create Squad** is the Holy Grail of the AntiGravity ecosystem. It governs how AIs create new AIs using a non-negotiable ethical principle: **MINDS FIRST**. Agents must not be generic hallucinations ("act like an SEO expert"), but real extractions of intellectual and behavioral DNA from biological authorities that exist in the world.

---

## 1. Usage Trigger (When to invoke)

Use this workflow exclusively when:

- It is required to hire hyper-niched specialists (e.g., A SaaS taxation lawyer in Brazil, an Unreal Engine 5 architect).
- The global file `squad-registry.yaml` indicates there is no coverage for the requested domain.

## 2. The Operational Journey (Phases)

### Phase 1: The Investigation of the Aether (@squad-chief)

Before writing a single prompt for the new agent, `@squad-chief` activates `search_web`. He doesn't search "how to do marketing", he searches "who are the top 3 living direct marketing biological experts in the world". He runs 3 to 5 iterations playing devil's advocate to prove the mind is not a fraud or generic. And then displays a list to the user. **Human approval is mandatory here.**

### Phase 2: Genetic Extraction (Skill: Clone Mind)

With the chosen biological expert (e.g., Dan Mall for Design Systems), the `clone-mind` skill scrapes the internet focusing on:

- **Voice DNA:** How does he write? Does he use jargon? Is he sarcastic or professorial?
- **Thinking DNA:** Which logical matrices and mental frameworks (`IF/THEN`) the biological person applies to judge a problem.
  The result of this dense grinding generates the file `mind_dna_complete.yaml`.

### Phase 3: Mechanical Incarnation (Physical Creation)

With the DNA injected into the mental syringe, the files are physically created:

1. Squad Folder in `squads/{squad-slug}/`
2. Agent markdown file `agents/{agent}.md` with the Scope, Heuristics injected Inline (min 5 IF/THEN rules) and core methodology.
3. Ratio nailed at 70% of the logic being about _how to work_ and 30% of the logic about _the avatar's profile_.

### Phase 4: The Stamp of Existence

The final bureaucracy dictates updating the squad's `README.md` teaching how to trigger them, the setup of `squad-config.yaml` mapping who the new hires are, and the global pointing in `squad-registry.yaml`.

## 3. Deliverables Matrix

- Validation report proving the methodological veracity of the inspiring Biological Mind.
- Extracted and static DNA file kept under lock and key.
- Operational agent ready to receive orders from the native Chief, carrying a self-contained prompt.
