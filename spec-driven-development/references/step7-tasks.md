# Step 7 - Tasks

## Purpose
Break the approved implementation plan into granular, ordered, executable tasks. The result is a `tasks.md` that any AI agent can follow to implement the Feature systematically.

In auto mode, create the task breakdown and proceed to implementation without waiting, unless the task list reveals that Step 8 will require a large rewrite, destructive operation, data migration, broad public API change, security-sensitive change, or irreversible action.

Tasks must preserve the architecture from Step 5. Do not produce a flat task list. Group work by module and workflow, and include each task's module, layer, workflow, requirement, and contract/data references.

Lean SDD applies here: tasks are not a place to smuggle future architecture back in. Generate the shortest task list that can implement and verify the approved Feature.

---

## Task Design Principles

1. **Atomic** - each task has one clear, verifiable outcome
2. **Ordered** - dependencies respected; nothing requires something that does not exist yet
3. **Traceable** - each task references its user story or requirement ID
4. **Specific** - file paths, function names, and acceptance criteria are explicit
5. **Parallelisable where possible** - mark tasks that can proceed concurrently with `[P]`
6. **Architecturally grouped** - each task belongs to a Module Map entry and, when relevant, a Workflow Map entry
7. **Project-shaped** - tasks create or modify files in the planned project structure; avoid dumping unrelated work into root-level files

---

## Task Organization

Prefer this hierarchy:

1. Cross-cutting foundation tasks
2. Module sections in the same order as `plan.md` Module Map
3. Workflow integration sections in the same order as `plan.md` Workflow Map
4. Test and hardening sections tied back to modules/workflows

Within each module, order by dependency: data -> service/domain -> API/adapter -> UI -> tests, unless the project architecture implies a better order.

## Task Pruning Pass

Before finalizing `tasks.md`, remove or merge tasks that match any of these:

- No approved requirement, module, workflow, contract, or data model reference
- "Prepare", "scaffold", "abstract", or "make extensible" work with no current caller
- New dependency setup when native/stdlib/existing dependency is enough
- Interface/factory/adapter with one implementation and no current second implementation requirement
- Separate task whose Done When is only "file exists" and can be included in a real implementation task
- Test scaffolding not tied to an acceptance criterion, module, workflow, or contract

Keep tasks that protect correctness: validation, auth/authz, migration safety, data-loss handling, accessibility basics, and spec-traced tests.

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

## Foundation

### T-001: Project Initialisation
**Module:** Cross-cutting / Project Structure
**Layer:** Infrastructure
**Workflow:** All
**Requirement:** Infrastructure
**Files:** [list key files to create]
**Action:** [What the AI should do - specific and unambiguous]
**Done when:** [Verifiable outcome - what the AI checks to confirm completion]

### T-002: Module Folder Setup `[P]`
**Module:** [Module name from Module Map]
**Layer:** Infrastructure
**Workflow:** [Workflow name or N/A]
**Requirement:** Infrastructure
**Files:** [list key files]
**Action:** [What the AI should do]
**Done when:** [Verifiable outcome]

---

**Checkpoint 1:** Foundation complete
Verify: [what state the project should be in at this point]

---

## Module: [Module Name from Module Map]

**Owns:** [Responsibility from Module Map]
**Workflows:** [Workflow names that touch this module]

### T-003: [Entity] Schema
**Module:** [Module name]
**Layer:** Data
**Workflow:** [Workflow name]
**Requirement:** US-NNN / FR-NNN
**Contract/Data:** `data-model.md#[Entity]`
**Requires:** T-001
**Files:** [list key files]
**Action:** [What to build - include field names, types, relationships, and validation]
**Done when:** [Verifiable outcome]

### T-004: [Service Name]
**Module:** [Module name]
**Layer:** Service
**Workflow:** [Workflow name]
**Requirement:** US-NNN
**Contract/Data:** `contracts/workflows.md#[Workflow]`, `data-model.md#[Entity]`
**Requires:** T-003
**Files:** [list key files]
**Action:** [What to build - include method signatures and expected behavior]
**Done when:** [Verifiable outcome - include that unit tests pass]

---

**Checkpoint 2:** [Module name] module complete
Verify: [module-level expected state]

---

## Workflow: [Workflow Name from Workflow Map]

### T-005: [Resource] Endpoints
**Module:** [API module name]
**Layer:** API
**Workflow:** [Workflow name]
**Requirement:** US-NNN
**Contract/Data:** `contracts/api-spec.json#[operationId]`
**Requires:** T-004
**Files:** [list key files]
**Action:** [List each endpoint with method, path, auth requirement, input/output schema, error format, and expected behavior]
**Done when:** [Verifiable outcome - include that integration tests pass]

### T-006: [Component Name] `[P]`
**Module:** [UI module name]
**Layer:** Frontend
**Workflow:** [Workflow name]
**Requirement:** US-NNN
**Contract/Data:** `contracts/api-spec.json#[operationId]`
**Requires:** T-005
**Files:** [list key files]
**Action:** [What to build - include all required states: loading, error, empty, success]
**Done when:** [Verifiable outcome - include all states and accessibility basics]

### T-007: Wire [Workflow] End-to-End
**Module:** Cross-module integration
**Layer:** Integration
**Workflow:** [Workflow name]
**Requirement:** US-NNN (full flow)
**Contract/Data:** `contracts/workflows.md#[Workflow]`
**Requires:** T-005, T-006
**Files:** [list key files]
**Action:** [Connect the modules in the order defined by Workflow Map]
**Done when:** [Verifiable outcome - user can complete the full workflow]

---

## Cross-Cutting Hardening

### T-008: Error Handling
**Module:** Shared errors + affected modules
**Layer:** Cross-cutting
**Workflow:** All affected workflows
**Requirement:** NFR - Reliability
**Requires:** T-005, T-006, T-007
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
- [ ] Every task maps to a Module Map entry or a justified cross-cutting concern
- [ ] Every workflow in Workflow Map has integration and test tasks
- [ ] No orphan tasks that do not trace to a requirement, module, workflow, contract, or data model
- [ ] Task pruning pass completed; speculative scaffolding deleted or deferred
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
   Total tasks: [N] across [M] modules/workflows

Review: Please review the task breakdown. When ready:
  - "continue" or "next" -> proceed to Step 8 (Implement)
  - "revise [what]" -> adjust tasks before starting implementation
  - "stop" -> pause here; say "continue from Step 8" to resume

WARNING:  Step 8 will begin writing actual code. Make sure your development environment is ready.
---
```

**Mode rule:** In detailed mode, wait at this gate. In auto mode, continue to Step 8 automatically unless an implementation risk trigger appears.
