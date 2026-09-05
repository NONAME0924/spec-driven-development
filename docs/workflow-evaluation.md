# Workflow Evaluation

[繁體中文](../README.md) | [English](../README.en.md)

These are behavioral evaluation scenarios, not executable application tests.
Use the same model settings, permissions and fixtures when comparing revisions.
Do not give expected outcomes to a forward-testing agent before it attempts the request.

## Scenarios and Review Criteria

| Scenario | User Request / State | Observable Behavior to Evaluate |
|----------|----------------------|---------------------------------|
| New Goal | CSV expense CLI: import and monthly summary; Goal, Step 0 confirmation explicitly waived | Epic still created; all specs aligned before planning/code; assembled workflow verified |
| Auto continuation | Existing React project; export Feature, Steps 0/2/3 approved; a suitable local library is absent | Reuse approval; justify dependency; finish this Feature without an invented dependency gate |
| Specs only | Booking system; Goal, initial confirmation waived, explicitly no implementation | Complete and review specs/spec pack; no code or implementation tasks; explanation states document-only scope |
| Interrupted Goal | Two Feature passes; shared contract changes; integration credentials unavailable | Refresh impacted evidence, preserve unaffected work, report blocked integration; no false project PASS |
| Detailed | Known product outcome, Detailed chosen, no epic | Confirm breakdown without re-asking mode, then Steps 2/3; Steps 1 and 4-9 continue with detailed reporting and no extra gates |
| Ordinary maintenance | Explain a function or fix a README typo without requesting SDD | No imposed epic/spec/task pipeline |
| Small local Feature | One module, no network API or persistent data | No invented API layers, empty contracts or unrelated domain checklists |
| Steering | During Goal execution, user revises one requirement and asks status | Answer status, update affected documents and tasks, continue unchanged authorized scope |
| Verification failure | Test fails within approved scope | Investigate and fix without waiting for "fix all"; record actual evidence |
| Existing schema | API schema already maintained under the application's source directory | Link canonical schema and verify its I/O/errors; do not create a second inconsistent contract |

## Evaluation Method

Structural checks cover the skill entrypoint, frontmatter, links, Markdown fences and
whitespace. Scenario review checks gates, scope, ordering and truthful completion.
Neither alone establishes application correctness or model performance.

For an actual forward run, use an isolated temporary project with no live credentials.
Give the agent the user request, candidate skill and raw fixtures. Observe its artifacts,
tool actions and stops. Assess against these criteria afterward.

Compare baseline and candidate across repeated runs. Record completion/acceptance success,
unnecessary clarification count, elapsed time, token usage, unrequested artifacts or
dependencies, and defects. Keep prompts and environment fixed; report failures as well
as successful runs.

## This Revision

2026-09-05: an independent agent read the entrypoint, all references and templates and
simulated the first five scenarios. It identified a specs-only Goal completion conflict;
the candidate was updated to define the documentation endpoint explicitly. The same
reviewer confirmed the targeted fix resolves that conflict.
This was read-only scenario evaluation, not an end-to-end build or performance benchmark.

Subsequent user-requested change: Detailed now shares Auto's Steps 0/2/3 gates and
provides fuller reporting. Its updated scenario was checked against the mode table,
Step 9 and both READMEs locally; the independent simulation above predates this change.
