# Goal Mode

**Input:** Project outcome, Feature breakdown, resolved Step 0 gate, repository constraints.
**Output:** Requested deliverables: aligned specs; blueprint and verified implementation
when requested; user-language explanation.
**Gate/authority:** [SKILL.md](../SKILL.md#modes-and-gates) is the shared policy.

## 1. Establish Scope

Run or resume Step 0 using recorded state. After its gate, reuse/create the shared
constitution once. Define the in-scope Feature set in `epic.md`.
A Goal request authorizes routine product and technical choices within that scope,
not silent removal of requested features or unrelated external actions.

## 2. Complete the Spec Sweep

Run Step 2 and Step 3 for every in-scope Feature. Use repository evidence and documented
assumptions; do not wait at individual Feature review gates in Goal.
Independent specs can be drafted in parallel with common terms and disjoint file
ownership. The parent agent owns cross-spec reconciliation.

Complete every in-scope `spec.md` before producing technical plans, tasks, or code.
Reuse valid specs; do not regenerate completed work. Update the spec pack as work progresses.

## 3. Align the Spec Pack

Read the full set of in-scope specs and resolve conflicting boundaries, dependencies,
terms, roles, shared entities, and cross-feature user journeys. Consolidate duplicated
responsibilities and make shared concepts consistent. Resolve ordinary choices within
scope; apply the shared decision policy for consequential unresolved questions.

Create `.specify/spec-pack.md` as an index, not a copy of every spec:

```markdown
# Spec Pack: [Project]
**Status:** Draft / Aligned / Executing / Complete / Blocked

## Feature Specs
| Feature | Spec Link | Status | Depends On | Material Assumptions |
|---------|-----------|--------|------------|----------------------|

## Cross-Spec Decisions
| Decision | Affected Features | Basis | Canonical Definition |
|----------|-------------------|-------|----------------------|

## Alignment
[Boundary, terminology, dependency and cross-feature flow checks; unresolved blockers]

## Execution Order
[Dependency order and safe parallel groups]

## Deferred Scope
[Items, reasons, and user scope decision when requested work is deferred]
```

Mark Aligned only when all in-scope specs exist, dependency conflicts are resolved,
and no blocker prevents coherent planning. Technical schemas are not required at this
stage; capture shared behavioral expectations. Run Step 4 requirements review across
the pack before global technical planning so that the blueprint uses reviewed specs.

For a specs-only request, stop after this review. Mark the requested documentation
deliverable complete in execution state and spec-pack.md, while leaving implementation
status uncompleted in epic.md. Write final-explanation.md with document-validation
evidence and state that no implementation was requested. Phases 4-6 apply only to
requested planning/implementation; a planning-only request ends after its requested
planning artifacts and consistency checks.

## 4. Build the Global Blueprint

Create `.specify/project-blueprint.md` using Step 5's design criteria:

- Project Structure: actual repository paths and intended additions.
- Global Module Map: owner, responsibility, affected Features, dependencies, justification.
- Global Workflow Map: cross-feature journeys, modules, contracts, data, verification.
- Shared definitions: canonical locations for contracts and data.
- Execution plan: prerequisites, parallel write ownership, and integration checks.

Keep shared definitions in one place (existing code/schema location, or a suitable
project-level contract/data artifact). Feature plans link to them and describe deltas.

## 5. Execute the Batch

For each dependency-ready Feature, finish Steps 5-9 using its reviewed spec and the
global blueprint. Revisit Step 4 only if requirements changed. Step 6 validates
completed technical schemas; Step 7 groups tasks by real owners and workflows.

Parallel implementation is useful only with stable shared contracts, satisfied
prerequisites, disjoint writes, and planned integration checks. A dependent Feature
normally waits for its dependencies to PASS; a blueprint may explicitly allow earlier
parallel work against a stable contract, with final integration still required.

If later evidence changes a shared assumption, update the affected specs and spec pack,
reconcile their dependencies, then refresh impacted plans/checks before resuming affected
implementation. Do not restart unrelated Features or bypass a new alignment blocker.

## 6. Verify the Project

After Feature verification, check the assembled cross-feature workflows, shared data
and contract compatibility, and project-required checks. Record this project evidence
in `spec-pack.md` with commands/results or linked reports.

For an implementation request, complete only when all requested, non-deferred Features have current passing evidence
and project integration passes. Record incomplete work as Blocked rather than Complete.
Keep `epic.md` execution state and blueprint consistent with delivered code.
Write the final user-language explanation according to [Completion](../SKILL.md#completion).
