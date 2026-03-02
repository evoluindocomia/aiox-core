# Definitive Onboarding Guide — Antigravity

Welcome to the definitive step-by-step guide to get started with the AIOS **Antigravity** environment. This guide is designed to help you bypass any current CLI limitations and start building incredible applications immediately using the Gemini provider.

---

## 1. Installation and Initial Setup

In the latest versions, the `aios-core init` command automatically configures the `.antigravity/` environment in your workspace, and IDE synchronization is enabled by default.

### INSTALLATION STEP-BY-STEP

1. **Install AIOS normally in your directed folder:**

   ```bash
   npx aios-core init my-project
   cd my-project
   ```

   _Note:_ The `.antigravity/` directory (including `agents/`, `rules/`, `skills/`, `workflows/`, `templates/`, and the `ANTIGRAVITY.md` file) will be automatically copied to your new project.

2. **IDE Synchronization:**
   The synchronization command automatically includes the Antigravity profile natively. Run the validation if necessary:

   ```bash
   npm run validate:antigravity-sync
   ```

---

## 2. API Keys Configuration

For Antigravity to fully utilize the core intelligence engine and advanced ecosystem integrations (such as interface generators and web search), you must ensure that your main provider is Gemini and that your API key is actively in your environment.

1. Choose the `gemini` provider when the IDE or CLI prompt asks which underlying model should be used.
2. Configure your master key before initializing agents. On Windows (PowerShell/CMD) or Unix (bash/zsh):

   ```bash
   # Unix / MacOS
   export GEMINI_API_KEY="your_gemini_key_here"

   # Windows PowerShell
   $env:GEMINI_API_KEY="your_gemini_key_here"
   ```

3. Ensure any legacy Claude Code permissions are properly bypassed or adapted for Antigravity, if migrating a workspace.

---

## 3. First Use: Running a Greenfield Fullstack

Now that directories are appropriately populated and API keys are defined, let's build your very first agent-driven application!

To trigger AIOS magic, your starting point is always to call upon initial orchestration directly in your IDE window.

1. **Open your AI assistant panel** (such as Gemini Code Assist or a docked terminal within your IDE).
2. **Explicitly request the Greenfield Fullstack workflow:**
   ```text
   I want to start a new project using the greenfield-fullstack workflow.
   Let's build a Task List application entirely in React and Supabase.
   ```
3. Antigravity will contextually inject the `.antigravity/workflows/greenfield-fullstack.md` document.
4. **Watch the agent chain in action:**
   - The `@analyst` agent will diagnose your needs and evaluate constraints.
   - The `@pm` agent will write the Product Requirements Document (PRD).
   - The `@architect` will define the Front-end and Back-end structure templates.
   - The `@po` will slice the specification into manageable executable Stories using `story-tmpl.yaml`.
   - The `@dev` will implement the backend logic and the `@qa` will formulate tests.

### 3.1. The Awareness Lock (YOLO Mode vs Default Squad)

If you trigger a global action without explicitly designating a Squad, Antigravity will intercept your request. It will warn you about the risk of **YOLO Mode** (direct and generic execution) and offer the option to dynamically activate the **Default Squad**, which will execute the step-by-step SDC cycle with all the agents above.

---

## 4. Common Troubleshooting

**The agent is missing governance rules and hook constraints**

- **Cause:** The `ANTIGRAVITY.md` file or the `rules/` folder are not properly loaded or present.
- **Solution:** Verify if the initialization command successfully created the `.antigravity/` structure. Ensure you are using the latest version and the folders aren't being blocked by your `.gitignore` file.

**"Unsupported provider or authentication error"**

- **Cause:** Missing `GEMINI_API_KEY` when running within restricted sandboxes.
- **Solution:** The terminal context might have been restarted or environment variables cleared. Re-export the variable as defined in Step 2.

**The assistant says the skill/agent does not exist**

- **Cause:** Context window rules imposed by the IDE assistant failed to autoload the requested skill structure fast enough.
- **Solution:** Explicitly invoke the structural map or file. Example: _"Please read the instructions inside `.antigravity/skills/synapse/SKILL.md` before answering"_.
