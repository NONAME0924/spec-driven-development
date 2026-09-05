---
name: spec-driven-development
description: >-
  Plan and deliver software through traceable specs, architecture, tasks, and verification.
  Use for requested SDD, PRD/spec writing, structured feature planning, or project-wide
  spec-first delivery. Supports Goal, Auto, and Detailed modes with Lean SDD.
  Do not impose the full workflow on routine fixes, reviews, explanations, or skill maintenance
  unless the user requests it.
---

# Lean Spec-Driven Development

Turn the requested outcome into a coherent, verifiable project. Keep requirements,
module ownership, interfaces, implementation, and evidence connected. Choose the
smallest correct solution using existing code and conventions where they fit.

## Scope and Authority

The user's instructions take precedence over this skill's defaults. Host instructions
and tool permissions still apply. Carry existing authorization and preferences forward;
do not ask the user to repeat them. A request for specs or planning alone ends at that
deliverable and does not authorize implementation.

Read only the current stage's reference and relevant project artifacts. Templates are
starting points: omit irrelevant sections, combine small sections, and link existing
canonical schemas instead of copying them. Preserve the stage outcomes below without
requiring a separate tool call, report, or conversation turn for every check.

## Modes and Gates

For a new or materially changed scope, start with Step 0. Present the concrete feature
breakdown and ask the user to choose Goal, Auto, or Detailed mode in their language.
If a mode was already chosen, ask for acceptance of the breakdown with that mode;
do not ask them to choose again. An explicit instruction to skip this confirmation
overrides the default. On an unchanged resume, retain the recorded mode and approvals.

| Stage | Detailed | Auto | Goal |
|-------|----------|------|------|
| 0: Feature breakdown and mode | Confirm | Confirm | Confirm |
| 1: Shared principles | Continue with explanation | Continue | Continue |
| 2: Feature requirements | Confirm | Confirm | Resolve autonomously |
| 3: Clarifications and assumptions | Confirm | Confirm | Resolve autonomously |
| 4-9: Review, plan, build, verify | Continue with detailed reporting | Continue | Continue in batch |

In Auto and Detailed, Step 2 and Step 3 remain separate review points unless the user explicitly
combines or waives them. Goal completes all in-scope specs and cross-spec alignment
before technical planning or implementation; follow [Goal Mode](references/goal-mode.md).
Auto and Detailed work on one selected Feature. Stop at the requested
scope boundary. Record mode switches without restarting completed, still-valid work.

Detailed uses the same approval points as Auto: Steps 0, 2, and 3. It explains each
stage's artifacts, decisions, tradeoffs, and verification results in more detail;
Auto reports concise progress and key outcomes. In Detailed, Steps 1 and 4-9 proceed
without waiting for a response. Detailed reporting is not an additional approval gate.
Both modes use the shared Autonomous Decisions policy for exceptional pauses.

At a required gate, give the artifact link, decisions or changes, and the specific
approval needed. If a skill rule causes a pause, identify this file and quote the
applicable rule. Progress updates outside gates do not require a response.

## Autonomous Decisions

Within the selected mode, finish authorized work through verification. Resolve routine
gaps from repository evidence and document consequential assumptions. Ask only for
missing information that materially affects correctness or scope and cannot reasonably
be inferred, or for an action beyond existing authorization (for example an unapproved
purchase, destructive live-data operation, or materially broader rewrite).

A new local dependency, authentication implementation, architecture adjustment, or
test failure is not automatically an approval gate. Evaluate the actual impact and
existing authorization. Prepare the reviewable plan or patch first when possible;
continue independent authorized work while a blocking decision is pending. Do not
silently drop requested requirements to make the plan or tests pass.

## Stage Routing

Paths below are in the target project's `.specify/`. Feature outputs live under
`specs/NNN-feature-name/`. Reuse valid artifacts; refresh affected outcomes when inputs
change. Do not inspect not-yet-created artifacts as prerequisites of an earlier stage.

| Step | Input | Required outcome / output | Reference |
|------|-------|---------------------------|-----------|
| 0 Epic | Request, repo, existing epic | Boundaries, dependencies, delivery order in `epic.md` | [Step 0](references/step0-epic.md) |
| 1 Constitution | Existing instructions and constraints | Reused or concise `memory/constitution.md` | [Step 1](references/step1-constitution.md) |
| 2 Specify | Feature scope and constraints | Testable requirements in `spec.md` | [Step 2](references/step2-specify.md) |
| 3 Clarify | Spec and relevant evidence | Decisions, assumptions, unresolved blockers in `spec.md` | [Step 3](references/step3-clarify.md) |
| 4 Checklist | Clarified spec | `checklists/requirements.md`; domain reviews only when applicable | [Step 4](references/step4-checklist.md) |
| 5 Plan | Reviewed spec, repo, Goal blueprint if present | `plan.md`: structure, modules, workflows, interfaces, verification approach | [Step 5](references/step5-plan.md) |
| 6 Analyze | Spec and planning artifacts | Coverage and consistency findings in `plan.md` or `analysis.md` | [Step 6](references/step6-analyze.md) |
| 7 Tasks | Consistent plan | Dependency-ordered, module/workflow-grouped `tasks.md` | [Step 7](references/step7-tasks.md) |
| 8 Implement | Spec, plan, tasks, current code | Working code, appropriate tests, task state and plan updates | [Step 8](references/step8-implement.md) |
| 9 Verify | Acceptance criteria and implementation | Evidence in `test-report.md`, accurate epic status | [Step 9](references/step9-test.md) |

## Project Shape and Lean Decisions

Plan around actual module ownership and user workflows. A small feature can belong to
one module; a directory tree is not a reason to invent services, repositories, or APIs.
Every task has an owner and a requirement or necessary implementation justification.
Interfaces describe input/output formats and errors at real boundaries; workflow
contracts also describe state changes and failure behavior.

Reuse existing modules, standard/platform capabilities, and installed libraries where
they satisfy the requirement. Add a dependency or abstraction when it reduces real
complexity or follows a required framework pattern; document the reason briefly.
Defer speculative additions, not requested functionality. Keep validation, permission
checks, data protection, accessibility, and verification appropriate to the actual task.

## Execution and Continuity

Batch independent reads and checks when the tools support it. Use available subagents
for independent spec drafting, bounded implementation, or review when that saves time
or improves confidence. Give each a scope, inputs, output contract, and file ownership.
The parent owns alignment and integration; parallelism must not bypass the Goal spec
barrier or introduce conflicting writes. Work sequentially when delegation is unavailable.

Keep a compact `Execution State` section in `epic.md`: active mode, requested scope,
current stage/Feature, recorded approvals, pending decisions, artifact links, and next
action. Update it at gates, meaningful milestones, and interruption. On resume, read
that state and inspect affected files rather than replaying the whole workflow.
Treat new user messages as steering unless they cancel or replace the task; refresh
only the affected specs, plans, and checks.

Verify proportionally to risk. Reuse meaningful tests, add coverage where behavior
changes, and distinguish passing, failing, blocked, and not-run evidence. After required
checks pass, expand testing only for new changes or unresolved concerns. Do not report
implementation completion based only on documents, unchecked tasks, or approval of a failure.

## Completion

When the requested deliverable is complete, write `.specify/final-explanation.md` in the
user's language: what was delivered, how to use it, important modules/files, verification
results, and remaining limitations. For a specs-only request, describe the documents
and say implementation was not requested. For an implemented Goal project, include
project integration evidence.
If work is blocked, record partial progress and the blocker without claiming completion.

## Templates

- [Constitution](templates/constitution-template.md): shared constraints and evidence sources.
- [Spec](templates/spec-template.md): requirements, stable acceptance IDs, assumptions.
- [Plan](templates/plan-template.md): project structure, ownership, flows, contracts.
- [Tasks](templates/tasks-template.md): executable work and verification outcomes.
