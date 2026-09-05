# Step 2 - Specify

**Input:** Feature scope from `epic.md`, shared constraints, existing behavior, user requirements.
**Output:** `.specify/specs/NNN-feature-name/spec.md`.
**Completion:** Required behavior is bounded and has observable acceptance criteria.
**Gate:** Use [Modes and Gates](../SKILL.md#modes-and-gates); Goal does not wait here.

Use the [spec template](../templates/spec-template.md). Capture what the user needs
and why, including relevant failure paths, permissions, and data lifecycle.
Record known technical constraints without prematurely designing the solution.

Give acceptance criteria stable IDs such as `AC-001`. There is no minimum count:
cover the actual behavior without padding. Use Feature-qualified IDs for cross-feature
references. Avoid duplicating the same requirement as both a story and a separate FR
unless the separate rule adds clarity.

Infer behavior necessary to make the requested workflow complete, but mark consequential
inferences as assumptions. Do not expand a login request into unrelated admin systems
or integrations. Preserve all requested functionality; put speculative additions in
Non-Goals or Deferred with a reason.

For existing projects, distinguish changed behavior from behavior to preserve.
Describe important external inputs and observable outputs at the requirements level;
technical schemas and internal stage contracts are designed in Step 5.

Update the Feature's state in `epic.md`. Present the reviewable spec at a required gate,
otherwise continue to clarification under the selected mode.
