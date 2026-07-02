# Step 5 - Plan

## Purpose
Translate the approved specification into a concrete technical architecture and implementation strategy. This is the **first step** where technology choices are made.

In auto mode, the AI agent chooses the most useful planning format for the feature instead of forcing every artifact shape. Small or code-local features may need only a compact `plan.md`; data-heavy or API-heavy features should still produce `data-model.md`, `research.md`, and `contracts/` when they earn their place.

The plan must read like a project blueprint, not a flat list of documents. Start by defining the feature's modules, layers, workflows, and file layout. Every later artifact - data model, API contracts, tasks, and tests - must map back to that structure.

Lean SDD applies here: design the smallest correct project blueprint. Use existing repo structure, existing modules, native platform features, standard libraries, and already-installed dependencies before adding new modules, services, layers, or packages.

## What to Ask the User

> "Now that we have a clear spec, let's make technical decisions. Tell me:
> - What's your preferred tech stack? (or should I recommend one based on the requirements?)
> - Any hard constraints? (cloud provider, existing infrastructure, team expertise)
> - Any existing codebase to integrate with?"

If the user has no preference, recommend a tech stack based on the spec's requirements and explain your reasoning. In auto mode, proceed with the smallest reasonable choice unless the decision triggers user confirmation: major architecture change, paid service, new external dependency, migration, or a stack decision not already implied by the project.

## Research Phase

Before writing the plan, research any rapidly-changing or unfamiliar parts of the chosen stack:
- Check latest stable versions of key dependencies
- Identify known compatibility issues
- Note any recent breaking changes in the ecosystem
- Document findings in `research.md`

## Outputs

Produce the planning artifacts that fit this Feature in `.specify/specs/NNN-feature-name/`.

Always produce:
- `plan.md`

Produce only when useful:
- `data-model.md` - when the Feature adds or changes persistent data, schemas, entities, or relationships
- `research.md` - when the plan depends on rapidly-changing technology, unfamiliar APIs, dependency versions, compatibility risk, or external services
- `contracts/` - when the Feature exposes or consumes API/event contracts

## Lean Planning Ladder

Before adding any module, dependency, service, API, data entity, workflow stage, or task source, run this ladder:

1. Does this need to exist for the approved Feature?
2. Does the existing codebase already have a module, helper, type, schema, route, test pattern, or convention for it?
3. Does the standard library or native platform cover it?
4. Does an already-installed dependency cover it?
5. Can an existing module own it without becoming unclear?
6. Can the same behavior be represented as a contract, validation rule, or DB constraint instead of new code?
7. Only then create the minimum new module, dependency, or custom code.

Document any new module or dependency with a one-line reason in the Module Map or Tech Stack Decisions. If the reason is "might need later", delete or defer it.

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

## Project Structure
[Show the intended project/file organization for this Feature. Use the actual existing repo layout when modifying an existing project.]

```text
src/
|-- features/
|   `-- albums/
|       |-- ui/
|       |-- api/
|       |-- service/
|       |-- data/
|       `-- tests/
|-- shared/
|   |-- auth/
|   `-- errors/
`-- app/
```

## Module Map
[Group the Feature by module/domain ownership. Every module must have a reason to exist and a clear boundary.]

| Module | Layer(s) | Owns | Key Files | Depends On | Requirements |
|--------|----------|------|-----------|------------|--------------|
| Albums UI | Frontend | Forms, states, user interactions | `features/albums/ui/*` | Albums API client | US-001, US-002 |
| Albums API | API | HTTP contract, auth checks, validation | `features/albums/api/*` | Albums Service | US-001, FR-003 |
| Albums Service | Domain | Business rules and orchestration | `features/albums/service/*` | Albums Data | US-001, US-003 |
| Albums Data | Data | Persistence model and queries | `features/albums/data/*` | Database | FR-004 |

## Workflow Map
[Map user-visible workflows to modules, contracts, data, and tests. This prevents parallel, disconnected documents.]

| Workflow | User Story | Modules Involved | Contract(s) | Data | Tests |
|----------|------------|------------------|-------------|------|-------|
| Create album | US-001 | Albums UI -> Albums API -> Albums Service -> Albums Data | `POST /api/albums` | Album | unit, integration, acceptance |

## Tech Stack Decisions

| Layer | Technology | Version | Rationale | Lean Check |
|-------|-----------|---------|-----------|------------|
| Frontend | [e.g. React] | [18.x] | [Why chosen] | Reuse existing frontend stack |
| Backend | [e.g. FastAPI] | [0.x] | [Why chosen] | Reuse existing backend stack |
| Database | [e.g. PostgreSQL] | [16.x] | [Why chosen] | Required by persistent data |
| Auth | [e.g. existing auth module] | - | [Why chosen] | Reuse existing auth before adding new auth |
| Hosting | [e.g. existing platform] | - | [Why chosen] | Reuse existing deployment target |

## Component Breakdown

### [Component Name]
**Responsibility:** [What this component owns]
**Module:** [Module name from Module Map]
**Key files:**
- `src/[path]/[file]` - [purpose]

### [Component Name 2]
[repeat]

## Data Flow

[Describe how data moves through the system for the primary use cases]

## API Design Summary
[List key endpoints; full spec in `contracts/api-spec.md` if needed. Include enough shape here that implementation does not need to guess.]

| Module | Method | Path | Auth | Input | Output | Errors | Description |
|--------|--------|------|------|-------|--------|--------|-------------|
| Auth API | POST | /api/auth/login | None | `{ email, password }` | `{ user, token }` | `400`, `401` | Authenticate user |
| Albums API | GET | /api/albums | Required | Query: `{ page, limit }` | `{ items, page, total }` | `401` | List user's albums |

## Workflow Stage Contracts
[For each important stage, define what enters, what leaves, and what state changes. Use this for API workflows, event flows, CLI commands, background jobs, or agent pipelines.]

| Workflow | Stage | Module | Input | Output | State Change | Failure Output |
|----------|-------|--------|-------|--------|--------------|----------------|
| Create album | Frontend submit | Albums UI | Form values | Validated payload | None | Field errors |
| Create album | API handler | Albums API | JSON request + auth context | Service command | Request logged | HTTP error body |
| Create album | Service | Albums Service | Command object | Domain result | Business state updated | Domain error |
| Create album | Repository | Albums Data | Persistence DTO | Stored record | Database row written | Storage error |
| Create album | Response | Albums API | Domain result | HTTP response body | None | Standard error body |

## Security Model
[Authentication approach, authorization rules, data protection]

## Implementation Phases

### Phase 1: Foundation
[Project structure, module folders, shared primitives, data models, auth]

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

### 2. `data-model.md` - Data Schema (if needed)

```markdown
# Data Model: [Feature Name]

## Module Ownership
| Entity | Owning Module | Used By | Requirements |
|--------|---------------|---------|--------------|
| [Entity] | [Module] | [Modules/workflows] | [US/FR IDs] |

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

### 3. `research.md` - Tech Stack Research (if needed)

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
- `contracts/api-spec.json` - OpenAPI/Swagger spec with request schemas, response schemas, status codes, auth requirements, and standard error schema
- `contracts/events.md` - Event/message schemas (if async)
- `contracts/workflows.md` - Stage-by-stage input/output contracts for multi-step workflows when OpenAPI alone is not enough

## Validation Checklist

Before presenting the plan, verify:
- [ ] Every user story in the spec has a corresponding technical component
- [ ] Project Structure shows where code will live
- [ ] Module Map groups responsibilities by domain/layer instead of leaving components flat
- [ ] Every module has a current requirement/workflow and a clear reason to exist
- [ ] Workflow Map ties user stories to modules, contracts, data, and tests
- [ ] Data model covers all entities mentioned in requirements
- [ ] No speculative module, dependency, service, abstraction, or config exists only for future flexibility
- [ ] Existing codebase patterns, native features, stdlib, and already-installed dependencies were checked before adding new custom code/dependencies
- [ ] Authentication and authorization addressed
- [ ] API/input/output contracts define schemas, status codes, validation rules, and error bodies
- [ ] Important workflow stages define input, output, state change, and failure output
- [ ] Error handling strategy defined
- [ ] No over-engineering (question every component - does it earn its place?)
- [ ] Plan is consistent with the constitution

## Gate

Show the full contents or a concise summary of the planning artifacts, then output the standard Gate block:

```
---
[PASS] Step 5 - Plan complete

Output: Output:
  - .specify/specs/NNN-feature-name/plan.md
  - .specify/specs/NNN-feature-name/data-model.md (if created)
  - .specify/specs/NNN-feature-name/research.md (if created)

Review: Please review the output above - especially research.md for tech stack accuracy. When ready, choose:
  - Type "continue" or "next" -> proceed to Step 6 (Analyze)
  - Type "revise [what]" -> rework part of the plan before moving on
  - Type "stop" -> pause here; to resume say "continue from Step 6"
---
```

**Mode rule:** In detailed mode, wait at this gate. In auto mode, continue to Step 6 automatically unless a risk trigger appears: major architecture choice, paid service, new external dependency, migration, or stack decision the user has not already approved.
