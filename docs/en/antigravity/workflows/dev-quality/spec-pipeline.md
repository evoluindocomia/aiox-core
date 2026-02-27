# Workflow: Spec Pipeline

**Native source file:** `.antigravity/workflows/spec-pipeline.md`

The **Spec Pipeline** is the backbone of Product and Requirements planning. It converts human abstractions based on a meeting or email into the classic organized technical PRDs, breaking them down into tickets consumable by the developer team.

---

## 1. Usage Trigger (When to invoke)

Use this workflow to:

- Add formal documentation in a Greenfield project.
- Bring business clarity and technical feasibility before the construction of ticket 1.
- Validate if the corporate idea makes mathematical and technical sense (Anti-Hallucination).

## 2. The Operational Journey (Phases)

### Phase 1: Market Discovery and Consolidation (@analyst & @pm)

If time permits, `@analyst` is delegated web sweeps with deep research (`search_web`) to support the argumentative base of a feature.
With the bullets made, `@pm` ties it up and creates the fundamental root of governance: The **PRD** (Product Requirements Document), stocking metrics, targeted personas, and premises in `docs/prd/`. And then a mandatory checkpoint with real human approval is imposed.

### Phase 2: Architectural Shock and Restricted Design (@architect)

The PRD falls into the hands of the pure `@architect`. Unlike creating the database, the check (`check-prd`) hunts for "Hidden Risks".

> **Exclusive Antigravity Integration:** If the PRD massively cries out for a New Visual injection, this is the section where `ui-guidelines.yaml` is forcibly generated. This file imprisons the team to visually build tied to the _Google Stitch_ model without deviations to unwanted independent libraries.

### Phase 3: Production of Administrative Packaging (@pm & @sm)

Validated and safe in terms of logic, the vision is ground:

- `@pm` extracts gigantically enclosed **Epics** based on the modules.
- `@sm` consumes the Epics meticulously dissecting and coining the **Stories** (Micro task tickets ready for the coder), with `story-tmpl.yaml` templates.

### Phase 4: The Product Owner's Slaughter (@po)

No programmer touches a Story that `@po` (Practical Rules Auditor) hasn't decapitated with its commercial adherence check via `po-master-checklist.md`. Receiving Status `>= 7/10`, the backlog turns `READY`.

## 3. Deliverables Matrix

- Initialed PRD that backs responsibility on scope.
- Front `ui-guidelines.yaml` locking limitless creativity if activated.
- Rich tree populating `/epics/` and `/stories/` ready for the SDC cycle.
