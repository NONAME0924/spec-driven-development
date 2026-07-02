# Step 6 - Analyze

## Purpose
Cross-artifact consistency and coverage analysis. Ensure that the `spec.md`, `plan.md`, and `data-model.md` are fully aligned before task breakdown begins. Catch gaps now - not during implementation.

## When to Run
- After Step 5 (Plan) is complete or approved, depending on the active mode
- Before Step 7 (Tasks) begins
- Can be re-run after significant plan changes

## Analysis Dimensions

### 0. Project Shape / Information Architecture
Verify the plan is organized as a project blueprint, not a flat list.

Check:
- `Project Structure` exists and matches the existing repo when applicable
- `Module Map` exists and every component belongs to exactly one module or a justified shared/cross-cutting area
- `Workflow Map` exists and ties user stories to modules, contracts, data, and tests
- Data model, API contracts, workflow contracts, tasks, and tests all reference modules/workflows instead of floating independently

Flag:
```
[FAIL] API endpoints listed but not assigned to modules
[FAIL] tasks.md has layer-only phases but no module/workflow grouping
WARNING: Shared helper has no owning module or cross-cutting justification
```

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

### Lean SDD / Overengineering Check
Flag complexity that is not earned by the approved spec:

- New dependency where native platform, standard library, existing code, or installed dependency is enough
- Interface, factory, adapter, plugin system, config flag, or extension point with one implementation and no current requirement
- Module with no workflow, contract, data, or test ownership
- Data entity or field that supports only future scope
- Task that scaffolds "later" instead of delivering the current Feature
- Custom code replacing a reliable built-in feature

```
[FAIL] AbstractAlbumRepository has one implementation and no second storage requirement
[FAIL] date picker dependency duplicates native date input for the approved requirement
WARNING: Redis cache has no performance target or measured need
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
Every action a user can perform (per the spec) must have a corresponding API endpoint, command, event, or UI action if no API layer exists.

For each contract, verify:
- Input schema exists: body/query/path parameters, required fields, optional fields, validation rules
- Output schema exists: success body, status code, headers if relevant
- Error schema exists: error body shape, status codes, validation errors, auth errors
- Auth and permission requirements are explicit
- Each important workflow stage defines input, output, state change, and failure output

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

### Project Shape
| Item | Status | Notes |
|------|--------|-------|
| Project Structure | [PASS] | Uses existing repo layout |
| Module Map | [FAIL] | Auth endpoints not assigned to a module |
| Workflow Map | WARNING: Partial | Create Album has no test mapping |

### Lean SDD
| Item | Status | Action |
|------|--------|--------|
| New dependency | [FAIL] Replace date picker with native input |
| AbstractRepository | [FAIL] Inline concrete repository until a second implementation exists |
| Redis cache | WARNING: Remove unless performance target requires it |

### Data Model: [N/N entities covered]
| Entity/Field | Status | Notes |
|-------------|--------|-------|
| Album.cover_photo | [FAIL] Missing | Add to data model |

### API / Workflow Contracts: [N/N actions covered]
| Action or Stage | Status | Notes |
|-----------------|--------|-------|
| POST /api/albums input | [PASS] | Body schema defined |
| POST /api/albums errors | [FAIL] | Missing validation error body |
| Album creation service stage | WARNING: Partial | Input defined, state change missing |

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
5. [ ] Assign every component, contract, and task to a Module Map or Workflow Map entry
6. [ ] Remove or justify speculative abstractions, dependencies, modules, config, and tasks
```

## Resolving Issues

For each gap found:
- **Missing from plan** -> Either add it to the plan, or explicitly mark as out-of-scope in the spec
- **Orphaned component** -> Either trace it to a requirement, or remove it
- **Orphaned artifact** -> Attach it to a module/workflow, or remove it if it has no owner
- **Data model gap** -> Add the missing field/entity
- **Contract gap** -> Add the missing input, output, error format, auth rule, or workflow stage state change
- **Lean SDD violation** -> Delete it, merge it, replace it with existing/native/stdlib behavior, or document the current requirement that earns it
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

**Mode rule:** In detailed mode, wait at this gate. In auto mode, resolve straightforward inconsistencies directly and continue to Step 7. Stop only when an unresolved issue changes approved requirements, introduces a risky architecture change, or needs user judgment.
