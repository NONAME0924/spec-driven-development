# Step 6 - Analyze

**Input:** `spec.md`, `plan.md`, relevant existing schemas/data models; Goal's shared artifacts.
**Output:** `plan.md#analysis`, or `analysis.md` for substantial findings.
**Completion:** No unresolved implementation-blocking inconsistency.
**Gate:** Use [Modes and Gates](../SKILL.md#modes-and-gates).

Check the artifacts that exist now:

1. Every in-scope requirement has a planned owner and verification approach.
2. Every new component has a current purpose; eliminate speculative work.
3. Project Structure and Module Map agree with the repository and each other.
4. Workflow Map connects real user flows to modules, contracts, data, and checks.
5. Contract inputs/outputs, validation, errors, permissions, and state transitions agree.
6. Data definitions and shared constraints support the required behavior.
7. Goal feature additions fit the global blueprint and shared canonical definitions.

Inspect authoritative schemas wherever they live; a missing optional `data-model.md`
is not a defect. Do not require `tasks.md` before Step 7. Check the task mapping when
tasks are produced, or here if updating an already-existing plan.

Record actionable findings with evidence, affected requirement/path, resolution, and
status. A short "coverage checked; no blockers" section is enough when there are none.
Correct plan/schema omissions in scope. Do not remove a requested requirement simply
because it is missing from the design.

Distinguish a real contradiction from a preference. Neither an interface with one
implementation nor a new dependency is automatically a failure. Evaluate its concrete
benefit against the simpler option. Update affected documents and recheck only the
changed relationships before proceeding.
