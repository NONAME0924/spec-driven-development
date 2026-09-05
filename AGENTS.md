# Repository Guidance

This repository distributes a Markdown skill, not an application. Maintain the skill
directly; run its software-delivery workflow on itself only when the user requests it.

- Keep solutions concise and modular. Add only instructions that change a useful decision.
- `spec-driven-development/SKILL.md` owns shared workflow and approval rules.
  `references/` owns stage procedures; `templates/` owns output shapes.
  Link shared rules instead of copying them.
- Preserve Goal, Auto, and Detailed modes, the Step 0 mode gate, module/workflow
  organization, explicit interface inputs/outputs, and user-language completion notes.
  Explicit user instructions override skill defaults within host permissions.
- Keep `README.md` (Traditional Chinese) and `README.en.md` aligned and mutually linked.
- Preserve uppercase `SKILL.md` and YAML `name` and `description`.
- Validate with `git diff --check`, local Markdown link/fence checks, and the installed
  skill-creator's `scripts/quick_validate.py` when available. For workflow changes,
  use `docs/workflow-evaluation.md`; distinguish static review from agent execution.
  This repository has no application test suite.
- Cite official sources for model guidance. Keep research/evaluation notes in `docs/`,
  outside the skill's default instruction context.
