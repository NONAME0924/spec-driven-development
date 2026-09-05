# Step 0 - Epic

**Input:** User request, existing project instructions, repository layout, and `.specify/epic.md` if present.
**Output:** `.specify/epic.md` with a feature map and execution state.
**Completion:** Requested scope has clear boundaries, dependencies, and a reviewable delivery order.
**Gate:** Use [Modes and Gates](../SKILL.md#modes-and-gates).

## Procedure

Inspect the existing project before decomposing it. Use information already supplied;
ask only for missing facts that prevent a useful scope proposal. A small request can
be one Feature. A Feature delivers a coherent outcome and can be verified once its
declared dependencies exist; it need not be independent of every other Feature.

For each Feature, record the goal, in/out of scope, dependencies, and delivered outcome.
Order by prerequisites, early user value, and significant technical uncertainty.
Do not add a backlog of imagined future features.

Preserve existing IDs and history. New IDs use the next unused number. Corrections
can update an existing Feature and reopen its verification; a distinct new capability
can be a follow-on Feature. Do not preserve a stale PASS status after changing the
behavior it described. On an unchanged resume, read execution state and continue.

## Artifact Shape

```markdown
# Epic: [Project]
## Outcome and Constraints
[Requested result, audience, boundaries, known repository constraints]

## Feature Map
| ID | Outcome | In Scope | Out of Scope | Depends On | Status |
|----|---------|----------|--------------|------------|--------|
| 001-feature | [Deliverable] | [Behaviors] | [Excluded] | None | TODO |

## Delivery Order
[Feature order and dependency rationale]

## Execution State
- Requested scope: [Specs only / selected Feature / whole project]
- Mode: [Pending / Goal / Auto / Detailed]
- Current stage and Feature: [Location]
- Approvals: [Decision, scope, user response reference]
- Pending decisions: [Blocking question or none]
- Artifacts: [Links]
- Next action: [Concrete continuation]

## Scope Changes
[Only meaningful changes, reasons, and affected Features]
```

Statuses: TODO, IN PROGRESS, TESTING, PASS, BLOCKED, DEFERRED.
PASS requires evidence for current acceptance criteria. DEFERRED must distinguish
out-of-scope ideas from requested work; removing requested work needs a scope decision.

After creating or materially updating the breakdown, present it and apply the mode
gate. Once resolved, reuse/create the shared constitution; then enter the selected
mode. Goal's next phase is a spec sweep, not Feature 001 implementation.
