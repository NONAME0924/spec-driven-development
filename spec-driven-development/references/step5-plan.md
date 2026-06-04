# Step 5 - Plan

## Purpose
Translate the approved specification into a concrete technical architecture and implementation strategy. This is the **first step** where technology choices are made.

## What to Ask the User

> "Now that we have a clear spec, let's make technical decisions. Tell me:
> - What's your preferred tech stack? (or should I recommend one based on the requirements?)
> - Any hard constraints? (cloud provider, existing infrastructure, team expertise)
> - Any existing codebase to integrate with?"

If the user has no preference, recommend a tech stack based on the spec's requirements and explain your reasoning.

## Research Phase

Before writing the plan, research any rapidly-changing or unfamiliar parts of the chosen stack:
- Check latest stable versions of key dependencies
- Identify known compatibility issues
- Note any recent breaking changes in the ecosystem
- Document findings in `research.md`

## Outputs

Produce these files in `.specify/specs/NNN-feature-name/`:

### 1. `plan.md` - Main Implementation Plan

```markdown
# Implementation Plan: [Feature Name]
**Feature ID:** NNN-feature-name
**Tech Stack:** [Summary line]
**Last Updated:** YYYY-MM-DD

## Architecture Overview
[High-level description of the system architecture]

### Architecture Diagram (text)
```
[Client] -> [API Layer] -> [Service Layer] -> [Data Layer]
         <->                              <->
    [Auth Service]              [External APIs]
```

## Tech Stack Decisions

| Layer | Technology | Version | Rationale |
|-------|-----------|---------|-----------|
| Frontend | [e.g. React] | [18.x] | [Why chosen] |
| Backend | [e.g. FastAPI] | [0.x] | [Why chosen] |
| Database | [e.g. PostgreSQL] | [16.x] | [Why chosen] |
| Auth | [e.g. JWT] | - | [Why chosen] |
| Hosting | [e.g. Vercel] | - | [Why chosen] |

## Component Breakdown

### [Component Name]
**Responsibility:** [What this component owns]
**Key files:**
- `src/[path]/[file]` - [purpose]

### [Component Name 2]
[repeat]

## Data Flow

[Describe how data moves through the system for the primary use cases]

## API Design Summary
[List key endpoints; full spec in `contracts/api-spec.md` if needed]

| Method | Path | Description |
|--------|------|-------------|
| POST | /api/auth/login | Authenticate user |
| GET | /api/albums | List user's albums |

## Security Model
[Authentication approach, authorization rules, data protection]

## Implementation Phases

### Phase 1: Foundation
[Core infrastructure, data models, auth]

### Phase 2: Core Features
[Primary user stories]

### Phase 3: Polish & Edge Cases
[Error handling, performance, accessibility]

## Risks & Mitigations
| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| [Risk 1] | Medium | High | [How to address] |

## Dependencies & Prerequisites
- [Tool/service that must exist before implementation starts]
```

### 2. `data-model.md` - Data Schema

```markdown
# Data Model: [Feature Name]

## Entities

### [Entity Name]
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| id | UUID | Yes | Primary key |
| created_at | Timestamp | Yes | Creation time |
| [field] | [type] | [Y/N] | [description] |

### Relationships
- [Entity A] has many [Entity B] (via [join table/foreign key])

## Database Schema (SQL / NoSQL structure)
[Include schema DDL or document structure as appropriate]

## Indexes
[List indexes and their purpose]
```

### 3. `research.md` - Tech Stack Research

```markdown
# Technical Research: [Feature Name]

## Stack Versions (Confirmed)
| Package | Version Used | Latest | Notes |
|---------|-------------|--------|-------|
| [package] | [x.y.z] | [x.y.z] | [compatibility notes] |

## Key Findings
[Important discoveries that affected the plan]

## Alternatives Considered
| Alternative | Why Rejected |
|-------------|-------------|
| [Option] | [Reason] |

## Open Technical Questions
- [ ] [Question that needs further investigation during implementation]
```

### 4. `contracts/` (if needed)

For systems with APIs:
- `contracts/api-spec.json` - OpenAPI/Swagger spec
- `contracts/events.md` - Event/message schemas (if async)

## Validation Checklist

Before presenting the plan, verify:
- [ ] Every user story in the spec has a corresponding technical component
- [ ] Data model covers all entities mentioned in requirements
- [ ] Authentication and authorization addressed
- [ ] Error handling strategy defined
- [ ] No over-engineering (question every component - does it earn its place?)
- [ ] Plan is consistent with the constitution

## Gate

Show the full contents of `plan.md`, `data-model.md`, and `research.md` to the user, then output the standard Gate block:

```
---
[PASS] Step 5 - Plan complete

Output: Output:
  - .specify/specs/NNN-feature-name/plan.md
  - .specify/specs/NNN-feature-name/data-model.md
  - .specify/specs/NNN-feature-name/research.md

Review: Please review the output above - especially research.md for tech stack accuracy. When ready, choose:
  - Type "continue" or "next" -> proceed to Step 6 (Analyze)
  - Type "revise [what]" -> rework part of the plan before moving on
  - Type "stop" -> pause here; to resume say "continue from Step 6"
---
```

**Do not proceed to Step 6 until the user responds.**
