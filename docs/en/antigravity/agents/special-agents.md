# Special Agents

The **4 Special Agents** have unique capabilities that go beyond the conventional functions of the AIOS development cycle.

---

## Overview

| Agent                   | Main Capability                       | Exclusive Tools                        |
| ----------------------- | ------------------------------------- | -------------------------------------- |
| `design-system`         | Complete design system (36 missions)  | `generate_image`, `mcp_stitch_*`       |
| `tools-orchestrator`    | Creating & reviewing frameworks/tools | `search_web`, `run_command`            |
| `nano-banana-generator` | Visual assets at scale                | `generate_image`, `mcp_stitch_*`       |
| `sop-extractor`         | SOP extraction from any media         | `read_url_content`, `browser_subagent` |

---

## `design-system` — Design System Specialist

**File:** `.antigravity/agents/design-system.md`

Based entirely on **Brad Frost**, this agent executes 36 different missions throughout a design system's lifecycle.

**Main flow:**

```
audit → tokenize → build → document → govern
```

**36 Missions organized by phases:**

| Phase        | Missions                                                        |
| ------------ | --------------------------------------------------------------- |
| **Audit**    | Existing visual inventory, spot inconsistencies, map components |
| **Tokenize** | Create design tokens, define color systems, typography, spacing |
| **Build**    | Build Atomic components, create a pattern library               |
| **Document** | Storybook, usage guidelines, do's & don'ts                      |
| **Govern**   | Contribution models, review processes, versioning               |

**Tools:**

```
generate_image      → Visual component examples
mcp_stitch_*        → Interactive prototyping
```

**When to activate:**

```
@design-system run a full audit of our design system
@design-system tokenize our current color system
```

---

## `tools-orchestrator` — Tools & Frameworks Orchestrator

**File:** `.antigravity/agents/tools-orchestrator.md`

An expert in **creating, reviewing, and extracting** tool frameworks. Operates across 7 domains.

**7 Domains:**

1. **Development Tools** — CLI, developer tooling, build systems
2. **AI/ML Tools** — AI frameworks, pipelines, models
3. **Data Tools** — ETL, warehouses, data visualization
4. **DevOps Tools** — CI/CD, monitoring, infrastructure
5. **Design Tools** — Design systems, prototyping, handoffs
6. **Documentation Tools** — Wikis, docs-as-code, knowledge bases
7. **Collaboration Tools** — Workflows, async work, team processes

**Capabilities:**

- **Review:** Evaluate existing tools (fit, gaps, alternatives)
- **Create:** Propose customized frameworks
- **Extract:** Extract patterns from popular frameworks

**When to activate:**

```
@tools-orchestrator evaluate whether we should use Turborepo or Nx for our monorepo
@tools-orchestrator create an evaluation framework for AI tools
```

---

## `nano-banana-generator` — Asset Visual Generator

**File:** `.antigravity/agents/nano-banana-generator.md`

An agent specialized in **generating visual assets at scale**. Combines `generate_image` with Stitch MCP for serial production.

**Use cases:**

- Product icons and illustrations
- Screen templates and widget mockups
- Marketing assets (banners, thumbnails, social media)
- Variations for brand identity
- Rapid visual prototypes

**Workflow:**

```
1. Receive visual brief (style, palette, dimensions)
2. Generate base variations using generate_image
3. Refine with mcp_stitch_* if necessary
4. Deliver an organized set of assets
```

**When to activate:**

```
@nano-banana-generator create 6 banner variations for an email campaign
@nano-banana-generator generate icons for dashboard sections
```

---

## `sop-extractor` — SOP Extractor

**File:** `.antigravity/agents/sop-extractor.md`

Extracts **Standard Operating Procedures (SOPs)** from any knowledge source.

**Supported sources:**

- 📹 **Videos** (YouTube, Loom, recordings) — via URL
- 📚 **Books and PDFs** — excerpts or summaries
- 🎙️ **Interviews** — transcripts or notes
- 🌐 **Web pages** — articles, posts, docs

**Typical Output:**

```yaml
sop:
  name: 'How to do X'
  trigger: 'When Y happens'
  steps:
    - step: 1
      action: 'Do A'
      condition: 'If B, then C'
  checkpoints:
    - 'Verify the outcome of A'
  owner: 'Responsible role'
```

**When to activate:**

```
@sop-extractor extract an SOP from this process presentation video: [URL]
@sop-extractor create an SOP from this book: "Getting Things Done" chapter 3
```
