# Goal Mode

## Purpose
Turn a broad project goal into a complete spec pack before planning or implementing. Goal Mode avoids local optimization: do not start building Feature 001 before the AI has seen the full set of Feature specs, dependencies, shared modules, contracts, and data needs.

Use Goal Mode when the user wants the whole project handled automatically from a high-level goal, especially when the project has multiple Features whose APIs, data model, modules, or workflows may affect each other.

---

## Core Rule

Goal Mode is **spec-first across all Features, then build**:

1. Step 0 creates or updates `epic.md`
2. Run a Spec Sweep for every Feature: Step 2 + Step 3 only
3. Run Cross-Spec Alignment across the whole spec pack
4. Build a global project blueprint
5. Execute Features in dependency order through Step 4 -> Step 9

Do not run Step 5, Step 7, or Step 8 for any Feature until the spec pack is complete and aligned.

---

## Goal Mode Artifacts

Create these project-level artifacts:

```text
.specify/
|-- epic.md
|-- spec-pack.md              <- all Features, status, assumptions, cross-spec decisions
|-- project-blueprint.md      <- global Project Structure, Module Map, Workflow Map, shared contracts
|-- final-explanation.md      <- user-language explanation after completion
|-- specs/
|   |-- 001-feature-name/
|   |   `-- spec.md
|   |-- 002-feature-name/
|   |   `-- spec.md
|   `-- ...
```

`spec-pack.md` is the project-level source of truth while Goal Mode is running.

---

## Phase A - Goal Intake and Epic

Run Step 0 normally, but optimize for the whole goal:

- Capture the user's outcome, audience, constraints, and success definition
- Split the goal into independently deliverable Features
- Mark dependencies and delivery order
- Apply Lean SDD: merge tiny Features, split giant Features, defer speculative scope

In Goal Mode, Step 0 is the only normal gate. If the user explicitly asked for "fully automatic goal mode", proceed after Step 0 using reasonable assumptions unless a risk trigger appears.

---

## Phase B - Spec Sweep

For each Feature in `epic.md`, in dependency order:

1. Create `.specify/specs/NNN-feature-name/spec.md`
2. Run Step 2 - Specify
3. Run Step 3 - Clarify using AI defaults where safe
4. Record assumptions and deferred scope in the Feature spec
5. Update `spec-pack.md`

Goal Mode clarification policy:

- Do not stop for ordinary product details. Make the smallest safe assumption and record it.
- Ask the user only when the decision is high-impact, irreversible, security-sensitive, legal/compliance-sensitive, paid-service-related, or changes the core product direction.
- Prefer private before public, existing roles before new roles, native/platform behavior before custom UI, synchronous flow before background jobs, and current Feature scope before future flexibility.

---

## Phase C - Cross-Spec Alignment

After all Feature specs exist, read every `spec.md` and audit the full spec pack.

Check:

- Feature boundaries: no duplicated or conflicting responsibilities
- Dependencies: order is correct and no circular dependency exists
- Shared concepts: terms, roles, permissions, entities, and states are consistent
- API/data overlap: common contracts and entities are shared instead of duplicated
- UX flow continuity: user journeys across Features make sense
- Lean SDD: speculative scope is deferred, tiny Features are merged, overlarge Features are split

Create or update `.specify/spec-pack.md`:

```markdown
# Spec Pack: [Project Name]
**Status:** Draft / Aligned / Executing / Complete
**Last Updated:** YYYY-MM-DD

## Feature Specs
| Feature | Spec | Status | Key Assumptions | Depends On |
|---------|------|--------|-----------------|------------|
| 001-feature | specs/001-feature/spec.md | Aligned | [summary] | - |

## Cross-Spec Decisions
| ID | Decision | Applies To | Reason |
|----|----------|------------|--------|
| CSD-001 | Use one Account role model | 001, 003, 004 | Avoid duplicated permission concepts |

## Shared Concepts
- Roles:
- Entities:
- Workflows:
- Contracts:

## Conflicts Resolved
- [Conflict] -> [Resolution]

## Deferred Scope
- [Deferred item] -> [Reason / later Feature]

## Execution Order
1. 001-feature
2. 002-feature
```

---

## Phase D - Global Project Blueprint

Before executing individual Features, create `.specify/project-blueprint.md`.

This is the global version of Step 5's project shape:

```markdown
# Project Blueprint: [Project Name]
**Generated:** YYYY-MM-DD

## Project Structure
[repo-aware file/folder layout]

## Global Module Map
| Module | Owns | Used By Features | Key Files | Depends On | Lean Check |
|--------|------|------------------|-----------|------------|------------|

## Global Workflow Map
| Workflow | Features | Modules | Contracts | Data | Tests |
|----------|----------|---------|-----------|------|-------|

## Shared Data Model
| Entity | Owning Module | Used By Features | Notes |
|--------|---------------|------------------|-------|

## Shared Contracts
| Contract | Type | Used By Features | Notes |
|----------|------|------------------|-------|

## Execution Plan
| Order | Feature | Why Now | Blocks |
|-------|---------|---------|--------|
```

Each Feature's later `plan.md`, `tasks.md`, contracts, and tests must map back to this blueprint.

---

## Phase E - Batch Execution

Execute Features in the order from `spec-pack.md` / `project-blueprint.md`.

For each Feature:

1. Step 4 - Checklist
2. Step 5 - Plan, using `project-blueprint.md` as the global parent
3. Step 6 - Analyze
4. Step 7 - Tasks
5. Step 8 - Implement
6. Step 9 - Test
7. Mark the Feature [PASS] in `epic.md`

Do not start a Feature if its dependencies are not [PASS], unless the plan explicitly supports parallel implementation without shared-state conflicts.

---

## Risk Triggers

Goal Mode is fully automatic except for these cases:

- Paid service or new external dependency that was not already approved
- Destructive migration, irreversible data operation, or broad public API change
- Security, privacy, legal, compliance, or auth decision that cannot be safely assumed
- Core product direction conflict across specs
- Requirement conflict that cannot be resolved with a conservative assumption
- Existing codebase architecture contradicts the generated project blueprint

When a risk trigger appears, stop and ask one concise question, then resume the batch.

---

## Completion

Goal Mode completes when:

- Every Feature in `epic.md` is [PASS], or explicitly [DEFERRED]
- `spec-pack.md` is updated with final decisions
- `project-blueprint.md` reflects the implemented structure
- All Feature `test-report.md` files pass
- `.specify/final-explanation.md` explains the completed project in the user's language

Before the final report, create `.specify/final-explanation.md` in the user's language. This is not an internal trace; it is the explanation a user should read to understand what was built, how to use it, where the main parts live, what passed tests, and what was deferred.

Template:

```markdown
# [Project Name] 說明

## 完成內容
[What the project now does]

## 如何使用
[How to run/open/use it]

## 主要功能
- [Feature and user value]

## 專案結構
[Important modules/files from project-blueprint.md]

## 測試結果
[Feature test reports and any tests that could not run]

## 延後範圍
[Deferred items from spec-pack.md]
```

Final report:

```markdown
[SUCCESS] Goal Mode complete

Features:
- [PASS] 001-feature
- [PASS] 002-feature
- [DEFERRED] 006-future-feature

Artifacts:
- .specify/spec-pack.md
- .specify/project-blueprint.md
- .specify/final-explanation.md
- .specify/specs/*/test-report.md

Notes:
- [major decisions]
- [deferred scope]
```
