# Workflow: Auto Worktree

**Native source file:** `.antigravity/workflows/auto-worktree.md`

The **Auto Worktree** process governs safe parallel development through isolated git directories. Unlike the original Claude Code which tried to manage this with opaque hooks, AntiGravity expressly delegates this responsibility to the `@devops` agent and explicit commands, ensuring the factory floor doesn't become a mess of invisible branches.

---

## 1. Usage Trigger (When to invoke)

Use this workflow to:

- Code `Feature A` and `Feature B` simultaneously without `A`'s compilation breaks affecting `B`.
- Make an urgent correction in production (`hotfix`) while you have a massive unfinished epic in your local folder.
- Run multiple local servers on different ports (e.g., backend in one worktree, worker in another).

## 2. The Operational Journey (Phases)

### Phase 1: Creation and Physical Bifurcation (@devops)

You start by invoking the command `*create-worktree {branch}`. `@devops` executes an associated shallow clone in the terminal `git worktree add ../aios-{feature} -b feat/{feature-name}`.
**Important:** The new folder is created _one level up_ or in a directory parallel to the main one, ensuring the original root remains clean.

### Phase 2: The Development Retreat

Developers (like `@dev` and `@qa`) are physically moved to `cd ../aios-{feature}`. Everything that happens there is isolated:

- New `node_modules` installed from scratch.
- Tests run only for what was touched there.
- The `.aios/` annotations of this worktree do not dirty the mother project.

### Phase 3: The Tribe Returns (Merge and Cleanup)

Upon hitting the hammer with `QA Approved`, you do not merge in there. The correct flow triggers `@devops` (`*merge-worktree {branch}`), which returns to the `main` directory (main project), performs the merge of the worktree branch (being able to apply _squash_), and then physically exterminates the parallel folder with `git worktree remove` and `git branch -d`.

## 3. Deliverables Matrix

- System built in virtual HD folders tied to git (Dependency isolation).
- Branches deleted after the merge to maintain the hygiene of the mother repository.
