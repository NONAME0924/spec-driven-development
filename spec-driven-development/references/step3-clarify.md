# Step 3 - Clarify

## Purpose
Surface and resolve ambiguities in the specification **before** committing to a technical plan. Gaps found here cost far less than gaps found during implementation.

## When to Run
- After Step 2 (Specify) is complete
- Before Step 4 (Checklist) begins
- Can be re-run anytime new ambiguity is introduced

## Clarification Strategy

Work through the spec systematically. For each user story and requirement, check:

### Coverage Dimensions
1. **Happy path** - Is the primary flow fully described?
2. **Error states** - What happens when things go wrong?
3. **Edge cases** - What about empty states, limits, unusual inputs?
4. **Permissions** - Who can do what? What happens if unauthorized?
5. **Data lifecycle** - How is data created, modified, deleted, retained?
6. **Concurrency** - What if two users act simultaneously?
7. **Integration** - What external systems are touched?
8. **Necessity** - Is this required for the current Feature, or is it future/nice-to-have?
9. **Simpler default** - Can a standard behavior, native platform feature, existing module, or documented assumption avoid extra scope?

## Structured Clarification Process

Run through each user story and ask targeted questions. Present them as a numbered list so the user can answer efficiently.

### Example Output Format

> "I've reviewed the spec and found the following areas that need clarification before we plan:
>
> **US-001 (User Login):**
> 1. Should users be able to log in with social providers (Google, GitHub), or only email/password?
> 2. What should happen after 5 failed login attempts?
> 3. Is "remember me" / persistent sessions required?
>
> **US-003 (Photo Albums):**
> 4. Is there a maximum number of photos per album?
> 5. Can albums be shared publicly, or are they always private?
> 6. What image formats must be supported?
> 7. Is album sharing required in v1, or should it be deferred to a later Feature?
>
> Please answer as many as you can - for anything you're unsure about, I'll make a reasonable default assumption and note it in the spec."

## Recording Answers

Add a `## Clarifications` section to `spec.md`:

```markdown
## Clarifications

| ID | Question | Answer | Date |
|----|----------|--------|------|
| CL-001 | Can users log in with social providers? | Email/password only for now | YYYY-MM-DD |
| CL-002 | Max failed login attempts? | 5 attempts, then 15-min lockout | YYYY-MM-DD |
| CL-003 | Max photos per album? | Assumed: no limit (note for future) | YYYY-MM-DD |
```

## Recording Assumptions

For any question the user can't answer, make a reasonable assumption and record it:

```markdown
## Assumptions (Updated After Clarification)
- **AL-001:** No limit on photos per album (assumed); can be revisited in v2
- **AL-002:** Mobile-responsive but no native app required
```

Prefer the smallest safe assumption: private before public, no admin override before admin requirement, existing account model before new roles, native/browser behavior before custom UI, synchronous flow before background jobs unless the spec requires scale or latency guarantees.

## Checklist Validation

After clarification, validate the spec against this checklist and update `spec.md`:

```markdown
## Review & Acceptance Checklist
- [x] All user roles identified
- [x] Each user story has acceptance criteria
- [x] Error states documented
- [x] Permission model defined
- [x] Data lifecycle clarified
- [x] Future/nice-to-have scope moved to Non-Goals or Deferred
- [ ] Performance targets confirmed <- still open
```

## Gate

Show the updated `spec.md` (with Clarifications section filled in) to the user, then output the standard Gate block:

```
---
[PASS] Step 3 - Clarify complete

Output: Output: .specify/specs/NNN-feature-name/spec.md (updated with clarifications)

Review: Please review the output above. When ready, choose:
  - Type "continue" or "next" -> proceed to Step 4 (Checklist)
  - Type "revise [what]" -> address more clarifications before moving on
  - Type "stop" -> pause here; to resume say "continue from Step 4"
---
```

**Do not proceed to Step 4 until the user responds.**
