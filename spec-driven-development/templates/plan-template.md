# Implementation Plan: [Feature Name]
**Feature ID:** NNN-feature-name
**Status:** Draft | Approved | In Progress | Complete
**Created:** YYYY-MM-DD
**Last Updated:** YYYY-MM-DD

---

## Architecture Overview
[2-3 paragraphs: overall system design, key architectural decisions, and the rationale]

### System Diagram
```
[Client / Browser]
      |
      v
[Frontend - Framework]
      |
      v
[API Gateway / BFF]
      |
      |---> [Service A]---> [Database]
      |
      `---> [Service B]---> [External API]
```

---

## Project Structure

```text
src/
|-- features/
|   `-- [feature-name]/
|       |-- ui/
|       |-- api/
|       |-- service/
|       |-- data/
|       `-- tests/
|-- shared/
|   |-- auth/
|   |-- errors/
|   `-- validation/
`-- app/
```

Use the existing project layout when modifying an existing codebase. Do not invent a new layout unless the current project has no clear structure.

---

## Module Map

| Module | Layer(s) | Owns | Key Files | Depends On | Requirements | Lean Check |
|--------|----------|------|-----------|------------|--------------|------------|
| [Feature] UI | Frontend | Screens, forms, user states | `src/features/[feature]/ui/*` | [Feature] API Client | US-NNN | Required by workflow; uses existing UI patterns |
| [Feature] API | API | Routes/controllers, auth checks, validation | `src/features/[feature]/api/*` | [Feature] Service | US-NNN, FR-NNN | Required contract boundary |
| [Feature] Service | Domain | Business rules and orchestration | `src/features/[feature]/service/*` | [Feature] Data | US-NNN | Keeps business logic out of controllers |
| [Feature] Data | Data | Persistence model and queries | `src/features/[feature]/data/*` | Database | FR-NNN | Required only if persistent data changes |

---

## Workflow Map

| Workflow | User Story | Modules Involved | Contract(s) | Data | Tests |
|----------|------------|------------------|-------------|------|-------|
| [Primary workflow] | US-NNN | UI -> API -> Service -> Data | `POST /api/...` | [Entity] | unit, integration, acceptance |

---

## Tech Stack

| Layer | Technology | Version | Rationale | Lean Check |
|-------|-----------|---------|-----------|------------|
| Frontend | [e.g. React] | [18.x] | [Why this over alternatives] | Already in project / required by existing app |
| Styling | [e.g. Tailwind CSS] | [3.x] | | Reuse existing styling system |
| Backend | [e.g. FastAPI] | [0.x] | | Already in project / smallest fit |
| Database | [e.g. PostgreSQL] | [16.x] | | Required by persistent data |
| Auth | [e.g. existing auth module] | | | Reuse existing auth before adding new auth |
| File Storage | [e.g. S3] | | | Include only if spec requires file persistence |
| Hosting | [e.g. existing platform] | | | Reuse existing deployment target |
| Testing | [e.g. Vitest + Playwright] | | | Use existing test stack |

---

## Component Breakdown

### [Component Name - e.g. AuthService]
**Module:** [Module from Module Map]
**Layer:** Service
**Responsibility:** [Single sentence - what this component owns]
**Key files:**
- `src/services/auth.service.ts` - Core business logic
- `src/services/auth.service.test.ts` - Unit tests
**Interfaces:**
- `register(email, password) -> User`
- `login(email, password) -> JWT`
**Dependencies:** UserRepository, PasswordHasher

### [Component Name - e.g. AlbumRepository]
**Layer:** Data
**Responsibility:** ...

---

## Data Flow

### Primary Flow: [e.g. User Creates Album]
```
1. User fills form -> Frontend validates input
2. POST /api/albums -> API validates + auth check
3. AlbumService.create() -> validates business rules
4. AlbumRepository.insert() -> writes to DB
5. Returns Album object -> Frontend updates UI
```

### Error Flow: [e.g. Validation Failure]
```
1. API receives invalid payload
2. Zod schema validation fails -> returns 400 { error, fields }
3. Frontend displays inline field errors
```

---

## API Design

| Module | Method | Path | Auth | Input | Output | Errors | Description |
|--------|--------|------|------|-------|--------|--------|-------------|
| Auth API | POST | /api/auth/login | None | `{ email, password }` | `{ user, token }` | `400`, `401` | Authenticate user |
| Auth API | POST | /api/auth/register | None | `{ email, password, name }` | `{ user, token }` | `400`, `409` | Create account |
| Albums API | GET | /api/albums | Required | Query: `{ page, limit }` | `{ items, page, total }` | `401` | List user's albums |
| Albums API | POST | /api/albums | Required | `{ title, description? }` | `{ album }` | `400`, `401` | Create album |
| Albums API | GET | /api/albums/:id | Required | Path: `{ id }` | `{ album }` | `401`, `403`, `404` | Get album detail |
| Albums API | DELETE | /api/albums/:id | Required | Path: `{ id }` | `{ success: true }` | `401`, `403`, `404` | Delete album |

See `contracts/api-spec.json` for full request/response schemas.

---

## Workflow Stage Contracts

| Workflow | Stage | Module | Input | Output | State Change | Failure Output |
|----------|-------|--------|-------|--------|--------------|----------------|
| Create album | Frontend submit | Albums UI | Form values | Validated payload | None | Field errors |
| Create album | API handler | Albums API | JSON request + auth context | Service command | Request logged | HTTP error body |
| Create album | Service | Albums Service | Command object | Domain result | Business state updated | Domain error |
| Create album | Repository | Albums Data | Persistence DTO | Stored record | Database row written | Storage error |
| Create album | Response | Albums API | Domain result | HTTP response body | None | Standard error body |

---

## Security Model

**Authentication:** [e.g. JWT Bearer token, 1h expiry, refresh token 7d]
**Authorization:** [e.g. Users can only access their own resources; admin role bypasses]
**Data Protection:** [e.g. Passwords hashed with argon2id; PII encrypted at rest]
**Rate Limiting:** [e.g. 100 req/min per IP on auth endpoints]

---

## Implementation Phases

### Phase 1: Foundation
- Project setup and configuration
- Database connection and schema
- Basic CI/CD pipeline
**Deliverable:** Running app skeleton with DB connected

### Phase 2: Core Features
- Authentication (register/login)
- Primary user stories (US-001 through US-NNN)
**Deliverable:** Core workflow end-to-end functional

### Phase 3: Polish & Hardening
- Error handling and edge cases
- Accessibility and performance
- Full test coverage
**Deliverable:** Production-ready feature

---

## Prerequisites

Tools that must be available in the development environment:
- [e.g. Node.js 20+]
- [e.g. Docker (for local PostgreSQL)]
- [e.g. pnpm]

---

## Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| [e.g. Third-party API rate limits] | Medium | High | Implement caching + retry with backoff |
| [e.g. Browser compatibility] | Low | Medium | Test on target browsers in CI |

---

## Implementation Notes
[Added during implementation - deviations from the plan, decisions made, lessons learned]

---

## Review Checklist
- [ ] Every user story has a corresponding component/endpoint
- [ ] Project Structure shows where code will live
- [ ] Module Map groups responsibilities by domain/layer
- [ ] Every module has a current requirement/workflow and a clear reason to exist
- [ ] Workflow Map ties user stories to modules, contracts, data, and tests
- [ ] Data model covers all entities in the spec
- [ ] No speculative module, dependency, service, abstraction, or config exists only for future flexibility
- [ ] Existing codebase patterns, native features, stdlib, and already-installed dependencies were checked before adding new custom code/dependencies
- [ ] Security model addresses all sensitive data
- [ ] API/input/output contracts define schemas, status codes, validation rules, and error bodies
- [ ] Important workflow stages define input, output, state change, and failure output
- [ ] Error handling strategy defined
- [ ] No over-engineering (each component justified by a requirement)
- [ ] Plan is consistent with `constitution.md`
- [ ] Performance approach addresses NFRs
