# SYNAPSE Context Engine

**SYNAPSE** (Synkra Adaptive Processing & State Engine) is the beating heart of Antigravity's memory retention. Unlike generic chats that forget things mid-conversation, SYNAPSE manages a strict local cache divided into 8 injection layers.

---

## 1. The Hidden File Structure

Inside your project's root resides the `.synapse/` folder. It's not just a log, it is a dashboard of injectables:

```text
.synapse/
├── manifest          # Central key registry
├── constitution      # L0 - Inviolable server rules
├── global            # L1 - Rules that affect everyone
├── context           # L1 - Instructions on context size
├── agent-*           # L2 - Scoped files (e.g., agent-dev)
├── workflow-*        # L3 - Injectable tips of the current Workflow
├── commands          # Saved Star Commands (*)
└── sessions/         # Where the IDE keeps the handoff cache
```

## 2. 8-Layer Injection (L0 to L7)

When an order is given to Antigravity, it doesn't just look at your `.md`. It stacks the following mental onion:

| Layer  | Name          | Function                                                            |
| ------ | ------------- | ------------------------------------------------------------------- |
| **L0** | Constitution  | What it must NEVER do (Ex: Drop DB in prod without asking).         |
| **L1** | Global        | Technology stack (React, Node, etc.).                               |
| **L2** | Agent-Scoped  | Active Agent's dictionary (e.g., @pm's heuristics).                 |
| **L3** | Workflow      | The current flow (If we are in `brownfield`, it loads legacy tips). |
| **L4** | Task          | Millimetric instructions from the current `task.md` file.           |
| **L5** | Squad         | Collective memory of the triggered expert pool.                     |
| **L6** | Session       | History of the user's chat tab.                                     |
| **L7** | Star-Commands | Operational definition if the user tries a shortcut.                |

## 3. Token Survival (Context Brackets)

AI models have _Context Window_ limits. The `.synapse/context` file acts as a pressure regulator in the IDE:

1. **FRESH (< 30% usage):** The model consumes all layers freely (L0 to L7).
2. **MODERATE (30-60% usage):** The system starts getting heavy, we drop cosmetic layers (keeping L0-L5).
3. **DEPLETED (60-80% usage):** Yellow token alert (cuts to L0-L3).
4. **CRITICAL (> 80% usage):** The IDE suggests session handoff and only injects the Constitution layer (L0).

Knowing how to manipulate the injection engine using the `*synapse` shortcuts allows you to train your computer's AI like a loyal dog.
