# Mind Clones — Design Squad

The **5 Mind Clones** are agents built via **DNA extraction** from real-world design and system experts. They are part of the **Design Squad** and act as subagents to `@squad-chief`.

---

## What is a Mind Clone?

A Mind Clone is an agent that replicates the **thinking, communication, and working patterns** of a real expert. Unlike generic bots, each Mind Clone has:

- **Voice DNA** — 5 signature phrases capturing their communication style
- **Thinking DNA** — Real frameworks and heuristics from the expert
- **Verifiable source** — Books, talks, documented posts

---

## The 5 Mind Clones in the Design Squad

| Agent           | Real Expert   | Specialty                               | File                                   |
| --------------- | ------------- | --------------------------------------- | -------------------------------------- |
| `brad-frost`    | Brad Frost    | Atomic Design, design systems           | `.antigravity/agents/brad-frost.md`    |
| `dan-mall`      | Dan Mall      | Design system adoption, business ROI    | `.antigravity/agents/dan-mall.md`      |
| `dave-malouf`   | Dave Malouf   | DesignOps, organizational maturity      | `.antigravity/agents/dave-malouf.md`   |
| `oalanicolas`   | Oala Nicolas  | Mind Cloning Architect (DNA extraction) | `.antigravity/agents/oalanicolas.md`   |
| `pedro-valerio` | Pedro Valério | Process Absolutist (workflow audit)     | `.antigravity/agents/pedro-valerio.md` |

---

## Detailed Profiles

### `brad-frost` — Atomic Design Expert

**File:** `.antigravity/agents/brad-frost.md`

Clone of **Brad Frost**, creator of Atomic Design. Expert in treating design systems as products.

**Domains of expertise:**

- Atomic Design (Atoms, Molecules, Organisms, Templates, Pages)
- Design system governance and contribution
- Pattern Lab and design system tooling
- Integration with **Stitch MCP** for prototypes

**Voice DNA:**

- _"Design systems are products serving products."_
- _"Start with the atomic pieces, not the pages."_

**When to activate:**

```
@brad-frost review the architecture of our design system
@brad-frost create an atomic design guide for the project
```

---

### `dan-mall` — Design System Business Strategist

**File:** `.antigravity/agents/dan-mall.md`

Clone of **Dan Mall**, an expert in design system adoption and ROI.

**Domains of expertise:**

- Convincing stakeholders (business cases for design systems)
- Adoption metrics and tangible ROI
- Super Friendly collaboration model (designer-developer)
- Strategy for design systems as a business product

**Voice DNA:**

- _"Design systems should be boring so products can be exciting."_
- _"Adoption is the only metric that matters."_

**When to activate:**

```
@dan-mall how do we convince our C-suite to invest in a design system
```

---

### `dave-malouf` — DesignOps Leader

**File:** `.antigravity/agents/dave-malouf.md`

Clone of **Dave Malouf**, a pioneer in DesignOps.

**Domains of expertise:**

- Organizational design maturity
- Design operations metrics
- Rhythms of work and team workflows
- Enabling and growing designers

**Voice DNA:**

- _"DesignOps is about the business of design."_
- _"Measure what matters to the design team's value."_

**When to activate:**

```
@dave-malouf evaluate the operational maturity of our design team
```

---

### `oalanicolas` — Mind Cloning Architect

**File:** `.antigravity/agents/oalanicolas.md`

The **meta-expert**: specialized in creating other mind clones. A direct subagent of `@squad-chief`.

**Responsibilities:**

- Curate sources for DNA extraction
- Extract Voice DNA (communication style)
- Extract Thinking DNA (frameworks and heuristics)
- Generate `mind_dna_complete.yaml`
- Validate clone fidelity

**Cloning Pipeline:**

```
*collect-sources      → Curate sources (books, talks, posts)
*extract-voice-dna    → Extract communication patterns
*extract-thinking-dna → Extract frameworks and heuristics
*create-agent         → Generate an agent using the extracted DNA
```

**When activated automatically:**

- When `@squad-chief` detects a request to create an agent based on a real person
- Whenever the triggers "clone mind", "extract DNA", or "fidelity" appear

---

### `pedro-valerio` — Process Absolutist

**File:** `.antigravity/agents/pedro-valerio.md`

Expert in workflow design and auditing. Subagent of `@squad-chief`.

**Domains of expertise:**

- Process design and veto conditions
- Checkpoint validation in workflows
- Handoff audits between agents
- Process consistency validation

**Voice DNA:**

- _"Process is not bureaucracy — it's the elimination of variation."_
- _"Every handoff is a potential point of failure."_

**When to activate:**

- Trigger words: `workflow design`, `process validation`, `veto conditions`, `checkpoint`, `handoff issues`

---

## Mind Clone Creation Pipeline

To create a new mind clone using `@squad-chief`:

```
1. @squad-chief *clone-mind "Expert Name"
2. → Routes to @oalanicolas
3. oalanicolas *collect-sources     → List of verifiable sources
4. oalanicolas *extract-voice-dna   → Voice DNA (5+ signature phrases)
5. oalanicolas *extract-thinking-dna → Thinking DNA (frameworks)
6. oalanicolas generates mind_dna_complete.yaml
7. @squad-chief *create-agent using mind_dna_complete.yaml
```

---

## Mind Clone Governance

Before creating any human-based agent, governance dictates:

```
squads/{pack}/data/minds/{agent_id}_dna.yaml  ← DNA must exist
```

If the DNA does not exist → **BLOCKED**. The extraction pipeline must run first.

> Formal rule: `.antigravity/rules/governance.md` — under "Before CREATING a file in squads/"

---

## Mind Clone Quality (Quality Gate SC_AGT_002)

| Check             | Criterion                                         |
| ----------------- | ------------------------------------------------- |
| DNA Extracted     | `mind_dna_complete.yaml` exists prior to creation |
| Voice DNA         | Accurately captures a verifiable style            |
| Thinking DNA      | Captures documented, real frameworks              |
| Verifiable Source | Book, talk, or post with clear referencing        |

**Threshold:** 4/4 — all checks are mandatory.
