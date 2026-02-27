# Chiefs — Specialized Orchestrators

The **8 Chiefs** are high-level agents specialized by business domain. Each chief orchestrates a set of sub-specialists using a progressive **Tier System**.

---

## What is a Chief?

A Chief is an agent that:

1. **Diagnoses** the request before acting (intelligent triage)
2. **Routes** it to the correct sub-specialist within the domain
3. **Oversees** the quality of the output using curated checklists

All Chiefs share the same philosophy: **diagnose before creating**, **route before executing**.

---

## Chiefs Table

| Chief                   | Squad             | Domain                   | Tier System                                                                     |
| ----------------------- | ----------------- | ------------------------ | ------------------------------------------------------------------------------- |
| `copy-chief`            | Copywriting       | Copy & persuasion        | Diagnosis (Hopkins) → T1 Foundations → T2 Techniques → T3 Masters + 30 Triggers |
| `cyber-chief`           | Cybersecurity     | Cybersecurity            | Urgency triage → Red Team → Blue Team → AppSec → Governance                     |
| `data-chief`            | Data Intelligence | Data & intelligence      | T0 Foundations → T1 Operational → T2 Communication                              |
| `design-chief`          | Design            | Product design           | Foundation → Masters → Specialists + Stitch MCP                                 |
| `legal-chief`           | Legal             | Law & compliance         | Diagnosis → Global Experts → Local Specialists                                  |
| `story-chief`           | Storytelling      | Narrative & storytelling | Structure + Genre → 12 Specialized Storytellers                                 |
| `traffic-masters-chief` | Paid Traffic      | Paid traffic & media     | Strategy → Platform Masters → Scaling                                           |
| `db-sage`               | Database          | Database                 | KISS Gate → Schema → RLS → Migrations → Performance                             |

---

## Detailed Profiles

### `copy-chief` — Chief of Copywriting

**File:** `.antigravity/agents/copy-chief.md`

Diagnosis based on **Claude Hopkins** principles — considers the product, the target audience, and the objective before writing any copy.

**Tier System:**

- **T1 — Foundations:** Headlines, leads, basic structure
- **T2 — Advanced Techniques:** Storytelling, social proof, urgency
- **T3 — Masters:** 30 Psychological triggers from Sugarman, Cialdini, Halbert

**How to activate:**

```
@copy-chief I need copy for a B2B SaaS landing page
```

---

### `cyber-chief` — Chief of Cybersecurity

**File:** `.antigravity/agents/cyber-chief.md`

**Urgency triage** as a first step — classifies severity before acting.

**Tier System:**

- **Red Team:** Offensive security, pen testing, ethical hacking
- **Blue Team:** Defensive, SIEM, incident response
- **AppSec:** Code review, vulnerabilities, OWASP
- **Governance:** Compliance, policies, frameworks (ISO 27001, NIST)

**How to activate:**

```
@cyber-chief we have a possible SQL injection on the login endpoint
```

---

### `data-chief` — Chief of Data Intelligence

**File:** `.antigravity/agents/data-chief.md`

**Tier System:**

- **T0 — Foundations:** Data modeling, warehouse design, governance
- **T1 — Operational:** ETL/ELT, pipelines, data engineering
- **T2 — Communication:** Dashboards, data storytelling, executive reporting

**How to activate:**

```
@data-chief analyze the conversion funnel for the last 90 days
```

---

### `design-chief` — Chief of Design

**File:** `.antigravity/agents/design-chief.md`

The only Chief with direct access to the **Stitch MCP** for prototyping.

**Tier System:**

- **Foundation:** Principles, color theory, typography
- **Masters:** Brad Frost (Atomic Design), Don Norman (UX), Dieter Rams
- **Specialists:** Motion design, design systems, accessibility

**Tools:**

```
mcp_stitch_*    → UI Prototyping
generate_image  → Visual assets and mockups
```

**How to activate:**

```
@design-chief review the visual consistency of our design system
```

---

### `legal-chief` — Chief of Legal

**File:** `.antigravity/agents/legal-chief.md`

Jurisdictional diagnosis before any guidance — identifies the legal context (US, UK, BR, EU, etc.).

**Tier System:**

- **Diagnosis:** Jurisdiction, issue type, urgency
- **Global Experts:** GDPR, international contracts, intellectual property
- **Local Specialists:** Local laws, labor laws, civil code

> ⚠️ **Warning:** Guidelines are informative. For real legal decisions, consult a qualified attorney.

**How to activate:**

```
@legal-chief review our terms of use for GDPR compliance
```

---

### `story-chief` — Chief of Storytelling

**File:** `.antigravity/agents/story-chief.md`

12 specialized storytellers organized by narrative structure and genre.

**Tier System:**

- **Structure:** Hero's Journey, 3 Act, Story Spine
- **Genre:** Brand storytelling, case studies, pitch narratives
- **12 Storytellers:** McKee, Pixar, Freytag, etc.

**How to activate:**

```
@story-chief create an origin narrative for our brand
```

---

### `traffic-masters-chief` — Chief of Paid Traffic

**File:** `.antigravity/agents/traffic-masters-chief.md`

**Tier System:**

- **Strategy:** Funnel, budget allocation, KPIs
- **Platform Masters:** Meta Ads, Google Ads, TikTok, LinkedIn
- **Scaling:** Creative testing, lookalike audiences, automation

**How to activate:**

```
@traffic-masters-chief optimize our Meta Ads campaigns
```

---

### `db-sage` — Database Sage

**File:** `.antigravity/agents/db-sage.md`

Chief specialized in databases, complementing `@data-engineer` with design and optimization expertise.

**KISS Gate:** Checks for simplicity over complexity.

**Tier System:**

- **Schema:** Relational design, normalization, indexes
- **RLS (Row-Level Security):** Supabase policies, row-level security
- **Migrations:** Safe strategy, rollbacks, zero-downtime
- **Performance:** EXPLAIN ANALYZE, query optimization, caching

**Golden Rule:**

```
Never CREATE TABLE directly. Always use:
supabase migration new {description}
```

**How to activate:**

```
@db-sage review the permissions schema and RLS policies
```
