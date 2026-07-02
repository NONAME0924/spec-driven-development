# Task Breakdown: [Feature Name]
**Feature ID:** NNN-feature-name
**Generated:** YYYY-MM-DD
**Total Tasks:** [N] | **Completed:** 0 / [N]

---

## Legend
| Marker | Meaning |
|--------|---------|
| `[P]` | Can proceed in parallel with adjacent `[P]` tasks |
| `[DONE]` | Task completed and verified |
| `[BLOCKED]` | Waiting on a dependency |
| `Requires: T-NNN` | Must complete that task first |

Every task must map to `plan.md`:
- **Module** -> a Module Map entry, or a justified cross-cutting concern
- **Workflow** -> a Workflow Map entry, or `N/A`
- **Contract/Data** -> relevant contract, workflow, data model, or `N/A`

---

## Foundation

### T-001: Project Structure Setup
**Module:** Cross-cutting / Project Structure
**Layer:** Infrastructure
**Workflow:** All
**Requirement:** Infrastructure
**Contract/Data:** `plan.md#project-structure`
**Files:** [list key files to create or modify]
**Action:** Create or adapt the project folders from `plan.md#project-structure`. Do not create unrelated root-level files when a module folder exists.
**Done when:** Planned module folders exist and match the project layout.

### T-002: Shared Primitives `[P]`
**Module:** Shared
**Layer:** Cross-cutting
**Workflow:** All affected workflows
**Requirement:** NFR / Infrastructure
**Contract/Data:** [shared error/auth/validation contracts]
**Requires:** T-001
**Files:** [list key files]
**Action:** Create shared helpers required by multiple modules, such as validation schemas, error types, auth context, or test utilities.
**Done when:** Shared primitives are imported by at least one module and covered by a minimal check.

---

**Checkpoint 1:** Foundation complete
Verify: Project structure, shared primitives, and module boundaries are ready.

---

## Module: [Module Name from Module Map]

**Owns:** [Responsibility from Module Map]
**Workflows:** [Workflow names that touch this module]

### T-003: [Entity] Data Model
**Module:** [Module name]
**Layer:** Data
**Workflow:** [Workflow name or N/A]
**Requirement:** US-NNN / FR-NNN
**Contract/Data:** `data-model.md#[Entity]`
**Requires:** T-001
**Files:** [list key files]
**Action:** Build the data model for this module, including field names, types, relationships, indexes, and validation rules.
**Done when:** Data model compiles/migrates and has a minimal verification check.

### T-004: [Service Name]
**Module:** [Module name]
**Layer:** Service
**Workflow:** [Workflow name]
**Requirement:** US-NNN
**Contract/Data:** `contracts/workflows.md#[Workflow]`, `data-model.md#[Entity]`
**Requires:** T-003
**Files:** [list key files, including test file]
**Action:** Build the module's business logic with explicit method signatures, inputs, outputs, and error cases.
**Done when:** Unit tests cover happy path and error cases.

---

**Checkpoint 2:** [Module name] module complete
Verify: Module responsibilities are implemented without leaking unrelated concerns into other modules.

---

## Workflow: [Workflow Name from Workflow Map]

### T-005: [Resource] API / Adapter
**Module:** [API or adapter module name]
**Layer:** API / Adapter
**Workflow:** [Workflow name]
**Requirement:** US-NNN
**Contract/Data:** `contracts/api-spec.json#[operationId]` or `contracts/events.md#[eventName]`
**Requires:** T-004
**Files:** [list key files, including test file]
**Action:** Implement each operation with method/path or event name, auth requirement, input schema, output schema, status codes, and standard error body.
**Done when:** Integration tests pass for success, validation failure, auth failure, and not-found/permission cases where applicable.

### T-006: [UI Component / Client Command] `[P]`
**Module:** [UI/client module name]
**Layer:** Frontend / Client
**Workflow:** [Workflow name]
**Requirement:** US-NNN
**Contract/Data:** `contracts/api-spec.json#[operationId]`
**Requires:** T-005
**Files:** [list key files, including test file]
**Action:** Build the user-facing or client-facing entry point, including loading, error, empty, success, and accessibility states.
**Done when:** All states render correctly and keyboard/accessibility basics pass.

### T-007: Wire [Workflow] End-to-End
**Module:** Cross-module integration
**Layer:** Integration
**Workflow:** [Workflow name]
**Requirement:** US-NNN (full flow)
**Contract/Data:** `contracts/workflows.md#[Workflow]`
**Requires:** T-005, T-006
**Files:** [list key files]
**Action:** Connect modules in the exact order defined by the Workflow Map.
**Done when:** User can complete the full workflow without errors.

---

## Cross-Cutting Hardening

### T-008: Error Handling
**Module:** Shared errors + affected modules
**Layer:** Cross-cutting
**Workflow:** All affected workflows
**Requirement:** NFR - Reliability
**Contract/Data:** Standard error schema
**Requires:** T-005, T-006, T-007
**Files:** [list key files]
**Action:** Ensure all error states are handled gracefully. No raw error messages exposed to users. All errors use the standard format from the contract.
**Done when:** All error paths produce appropriate user-facing messages; no unhandled exceptions.

### T-009: Acceptance Coverage `[P]`
**Module:** Tests
**Layer:** Testing
**Workflow:** [Workflow name]
**Requirement:** All acceptance criteria touched by this Feature
**Contract/Data:** `spec.md`, `contracts/*`, `data-model.md`
**Requires:** T-007
**Files:** [test files]
**Action:** Add tests that trace each acceptance criterion to the module/workflow it verifies.
**Done when:** Coverage map in `test-report.md` has no untested acceptance criteria.

---

**Checkpoint 3:** All modules and workflows complete
Verify: Every Module Map entry and Workflow Map entry is implemented or explicitly scoped out.

---

## Final Checklist
- [ ] All tasks marked `[DONE]`
- [ ] All checkpoints passed
- [ ] Every task maps to a Module Map entry or justified cross-cutting concern
- [ ] Every workflow in Workflow Map has integration and test tasks
- [ ] No orphan tasks that do not trace to a requirement, module, workflow, contract, or data model
- [ ] Task pruning pass completed; speculative scaffolding deleted or deferred
- [ ] No unhandled error states
- [ ] Accessibility requirements met
- [ ] spec.md Review & Acceptance Checklist fully checked
- [ ] plan.md Implementation Notes updated with any deviations
