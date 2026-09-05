# Step 3 - Clarify

**Input:** Draft spec, current repository behavior, constraints, previous answers.
**Output:** Updated `spec.md` with decisions, assumptions, and explicit blockers.
**Completion:** No unresolved question prevents a correct plan.
**Gate:** Use [Modes and Gates](../SKILL.md#modes-and-gates); Goal resolves ordinary details autonomously.

Check the relevant user flows, failure cases, permissions, data lifecycle, concurrency,
and integration boundaries. Review only dimensions the Feature touches.

Classify gaps by consequence. Resolve routine choices using existing conventions and
the smallest sufficient behavior. Ask focused questions when answers materially change
scope or correctness and cannot be inferred. Bundle related questions; continue useful
independent work while a blocking answer is pending.

Record meaningful decisions in the spec:
`ID | Question | Decision | Basis (user/repo/assumption) | Affected ACs`.
Update the affected requirements, not just the decision table. Assumptions must not
appear as user approvals. Do not invent arbitrary resource limits, unlimited storage,
new roles, or new integrations as default answers.

In Auto/Detailed, present the clarified spec and assumptions at the Step 3 gate,
including a brief "no unresolved ambiguities" result when applicable. In Goal, update
the spec pack and continue to the next Feature's spec until the sweep is complete.
