# Step 1 - Constitution

## Purpose
Establish the project's governing principles **before** any specification or code is written. The constitution guides every subsequent decision made by the AI agent.

## When to Run
- At the very beginning of any new project
- When the project's scope, standards, or stakeholders significantly change

## What to Ask the User

Prompt the user with questions across these dimensions (ask all at once, not one-by-one):

1. **Code Quality** - What standards matter? (test coverage targets, linting rules, documentation requirements)
2. **Architecture** - Any hard constraints? (monorepo vs multi-repo, microservices vs monolith, specific patterns)
3. **User Experience** - Consistency rules? (design system, accessibility requirements, supported browsers/devices)
4. **Performance** - Any SLAs? (response time targets, throughput, uptime)
5. **Security** - Compliance requirements? (authentication standards, data handling, encryption)
6. **Team & Process** - How should the AI work? (PR size limits, commit message format, review gates)

## Output

Create `.specify/memory/constitution.md` using this structure:

```markdown
# Project Constitution

## Core Principles
[High-level values that govern all decisions]

## Code Quality Standards
- Test coverage: [target %]
- Code style: [linter/formatter]
- Documentation: [required for public APIs / all functions / etc.]

## Architecture Guidelines
- Pattern: [chosen architecture pattern]
- Key constraints: [non-negotiable decisions]

## User Experience Standards
- Design system: [if any]
- Accessibility: [WCAG level, etc.]
- Supported environments: [browsers, devices, OS]

## Performance Requirements
- Response time: [p95 target]
- Availability: [uptime SLA]

## Security & Compliance
- Auth standard: [OAuth2, SAML, etc.]
- Data classification: [handling rules]

## Development Process
- Branch strategy: [gitflow / trunk-based / etc.]
- PR guidelines: [size, review requirements]
- Commit format: [conventional commits, etc.]

## AI Agent Guidelines
[How the AI should behave in this project - what it can decide autonomously, what requires human approval]
```

## Example Prompt to User

> "Before we start building, let's establish your project's governing principles. These will guide every technical decision going forward. Tell me about:
> - What code quality standards matter most to you?
> - Any hard architectural constraints?
> - Performance or security requirements?
> - How should I (the AI) work with you - what can I decide independently vs. what needs your approval?"

## Gate

Show the full contents of `constitution.md` to the user, then output the standard Gate block:

```
---
[PASS] Step 1 - Constitution complete

Output: Output: .specify/memory/constitution.md

Review: Please review the output above. When ready, choose:
  - Type "continue" or "next" -> proceed to Step 2 (Specify)
  - Type "revise [what]" -> rework this step before moving on
  - Type "stop" -> pause the workflow here; to resume say "continue from Step 2"
---
```

**Mode rule:** In detailed mode, wait at this gate. In auto mode, continue to Step 2 automatically after creating or reusing `constitution.md`, unless the constitution introduces a process rule or approval boundary the user has not already accepted.
