# Step 8 - Implement

**Input:** Current spec, plan, tasks, relevant repository files and mode authorization.
**Output:** Working changes and tests; updated task state and significant plan deviations.
**Completion:** Implementation tasks are verified; final acceptance verification follows in Step 9.
**Gate:** Use [Modes and Gates](../SKILL.md#modes-and-gates).

Read the planned structure, owning modules, workflow contracts, and affected code.
Verify prerequisites for the active tasks. Goal's spec decisions need not be individually
user-approved; they must satisfy its aligned-spec-pack barrier.

Implement dependency-ready tasks in the existing architecture. Use available subagents
for independent bounded tasks when useful, with distinct write ownership and explicit
integration checks. Otherwise execute locally. Keep progress updates concise.

Implement and test in useful increments. Reuse appropriate tests and add coverage for
changed behavior and meaningful failure cases. Fix root causes and update tasks only
after their completion conditions pass. Step 9 consolidates evidence; it is not the
first opportunity to discover whether the code runs.

Adapt incidental plan details as the code teaches you more. Record material deviations
and update affected contracts/spec assumptions. If requirements change, apply the
shared decision policy and revalidate the affected artifacts. File count alone does
not define a large rewrite. Preparing a migration script and running it against live
data are different actions with different authorization needs.

Investigate failures autonomously within scope. If progress requires missing access,
a product decision, or an external change, record a precise blocker and continue
independent work. Repeating the same failed operation without new evidence is not progress.

Do not mark the Feature PASS here. Keep the repository's commit conventions when a
commit is authorized; this step does not itself authorize publishing or deployment.
