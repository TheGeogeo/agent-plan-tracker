# Execution: import preview

Back to [TRACKING.md](TRACKING.md).

## Mode

- Proposed: orchestrated subagents, awaiting the user's choice.
- Reason: three dependent, well-specified tasks with independent verification; a fresh subagent per task keeps each context small, and the orchestrator checks every result before committing it.
- Alternatives offered: all tasks in the current chat, or one task per chat with a handoff prompt between tasks.
- Orchestrating chat: most capable tier, high effort, for verification and the final review.

## Model and effort per task

Example host: Claude Code. Map the tiers onto the models that the host offers.

| Task | Executor | Model | Effort | Why |
| --- | --- | --- | --- | --- |
| IMP-01 | Read-only exploration subagent | Balanced tier | Medium | Reading and tracing callers; no edits, moderate breadth |
| IMP-02 | General-purpose subagent | Balanced tier | High | Implementation on a clear contract, but a wrong result could change stored data |
| IMP-03 | General-purpose subagent | Balanced tier | Medium | Runs existing checks and failure scenarios defined by IMP-01 |

## Commits and push

- Commits: after each verified task, on the project's working branch, following the project's commit conventions.
- Tracking files in commits: no, the tracking is local.
- Push: only on the user's explicit request.

## Usage gate

- Host and provider: Claude Code, Anthropic.
- Script: written by the orchestrating model into `.claude/scripts/` and verified once the user confirms the orchestrated mode, as described in the skill's usage-gate reference.
- Thresholds: short window (5 hours) above 80% before a task, except the last one; weekly above 90% before and after a task.
- Source: to check when the gate is written.
- Verification at creation: not run.

| Time | Check point | Output |
| --- | --- | --- |

## Handoff prompt

To write once the user chooses the mode.
