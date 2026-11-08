# Task and resume contract

These fields are the minimum information needed to act, verify, and resume. In a tracking folder they live in the files described in [tracking-folder.md](tracking-folder.md). In an existing project convention, map them onto that convention instead.

Write in the tracking's language: English unless the user asked for another one. Quote user requests and decisions verbatim.

## Where each record lives

| Information | File in the tracking folder |
| --- | --- |
| Resume record and task table | `TRACKING.md` |
| Requests, goal, observable acceptance, scope, exclusions, constraints, work limits, unknowns | `scope.md` |
| Execution mode, model and effort per task, commit and push rules, usage gate, handoff prompt | `execution.md` |
| User decisions and their consequences | `decisions.md` |
| One task record per task | `tasks/<ID>-<slug>.md` |
| Logs, outputs, and other proof cited by tasks | `evidence/<id>/` |

## Task record

Start from [the task template](../assets/templates/task.md).

```markdown
# <ID> — Concrete result

- State: Planned | Active | Awaiting verification | Done | Blocked | Deferred
- Dependencies: Existing task IDs, or none.
- Why: The need this task addresses, with references.
- Work: The bounded outcome and affected area.
- Acceptance: Observable conditions that establish this task's result.
- Verification: The applicable command, inspection, or runtime scenario and expected observation.
- Evidence: Not run, or the observed result with revision/input and a usable reference.
- Limits: What the evidence does not cover, or none.
- Accepted deviations: User-approved differences from the planned work, or none.
- Resume: The next concrete action, or the exact missing condition when blocked.
```

Keep the project's existing state names when they carry the same distinctions. Distinguish the task's state from the overall project's or delivery phase's state.

The task file holds the details; the task table in `TRACKING.md` holds one line per task (ID, result, state, dependencies, next action). Update both together so they always agree.

## State rules

- Planned tasks may start only when their dependencies and required decisions are satisfied.
- Active means work has begun; it does not imply verification succeeded.
- Awaiting verification means the intended change exists but some required acceptance proof is missing.
- Done requires the task's acceptance evidence, or a clearly recorded owner decision changing that acceptance with stated limits. Dependent tasks must account for any limits relevant to them.
- Blocked names an actual missing capability, input, permission, or external condition and the action that can resolve it.
- Deferred keeps the reason and relevant owner decision. It does not satisfy a dependency merely by being deferred.
- Review and update an affected task after a new failure; retain the superseded evidence and identify the revision it described.

## Evidence record

Record enough to assess the claim: revision or input, configuration when relevant, command or scenario, observed result, and artifact or source location. A future command and its expected output belong under verification, not evidence. Store evidence files under `evidence/<id>/` and cite them by relative path; link existing reports rather than copying long logs into the task. Never store credentials, tokens, or personal data in evidence.

## Resume record

The resume record opens `TRACKING.md`.

```markdown
- Active goal and phase:
- Active task and state:
- Last verified result and evidence:
- Remaining work, blocker, or required decision:
- Existing changes and artifacts to preserve:
- Next concrete action:
```

Refresh this record before a session stops and whenever its next action becomes obsolete. Track progress by task acceptance and evidence rather than invented percentages, elapsed-time guesses, or code volume.
