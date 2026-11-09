# Task and resume contract

These fields are the minimum information needed to act, verify, and resume. In a tracking folder, [tracking-folder.md](tracking-folder.md#what-each-file-owns) says which file holds each record. In an existing project convention, map them onto that convention instead.

## Task record

One file per task, started from [the task template](../assets/templates/task.md):

```markdown
# <ID> — Concrete result

- State: Planned | Active | Awaiting verification | Done | Blocked | Deferred
- Dependencies: Existing task IDs, or none.
- Why: The need this task addresses, with references.
- Work: The bounded outcome and affected area.
- Acceptance: Observable conditions that establish this task's result.
- Verification: The applicable command, inspection, or runtime scenario and expected observation.
- Evidence: Not run, or the observed result with revision/input and a usable reference.
- Limits: What the evidence does not cover. Optional: omit when empty.
- Accepted deviations: User-approved differences from the planned work. Optional: omit when empty.
- Resume: The next step of this task's own work, or the exact missing condition when blocked. Orchestration steps, such as the usage gate, a subagent launch, or a commit, go in the resume record of `TRACKING.md`.
```

Keep the project's existing state names when they carry the same distinctions. Distinguish the task's state from the overall project's or delivery phase's state.

Update the task table's state in `TRACKING.md` whenever the task's state changes.

## State rules

- Planned tasks may start only when their dependencies and required decisions are satisfied.
- Active means work has begun; it does not imply verification succeeded.
- Awaiting verification means the intended change exists but some required acceptance proof is missing.
- Done requires the task's acceptance evidence, or a clearly recorded owner decision changing that acceptance with stated limits. Dependent tasks must account for any limits relevant to them.
- Blocked names an actual missing capability, input, permission, or external condition and the action that can resolve it.
- Deferred keeps the reason and relevant owner decision. It does not satisfy a dependency merely by being deferred.
- A Done task whose proof is missing, contradicted, or invalidated by later evidence goes back to Awaiting verification, in its file and the task table, before you run any check again. Retain the superseded evidence with its revision and the reason.

## Evidence record

Record enough to assess the claim: revision or input, configuration when relevant, command or scenario, observed result, and artifact or source location. A future command and its expected output belong under verification, not evidence. Store evidence files under `evidence/<id>/` and cite them by relative path; link existing reports rather than copying long logs into the task. Never store credentials, tokens, or personal data in the tracking.

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

Refresh this record whenever the active task, phase, blocker, or next action changes, and before a session stops or hands off. Track progress by task acceptance and evidence rather than invented percentages, elapsed-time guesses, or code volume.
