# Project Constitution
**Project:** [Project Name]
**Established:** YYYY-MM-DD
**Last Revised:** YYYY-MM-DD

> This document governs all technical and process decisions for this project. Every contributor (human or AI) must consult and adhere to these principles.

---

## Core Principles
1. [e.g. Correctness over cleverness - prefer clear, boring code]
2. [e.g. User-first - every decision is evaluated by its impact on the end user]
3. [e.g. Iterative delivery - ship small, working increments]

---

## Code Quality Standards

### Testing
- Coverage target: [e.g. 80% line coverage minimum]
- Test types required: [e.g. unit + integration; E2E for critical flows]
- Test must be written [before / alongside / after] implementation
- Tests must pass in CI before merging

### Code Style
- Formatter: [e.g. Prettier / Black / gofmt] - **no exceptions**
- Linter: [e.g. ESLint / Ruff / golangci-lint]
- Configuration: see [config file path]

### Documentation
- [e.g. All public functions/methods must have docstrings]
- [e.g. All API endpoints must have OpenAPI annotations]
- [e.g. README must be updated with any setup changes]

---

## Architecture Guidelines

### Pattern
[e.g. Layered architecture: routes -> services -> repositories -> database]

### Key Constraints
- [e.g. No business logic in route handlers]
- [e.g. All database access through repository layer only]
- [e.g. Services must not depend on other services directly - use events or dependency injection]

### Module Boundaries
[e.g. Each feature lives in its own directory; no cross-feature imports except through shared interfaces]

---

## User Experience Standards

### Design System
[e.g. Follows internal design tokens in `src/design/tokens.ts`; no hardcoded colours or spacing]

### Accessibility
- Standard: [e.g. WCAG 2.1 Level AA]
- Must: keyboard navigable, screen-reader compatible, sufficient colour contrast

### Supported Environments
- Browsers: [e.g. Chrome 120+, Firefox 120+, Safari 16+, Edge 120+]
- Devices: [e.g. Desktop + tablet; mobile optional for v1]
- Screen sizes: [e.g. 768px minimum width]

---

## Performance Requirements

| Metric | Target | Measurement |
|--------|--------|-------------|
| Page load (LCP) | < 2.5s | Lighthouse on 4G |
| API response time | < 200ms p95 | Under normal load |
| Time to interactive | < 4s | Lighthouse |

---

## Security & Compliance

### Authentication
[e.g. JWT with 1h access token + 7d refresh token; stored in httpOnly cookies]

### Data Handling
- [e.g. Passwords: argon2id, minimum cost factor 3]
- [e.g. PII: encrypted at rest; never logged]
- [e.g. Secrets: environment variables only; never in source code]

### Compliance
[e.g. GDPR compliant: users can export and delete their data]

---

## Development Process

### Branching
[e.g. Feature branches named `NNN-feature-name`; merge to main via PR]

### Commits
[e.g. Conventional Commits format: `feat(scope): description`]

### Pull Requests
- [e.g. Maximum 400 lines changed per PR]
- [e.g. Must include link to spec and task ID in description]
- [e.g. Requires 1 human review + passing CI]

### Releases
[e.g. Semantic versioning; changelog generated from commit messages]

---

## AI Agent Guidelines

### What the AI can decide independently
- Code structure within established patterns
- Variable/function naming
- Test case design
- Documentation wording

### What requires human approval
- New dependencies (especially with security implications)
- Architecture deviations from the plan
- Changes that affect >3 files simultaneously
- Anything that changes the public API contract

### AI behaviour rules
- Always reference task IDs in commit messages
- Never modify `spec.md` or `plan.md` without explicit instruction
- If a task is ambiguous, surface the ambiguity - don't guess
- Prefer the simplest solution that satisfies the requirement
