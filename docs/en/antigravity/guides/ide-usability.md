# Usability: Antigravity as your Primary IDE

The Antigravity framework is **not** just a long set of markdown instructions. It was designed to replace your use of VSCode in flows where manual creative effort needs to focus on Requirements Engineering. We run the agent inside powerful terminals and use the interface to our advantage.

---

## 1. The Daily Drive

The senior Antigravity developer wakes up, opens their IDE, and instead of coding a `for loop`, opens a conversation with the instantiated environment and acts as the _Executive Director_.

### The Conversational Approach

**You do not type code, you stack context.**

1. You use the chat triggering `@agents` like real people: `"@ux analyze the competition on the login page and @ui-builder uses Stitch to forecast how we will do ours"`.
2. The IDE enters "Task Mode" generating checkboxes, assuming it started reading `.antigravity/workflows`, turning on **SYNAPSE**.

### The Terminal Approach

Despite looking like a chat interface, we embrace quick injectable commands (Star Commands `*`):

- You enter `*synapse status` and the IDE understands you ordered to print the agents' memory cache state right there in the chat.
- You command `*create-worktree new-panel` and without asking, it dispatches `git` commands on the real machine using the native Sub-Terminal skill.

## 2. Documentation View (Read Mode vs Execute Mode)

You need to keep a window where you read the progress of open `task.md` files on the right side.
In Antigravity there is a gentleman's agreement on Modification:
The artificial intelligence **DOES NOT** randomly alter a thousand lines in the main source code if the `implementation_plan.md` panel was not stamped by you.
The way you use it is:

1. You ask for planning (The agent creates .md)
2. You inspect and comment "Remove library X, use native"
3. The agent remakes the `.md`
4. You issue the permission flag. It enters Execution Mode.

## 3. Dealing with Logs and Failures (The Sudden Death Rule)

The IDE can fail due to Context Limits.

- If **"Context Bracket > 80% (CRITICAL)"** appears in the console, you physically **must** force the hand-off command to open a new clean intelligence tab (Clearing the L6 Session context).
- If tools like Stitch MCP break, ask `@devtools` itself to investigate its trace log without leaving the IDE.

The fundamental rule: Intelligence in the Antigravity system acts best as a scalpel, not a broom. Guide your sub-agents row by row instead of giving empty orders like "Make a complete netflix clone".
