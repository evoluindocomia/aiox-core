# Workflow: Brownfield Service

**Native source file:** `.antigravity/workflows/brownfield-service.md`

The **Brownfield Service** process is tactically shielded, focused only on the sub-world of Servers, APIs, and Databases that are already hot (operating real human data) in an ecosystem.

---

## 1. Usage Trigger (When to invoke)

Use this workflow exclusively to:

- Alter Response Payload on publicly consumed Endpoints.
- Insert/Update Models in the database without shutting down the application (Live Migrations).
- Surgical refactoring in purely backend routines.

## 2. The Operational Journey (Phases)

### Phase 1: Contract Analysis (Rearguard Impact)

The colossal difference here is that `@pm` and `@architect` spend almost 50% of the ticket time looking for **Breaking Changes**. If the engineer wants to change the Response of the _"v1/users"_ JSON object that the old Mobile App is using to show a profile, they veto and force the creation of the _"v2/users"_ endpoint.

### Phase 2: The Data Surgeon (@data-engineer)

If there is a database, a blind flight protocol is required before programming:

1. `*db-dry-run` — Tries to run the migration without writing.
2. `*db-snapshot` — Safety backup enabled.
3. `*db-apply-migration` — Runs the real relational commit.
4. `*db-smoke-test` — Checks if the server booted or the schema panicked after the table changed.

### Phase 3: Restricted Story Loop

During the `@dev`'s work, the supreme execution rule consists primarily of running the legacy test suite BEFORE trying to touch a comma of Node/Python. You create code respecting backward compatibility always.
The Quality Bot `@qa` will exhaustively look for _Error Handling_ issues, blowing up _Integration Tests_ if you try to violate old contracts.

## 3. Deliverables Matrix

- API change made side-by-side or overlapped via v1/v2 with immaculate backward compatibility.
- Code 100% covered by Test meshes (High coverage where it was touched).
- No active data deletion (no accidental DROPS in prod).
