# Step 8 - Implement

## Purpose
Execute the approved task list in `tasks.md` systematically to produce working code. Follow every task in order, verify each one is complete before moving on, and keep the user informed at each checkpoint.

---

## Pre-Implementation Checks

Before starting, verify all prerequisites exist and are approved:

- [ ] `.specify/memory/constitution.md` - exists
- [ ] `.specify/specs/NNN-feature-name/spec.md` - approved
- [ ] `.specify/specs/NNN-feature-name/plan.md` - approved
- [ ] `.specify/specs/NNN-feature-name/tasks.md` - approved
- [ ] No unresolved [FAIL] items in any checklist

If any are missing or unapproved, return to the appropriate earlier step.

---

## Execution Strategy

### Task Ordering
1. Read `tasks.md` fully before starting any task
2. Begin with Phase 1 (Foundation) tasks
3. Respect all `Requires: T-NNN` dependencies
4. Tasks marked `[P]` may be worked on concurrently where practical
5. Verify each Checkpoint before moving to the next phase

### Per-Task Pattern

For each task:
1. **Read** the task's Action and Done When criteria
2. **Confirm** all dependencies are marked `[DONE]`
3. **Implement** - write the code as specified
4. **Verify** - check the Done When criterion is satisfied
5. **Mark** the task as `[DONE]` in `tasks.md`

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

After each phase checkpoint, report progress to the user:

```
[PASS] Checkpoint [N] passed - [Phase Name]
  T-001: done
  T-002: done
  T-003: done
  Verified: [what was confirmed at this checkpoint]

Starting: Starting [next phase name]
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
