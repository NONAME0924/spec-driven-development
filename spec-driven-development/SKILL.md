---
name: spec-driven-development
description: >
  Spec-Driven Development (SDD) workflow skill. Use this skill whenever the user wants to build software by starting from an idea or requirements - whether it's a new greenfield project, adding features to an existing system, or modernizing legacy code. Triggers on phrases like "I want to build", "help me create an app", "let's develop a feature", "I have an idea for", "build me a", "help me plan this project", or any request to design, spec out, or implement software in a structured way. Also triggers when the user asks to create a spec, write a PRD, plan tasks, or break down implementation. This skill guides the AI through a gated workflow: decompose the project into Features (Step 0 - Epic), establish or reuse the project constitution (Step 1), then run each Feature through specify -> clarify -> checklist -> plan -> analyze -> tasks -> implement -> test.
---

# Spec-Driven Development (SDD) Skill

Build high-quality software faster by starting from structured specifications - not vibe coding.

## Core Philosophy

SDD flips traditional development: instead of jumping from idea to code, we move through structured phases where each step produces living documentation. The specification **is** the source of truth. Any AI agent can pick up where another left off because everything is written down.

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

---

## Directory Structure

```
.specify/
|-- epic.md                      <- Project feature map (Step 0)
|-- memory/
|   `-- constitution.md          <- Project principles (Step 1, shared across features)
|-- specs/
|   |-- 001-feature-name/
|   |   |-- spec.md              <- Requirements & user stories (Step 2)
|   |   |-- checklists/          <- Spec quality audit (Step 4)
|   |   |   |-- requirements.md
|   |   |   |-- ux.md
|   |   |   |-- api.md
|   |   |   `-- security.md
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
7. **Pause at gates** - never auto-proceed; always wait for explicit user approval
8. **Stay technology-agnostic** in Steps 1-4; only introduce tech stack in Step 5
9. **Checklist blocks planning** - resolve all [FAIL] items before proceeding to Step 5
10. **Tests must trace to spec** - every test references the AC it validates
11. **Feature is not done until tests pass** - Step 9 is the final gate

---

## Gate Protocol - CRITICAL

Every step ends with a Gate. The AI **must not proceed** until the user explicitly approves.

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

- **Never auto-proceed.** Even if the user seems happy, always show the Gate and wait.
- **Never combine two steps in one message.** One step -> one Gate -> one user response.
- **No skipping steps.** A step may only be bypassed when its approved artifact already exists and the step's reference file explicitly allows reuse.
- **On "revise":** update the document, re-output it, show the Gate again.
- **On "stop":** state which step was completed, which comes next, and how to resume.
- **On resume:** re-read the relevant documents before continuing.

### Step Transition Map

| Step | Next | Mandatory? | Special Rule |
|------|------|------------|--------------|
| Step 0 - Epic | Step 1 - Constitution | [PASS] Yes | - |
| Step 1 - Constitution | Step 2 - Specify | [PASS] Yes | Reuse if constitution.md already exists |
| Step 2 - Specify | Step 3 - Clarify | [PASS] Yes | - |
| Step 3 - Clarify | Step 4 - Checklist | [PASS] Yes | - |
| Step 4 - Checklist | Step 5 - Plan | [PASS] Yes | All [FAIL] must be resolved first |
| Step 5 - Plan | Step 6 - Analyze | [PASS] Yes | - |
| Step 6 - Analyze | Step 7 - Tasks | [PASS] Yes | - |
| Step 7 - Tasks | Step 8 - Implement | [PASS] Yes | - |
| Step 8 - Implement | Step 9 - Test | [PASS] Yes | - |
| Step 9 - Test | Next Feature (Step 2) | [PASS] Yes | Mark current Feature [PASS] in epic.md first |
| All Features [PASS] | Project Complete | - | - |
