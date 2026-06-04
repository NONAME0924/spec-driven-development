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

## Tech Stack

| Layer | Technology | Version | Rationale |
|-------|-----------|---------|-----------|
| Frontend | [e.g. React] | [18.x] | [Why this over alternatives] |
| Styling | [e.g. Tailwind CSS] | [3.x] | |
| Backend | [e.g. FastAPI] | [0.x] | |
| Database | [e.g. PostgreSQL] | [16.x] | |
| Auth | [e.g. JWT + bcrypt] | | |
| File Storage | [e.g. S3] | | |
| Hosting | [e.g. Vercel + Railway] | | |
| Testing | [e.g. Vitest + Playwright] | | |

---

## Component Breakdown

### [Component Name - e.g. AuthService]
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

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| POST | /api/auth/login | None | Authenticate user |
| POST | /api/auth/register | None | Create account |
| GET | /api/albums | Required | List user's albums |
| POST | /api/albums | Required | Create album |
| GET | /api/albums/:id | Required | Get album detail |
| DELETE | /api/albums/:id | Required | Delete album |

See `contracts/api-spec.json` for full request/response schemas.

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
- [ ] Data model covers all entities in the spec
- [ ] Security model addresses all sensitive data
- [ ] Error handling strategy defined
- [ ] No over-engineering (each component justified by a requirement)
- [ ] Plan is consistent with `constitution.md`
- [ ] Performance approach addresses NFRs
