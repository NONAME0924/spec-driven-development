# Step 7 - Tasks

## Purpose
Break the approved implementation plan into granular, ordered, executable tasks. The result is a `tasks.md` that any AI agent can follow to implement the Feature systematically.

---

## Task Design Principles

1. **Atomic** - each task has one clear, verifiable outcome
2. **Ordered** - dependencies respected; nothing requires something that does not exist yet
3. **Traceable** - each task references its user story or requirement ID
4. **Specific** - file paths, function names, and acceptance criteria are explicit
5. **Parallelisable where possible** - mark tasks that can proceed concurrently with `[P]`

---

## Task Categories (in execution order)

| Order | Category | Examples |
|-------|----------|---------|
| 1 | Infrastructure | Project setup, config |
| 2 | Data layer | Database schema, models |
| 3 | Service layer | Business logic, validation |
| 4 | API / Controller layer | Endpoints, request handling |
| 5 | Frontend | UI components, state |
| 6 | Integration | Wire layers together |
| 7 | Testing | Unit, integration, acceptance |
| 8 | Polish | Error handling, accessibility |

---

## Output: `tasks.md`

Create `.specify/specs/NNN-feature-name/tasks.md`:

```markdown
# Task Breakdown: [Feature Name]
**Feature ID:** NNN-feature-name
**Generated:** YYYY-MM-DD
**Total Tasks:** [N]

## Legend
- `[P]` - Can proceed in parallel with adjacent `[P]` tasks
- `[DONE]` - Completed
- `[BLOCKED]` - Waiting on dependency
- Dependencies listed as `Requires: T-NNN`

---

## Phase 1: Foundation

### T-001: Project Initialisation
**Requirement:** Infrastructure
**Files:** [list key files to create]
**Action:** [What the AI should do - specific and unambiguous]
**Done when:** [Verifiable outcome - what the AI checks to confirm completion]

### T-002: Database Setup `[P]`
**Requirement:** Infrastructure
**Files:** [list key files]
**Action:** [What the AI should do]
**Done when:** [Verifiable outcome]

---

**Checkpoint 1:** Foundation complete
Verify: [what state the project should be in at this point]

---

## Phase 2: Data Layer

### T-003: [Entity] Schema
**Requirement:** US-NNN
**Requires:** T-001
**Files:** [list key files]
**Action:** [What the AI should do]
**Done when:** [Verifiable outcome]

---

**Checkpoint 2:** Data layer complete
Verify: [what state the project should be in]

---

## Phase 3: Service Layer

### T-004: [Service Name]
**Requirement:** US-NNN
**Requires:** T-003
**Files:** [list key files]
**Action:** [What the AI should do]
**Done when:** [Verifiable outcome - include that unit tests pass]

---

## Phase 4: API Layer

### T-005: [Resource] Endpoints
**Requirement:** US-NNN
**Requires:** T-004
**Files:** [list key files]
**Action:** [What the AI should do]
**Done when:** [Verifiable outcome - include that integration tests pass]

---

## Phase 5: Frontend

### T-006: [Component Name] `[P]`
**Requirement:** US-NNN
**Requires:** T-005
**Files:** [list key files]
**Action:** [What the AI should do]
**Done when:** [Verifiable outcome - include all states: loading, error, empty, success]

---

## Phase 6: Polish

### T-007: Error Handling
**Requirement:** NFR - Reliability
**Requires:** T-005, T-006
**Files:** [list key files]
**Action:** [What the AI should do]
**Done when:** No raw error messages visible to users; all errors handled gracefully

---

**Checkpoint 3:** All features complete
Verify: [full end-to-end state]

---

## Final Checklist
- [ ] All tasks marked `[DONE]`
- [ ] All checkpoints passed
- [ ] No unhandled error states
- [ ] Accessibility: keyboard navigation works throughout
- [ ] spec.md Review & Acceptance Checklist fully checked
```

---

## Gate

Show the complete `tasks.md` to the user, then output:

```
---
[PASS] Step 7 - Tasks complete  (Feature: NNN-feature-name)

Output: Output: .specify/specs/NNN-feature-name/tasks.md
   Total tasks: [N] across [M] phases

Review: Please review the task breakdown. When ready:
  - "continue" or "next" -> proceed to Step 8 (Implement)
  - "revise [what]" -> adjust tasks before starting implementation
  - "stop" -> pause here; say "continue from Step 8" to resume

WARNING:  Step 8 will begin writing actual code. Make sure your development environment is ready.
---
```

Do not proceed to Step 8 until the user responds.
