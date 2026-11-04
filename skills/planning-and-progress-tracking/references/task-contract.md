# Task and resume contract

Use the project's language and existing layout. The following fields describe the minimum information needed to act, verify, and resume; they do not require a separate file per task.

## Plan header

- Goal and observable acceptance.
- Scope and exclusions; links to authoritative architecture or constraints.
- Canonical state and evidence locations.
- Material decisions, unknowns, and dependency order.

## Task record

```markdown
### TASK-ID — Concrete result

- State: Planned | Active | Awaiting verification | Done | Blocked | Deferred
- Dependencies: Existing task IDs, or none.
- Work: The bounded outcome and affected area.
- Acceptance: An observable condition that establishes this task's result.
- Verification: The applicable command, inspection, or runtime scenario and expected observation.
- Evidence: Not run, or the observed result with revision/input and a usable reference.
- Resume: The next concrete action or the exact missing condition when blocked.
```

Keep the project's existing state names when they carry the same distinctions. Distinguish the task's state from the overall project's or delivery phase's state. Use a table for compact records when it remains readable.

## State rules

- Planned tasks may start only when their dependencies and required decisions are satisfied.
- Active means work has begun; it does not imply verification succeeded.
- Awaiting verification means the intended change exists but some required acceptance proof is missing.
- Done requires the task's acceptance evidence, or a clearly recorded owner decision changing that acceptance with stated limits. Dependent tasks must account for any limits relevant to them.
- Blocked names an actual missing capability, input, permission, or external condition and the action that can resolve it.
- Deferred keeps the reason and relevant owner decision. It does not satisfy a dependency merely by being deferred.
- Review and update an affected task after a new failure; retain the superseded evidence and identify the revision it described.

## Evidence record

Record enough to assess the claim: revision or input, configuration when relevant, command or scenario, observed result, and artifact or source location. A future command and its expected output belong under verification, not evidence. Reuse existing reports rather than copying long logs into the plan.

## Resume record

```markdown
- Active goal and phase:
- Active task and state:
- Last verified result and evidence:
- Remaining work, blocker, or required decision:
- Existing changes and artifacts to preserve:
- Next concrete action:
- Canonical plan and evidence links:
```

Refresh this record before a session stops and whenever its next action becomes obsolete. Track progress by task acceptance and evidence rather than invented percentages, elapsed-time guesses, or code volume.
