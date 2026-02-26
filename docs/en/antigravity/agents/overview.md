# Agents Overview

Antigravity operates on a multi-agent orchestration model where specialized AI personas collaborate to fulfill high-level system objectives.

---

## Hierarchy & Roles

The system is organized into three main categories:

### 1. Core AIOS Agents

The fundamental squad that handles the software development life cycle (SDLC).

- **Available:** `@dev`, `@qa`, `@architect`, `@pm`, `@po`, `@sm`, `@analyst`, `@data-engineer`, `@ux`, `@devops`, `@brad-frost`, `@squad-chief`, `@research-specialists`.
- **Location:** `.antigravity/agents/`

### 2. Specialized Chiefs

Domain-specific orchestrators that manage complex subsystems.

- **Examples:** `@copy-chief`, `@cyber-chief`, `@legal-chief`, `@db-sage`.
- **Location:** `.antigravity/agents/`

### 3. Mind Clones (Design Squad)

High-fidelity clones of real-world experts, created via the DNA Mental™ process.

- **Members:** `brad-frost`, `dan-mall`, and other domain-specific clones.
- **Location:** `.antigravity/agents/`

---

## Activation and Interaction

To interact with an agent, simply `@mention` them in your prompt:

```bash
@dev implement the login form validation
@architect review the database schema migration
@squad-chief create a squad for digital marketing
```

### Star Commands (`*`)

Many agents have specific action triggers known as **Star Commands**:

- `@po *create-story`
- `@squad-chief *create-squad`
- `@qa *run-tests`

---

## Agent Autonomy & Memory

### Inline Persona

Every agent's instructions, scope, and rules are defined within their `.md` file. This makes them fully self-contained.

### Persistent Memory

Agents save their state and learnings in `.antigravity/agent-memory/{agent-name}/MEMORY.md`. This ensures they remember project-specific preferences and past decisions.

### Tool Optimization

Each agent is pre-configured with the tools most relevant to their role. For example, `@devops` is the only agent authorized to execute `git push`, while `@ux-design-expert` has exclusive access to professional design tools.
