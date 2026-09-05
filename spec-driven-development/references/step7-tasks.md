# Step 7 - Tasks

**Input:** Consistent plan, requirements, relevant contracts and existing project state.
**Output:** `tasks.md` grouped by owning modules and integration workflows.
**Completion:** Work is executable, ordered by real dependencies, and verifiable.
**Gate:** Use [Modes and Gates](../SKILL.md#modes-and-gates).

Use the [task template](../templates/tasks-template.md). Each task needs a stable ID,
owner/module, affected paths, requirement or implementation justification, dependencies,
action, and observable completion condition. Link workflow/contract/data only when relevant.

Group by module and workflow. Add Foundation or cross-cutting sections only for actual
shared work. Prefer useful vertical increments where possible. Include verification
alongside implementation, not only in a final testing phase.

Remove speculative scaffolding and merge tiny steps into meaningful outcomes.
"Folder exists" is not a useful standalone delivery task. Do not create shared
primitives before identifying current callers.

Mark a task `[P]` only when dependencies are satisfied and files/state permit concurrent
work. Adjacency in the document does not imply independence. Record file ownership
for parallel writes and an integration task for work that must be assembled.

Check every task against the Module/Workflow Map and requested acceptance criteria.
Use TODO, IN PROGRESS, DONE, BLOCKED; DONE means its stated check has actually passed.
