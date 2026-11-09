# Execution: import preview

Back to [TRACKING.md](TRACKING.md).

## Mode

- Proposed: orchestrated subagents, awaiting the user's choice.
- Reason: three dependent, well-specified tasks with independent verification; a fresh subagent per task keeps each context small, and the orchestrator checks every result before committing it.
- Alternatives offered: all tasks in the current chat, or one task per chat with a handoff prompt between tasks.
- Orchestrating chat: most capable model, high effort, for verification and the final review.

## Model and effort per task

Each tier maps onto the host's current model when the task starts.

| Task | Executor | Model tier | Effort | Why |
| --- | --- | --- | --- | --- |
| IMP-01 | Read-only exploration subagent | Balanced | Medium | Reading and tracing callers; no edits, moderate breadth |
| IMP-02 | General-purpose subagent | Balanced | High | Implementation on a clear contract, but a wrong result could change stored data |
| IMP-03 | General-purpose subagent | Balanced | Medium | Runs existing checks and failure scenarios defined by IMP-01 |

## Commits and push

- Commits: after each verified task, on the project's working branch, following the project's commit conventions.
- Tracking files in commits: no, the tracking is local.
- Push: only on the user's explicit request.

## Usage gate

Written only if the user chooses the orchestrated mode, as described in the skill's usage-gate reference, with the default thresholds unless the user sets others.

## Handoff prompt

To write once the user chooses the mode.
