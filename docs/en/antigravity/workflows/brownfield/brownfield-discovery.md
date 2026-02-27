# Workflow: Brownfield Discovery

**Native source file:** `.antigravity/workflows/brownfield-discovery.md`

The **Brownfield Discovery** process is the strict and mandatory entry point of Antigravity when landing on a legacy project or existing codebase. No new logic is written without the Discovery of the old logic.

---

## 1. Usage Trigger (When to invoke)

Use this workflow to:

- Adopt a legacy repository built by former employees.
- Start a mass refactoring.
- Update architectural documentation that fell behind before starting the next major Sprint.

## 2. The Operational Journey (Phases)

The process flows from mapping the infrastructure to cataloging code "gotchas" (bear traps).

### Step 1: Tactical Reconnaissance

Agents query `git log --oneline -20`, `git status` and read the active branches to understand the repository's status on Github/Gitlab.

### Step 2: Raw Mapping (@architect)

The `@architect` invades the folders:

- Lists the real tech-stack (`package.json`, `pom.xml`, etc).
- Understands the current _design pattern_ (e.g., Hexagonal, raw MVC).
- Generates the `docs/architecture/project-structure.md` file.

### Step 3: Database Audit (@data-engineer)

If there is a relational DB (Postgres/Supabase), the `@data-engineer` is triggered to run the SQL command and extract current migrations, orphan tables, and flawed Row-Level Security Policies, dropping everything into `supabase/docs/SCHEMA.md`.

### Step 4: Design Audit (@ux)

If it is front-heavy, `@ux` enters hunting for UI Tokens, components that are never reused, and formats an Inconsistency Report.

### Step 5: Gotchas Cataloging (Bear Traps)

The most vital phase: The team consolidates all "ugly code that cannot be touched now because it breaks x" or "strange V1 behavior" within the framework's memory in the Json file: `.aios/gotchas.json`. All devs read this before coding in the future.

### Step 6: The Great Document

The `@architect` writes `docs/architecture/brownfield-architecture.md` uniting all reports from phases 2, 3, 4, and 5.

## 3. Deliverables Matrix

- `brownfield-architecture.md` generated.
- Database mapped.
- The "Gotchas" (known coupled bugs) formally saved in the agents' JSON memory.
