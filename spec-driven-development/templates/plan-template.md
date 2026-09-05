# Implementation Plan: [Feature]
**Feature ID:** [NNN-feature-name]
**Spec:** [Canonical spec path]
**Updated:** [Date]
**Goal blueprint:** [Link when applicable]

Adapt the format to the Feature. Preserve ownership and flow relationships; do not
create layers, dependencies, or files simply to fill the template.

## Project Structure
[Existing paths to change and justified additions. A small file tree is sufficient.]

## Module Map
| Module | Responsibility | Key Paths | Depends On | Requirement / Justification |
|--------|----------------|-----------|------------|-----------------------------|
| [Actual owner] | [Current responsibility] | [Paths] | [Actual dependency] | [AC/FR or necessary support] |

## Workflow Map
| Workflow | Requirement | Module Sequence | Contracts / Data | Verification |
|----------|-------------|-----------------|------------------|--------------|
| [User outcome] | [AC] | [Actual handoffs] | [Canonical links] | [Behavior check] |

## Technical Decisions
| Decision | Evidence / Constraint | Reason |
|----------|-----------------------|--------|
| [Only consequential choice] | [Existing configuration / source / assumption] | [Why it fits] |

## Interface Contracts
[Link canonical schemas. Add a summary for changed boundaries only.]

| Owner | Operation | Auth | Input Schema | Output Schema | Errors |
|-------|-----------|------|--------------|---------------|--------|
| [Module] | [Method/path, command or event] | [Requirement] | [Schema link] | [Schema link/status] | [Schema link/status] |

## Workflow Stage Contracts
[Inline for a short flow, or link contracts/workflows.md.]

| Workflow | Stage | Owner | Input Schema | Output Schema | State Change | Failure Output |
|----------|-------|-------|--------------|---------------|--------------|----------------|
| [Flow] | [Actual handoff] | [Module] | [Fields/types or link] | [Fields/types or link] | [Effect or none] | [Failure behavior] |

## Data
[Changed fields, validation, relationships, owner, migration implications; link canonical
schema or data-model.md when detailed. Omit if no data contract changes.]

## Verification Approach
[Affected acceptance criteria, existing checks, new tests/manual checks, required environment]

## Analysis
[Step 6 coverage/consistency findings and resolutions, or link analysis.md]

## Implementation Notes
[Material deviations, evidence, and affected contracts/requirements]
