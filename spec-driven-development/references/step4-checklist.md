# Step 4 - Checklist

## Purpose
Audit the quality of `spec.md` **before entering technical planning**. The checklist acts like "unit tests for English" - it catches vague, unmeasurable, or missing requirements that would cause expensive rework during implementation.

Any [FAIL] items must be resolved by updating `spec.md` before proceeding to Step 5, unless the user explicitly accepts the risk. In auto mode, resolve clear checklist failures directly when they can be handled by applying the approved Step 2/3 requirements or by recording a conservative assumption.

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
- For every endpoint, command, event, or workflow stage, are inputs and outputs explicitly defined?
- Are request/response schemas, required fields, optional fields, validation rules, and error formats specified?
- Are stage transitions clear: what enters the stage, what it produces, and what state changes happen?

**Security:**
- Is authentication and authorisation explicitly defined?
- Is sensitive data (PII, passwords, tokens) handling specified?
- Are rate limiting and abuse prevention requirements present?

**Performance:**
- Are response time targets specified with percentile (p95, p99)?
- Are throughput and scalability targets defined?

**Lean SDD / Anti-Overengineering:**
- Does every requirement trace to a user story, goal, or risk?
- Are future-only features moved to Non-Goals or Deferred?
- Are there speculative settings, roles, dashboards, integrations, or extension points?
- Could an existing module, native platform feature, standard library, or already-installed dependency satisfy the need?
- Are there modules, APIs, data entities, or tasks that exist only "for later"?

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
- [ ] [FAIL] POST /api/albums input schema not specified (required fields, optional fields, validation)
- [ ] [FAIL] POST /api/albums response schema not specified (success body, status code, error body)
- [ ] [FAIL] Album creation workflow stages do not define inputs/outputs (frontend form -> API -> service -> repository -> response)

## Issues to Resolve
1. [ ] Add pagination requirement to album list
2. [ ] Specify file upload format
3. [ ] Define input/output schema for each endpoint or stage
4. [ ] Define standard error response format
```

### `checklists/minimalism.md` - Lean SDD quality

```markdown
# Minimalism Checklist
**Feature:** NNN-feature-name
**Audited:** YYYY-MM-DD

## Scope
- [x] Every Must requirement traces to a user story or goal
- [ ] [FAIL] FR-008 export dashboard has no current user story; move to Deferred or a later Feature
- [x] Nice-to-have sharing controls are listed under Non-Goals

## Architecture
- [x] Every module has a workflow and requirement
- [ ] [FAIL] NotificationAdapter has one caller and no external integration requirement; inline or defer
- [ ] [FAIL] AbstractRepository has one implementation; use concrete repository until a second implementation exists

## Dependencies / Platform
- [x] Existing auth module reused
- [ ] [FAIL] New date picker dependency requested; native date input satisfies the requirement
- [ ] [FAIL] Custom CSV parser proposed; standard library or existing dependency can handle it

## Tasks
- [x] Every task maps to a module/workflow/contract
- [ ] [FAIL] T-014 "prepare plugin architecture" is scaffolding for later; delete

## Issues to Resolve
1. [ ] Move unowned requirements to Non-Goals / Deferred
2. [ ] Remove or merge modules with no current workflow
3. [ ] Replace custom/dependency work with native, stdlib, existing code, or already-installed dependency where sufficient
4. [ ] Delete tasks that do not trace to approved scope
```

---

## Resolving Issues

For each [FAIL] item:
1. Update `spec.md` directly with the missing/corrected information
2. Mark the checklist item as `[x]` after resolving
3. Note the change in the `## Clarifications` table in `spec.md`

---

## Gate

Show or summarize all checklist files. Count [FAIL] items remaining. Then output:

```
---
[PASS] Step 4 - Checklist complete

Output: Output:
  - .specify/specs/NNN-feature-name/checklists/requirements.md
  - .specify/specs/NNN-feature-name/checklists/ux.md
  - .specify/specs/NNN-feature-name/checklists/security.md
  - .specify/specs/NNN-feature-name/checklists/api.md
  - .specify/specs/NNN-feature-name/checklists/minimalism.md

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

**Mode rule:** In detailed mode, wait at this gate. In auto mode, continue to Step 5 automatically when N = 0. If N > 0 and the issue requires a user decision, stop and ask for approval or clarification; otherwise resolve it in `spec.md`, update the checklist, and continue.
