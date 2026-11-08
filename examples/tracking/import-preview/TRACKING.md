# Tracking: import preview

Created on 2026-01-15 with the `planning-and-progress-tracking` skill. Scope: [scope.md](scope.md). Execution: [execution.md](execution.md). Decisions: [decisions.md](decisions.md).

This illustrative tracking demonstrates the format. Every task is planned and every verification is unexecuted.

## Resume

- Active goal and phase: let a user preview an import before applying it; planning done, execution mode awaiting the user's choice.
- Active task and state: IMP-01, Planned.
- Last verified result and evidence: none; this is an illustrative starting plan.
- Remaining work, blocker, or required decision: the user chooses an execution mode (proposed in [execution.md](execution.md#mode)), then IMP-01 replaces the stated unknowns with findings from the actual project.
- Existing changes and artifacts to preserve: check the working tree and current project records before editing.
- Next concrete action: record the user's mode choice, then find the existing importer entry point, its callers, and its focused tests.

## Tasks

In execution order. Details are in each task file.

| # | ID | Result | State | Depends on | Next action |
| --- | --- | --- | --- | --- | --- |
| 1 | [IMP-01](tasks/IMP-01-preview-contract.md) | Preview contract fits the existing importer | Planned | None | Find the importer entry point |
| 2 | [IMP-02](tasks/IMP-02-preview-without-apply.md) | Preview produced without applying the import | Planned | IMP-01 | Wait for the IMP-01 contract |
| 3 | [IMP-03](tasks/IMP-03-failure-cases.md) | Failure cases verified and work closed | Planned | IMP-02 | Wait for IMP-02 acceptance |

States: Planned, Active, Awaiting verification, Done, Blocked, Deferred.
