# Feature Specification: [Feature Name]
**Feature ID:** NNN-feature-name
**Status:** Draft | In Review | Approved | Implemented
**Created:** YYYY-MM-DD
**Last Updated:** YYYY-MM-DD

---

## Overview
[1-2 paragraph summary: what this feature is and why it exists]

## Problem Statement
[The specific problem this feature solves. Who experiences it? How often? What is the current workaround?]

## Goals
- [ ] [Measurable, verifiable goal 1]
- [ ] [Measurable, verifiable goal 2]

## Non-Goals (Out of Scope)
- [Item explicitly excluded - be specific to prevent scope creep]

---

## User Roles
| Role | Description | Volume |
|------|-------------|--------|
| [Role 1] | [Who they are and what they do] | [e.g. Primary user] |
| [Role 2] | [Who they are and what they do] | [e.g. Admin only] |

---

## User Stories

### US-001: [Story Title]
**As a** [role]
**I want to** [action]
**So that** [benefit / value delivered]

**Acceptance Criteria:**
- [ ] [Specific, testable - use "Given/When/Then" or plain assertions]
- [ ] [Happy path criterion]
- [ ] [Error state criterion]
- [ ] [Edge case criterion]

**Priority:** Must / Should / Could / Won't
**Notes:** [Dependencies, open questions, or design constraints]

---

### US-002: [Story Title]
**As a** [role]
**I want to** [action]
**So that** [benefit]

**Acceptance Criteria:**
- [ ] ...

**Priority:** Must / Should / Could / Won't

---

## Functional Requirements

### FR-001: [Requirement Name]
**Priority:** Must / Should / Could / Won't
**Related Stories:** US-001
**Description:** [Unambiguous description of the system behaviour]
**Constraints:** [Performance limits, data limits, validation rules]

### FR-002: [Requirement Name]
**Priority:** Must
**Related Stories:** US-002
**Description:** ...

---

## Non-Functional Requirements
| Category | Requirement | Measurement |
|----------|-------------|-------------|
| Performance | [e.g. All pages load < 2s] | [p95 under normal load] |
| Accessibility | [e.g. WCAG 2.1 AA compliant] | [Automated + manual audit] |
| Security | [e.g. All PII encrypted at rest] | [Security review] |
| Reliability | [e.g. 99.9% uptime] | [Monthly measurement] |
| Scalability | [e.g. Support 10,000 concurrent users] | [Load test] |

---

## Assumptions
- **AS-001:** [Something assumed true that hasn't been confirmed]
- **AS-002:** [Another assumption]

## Open Questions
- [ ] **OQ-001:** [Question] - *Owner: [name/team], Due: YYYY-MM-DD*
- [ ] **OQ-002:** [Question]

---

## Clarifications
| ID | Question | Answer | Date |
|----|----------|--------|------|
| CL-001 | [Question asked] | [Answer received] | YYYY-MM-DD |

---

## Review & Acceptance Checklist
- [ ] All user roles identified and described
- [ ] Each user story has at least 3 acceptance criteria
- [ ] Error states and edge cases documented
- [ ] Permission model explicitly defined
- [ ] Data lifecycle (create/read/update/delete) covered
- [ ] Non-functional requirements specified with measurable targets
- [ ] Out-of-scope items explicitly listed
- [ ] No technology assumptions made (tech stack is for the plan)
- [ ] All open questions have owners and due dates
- [ ] Spec reviewed with stakeholder(s)
