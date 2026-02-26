# AntiGravity Practical Guide

> **EN** | [PT](../../pt/guides/antigravity-guide.md)

---

Complete step-by-step guide for using AIOS with the **AntiGravity** environment + Gemini Code Assist.

**Version:** 1.0.0  
**Created:** 2026-02-26  
**Technical reference:** [AntiGravity Getting Started](../../en/antigravity/getting-started.md)

---

## 1. Why AntiGravity?

**AntiGravity** is AIOS's native environment for use with Google's **Gemini Code Assist**. It provides full functional parity with Claude Code and adds exclusive tools from the Gemini ecosystem.

| Feature            | Claude Code         | AntiGravity           |
| ------------------ | ------------------- | --------------------- |
| IDE                | Claude Code         | Gemini Code Assist    |
| AI Provider        | `anthropic`         | `gemini`              |
| API Key            | `ANTHROPIC_API_KEY` | `GEMINI_API_KEY`      |
| Config directory   | `.claude/`          | `.antigravity/`       |
| Image generation   | ✗                   | ✅ `generate_image`   |
| UI design          | ✗                   | ✅ Stitch MCP         |
| Browser automation | ✗                   | ✅ `browser_subagent` |
| AIOS Agents        | 11 agents           | 11 agents (same)      |
| Workflows          | Full                | Full (parity)         |
| Squads             | Full                | Full (parity)         |

> **Summary:** If you use Gemini / Google AI Studio or prefer the Google ecosystem, AntiGravity is the right choice.

---

## 2. Prerequisites and Installation

### What you need

| Item               | Version           | Get at                                                                                                       |
| ------------------ | ----------------- | ------------------------------------------------------------------------------------------------------------ |
| Node.js            | 18.0.0+           | [nodejs.org](https://nodejs.org)                                                                             |
| npm                | 9.0.0+            | (included with Node.js)                                                                                      |
| Git                | 2.30+             | [git-scm.com](https://git-scm.com)                                                                           |
| Gemini Code Assist | VS Code Extension | [marketplace.visualstudio.com](https://marketplace.visualstudio.com/items?itemName=Google.google-cloud-code) |
| Google Account     | —                 | Login via extension                                                                                          |

> **No API key needed!** Gemini Code Assist authenticates via your Google account — you do not need a `GEMINI_API_KEY` for standard IDE usage.

### Installing the extension

1. In VS Code, open the Extensions tab (`Ctrl+Shift+X`)
2. Search for `Gemini Code Assist`
3. Click **Install**
4. Sign in with your Google account when prompted
5. Done — the chat is ready!

### Installing AIOS

```bash
# New project (Greenfield)
npx aios-core init my-project

# Existing project (Brownfield)
cd existing-project
npx aios-core install
```

---

## 3. Initial Setup

### Step 1: Configure environment variables (optional)

For standard **Gemini Code Assist** usage, no API key is required — authentication is handled by your Google account through the extension.

If you need direct programmatic access to the Gemini API (e.g., scripts, automations):

```bash
# Optional — only for programmatic API calls
GEMINI_API_KEY=your-gemini-api-key
```

### Step 2: Verify `.antigravity/` is present

```bash
ls .antigravity/
# Expected: ANTIGRAVITY.md  agents/  rules/  skills/  workflows/  templates/
```

> If `.antigravity/` is missing, run `npx aios-core install` again.

### Step 3: Configure `aios.config.yaml`

```yaml
# .aios-core/core/config/aios.config.yaml
ai:
  provider: gemini
  model: gemini-2.0-flash
```

### Step 4: Sync agents to AntiGravity

```bash
# Sync agents to all IDEs (AntiGravity included by default)
npm run sync:ide

# Or only AntiGravity
npm run sync:ide:antigravity

# Validate
npm run validate:antigravity-sync
```

### Step 5: Verify installation

```bash
npx aios-core doctor
```

---

## 4. First Project

Here's how to create a project from scratch using the `greenfield-fullstack` workflow.

### Step 1: Activate the PM and create the PRD

In the Gemini Code Assist chat, type:

```
@pm
*create-prd
```

Agent **Kai** (`@pm`) will guide you through the PRD creation process.

### Step 2: Run the Greenfield workflow

```
@sm
*draft
```

Agent **River** (`@sm`) starts the `greenfield-fullstack` workflow:

```
@sm *draft → @po *validate → @dev *develop → @qa *review → @devops *push
```

### Step 3: Development cycle

1. **`@sm *draft`** — Creates the story with requirements
2. **`@po *validate`** — Validates acceptance criteria
3. **`@dev`** — Implements the code
4. **`@qa *review`** — Reviews and tests
5. **`@devops *push`** — Deploy and operations

---

## 5. SDC Development Cycle

The SDC (Story-Driven Cycle) is the standard AIOS flow:

```
@sm *draft
  └─► creates docs/stories/story-X.X.md
      └─► @po *validate
              └─► @dev (implementation)
                      └─► @qa *review
                                └─► @devops *push (deploy)
```

### Key commands per agent

| Agent        | Command           | What it does                  |
| ------------ | ----------------- | ----------------------------- |
| `@pm`        | `*create-prd`     | Creates product PRD           |
| `@sm`        | `*draft`          | Creates story from PRD        |
| `@po`        | `*validate`       | Validates acceptance criteria |
| `@dev`       | `*develop`        | Implements story code         |
| `@qa`        | `*review`         | Reviews code quality          |
| `@devops`    | `*push`           | Deploy to production          |
| `@architect` | `*analyze-impact` | Analyzes architectural impact |

---

## 6. AntiGravity Exclusive Tools

### 6.1 `generate_image` — Image generation

Generate visual assets directly in the chat:

```
@dev
Create a logo for project MyApp — dark background, minimalist style, colors #6366f1 and white.
```

The assistant uses `generate_image` to create and save the file to the project.

### 6.2 Stitch MCP — UI design

Create visual interfaces with the Stitch MCP integrated into AntiGravity:

```
@ux-expert
*design-screen "Metrics dashboard with line charts and KPI cards"
```

Stitch MCP generates exportable screen prototypes directly into the project.

### 6.3 `browser_subagent` — Browser automation

Test and explore web pages automatically:

```
@qa
*browser-test "https://my-project.vercel.app" — Verify login flow
```

`browser_subagent` opens, navigates, and reports the result with screenshots.

---

## 7. Troubleshooting

### `.antigravity/` was not created

```bash
# Reinstall
npx aios-core install --force

# Verify
ls .antigravity/
```

### Agent won't activate in Gemini Code Assist

1. Verify `ANTIGRAVITY.md` is present:
   ```bash
   cat .antigravity/ANTIGRAVITY.md
   ```
2. Confirm the Gemini Code Assist extension is active in VS Code
3. Reload the window: `Ctrl+Shift+P` → `Developer: Reload Window`

### `GEMINI_API_KEY` not recognized

```bash
# Check the .env file is correct
cat .env | grep GEMINI

# Test the key
node -e "console.log(process.env.GEMINI_API_KEY)" # should return the key
```

### Stitch MCP not working

1. Check that the MCP server is configured in `.antigravity/`
2. See [MCP Configuration](./mcp-global-setup.md)
3. Run `npx aios-core doctor` for diagnostics

### Agents not synced

```bash
npm run sync:ide:antigravity
npm run validate:antigravity-sync
```

---

## References

- [AntiGravity Technical Reference](../../en/antigravity/getting-started.md)
- [AIOS User Guide](./user-guide.md)
- [Development Setup](./development-setup.md)
- [Squads Guide](./squads-guide.md)
- [MCP Integration](./mcp-global-setup.md)

---

_AntiGravity Practical Guide v1.0 — 2026-02-26_
