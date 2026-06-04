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

---

## Phase 1: Foundation

### T-001: Project Initialisation
**Requirement:** Infrastructure
**Files:** [list key files to create or modify]
**Action:** [Specific description of what to build - unambiguous enough that any agent can follow it]
**Done when:** [Verifiable outcome - what state confirms this is complete]

### T-002: Database / Storage Setup `[P]`
**Requirement:** Infrastructure
**Files:** [list key files]
**Action:** [What to build]
**Done when:** [Verifiable outcome]

---

**Checkpoint 1:** Foundation complete
Verify: [describe the expected state of the project at this point]

---

## Phase 2: Data Layer

### T-003: [Entity] Data Model
**Requirement:** US-NNN
**Requires:** T-001
**Files:** [list key files]
**Action:** [What to build - include field names, types, and relationships]
**Done when:** [Verifiable outcome]

### T-004: [Entity 2] Data Model `[P]`
**Requirement:** US-NNN
**Requires:** T-003
**Files:** [list key files]
**Action:** [What to build]
**Done when:** [Verifiable outcome]

---

**Checkpoint 2:** Data layer complete
Verify: [describe expected state]

---

## Phase 3: Service Layer

### T-005: [Service Name]
**Requirement:** US-NNN
**Requires:** T-003
**Files:** [list key files, including test file]
**Action:** [What to build - include method signatures and their expected behaviour]
**Done when:** [Verifiable outcome - unit tests covering happy path and error cases pass]

---

## Phase 4: API / Controller Layer

### T-006: [Resource] Endpoints
**Requirement:** US-NNN
**Requires:** T-005
**Files:** [list key files, including test file]
**Action:** [List each endpoint with method, path, auth requirement, and expected behaviour]
**Done when:** [Verifiable outcome - integration tests for all endpoints pass; invalid input returns descriptive errors]

---

## Phase 5: Frontend

### T-007: [Component Name] `[P]`
**Requirement:** US-NNN
**Requires:** T-006
**Files:** [list key files, including test file]
**Action:** [What to build - include all required states: loading, error, empty, success]
**Done when:** [Verifiable outcome - all states render correctly; keyboard navigation works]

---

## Phase 6: Integration

### T-008: Wire [Feature] End-to-End
**Requirement:** US-NNN (full flow)
**Requires:** T-006, T-007
**Files:** [list key files]
**Action:** [Connect the layers - describe what the complete user flow should look like when wired together]
**Done when:** [Verifiable outcome - user can complete the full flow without errors]

---

## Phase 7: Polish & Edge Cases

### T-009: Error Handling
**Requirement:** NFR - Reliability
**Requires:** T-006, T-007
**Files:** [list key files]
**Action:** Ensure all error states are handled gracefully. No raw error messages exposed to users. All errors handled with clear, user-friendly feedback.
**Done when:** All error paths produce appropriate user-facing messages; no unhandled exceptions

### T-010: Accessibility `[P]`
**Requirement:** NFR - Accessibility
**Requires:** T-007
**Files:** [may require changes across multiple components]
**Action:** Verify keyboard navigation works for all interactive elements. All images have descriptive alt text. All form fields have associated labels. Colour contrast meets the standard in constitution.md.
**Done when:** All interactive elements reachable by keyboard; no accessibility violations found

---

**Checkpoint 3:** All phases complete
Verify: [full end-to-end state of the feature]

---

## Final Checklist
- [ ] All tasks marked `[DONE]`
- [ ] All checkpoints passed
- [ ] No unhandled error states
- [ ] Accessibility requirements met
- [ ] spec.md Review & Acceptance Checklist fully checked
- [ ] plan.md Implementation Notes updated with any deviations
