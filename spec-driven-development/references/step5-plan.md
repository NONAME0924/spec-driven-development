# Step 5 - Plan

**Input:** Reviewed spec, repository structure/configuration, shared constraints;
in Goal, the aligned spec pack and project blueprint.
**Output:** `plan.md`, plus supporting artifacts only where useful.
**Completion:** Requirements map to an implementable structure with defined boundaries and verification.
**Gate:** Use [Modes and Gates](../SKILL.md#modes-and-gates).

## Project Blueprint

Use the [plan template](../templates/plan-template.md), adapting the presentation to
the Feature. Start with actual file layout and ownership, then connect workflows,
contracts, data, and verification. Include:

- Project Structure: files/modules that will change, following the repository.
- Module Map: responsibility, key paths, dependencies, and requirement justification.
- Workflow Map: user outcome, participating modules, interfaces, data, and verification.
- Decisions: important choices, consequences, and why new complexity is needed.
- Verification approach: relevant existing tests, new checks, and known environment needs.

A one-module feature can use compact tables or prose. Do not add UI/API/service/data
layers just because the template names them. In Goal, link the shared blueprint and
describe only feature-specific additions. Prefer one canonical definition for shared
contracts/data; every consumer links to it.

## Artifact Selection

| Artifact | Create when | Required content |
|----------|-------------|------------------|
| `plan.md` | Always for implementation planning | Structure, ownership, workflows, decisions, verification |
| `data-model.md` | Data changes need more detail than the plan | Owner, fields/types, requiredness, validation, relationships, lifecycle and migration implications |
| `research.md` | A consequential technical uncertainty needs investigation | Question, findings, source/version/date, decision and remaining uncertainty |
| `contracts/api-spec.json` | HTTP API schema is needed and no canonical schema exists | Valid OpenAPI document with request, response, error and authorization definitions |
| `contracts/events.md` | Event/message boundaries exist | Producer/consumer, schema, delivery/order assumptions, failures |
| `contracts/workflows.md` | Multi-stage flow is not fully described by the API schema | Stage inputs/outputs, owners, state transitions and failure behavior |

Existing canonical contracts can stay in their current location. Choose a compatible
machine-readable format for HTTP APIs; Markdown-only schemas are suitable for internal
workflows when no tooling consumes them. Do not create duplicate empty files.

## Input/Output Contracts

At each actual boundary specify field names, types, required/optional/null semantics,
validation, success output and failure output. HTTP contracts include method/path,
path/query/body parameters, status codes, relevant headers, error schema, and auth.
Include examples when they clarify semantics, but examples do not replace schemas.

For each meaningful workflow stage, record:
`Workflow | Stage | Owner | Input schema | Output schema | State change | Failure output`.
Define ordering, retries, idempotency, or rollback when the flow needs them. This applies
to API, CLI, event, job, and agent pipelines. Document real handoffs, not every helper call.

## Evidence and Choices

Inspect manifests, lockfiles, actual APIs, and existing test conventions first. Research
only unresolved or time-sensitive facts; use official sources matching the installed
version. Do not upgrade to the latest package or research every dependency by default.

Choose tools and abstractions based on current requirements and repository fit.
A single implementation can justify an interface when a framework or genuine boundary
needs it. New local dependencies can be selected within authorized scope; purchases or
material scope changes follow the shared decision policy.
