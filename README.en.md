# Spec-Driven Development Skill

English | [繁體中文](README.md)

**Lean SDD (Lean Spec-Driven Development)** connects requirements, modules, workflows,
interfaces, tasks, and verification into a coherent project without unnecessary
documentation or architecture.

It supports Goal, Auto, and Detailed modes. Instructions have been reviewed against
official GPT-6 Astra guidance; the skill neither pins a model nor changes your settings.
[Optimization report (Traditional Chinese)](docs/astra-review.md)

## Usage

Install the repository's `spec-driven-development/` folder as a skill in a location
supported by your agent. The entrypoint is uppercase `SKILL.md`. Once installed,
invoke it explicitly in a supported agent:

```text
Use $spec-driven-development to plan and build an expense tool.
It needs CSV import and monthly summaries. Keep the existing stack.
```

Provide the outcome, required features, constraints, and whether you want documents only
or implementation too. Routine fixes, explanations, reviews, and skill maintenance do
not automatically require the full SDD workflow.

1. The agent inspects the project and creates or updates the Feature breakdown in Step 0.
2. It presents the breakdown and asks you to choose Goal, Auto, or Detailed.
3. It follows that mode and finishes with `.specify/final-explanation.md` in your language.

If you already selected a mode, Step 0 confirms the breakdown with that choice instead
of asking you to choose again. You can explicitly waive this confirmation. Resuming
unchanged work preserves recorded approvals, mode, and valid artifacts.

```text
Use Goal mode. After Step 0, continue without asking for confirmation.
Complete every Feature spec before global planning and implementation.
```

For documents only:

```text
Use Goal mode and skip the initial confirmation.
Write all booking-system specs and align them; do not implement.
```

## Modes

| Mode | Scope | Review Points | Execution |
|------|-------|---------------|-----------|
| Goal | Whole project | Step 0 breakdown and mode | Complete and align all specs, then plan globally and execute the batch |
| Auto | Selected Feature | Steps 0, 2, 3 | Continue through Steps 4-9 after Step 3 approval |
| Detailed | Selected Feature with detailed explanations | Steps 0, 2, 3 | Continue automatically with detailed artifacts, decisions and verification reporting |

Auto and Detailed keep Steps 2 and 3 separate unless you explicitly combine or waive them.
Detailed explains each stage's artifacts, tradeoffs and evidence more fully; Auto gives
concise updates. Steps 1 and 4-9 proceed without waiting in both modes. Detailed reports
do not introduce additional approval gates. A Step 8 rewrite beyond existing authorization
still requires confirmation; routine implementation, design adjustments and test fixes do not.
Goal resolves ordinary assumptions autonomously, asking about material facts it cannot
infer or actions beyond existing authorization. A local dependency, authentication
implementation, or test failure is not automatically an approval gate.

Automation stays inside the requested scope. A specs-only request does not authorize
implementation, and the agent must not drop requirements to declare success.

## Stage Guide

Feature files below live under `.specify/specs/NNN-feature-name/`.

| Stage | Input | Work and Output | Artifact Purpose |
|-------|-------|-----------------|------------------|
| [0 Epic](spec-driven-development/references/step0-epic.md) | Goal, existing project | `.specify/epic.md` | Feature boundaries, dependencies, delivery order, mode and resume state |
| [1 Constitution](spec-driven-development/references/step1-constitution.md) | User constraints, repo instructions/config | Reuse/create `.specify/memory/constitution.md` | Shared constraints and their sources, without invented governance |
| [2 Specify](spec-driven-development/references/step2-specify.md) | Feature scope | `spec.md` | User needs, non-goals, observable criteria and stable AC IDs |
| [3 Clarify](spec-driven-development/references/step3-clarify.md) | Draft spec, existing behavior | Update `spec.md` | Answers, assumptions, evidence and real blockers |
| [4 Checklist](spec-driven-development/references/step4-checklist.md) | Clarified spec | `checklists/requirements.md` | Completeness, clarity, consistency and verifiability |
| [5 Plan](spec-driven-development/references/step5-plan.md) | Spec, repo, Goal blueprint | `plan.md` and necessary supporting files | File layout, ownership, connected workflows, formats and verification approach |
| [6 Analyze](spec-driven-development/references/step6-analyze.md) | Spec and technical design | Analysis in `plan.md`; separate `analysis.md` for substantial findings | Consistency across requirements, modules, data and contracts |
| [7 Tasks](spec-driven-development/references/step7-tasks.md) | Consistent plan | `tasks.md` | Module/workflow groups, real paths, dependencies and completion conditions |
| [8 Implement](spec-driven-development/references/step8-implement.md) | Spec, plan, tasks, code | Code and appropriate tests; updated tasks/plan | Working behavior, verified incrementally |
| [9 Verify](spec-driven-development/references/step9-test.md) | Criteria, implementation, environment | `test-report.md` and epic status | Actual evidence distinguishing passed, failed, not-run and blocked checks |

Stage outcomes remain, but valid artifacts can be reused and small checks combined.
Template fields and examples do not require identical layers or files in every project.

## UX, API, and Supporting Files

| File | When Useful | Contents |
|------|-------------|----------|
| `checklists/ux.md` | Substantial UX review | Flows, applicable loading/empty/error/success states, accessibility |
| `checklists/api.md` | Substantial integration review | Operations, permissions, external input/output expectations and compatibility |
| `checklists/security.md` | Actual data/access concerns | Trust boundaries, sensitive data, permission requirements |
| `checklists/minimalism.md` | Separate scope review helps | Unrequested work, duplication and speculative complexity |
| `data-model.md` | Data detail exceeds a short plan | Ownership, types, requiredness, validation, relationships, lifecycle and migration effects |
| `research.md` | Consequential technical uncertainty | Question, official sources, version/date, findings and uncertainty |
| `contracts/api-spec.json` | New HTTP API schema needed | OpenAPI requests/responses/errors, status codes and auth |
| `contracts/events.md` | Event/message boundaries exist | Producers/consumers, schemas, delivery and failure semantics |
| `contracts/workflows.md` | API schemas cannot describe a multi-stage flow fully | Stage owners, input/output schemas, state changes and failures |

Small domain reviews can be sections of `requirements.md`; five empty checklists are
unnecessary. Keep existing canonical schemas in place and link them to avoid drift.

**UX/API checklists review requirements; Step 5 contracts define actual formats.**
Contracts specify fields, types, required/optional/null semantics, validation and errors.
JSON examples alone are insufficient. Workflow contracts cover API, CLI, event, job,
and agent-pipeline handoffs.

## Goal Workflow

```text
Step 0: breakdown and mode gate
  -> Step 1: shared principles
  -> Steps 2 + 3 for every Feature
  -> spec-pack alignment + Step 4 across the specs
  -> global project-blueprint
  -> Steps 5-9 per Feature
  -> cross-feature integration verification
  -> user-language completion explanation
```

| Project Artifact | Purpose |
|------------------|---------|
| `.specify/spec-pack.md` | Spec index, shared concepts, decisions, dependency order and project integration evidence |
| `.specify/project-blueprint.md` | Global structure, module ownership, flows, canonical shared contracts/data and execution order |
| `.specify/final-explanation.md` | Deliverables, usage, important files, verification and limitations; states when implementation was not requested |

Parallelize only when dependencies and write ownership permit it. Shared contract
changes require realigning affected specs/designs, not restarting unrelated Features.
Individual Feature passes must be followed by assembled-project verification.

## Lean SDD and Verification

Prefer existing modules, platform capabilities, and suitable libraries. Add abstractions
for real needs or framework boundaries; a single implementation is not automatically
wrong. Preserve necessary data protection, permission checks, accessibility and verification.

Scale verification to risk. Reuse meaningful tests and add coverage for important changed
behavior; low-impact documents may use inspection or reproducible manual checks.
Every acceptance criterion needs suitable evidence. Not-run checks are not passing.
After required checks pass, expand testing only for new changes or unresolved concerns.

## Maintenance and Sources

- [AGENTS.md](AGENTS.md): concise instructions for maintaining this repository.
- [SKILL.md](spec-driven-development/SKILL.md): shared rules and stage routing.
- `references/`: load for the current stage; `templates/`: use as needed.
- [Astra review (Traditional Chinese)](docs/astra-review.md): rationale, evidence and limitations.
- [Workflow evaluation](docs/workflow-evaluation.md): gates, scope, resume and verification scenarios.

Official references: [GPT-6 Astra guidance](https://developers.openai.com/api/docs/guides/latest-model?model=gpt-6-astra),
[Build skills](https://learn.chatgpt.com/docs/build-skills),
[AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md).
Reviewed 2026-09-05.

## Attribution

Workflow concepts reference [github/spec-kit](https://github.com/github/spec-kit).
Lean SDD adapts simplicity and anti-overengineering ideas from
[DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) for this workflow.

## License

MIT. See [LICENSE](LICENSE).
