# Spec-Driven Development Skill

English | [繁體中文](README.md)

This is a **Spec-Driven Development (SDD)** skill for AI coding agents. Its goal is to prevent pure vibe coding by turning requirements, Feature boundaries, specs, architecture, tasks, implementation, and tests into durable, traceable documents that another agent or human can continue from.

This skill currently supports three modes:

- **Goal Mode**: Fully automatic project/goal execution. Write all Feature specs first, then perform global planning and batch implementation.
- **Auto Mode**: Automatic execution for one Feature. Step 0/2/3 are the main confirmation points, then the rest proceeds automatically.
- **Detailed Mode**: Manual detailed execution. Every step pauses for user approval.

It also includes **Lean SDD (Lean Spec-Driven Development)**: build the smallest correct requirements, architecture, tasks, and implementation while preserving security, validation, data protection, accessibility, and spec-traced tests.

---

## Usage

### 1. Trigger the skill

Use this skill when the user asks for work such as:

- "I want to build an app"
- "Help me plan this project"
- "Write a PRD / spec"
- "Break this feature into tasks"
- "Finish this in auto mode"
- "Use goal mode for the whole project"
- "Build the smallest viable but complete implementation"

### 2. Always start with Step 0

Regardless of the eventual mode, first run **Step 0 - Epic** to decompose the big goal into Features.

After Step 0, ask the user to choose a mode:

```text
Choose execution mode:
- goal mode: write all Feature specs first, then batch plan and execute automatically
- auto mode: process one Feature at a time; Step 2/3 are the main approval gates
- detailed mode: pause for approval at every step
```

### 3. Execute by mode

After a mode is selected, follow that workflow. When the requested scope is complete, create a user-language explanation file:

```text
.specify/final-explanation.md
```

Match the user's language. If the user wrote in Chinese, write Chinese. If the user wrote in English, write English.

---

## Modes

### Goal Mode

Use for a whole project or broad goal, such as "build a SaaS", "build a game", or "finish the whole system".

Flow:

1. Step 0 creates `epic.md`
2. Run Step 2 + Step 3 for every Feature to create all `spec.md` files
3. Create `.specify/spec-pack.md`
4. Create `.specify/project-blueprint.md`
5. Automatically run Step 4-9 for Features in dependency order
6. Create `.specify/final-explanation.md` after all non-deferred Features are complete

Goal Mode is valuable because it sees the full project before implementation begins, reducing later rework in APIs, data models, module boundaries, and shared workflows.

### Auto Mode

Use for a single Feature or smaller request.

Flow:

1. Step 0 creates or updates `epic.md`
2. User selects `auto mode`
3. Step 2 creates `spec.md` and confirms the requirements
4. Step 3 records clarifications and assumptions
5. Step 4-9 run automatically
6. Create or update `.specify/final-explanation.md`

Auto Mode stops only for major risks, such as:

- New external dependency or paid service
- Destructive migration
- Large rewrite
- Security, permission, or privacy decision
- Spec conflict that cannot be safely assumed

### Detailed Mode

Use for teaching, review-heavy workflows, or strict process control.

Step 0 through Step 9 each pause for user approval. The user must type `continue` / `next` before the next step begins.

---

## Step Guide

### Step 0 - Epic

Purpose: split the big goal into deliverable Features.

Does:

- Understand the full project goal
- Identify Features
- Define each Feature's scope, out of scope, and dependencies
- Decide delivery order

Main output:

- `.specify/epic.md`

### Step 1 - Constitution

Purpose: establish project governance.

Does:

- Define coding style
- Define testing expectations
- Define security, performance, and accessibility principles
- Define what the AI can decide alone and what needs user approval

Main output:

- `.specify/memory/constitution.md`

### Step 2 - Specify

Purpose: write one Feature as a clear requirements spec.

Does:

- Write overview, problem statement, and goals
- Write user stories
- Write acceptance criteria
- Write functional requirements
- Write non-goals and deferred scope
- Apply Lean SDD to remove speculative scope

Main output:

- `.specify/specs/NNN-feature-name/spec.md`

### Step 3 - Clarify

Purpose: resolve ambiguity and record assumptions.

Does:

- Identify happy paths, error states, and edge cases
- Clarify permissions, data lifecycle, and integrations
- Make the smallest safe assumption where appropriate
- Record clarifications and assumptions

Main output:

- Updates `.specify/specs/NNN-feature-name/spec.md`

### Step 4 - Checklist

Purpose: audit spec quality.

Does:

- Check whether requirements are complete, clear, and testable
- Check UX states
- Check API / integration formats
- Check security, permissions, and data handling
- Check Lean SDD issues such as overengineering and speculative scope

Main outputs:

- `.specify/specs/NNN-feature-name/checklists/requirements.md`
- `.specify/specs/NNN-feature-name/checklists/ux.md`
- `.specify/specs/NNN-feature-name/checklists/api.md`
- `.specify/specs/NNN-feature-name/checklists/security.md`
- `.specify/specs/NNN-feature-name/checklists/minimalism.md`

### Step 5 - Plan

Purpose: turn the spec into a project blueprint and technical plan.

Does:

- Create Project Structure
- Create Module Map
- Create Workflow Map
- Design API contracts
- Design workflow stage contracts
- Design data model
- Decide tech stack
- Use the Lean Planning Ladder to avoid unnecessary modules, dependencies, and abstractions

Main outputs:

- `.specify/specs/NNN-feature-name/plan.md`
- `.specify/specs/NNN-feature-name/data-model.md` when data modeling is needed
- `.specify/specs/NNN-feature-name/research.md` when technical research is needed
- `.specify/specs/NNN-feature-name/contracts/` when API / event / workflow contracts are needed

### Step 6 - Analyze

Purpose: check consistency across artifacts.

Does:

- Verify spec coverage in the plan
- Find orphan components with no requirement
- Verify data model coverage
- Verify API / workflow contracts
- Verify Module Map / Workflow Map
- Find Lean SDD violations such as one-implementation interfaces, unnecessary caches, or unnecessary dependencies

Main output:

- `.specify/specs/NNN-feature-name/analysis.md`

### Step 7 - Tasks

Purpose: turn the plan into executable tasks.

Does:

- Group tasks by Module Map
- Group tasks by Workflow Map
- Ensure every task maps to a requirement, module, workflow, contract, or data model
- Run a Task Pruning Pass to remove speculative scaffolding

Main output:

- `.specify/specs/NNN-feature-name/tasks.md`

### Step 8 - Implement

Purpose: implement according to `tasks.md`.

Does:

- Read Project Structure / Module Map / Workflow Map first
- Implement in the correct module and folder
- Reuse existing codebase patterns
- Avoid unapproved new dependencies
- Avoid one-implementation abstractions
- Mark completed tasks as `[DONE]`

Main outputs:

- Code changes
- Updated `.specify/specs/NNN-feature-name/tasks.md`
- Updated `plan.md` Implementation Notes when needed

### Step 9 - Test

Purpose: verify that implementation satisfies the spec.

Does:

- Create acceptance criteria coverage map
- Write unit / integration / acceptance tests
- Run tests
- Fix failing tests
- Update epic Feature status

Main outputs:

- `.specify/specs/NNN-feature-name/test-report.md`
- Creates or updates `.specify/final-explanation.md` when the requested scope is complete

---

## Goal Mode Project Artifacts

### `.specify/spec-pack.md`

Purpose: cross-Feature spec overview for Goal Mode.

Includes:

- Status of each Feature spec
- Cross-Feature decisions
- Shared roles, data, workflows, and contracts
- Conflicts and resolutions
- Deferred scope
- Execution order

### `.specify/project-blueprint.md`

Purpose: global project blueprint for Goal Mode.

Includes:

- Global Project Structure
- Global Module Map
- Global Workflow Map
- Shared Data Model
- Shared Contracts
- Execution Plan

### `.specify/final-explanation.md`

Purpose: user-facing completion explanation.

Includes:

- What was completed
- How to use it
- Main features
- Project structure
- Test results
- Deferred scope
- Suggested next steps

---

## Lean SDD Principles

Lean SDD = **Lean Spec-Driven Development**.

Core rules:

1. If it is not needed now, do not build it
2. If the codebase already has it, reuse it
3. If native / stdlib can solve it, do not reinvent it
4. If an installed dependency can solve it, do not add a new dependency
5. If one existing module can own it, do not create another module
6. If one clear task / contract can describe it, do not split it into ceremony
7. Only add architecture, dependencies, tasks, or code when the spec earns them

Do not remove:

- Trust-boundary validation
- Auth / authorization
- Security controls
- Data-loss protection
- Migration safety
- Accessibility basics
- Spec-traced tests

---

## Skill File Structure

```text
.
|-- README.md
|-- README.en.md
|-- LICENSE
|-- .gitignore
|-- .gitattributes
`-- spec-driven-development/
    |-- SKILL.md
    |-- references/
    |   |-- goal-mode.md
    |   |-- step0-epic.md
    |   |-- step1-constitution.md
    |   |-- step2-specify.md
    |   |-- step3-clarify.md
    |   |-- step4-checklist.md
    |   |-- step5-plan.md
    |   |-- step6-analyze.md
    |   |-- step7-tasks.md
    |   |-- step8-implement.md
    |   `-- step9-test.md
    `-- templates/
        |-- constitution-template.md
        |-- spec-template.md
        |-- plan-template.md
        `-- tasks-template.md
```

---

## Attribution

Some workflow concepts reference [github/spec-kit](https://github.com/github/spec-kit).

## License

MIT. See [LICENSE](LICENSE).
