# Workflow: Greenfield Service

**Native source file:** `.antigravity/workflows/greenfield-service.md`

The **Greenfield Service** process is laser-focused on the **silent construction of Backend and pure APIs**, operating from Relational Design to logical implementation where screens or visual markup layers (Frontend) are abstracted or non-existent.

---

## 1. Usage Trigger (When to invoke)

Use this workflow exclusively for:

- Creating headless Microservices (GraphQL, REST APIs).
- Background Tools, Lambdas / Edge Functions, and pure systemic integrations.
- Processing pipelines without human interface.

## 2. The Operational Journey (Phases)

### Phase 0: Base Bootstrap

Same as the `fullstack` standard, the `@devops` agent ties the local and remote foundation without code involvement.

### Phase 1: Deep Backend Planning

The focus in Phase 1 differs in the entry of architectural database weight:

1. `@analyst` and `@pm` define the raw rules in the **Corporate PRD**.
2. `@architect` unravels the PRD into a robust **Service Architecture** (Creates endpoints, payload design, and in/out flows).
3. `@data-engineer` (DB Sage) enters, executing critical design: Analyzes the proposed schema with _KISS_ logic, configures the rigid RLS Policies (e.g., Supabase), and elaborates the first root PostgreSQL migration.
4. `@po` homologates all documents against the master quality checklist.

### Phase 2: Configuration and Initial Database Load

Here `@data-engineer` intercedes assembling the raw beams:

- Runs the initial Migration dry-run.
- Applies the modeling to the tables.
- Instantiates the Seeds (crucial dummy data for testing) and nails it with the `smoke-test`.

### Phase 3: The Endpoint Factory (Sprint Loop)

Guided by the Stories fractionated by `@po`:

- `@sm` extracts the isolated database manipulation and route tasks.
- `@dev` types the Service Layer.
- `@qa` raises the testing meshes testing strictly: Endpoints returning shielded Payload, systemic Edge Cases, and severe Security validations on Auth Tokens.

## 3. Binary Expectation at the End

- Live PostgreSQL architecture schema running Row-Level-Security against injections.
- Every request documented in a Swagger or spec based on committable code.
