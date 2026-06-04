# Step 2 - Specify

## Purpose
Transform the current Feature's scope (as defined in `epic.md`) into a structured specification with user stories and functional requirements. Focus entirely on **what** the system should do and **why** - never **how**.

Scope discipline is critical: this spec covers only the current Feature. If anything belongs to another Feature in `epic.md`, note it as out of scope and reference the correct Feature ID.

---

## What to Ask the User

Ask the user to describe the Feature in detail:
- What should it do?
- Who uses it?
- What does success look like?
- Are there any edge cases they already know about?

If the user has already described this in Step 0, use that as a starting point and ask only for clarification.

---

## Processing the User's Input

1. **Extract** - identify all distinct behaviours, actors, and workflows mentioned
2. **Expand** - infer logical consequences (e.g. "login" implies "logout", "session expiry")
3. **Scope check** - verify everything belongs to this Feature; move anything that doesn't to the Open Questions or reference the correct Feature
4. **Structure** - organise into user stories and requirements using the template below

---

## Create the Feature Directory

Create `.specify/specs/NNN-feature-name/` if it does not already exist.

---

## Output: `spec.md`

Create `.specify/specs/NNN-feature-name/spec.md` using `templates/spec-template.md`:

```markdown
# Feature Specification: [Feature Name]
**Feature ID:** NNN-feature-name
**Status:** Draft
**Created:** YYYY-MM-DD

## Overview
[1-2 paragraph summary of what this feature is and why it exists]

## Problem Statement
[The problem this feature solves for users]

## Goals
- [Measurable goal 1]
- [Measurable goal 2]

## Non-Goals (Out of Scope)
- [Explicitly excluded - reference the Feature that handles it where relevant]

## User Roles
| Role | Description |
|------|-------------|
| [Role] | [Who they are and what they do] |

## User Stories

### US-001: [Story Title]
**As a** [role]
**I want to** [action]
**So that** [benefit]

**Acceptance Criteria:**
- [ ] [Specific, testable criterion]
- [ ] [Error state criterion]
- [ ] [Edge case criterion]

## Functional Requirements

### FR-001: [Requirement Name]
**Priority:** Must / Should / Could / Won't
**Description:** [Unambiguous description]

## Non-Functional Requirements
| Category | Requirement |
|----------|-------------|
| Performance | [e.g. Responds in < 2s] |
| Accessibility | [e.g. WCAG 2.1 AA] |
| Security | [e.g. All data encrypted at rest] |

## Assumptions
- [Things assumed true but not yet confirmed]

## Open Questions
- [ ] [Unresolved question]

## Review & Acceptance Checklist
- [ ] All user roles identified
- [ ] Each user story has clear acceptance criteria
- [ ] All functional requirements are unambiguous
- [ ] Non-functional requirements specified
- [ ] Out-of-scope items explicitly listed
- [ ] No technology assumptions made
```

---

## Update `epic.md`

After creating `spec.md`, update the Active Feature line in `epic.md` and set this Feature's status to [IN PROGRESS] In Progress.

---

## Gate

Show the completed `spec.md` to the user, then output:

```
---
[PASS] Step 2 - Specify complete  (Feature: NNN-feature-name)

Output: Output: .specify/specs/NNN-feature-name/spec.md

Review: Please review the spec above. When ready:
  - "continue" or "next" -> proceed to Step 3 (Clarify)
  - "revise [what]" -> rework before moving on
  - "stop" -> pause here; say "continue from Step 3" to resume
---
```

Do not proceed to Step 3 until the user responds.
