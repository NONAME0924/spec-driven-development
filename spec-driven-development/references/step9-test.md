# Step 9 - Test

## Purpose
Write and verify tests that confirm the implementation satisfies every acceptance criterion in `spec.md`. The Feature is not complete until all tests pass.

Tests in this step are spec-driven: each test traces directly to a user story or acceptance criterion. If it is in the spec, it must be tested. If a test fails, either the implementation is wrong or the spec needs updating - both require resolution before closing.

---

## Pre-Conditions

Before starting, verify:
- [ ] Step 8 (Implement) is complete - all tasks in `tasks.md` marked `[DONE]`
- [ ] The application works end-to-end without errors
- [ ] `spec.md` is the final approved version with no open [FAIL] checklist items

---

## Test Strategy

### Map Every Acceptance Criterion to a Test

Go through every user story in `spec.md` and map each acceptance criterion to at least one test:

```
US-001 AC-1: "User can log in with valid email and password"
  -> test: valid credentials are accepted and a session is established
  -> test: user is redirected to the correct page after login

US-001 AC-2: "Invalid password shows error message"
  -> test: wrong password is rejected with a clear error
  -> test: the error message is visible to the user
```

### Test Layers

Write tests at the appropriate layer for each criterion:

| Layer | What it tests |
|-------|--------------|
| **Unit** | Individual functions and business logic in isolation |
| **Integration** | How components work together (e.g. API + database) |
| **Acceptance** | Full user flows from the user's perspective |

Each acceptance criterion must have at least one test. Prefer the lowest layer that meaningfully validates the criterion.

---

## Process

### 1. Build the Coverage Map

Before writing any tests, create the mapping in `test-report.md`:

```markdown
## Coverage Map

| AC ID | Acceptance Criterion | Test Description | Layer | Status |
|-------|---------------------|-----------------|-------|--------|
| US-001 AC-1 | Valid credentials accepted | valid login succeeds | Integration | [TODO] |
| US-001 AC-2 | Invalid password shows error | wrong password rejected | Integration | [TODO] |
| US-002 AC-1 | User can create album | create album success | Integration | [TODO] |
```

### 2. Write the Tests

For each row in the coverage map, write a test that:
- Sets up the required state (arrange)
- Performs the action described in the acceptance criterion (act)
- Asserts the outcome matches the criterion exactly (assert)

Write tests using whatever testing framework is specified in `plan.md`.

### 3. Verify All Tests Pass

After writing all tests, verify they all pass. Update the Status column in the Coverage Map:

| Status | Meaning |
|--------|---------|
| [TODO] | Not yet written |
| [TESTING] | Written, not yet verified |
| [PASS] | Passes |
| [FAIL] | Fails - requires action |

### 4. When Tests Fail

A failing test means one of three things - determine which before acting:

1. **Implementation bug** -> fix the code, re-verify
2. **Test is wrong** -> fix the test logic, re-verify
3. **Spec was ambiguous** -> stop and get user approval before changing approved requirements, then fix implementation or test accordingly

Never mark a failing test as done without user approval. Every failing test against a spec criterion is a real defect.

---

## Output: `test-report.md`

Create `.specify/specs/NNN-feature-name/test-report.md`:

```markdown
# Test Report: [Feature Name]
**Feature ID:** NNN-feature-name
**Date:** YYYY-MM-DD
**Result:** [PASS] ALL PASS / [FAIL] FAILURES REMAIN

## Summary
| Layer | Total | Passing | Failing |
|-------|-------|---------|---------|
| Unit | [N] | [N] | 0 |
| Integration | [N] | [N] | 0 |
| Acceptance | [N] | [N] | 0 |
| **Total** | **[N]** | **[N]** | **0** |

## Coverage Map

| AC ID | Acceptance Criterion | Test Description | Layer | Result |
|-------|---------------------|-----------------|-------|--------|
| US-001 AC-1 | Valid credentials accepted | valid login succeeds | Integration | [PASS] |
| US-001 AC-2 | Invalid password shows error | wrong password rejected | Integration | [PASS] |

## Untested Criteria
[List any acceptance criteria not covered by tests and the reason why]

## Notes
[Observations, edge cases found during testing, areas needing future attention]
```

---

## Gate

Show the full `test-report.md` to the user, then output:

```
---
[If all tests pass:]

[SUCCESS] Step 9 - Test complete  (Feature: NNN-feature-name)

Output: Output: .specify/specs/NNN-feature-name/test-report.md
   Tests: [N] passing / 0 failing
   Coverage: [N] acceptance criteria verified

[PASS] Feature NNN-feature-name is COMPLETE.
   Every acceptance criterion in spec.md has a passing test.

Updating epic.md -> marking NNN-feature-name as [PASS] Complete.

Next:
  - "continue" or "next" -> begin the next Feature (NNN) at Step 2
  - "stop" -> pause here; say "continue from Feature NNN" to resume
---

[If any tests fail:]

[FAIL] Step 9 - Test incomplete  (Feature: NNN-feature-name)

Output: Output: .specify/specs/NNN-feature-name/test-report.md
   Tests: [N] passing / [M] failing

The following acceptance criteria have failing tests:
  - US-NNN AC-N: [criterion] -> [failure reason]

The feature is NOT complete. Choose how to proceed:
  - "fix [test ID]" -> investigate and fix that specific failure
  - "fix all" -> work through all failures systematically
  - "revise spec [AC ID]" -> the spec was ambiguous; update it first
  - "stop" -> pause here; say "continue from Step 9" to resume
---
```

The Feature is only complete when `test-report.md` shows 0 failing tests and `epic.md` is updated to [PASS].

## Final Explanation

When the active requested scope is complete, create or update `.specify/final-explanation.md` in the user's language.

- If this is a single Feature request, explain that Feature.
- If this completes the last Feature in the project, explain the whole project.
- If more Features remain, note the completed Feature and the next pending Feature, but do not claim the whole project is complete.

Include:
- What was completed
- How to use or run it
- Important project/module structure
- Test result summary
- Known limitations or deferred scope

**Mode rule:** In detailed mode, wait at this final gate. In auto mode, stop here and report the final result before starting the next Feature. Do not begin another Feature without user direction.
