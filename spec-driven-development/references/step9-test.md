# Step 9 - Verify

**Input:** Acceptance criteria, implemented changes, existing/new tests, execution environment.
**Output:** `test-report.md`, accurate task/epic state, completion explanation when scope is done.
**Completion:** Current in-scope criteria have passing evidence and required checks pass.
**Gate:** Use [Modes and Gates](../SKILL.md#modes-and-gates).

## Evidence

Map each acceptance criterion to appropriate evidence: an existing or new automated
test, a reproducible manual check, or inspection for non-executable deliverables.
Prefer automation for important behavior/regressions; do not write tests that merely
mirror low-impact wording or file structure. One meaningful test can cover several ACs,
and one AC may need several checks.

Run the project's required checks and the affected behavior checks. Broaden for shared
behavior, changed contracts, or remaining uncertainty. Avoid rerunning unchanged checks
that already passed on the current relevant state. Record actual commands, environment,
outcomes, and evidence locations; never infer a pass from an unexecuted test.

## Report Shape

```markdown
# Verification Report: [Feature]
**Result:** PASS / FAIL / BLOCKED
**Verified state:** [Commit if available, plus relevant uncommitted changes]

## Acceptance Evidence
| AC | Check or Test | Evidence / Command | Result |
|----|---------------|--------------------|--------|
| AC-001 | [Observable behavior] | [Reproducible check] | PASS / FAIL / NOT RUN / BLOCKED |

## Required Checks
[Commands, outcomes, relevant environment and scope]

## Limitations
[Missing access, unavailable environments, unverified behavior, or none]
```

NOT RUN and BLOCKED do not count as passing. An acceptable alternative verification
method must establish the same criterion, not just make the report green. User approval
does not transform a known failure into PASS.

## Resolution and Completion

Fix implementation or test defects within scope and rerun affected checks.
For requirement ambiguity, apply the shared decision policy; record authorized scope
changes explicitly. Do not wait for a new "fix all" instruction to repair normal defects.

Update `epic.md` to PASS only for the verified current Feature. For Goal, also verify
cross-feature user journeys and shared contracts against the assembled project before
declaring the batch complete; isolated feature passes are insufficient.

Auto and Detailed report the selected Feature's result without starting an unrequested Feature.
Goal continues dependency-ready Features and finishes at the requested project boundary.
Detailed explains the evidence and limitations more fully without an extra approval gate.
At scope completion, follow
[Completion](../SKILL.md#completion) to write `.specify/final-explanation.md` in the
user's language. If blocked, report the exact remaining work honestly.
