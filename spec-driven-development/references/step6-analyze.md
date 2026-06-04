# Step 6 - Analyze

## Purpose
Cross-artifact consistency and coverage analysis. Ensure that the `spec.md`, `plan.md`, and `data-model.md` are fully aligned before task breakdown begins. Catch gaps now - not during implementation.

## When to Run
- After Step 5 (Plan) is approved
- Before Step 7 (Tasks) begins
- Can be re-run after significant plan changes

## Analysis Dimensions

### 1. Spec -> Plan Coverage
Every user story and functional requirement must have a corresponding implementation component.

Go through each item in `spec.md` and verify it appears in `plan.md`:

```
Checking coverage:
[PASS] US-001 (Login) -> Auth Service + JWT implementation
[PASS] US-002 (Create Album) -> Albums API + AlbumsService
[FAIL] US-005 (Export Photos) -> NOT FOUND IN PLAN
WARNING:  FR-008 (Rate Limiting) -> Mentioned but not designed
```

### 2. Plan -> Spec Alignment
Every component in `plan.md` should trace back to a requirement. Flag anything that has no spec justification (potential over-engineering).

```
Checking for orphaned components:
WARNING:  Redis cache layer -> No spec requirement for caching; confirm needed
[PASS] Photo storage service -> FR-003 (Store photos)
```

### 3. Data Model Coverage
Every entity and field mentioned in user stories must exist in `data-model.md`.

```
Checking data model:
[PASS] User entity -> US-001, US-002
[PASS] Album entity -> US-002, US-003
[FAIL] "album cover photo" mentioned in US-003 -> No field in Album entity
```

### 4. API Contract Coverage
Every action a user can perform (per the spec) must have a corresponding API endpoint (or UI action if no API layer).

### 5. Constitution Alignment
Check that the plan doesn't violate any principle from `constitution.md`:

```
Checking constitution compliance:
[PASS] Test coverage target: plan includes testing strategy
[PASS] Accessibility: plan references WCAG 2.1 AA
[FAIL] Commit format: not addressed in plan (add to tasks)
```

## Output: Analysis Report

Add an `## Analysis` section to the feature directory, or create `analysis.md`:

```markdown
# Cross-Artifact Analysis: [Feature Name]
**Analyzed:** YYYY-MM-DD

## Coverage Status

### Spec -> Plan: [N/N requirements covered]
| Requirement | Status | Notes |
|-------------|--------|-------|
| US-001 | [PASS] Covered | Auth Service |
| US-005 | [FAIL] Missing | Export feature not in plan |
| FR-008 | WARNING: Partial | Rate limiting mentioned but undesigned |

### Plan -> Spec: [N components, N orphaned]
| Component | Justification | Action |
|-----------|--------------|--------|
| Redis Cache | WARNING: No spec req | Confirm with user or remove |

### Data Model: [N/N entities covered]
| Entity/Field | Status | Notes |
|-------------|--------|-------|
| Album.cover_photo | [FAIL] Missing | Add to data model |

### Constitution Compliance
| Principle | Status | Notes |
|-----------|--------|-------|
| Test coverage | [PASS] | |
| Commit format | [FAIL] | Add task for CI setup |

## Required Actions Before Tasks
1. [ ] Add export functionality to `plan.md` or explicitly scope out in spec
2. [ ] Confirm Redis cache requirement with user
3. [ ] Add `cover_photo_id` field to Album entity in `data-model.md`
4. [ ] Design rate limiting in `plan.md`
```

## Resolving Issues

For each gap found:
- **Missing from plan** -> Either add it to the plan, or explicitly mark as out-of-scope in the spec
- **Orphaned component** -> Either trace it to a requirement, or remove it
- **Data model gap** -> Add the missing field/entity
- **Constitution violation** -> Fix the plan or add a task to address it

After resolving all issues, update the relevant documents before proceeding.

## Gate

Show the full analysis report and list any unresolved issues, then output the standard Gate block:

```
---
[PASS] Step 6 - Analyze complete

Output: Output: .specify/specs/NNN-feature-name/analysis.md
   Issues found: [N] | Auto-resolved: [M] | Needs your input: [K]

Review: Please review the analysis above. When ready, choose:
  - Type "continue" or "next" -> proceed to Step 7 (Tasks)
  - Type "revise [what]" -> address specific issues before moving on
  - Type "stop" -> pause here; to resume say "continue from Step 7"
---
```

**Do not proceed to Step 7 until the user responds.** If there are unresolved issues that need user input, explicitly list them before showing the Gate block.
