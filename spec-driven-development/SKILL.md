---
name: spec-driven-development
description: >
  Spec-Driven Development (SDD) workflow skill. Use this skill whenever the user wants to build software by starting from an idea or requirements - whether it's a new greenfield project, adding features to an existing system, or modernizing legacy code. Triggers on phrases like "I want to build", "help me create an app", "let's develop a feature", "I have an idea for", "build me a", "help me plan this project", or any request to design, spec out, or implement software in a structured way. Also triggers when the user asks to create a spec, write a PRD, plan tasks, break down implementation, choose between detailed/manual approval and automatic execution, wants goal/project-wide execution, or wants minimal/YAGNI/anti-overengineering project planning. Supports three workflow modes: detailed mode with approval at every step, auto mode where Step 0/2/3 are the main gates for one Feature, and goal mode where all Feature specs are written first as a spec pack before global planning and fully automatic batch execution. Includes Lean SDD discipline: smallest correct scope, architecture, task list, and implementation while preserving validation, security, accessibility, and spec-traced tests.
---

# Spec-Driven Development (SDD) Skill

Build high-quality software faster by starting from structured specifications - not vibe coding.

## Core Philosophy

SDD flips traditional development: instead of jumping from idea to code, we move through structured phases where each step produces living documentation. The specification **is** the source of truth. Any AI agent can pick up where another left off because everything is written down.

Lean SDD keeps that structure small. The best project artifact is the one that prevents mistakes without inventing future work. Prefer the smallest correct scope, the fewest justified modules, existing codebase patterns, native platform features, standard libraries, and already-installed dependencies before adding custom layers or new dependencies.

```
Big Idea
   |
   v
Step 0 - Epic (decompose into Features)
   |
   |-- Feature 001 -> Steps 1-9
   |-- Feature 002 -> Steps 1-9
   |-- Feature 003 -> Steps 1-9
   `-- ...
```

**Key principle:** Always decompose first. Never start specifying before you know what the pieces are.

**Lean principle:** Do not simplify away trust-boundary validation, data-loss protection, security, accessibility basics, or tests that prove acceptance criteria. Delete speculation, not safety.

---

## Directory Structure

```
.specify/
|-- epic.md                      <- Project feature map (Step 0)
|-- spec-pack.md                 <- Goal Mode cross-feature spec pack
|-- project-blueprint.md         <- Goal Mode global structure, modules, workflows
|-- final-explanation.md         <- User-language completion explanation
|-- memory/
|   `-- constitution.md          <- Project principles (Step 1, shared across features)
|-- specs/
|   |-- 001-feature-name/
|   |   |-- spec.md              <- Requirements & user stories (Step 2)
|   |   |-- checklists/          <- Spec quality audit (Step 4)
|   |   |   |-- requirements.md
|   |   |   |-- ux.md
|   |   |   |-- api.md
|   |   |   |-- security.md
|   |   |   `-- minimalism.md
|   |   |-- plan.md              <- Technical architecture (Step 5)
|   |   |-- data-model.md        <- Data schema (Step 5)
|   |   |-- research.md          <- Tech stack research (Step 5)
|   |   |-- tasks.md             <- Actionable task list (Step 7)
|   |   `-- test-report.md       <- Test results vs spec (Step 9)
|   |-- 002-feature-name/
|   |   `-- ...
|   `-- 003-feature-name/
|       `-- ...
`-- templates/
    |-- spec-template.md
    |-- plan-template.md
    `-- tasks-template.md
```

---

## Workflow Modes

Step 0 always comes first. After Step 0 creates or updates `epic.md`, stop and ask the user which mode to use. Do not proceed to Step 1, Step 2, Spec Sweep, planning, or implementation until the user chooses a mode.

If the user already explicitly chose a mode before Step 0, confirm that choice in the Step 0 gate and proceed only after the user accepts the feature breakdown.

### Auto Mode

Use when the user wants the agent to handle the whole feature after the important requirements are confirmed.

Hard approval gates:
- **Step 0 - Epic:** approve feature boundaries and delivery order.
- **Step 2 - Specify:** approve what the feature must and must not do.
- **Step 3 - Clarify:** approve answers, assumptions, and edge cases.

After Step 3 is approved, continue through Step 4 -> Step 9 without stopping unless a risk trigger appears.

Risk triggers that require user confirmation:
- Step 4 finds unresolved [FAIL] items that cannot be safely resolved with a documented assumption.
- Step 5 needs a major architecture choice, paid service, new external dependency, migration, or stack decision the user has not already approved.
- Step 8 would perform a large rewrite, destructive operation, data migration, broad public API change, security-sensitive change, or irreversible action.
- Step 9 reveals a spec ambiguity or failing acceptance criterion that requires changing approved requirements.

### Detailed Mode

Use when the user asks for detailed mode, manual mode, strict review, teaching flow, or approval at every stage. In this mode, every step ends with a gate and the agent waits for explicit approval before continuing.

### Goal Mode

Use when the user gives a broad goal/project and wants AI to handle the whole thing automatically. Goal Mode is project-wide:

1. Run Step 0 to split the goal into Features
2. Write all Feature specs first: Step 2 + Step 3 for every Feature
3. Create `.specify/spec-pack.md` and resolve cross-spec conflicts
4. Create `.specify/project-blueprint.md` with global Project Structure, Module Map, Workflow Map, shared contracts, and shared data
5. Execute Features in dependency order through Step 4 -> Step 9 automatically

Goal Mode does not start implementation for any Feature until the whole spec pack is complete and aligned. Read `references/goal-mode.md`.

### Mode Switching

- "auto mode" / "automatic mode" -> use Auto Mode from the current step onward.
- "detailed mode" / "manual mode" -> use Detailed Mode from the current step onward.
- "goal mode" / "project mode" / "whole goal" / "fully automatic goal" -> use Goal Mode from Step 0 or from the current epic state.
- If switching modes mid-feature, re-read the current feature documents before continuing.

### Step 0 Mode Gate

After Step 0, always ask:

```text
Choose execution mode:
- "goal mode" -> write all Feature specs first, align the spec pack, then batch execute automatically
- "auto mode" -> work one Feature at a time; Step 2/3 are the main approval gates, then continue automatically
- "detailed mode" -> pause for approval at every step
```

Use the user's language when asking.

---

## The Full Workflow

### Step 0 - Epic
**Purpose:** Decompose the project into independently deliverable Features. Define boundaries, dependencies, and delivery order. Produces `epic.md`.
**Runs:** Once per project (re-run if scope changes significantly)
-> Read: `references/step0-epic.md`

---

*For the first Feature, run Step 1 once, then Steps 2-9. For later Features, reuse the existing constitution and run Steps 2-9.*

### Step 1 - Constitution
**Purpose:** Establish governing principles before any work begins.
**Note:** Only needed once per project. If `constitution.md` already exists, reuse it and continue to Step 2.
-> Read: `references/step1-constitution.md`

### Step 2 - Specify
**Purpose:** Transform the current Feature's scope into structured requirements and user stories. Scoped strictly to this Feature - do not bleed into other Features.
-> Read: `references/step2-specify.md`

### Step 3 - Clarify
**Purpose:** Surface and resolve ambiguities in this Feature's spec before committing to a technical plan.
-> Read: `references/step3-clarify.md`

### Step 4 - Checklist
**Purpose:** Audit the spec's quality - ensure every requirement is specific, measurable, and complete. Hard gate: no [FAIL] items allowed before proceeding.
-> Read: `references/step4-checklist.md`

### Step 5 - Plan
**Purpose:** Translate this Feature's requirements into a concrete technical architecture.
-> Read: `references/step5-plan.md`

### Step 6 - Analyze
**Purpose:** Cross-artifact consistency validation - verify spec, plan, and data model are fully aligned.
-> Read: `references/step6-analyze.md`

### Step 7 - Tasks
**Purpose:** Break the plan into granular, ordered, executable tasks.
-> Read: `references/step7-tasks.md`

### Step 8 - Implement
**Purpose:** Execute tasks systematically to produce working code.
-> Read: `references/step8-implement.md`

### Step 9 - Test
**Purpose:** Write and run tests that verify the implementation satisfies every acceptance criterion in spec.md. The Feature is not complete until all tests pass.
-> Read: `references/step9-test.md`

---

*After Step 9 passes -> mark Feature [PASS] in epic.md -> begin next Feature at Step 2*

### Goal Mode - Project-Wide Batch
**Purpose:** Write every Feature spec first, align the full spec pack, create a global project blueprint, then execute all Features automatically in dependency order.
-> Read: `references/goal-mode.md`

---

## Completion Explanation

When the requested Feature, project, or Goal Mode batch is complete, create `.specify/final-explanation.md` in the user's language. If the user wrote Chinese, write the explanation in Chinese; if English, write English; otherwise match the user's primary language.

The explanation must be user-facing, not internal process notes:

```markdown
# [Project/Feature Name] 說明

## 完成內容
[Plain-language summary of what was built]

## 如何使用
[How the user runs, opens, or uses the result]

## 主要功能
- [Feature]

## 專案結構
[Short explanation of important modules/files]

## 測試結果
[What passed, what could not be run, any known limitations]

## 後續建議
[Only practical next steps, if useful]
```

Do not write this file before implementation and tests are complete. In Goal Mode, write it once after all non-deferred Features are [PASS]. In Auto/Detailed mode, write it when the active Feature or requested project scope is complete.

---

## Templates

- `templates/spec-template.md` - User stories, functional requirements, acceptance criteria
- `templates/plan-template.md` - Architecture, tech stack, data model, API contracts
- `templates/tasks-template.md` - Task breakdown with dependencies and parallel markers

---

## Guiding Principles for AI Agents

1. **Always start with Step 0** - never begin specifying without decomposing the project first
2. **One Feature at a time** - complete all 9 steps for a Feature before starting the next
3. **Scope discipline** - a Feature's spec.md must not describe behaviour belonging to another Feature
4. **Constitution is shared** - write it once in Step 1; all subsequent Features reference the same file
5. **All required steps are mandatory** - Step 1 may be reused if `constitution.md` already exists; Steps 2-9 may not be skipped
6. **Documents are the product** - spec/plan/tasks are first-class deliverables
7. **Project shape matters** - planning artifacts must form a project blueprint with modules, workflows, contracts, data, tasks, and tests mapped together; never leave outputs as disconnected parallel lists
8. **Lean SDD discipline** - choose the smallest correct requirement, module, contract, task, and implementation; remove speculative features, future-proof abstractions, new dependencies, and orphan work unless the approved spec earns them
9. **Respect the active mode** - detailed mode pauses at every gate; auto mode pauses mainly at Step 0/2/3 and at risk triggers
10. **Goal Mode specs first** - in Goal Mode, finish all Feature `spec.md` files and cross-spec alignment before planning or implementing any Feature
11. **Step 0 mode choice** - after Step 0, always ask the user to choose Goal, Auto, or Detailed mode before continuing
12. **User-language final explanation** - after completion, create `.specify/final-explanation.md` in the user's language
13. **Stay technology-agnostic** in Steps 1-4; only introduce tech stack in Step 5, except Goal Mode's project blueprint after the spec pack is aligned
14. **Checklist blocks planning** - resolve all [FAIL] items before proceeding to Step 5
15. **Tests must trace to spec** - every test references the AC it validates
16. **Feature is not done until tests pass** - Step 9 is the final gate

## Lean SDD Ladder

Before adding scope, architecture, tasks, code, dependencies, or files, stop at the first rung that works:

1. **Does this need to exist now?** If not required by the approved Feature, move it to Non-Goals or a later Feature.
2. **Already in this codebase?** Reuse existing helpers, modules, patterns, conventions, and tests.
3. **Standard library or native platform covers it?** Use that before custom code or dependencies.
4. **Already-installed dependency solves it?** Use it without adding another package.
5. **Can one existing module own it?** Extend the smallest appropriate module before creating a new one.
6. **Can one task or contract cover it clearly?** Avoid splitting work into ceremony.
7. **Only then:** create the minimum new module, contract, task, or implementation that satisfies the spec.

Lean SDD is efficient, not careless. Never cut validation at trust boundaries, security controls, authorization, accessibility basics, migration safety, data-loss handling, or tests required to prove acceptance criteria.

---

## Approval Protocol - CRITICAL

The active mode controls how gates behave.

- **Detailed mode:** every step ends with a Gate. The AI must not proceed until the user explicitly approves.
- **Auto mode:** Step 0, Step 2, and Step 3 are hard gates. Steps 4-9 produce artifacts and continue automatically unless a risk trigger appears.
- **Goal mode:** Step 0 creates the Feature map, then the AI writes all Feature specs, aligns the spec pack, creates a project blueprint, and batch-executes Features automatically. Stop only for risk triggers.

### Standard Gate Format

```
---
[PASS] Step [N] - [Step Name] complete  (Feature: NNN-feature-name)

Output: Output: [file path(s) created or updated]

Review: Please review the output above. When ready, choose:
  - Type "continue" or "next" -> proceed to Step [N+1] ([Step Name])
  - Type "revise [what]" -> rework this step before moving on
  - Type "stop" -> pause here; to resume say "continue from Step [N+1]"
---
```

### Gate Rules

- **Detailed mode:** never auto-proceed. One step -> one Gate -> one user response.
- **Auto mode:** after Step 3 approval, run the remaining steps as a pipeline. Report progress and artifacts, but do not wait unless a risk trigger appears.
- **Goal mode:** do not implement any Feature until every Feature spec is written and `.specify/spec-pack.md` is aligned. After that, run batch execution in dependency order and report progress.
- **No skipping steps.** A step may only be bypassed when its approved artifact already exists and the step's reference file explicitly allows reuse.
- **On "revise":** update the document, re-output it, show the Gate again.
- **On "stop":** state which step was completed, which comes next, and how to resume.
- **On resume:** re-read the relevant documents before continuing.

### Step Transition Map

| Step | Next | Detailed Mode | Auto Mode | Goal Mode | Special Rule |
|------|------|---------------|-----------|-----------|--------------|
| Step 0 - Epic | Mode choice | Wait | Wait | Wait | Always ask user to choose Goal, Auto, or Detailed mode |
| Step 1 - Constitution | Step 2 - Specify | Wait | Continue | Reuse/create once before Spec Sweep | Reuse if constitution.md already exists |
| Step 2 - Specify | Step 3 - Clarify | Wait | Wait | Run for every Feature without waiting | Main requirements approval in Auto/Detailed |
| Step 3 - Clarify | Step 4 / Next Feature Spec | Wait | Wait | Continue to next Feature spec | Main ambiguity approval in Auto/Detailed |
| Cross-Spec Alignment | Project Blueprint | - | - | Required | Create `.specify/spec-pack.md` |
| Project Blueprint | Batch Execution | - | - | Required | Create `.specify/project-blueprint.md` |
| Step 4 - Checklist | Step 5 - Plan | Wait | Continue unless unresolved [FAIL] needs user decision | Continue per Feature unless risk-triggered | All [FAIL] must be resolved or explicitly accepted |
| Step 5 - Plan | Step 6 - Analyze | Wait | Continue unless major architecture/risk decision appears | Continue, mapping to project-blueprint.md | Agent chooses the most useful artifact format |
| Step 6 - Analyze | Step 7 - Tasks | Wait | Continue unless unresolved inconsistency needs user decision | Continue unless cross-feature conflict appears | - |
| Step 7 - Tasks | Step 8 - Implement | Wait | Continue unless Step 8 risk trigger appears | Continue unless Step 8 risk trigger appears | - |
| Step 8 - Implement | Step 9 - Test | Wait | Continue unless large/destructive change needs approval | Continue unless large/destructive change needs approval | - |
| Step 9 - Test | Next Feature (Step 2 / Batch next) | Wait | Stop and report | Continue to next Feature until all [PASS] | Mark current Feature [PASS] in epic.md first |
| All Features [PASS] | Final Explanation | - | - | Stop and report | Create `.specify/final-explanation.md` in user's language |
