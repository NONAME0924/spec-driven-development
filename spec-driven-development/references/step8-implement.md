# Step 8 - Implement

## Purpose
Execute the task list in `tasks.md` systematically to produce working code. Follow every task in order, verify each one is complete before moving on, and keep the user informed at each checkpoint.

In auto mode, implementation starts automatically after Step 7 unless a risk trigger appears. Ask for user approval before a large rewrite, destructive operation, data migration, broad public API change, security-sensitive change, irreversible action, or dependency/service choice not already approved.

---

## Pre-Implementation Checks

Before starting, verify all prerequisites exist and meet the active mode's approval profile:

- [ ] `.specify/memory/constitution.md` - exists
- [ ] `.specify/specs/NNN-feature-name/spec.md` - approved through Step 2/3
- [ ] `.specify/specs/NNN-feature-name/plan.md` - complete; explicitly approved only in detailed mode or when risk-triggered
- [ ] `.specify/specs/NNN-feature-name/tasks.md` - complete; explicitly approved only in detailed mode or when risk-triggered
- [ ] No unresolved [FAIL] items in any checklist

If any are missing or unapproved, return to the appropriate earlier step.

---

## Execution Strategy

### Architecture First
1. Read `plan.md#Project Structure`, `plan.md#Module Map`, and `plan.md#Workflow Map` before editing code
2. Implement inside the planned module folders unless the existing repo has a stronger local convention
3. Do not create orphan files at the project root when a module/layer folder owns the responsibility
4. If a task appears not to belong to any module or workflow, stop and fix `tasks.md` or `plan.md` before implementing it

### Lean Implementation
1. Reuse existing codebase patterns, helpers, modules, validators, errors, and tests before writing new ones
2. Use standard library, native platform features, or already-installed dependencies before custom code or new packages
3. Do not add a new dependency unless Step 5 already justified it or the user approves it as a risk trigger
4. Do not create interfaces, factories, adapters, registries, plugin systems, config flags, or base classes with one implementation unless the approved spec requires the abstraction
5. Prefer root-cause fixes in shared code over repeated symptom patches in callers
6. Prefer deletion or consolidation when fixing overbuilt code, as long as acceptance criteria still pass
7. Keep validation, auth/authz, data-loss protection, migration safety, accessibility basics, and spec-traced tests even when they add lines

### Task Ordering
1. Read `tasks.md` fully before starting any task
2. Begin with Foundation tasks, then follow module and workflow sections in dependency order
3. Respect all `Requires: T-NNN` dependencies
4. Tasks marked `[P]` may be worked on concurrently where practical
5. Verify each Checkpoint before moving to the next module or workflow section

### Per-Task Pattern

For each task:
1. **Read** the task's Action and Done When criteria
2. **Confirm** Module, Layer, Workflow, Requirement, and Contract/Data fields are present or explicitly `N/A`
3. **Confirm** all dependencies are marked `[DONE]`
4. **Implement** - write the code in the planned module/layer
5. **Lean check** - confirm no speculative dependency, abstraction, module, or file was introduced
6. **Verify** - check the Done When criterion is satisfied
7. **Mark** the task as `[DONE]` in `tasks.md`

### Commit Message Format

Follow the convention in `constitution.md`. Default format:
```
feat(T-NNN): short description

- Detail 1
- Detail 2

Refs: US-NNN
```

---

## Checkpoint Reporting

After each foundation, module, or workflow checkpoint, report progress to the user:

```
[PASS] Checkpoint [N] passed - [Foundation / Module / Workflow Name]
  T-001: done
  T-002: done
  T-003: done
  Verified: [what was confirmed at this checkpoint]

Starting: [next module or workflow name]
```

---

## When Tasks Fail or Produce Unexpected Output

1. Do not skip - investigate the root cause first
2. If a significant architectural change is needed, surface it to the user before continuing
3. Record any deviations in a `## Implementation Notes` section in `plan.md`

---

## Implementation Notes

Record significant decisions made during implementation in `plan.md`:

```markdown
## Implementation Notes

### T-NNN: [Task Name]
- [Decision made and why]
- [Deviation from original plan and reason]
```

---

## Gate

After all tasks are marked `[DONE]` and the application runs without errors, output:

```
---
[PASS] Step 8 - Implement complete  (Feature: NNN-feature-name)

Output: All tasks in tasks.md marked [DONE]

Review: The implementation is complete, but the feature is not yet verified.
   Step 9 (Test) will write tests against every acceptance criterion in spec.md
   and confirm the implementation is correct.

When ready:
  - "continue" or "next" -> proceed to Step 9 (Test)
  - "revise [what]" -> fix something in the implementation first
  - "stop" -> pause here; say "continue from Step 9" to resume
---
```

Do not mark the feature as complete here. Implementation without passing tests is unfinished work.

**Mode rule:** In detailed mode, wait at this gate. In auto mode, continue to Step 9 automatically after implementation succeeds.
