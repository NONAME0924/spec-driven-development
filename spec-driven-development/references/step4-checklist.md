# Step 4 - Checklist

## Purpose
Audit the quality of `spec.md` **before entering technical planning**. The checklist acts like "unit tests for English" - it catches vague, unmeasurable, or missing requirements that would cause expensive rework during implementation.

**This step is a hard gate before Plan.** Any [FAIL] items must be resolved by updating `spec.md` before proceeding to Step 5.

## When to Run
- After Step 3 (Clarify) is complete
- Before Step 5 (Plan) begins
- Can be re-run any time the spec changes significantly

---

## How It Works

Read through the entire `spec.md` and evaluate every user story, acceptance criterion, and functional requirement against the quality dimensions below. Then produce one checklist file per domain.

---

## Quality Dimensions to Check

### 1. Completeness
- Does every user story have at least 3 acceptance criteria?
- Are all user roles defined?
- Are error states and edge cases covered?
- Are non-functional requirements (performance, security, accessibility) present?
- Is the "out of scope" section explicitly defined?

### 2. Clarity & Measurability
- Are all requirements **specific and unambiguous**?
- Are all qualitative terms **quantified**?
  - [FAIL] "fast loading" -> [PASS] "page loads in < 2s (p95)"
  - [FAIL] "many users" -> [PASS] "up to 10,000 concurrent users"
  - [FAIL] "secure" -> [PASS] "all data encrypted at rest with AES-256"
  - [FAIL] "easy to use" -> [PASS] "user can complete onboarding in < 3 minutes"
- Are acceptance criteria **testable** (can a QA engineer write a test for it)?

### 3. Consistency
- Do user stories contradict each other?
- Are the same terms used consistently throughout? (e.g., "user" vs "member" vs "account")
- Do acceptance criteria align with the stated goals?

### 4. Feasibility
- Are there any requirements that seem technically impossible or contradictory?
- Are dependencies on external systems identified?

### 5. Domain-Specific Checks

**UX / User Experience:**
- Are all user-facing flows described end-to-end?
- Are empty states, loading states, and error states specified?
- Are accessibility requirements stated?

**API / Integration:**
- Are all external integrations identified?
- Are data formats and protocols specified?
- Are authentication requirements for each endpoint stated?

**Security:**
- Is authentication and authorisation explicitly defined?
- Is sensitive data (PII, passwords, tokens) handling specified?
- Are rate limiting and abuse prevention requirements present?

**Performance:**
- Are response time targets specified with percentile (p95, p99)?
- Are throughput and scalability targets defined?

---

## Output: Checklist Files

Create `.specify/specs/NNN-feature-name/checklists/` and produce these files:

### `checklists/requirements.md` - Core requirements quality

```markdown
# Requirements Checklist
**Feature:** NNN-feature-name
**Audited:** YYYY-MM-DD
**Status:** PASS / FAIL

## Completeness
- [x] All user roles defined
- [x] Every user story has >= 3 acceptance criteria
- [ ] [FAIL] Error states missing for US-003 (photo upload failure not specified)
- [x] Non-functional requirements present
- [ ] [FAIL] Out-of-scope section missing

## Clarity & Measurability
- [ ] [FAIL] US-001 AC-2: "responds quickly" - needs specific time target
- [x] US-002: all acceptance criteria are testable
- [ ] [FAIL] FR-004: "supports large files" - define maximum file size

## Consistency
- [x] Terminology consistent throughout
- [x] No contradictory requirements found

## Issues to Resolve Before Planning
1. [ ] Add error state for photo upload failure (US-003)
2. [ ] Define "responds quickly" in US-001 AC-2 with a time target
3. [ ] Define maximum file size in FR-004
4. [ ] Add explicit out-of-scope section
```

### `checklists/ux.md` - User experience quality

```markdown
# UX Checklist
**Feature:** NNN-feature-name
**Audited:** YYYY-MM-DD

## User Flows
- [x] Happy path described end-to-end for all user stories
- [ ] [FAIL] Empty state not specified (what does user see with no albums?)
- [x] Loading state mentioned in US-002
- [ ] [FAIL] Error messages not described - what text does the user see?

## Accessibility
- [ ] [FAIL] No accessibility requirements stated - add WCAG level

## Issues to Resolve
1. [ ] Define empty state for album list
2. [ ] Specify error message copy for upload failure
3. [ ] Add accessibility standard to NFRs
```

### `checklists/security.md` - Security quality

```markdown
# Security Checklist
**Feature:** NNN-feature-name
**Audited:** YYYY-MM-DD

## Authentication & Authorisation
- [x] Auth requirement stated (JWT)
- [x] Users can only access their own albums (FR-007)
- [ ] [FAIL] Admin access not defined - can admins see all albums?

## Data Handling
- [x] Password hashing mentioned in constitution
- [ ] [FAIL] Photo storage access control not specified (are URLs guessable?)

## Issues to Resolve
1. [ ] Define admin access model
2. [ ] Specify photo URL access control (signed URLs or auth-gated)
```

### `checklists/api.md` - API / integration quality (if applicable)

```markdown
# API Checklist
**Feature:** NNN-feature-name
**Audited:** YYYY-MM-DD

## Endpoints
- [x] All CRUD operations for albums specified
- [ ] [FAIL] Pagination not specified for album list endpoint

## Data Formats
- [x] Request/response format mentioned (JSON)
- [ ] [FAIL] File upload format not specified (multipart? base64?)

## Issues to Resolve
1. [ ] Add pagination requirement to album list
2. [ ] Specify file upload format
```

---

## Resolving Issues

For each [FAIL] item:
1. Update `spec.md` directly with the missing/corrected information
2. Mark the checklist item as `[x]` after resolving
3. Note the change in the `## Clarifications` table in `spec.md`

---

## Gate

Show all checklist files to the user. Count [FAIL] items remaining. Then output:

```
---
[PASS] Step 4 - Checklist complete

Output: Output:
  - .specify/specs/NNN-feature-name/checklists/requirements.md
  - .specify/specs/NNN-feature-name/checklists/ux.md
  - .specify/specs/NNN-feature-name/checklists/security.md
  - .specify/specs/NNN-feature-name/checklists/api.md

WARNING:  Issues found: [N] items marked [FAIL]

[If N > 0:]
WARNING: The following must be resolved in spec.md before proceeding to Plan:
  1. [Issue description]
  2. [Issue description]

Please update spec.md for each item above, then type "continue" to re-run the checklist,
or "override [reason]" to proceed despite open issues (not recommended for production).

[If N = 0:]
[SUCCESS] All checklist items passed - spec is ready for technical planning.

Review: When ready, choose:
  - Type "continue" or "next" -> proceed to Step 5 (Plan)
  - Type "revise [what]" -> refine the spec further
  - Type "stop" -> pause here; to resume say "continue from Step 5"
---
```

**Special rule:** If there are unresolved [FAIL] items and the user types "continue", remind them of the open issues and ask for explicit confirmation before proceeding. This gate is a quality checkpoint, not a formality.
