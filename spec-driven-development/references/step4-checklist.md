# Step 4 - Checklist

**Input:** Clarified `spec.md` and shared constraints.
**Output:** `checklists/requirements.md`; optional domain review files.
**Completion:** No unresolved requirement blocker.
**Gate:** Use [Modes and Gates](../SKILL.md#modes-and-gates).

Check whether the requested behavior is complete, consistent, feasible, and observable.
There is no quota for acceptance criteria or requirement metrics. Performance targets,
security constraints, and supported environments must come from actual needs or clearly
identified assumptions.

Create a compact findings table:
`Requirement | Finding | Impact | Resolution | Status`.
Use PASS, FAIL, or N/A. Keep unresolved FAIL visible; fix it within scope or request the
needed decision. A user-approved scope change updates the spec and records deferred
work; it does not turn a known unmet criterion into a passing test.

## Domain Reviews

Keep small domain reviews as sections in `requirements.md`. Split them into the
following files when the domain warrants a separate review:

| File | Checks | Does not replace |
|------|--------|------------------|
| `ux.md` | End-to-end user flows, applicable loading/empty/error/success states, accessibility | UI design or implementation |
| `api.md` | Required operations, permissions, external input/output expectations and compatibility constraints | Executable API schema |
| `security.md` | Actual trust boundaries, sensitive data and access requirements | Implemented controls and their tests |
| `minimalism.md` | Unrequested scope, redundant requirements, speculative complexity | Architecture analysis in Step 6 |

An API review applies only when an integration exists. Do not require internal schemas,
architecture modules, or task lists before Step 5/7 creates them. Record technical
contract design as Step 5 work; Step 6 will verify the completed schemas. UX and API
checklists are reviews of requirements, not the contract or design documents themselves.

Resolve clear defects directly using the clarified scope. Do not manufacture an admin
role, encryption algorithm, rate limit, or separate audit merely to satisfy an example.
