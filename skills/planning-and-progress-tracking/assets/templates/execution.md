# Execution: <title>

Back to [TRACKING.md](TRACKING.md).

## Mode

- Chosen: <current chat | one task per chat | orchestrated subagents>, by the user on <YYYY-MM-DD>.
- Reason: <why this mode fits the tracking>.
- Main or orchestrating chat: <model>, <effort>.

## Model and effort per task

| Task | Executor | Model | Effort | Why |
| --- | --- | --- | --- | --- |
| T1 | <subagent type, this chat, or new chat> | <model> | <effort> | <reason> |

## Commits and push

- Commits: <after each verified task | at the end | not allowed>, on <branch>, following <commit rules>.
- Tracking files in commits: <yes, the tracking is versioned | no, the tracking is local>.
- Push: <only on the user's explicit request | requested on YYYY-MM-DD: "<quote>">.

## Usage gate

<!-- Orchestrated mode only. Otherwise, or when the host's usage cannot be read, replace this section with: "Not used: <reason>." -->

- Host and provider: <host>, <provider>.
- Script: `<host configuration folder>/scripts/usage-gate.<extension>`, excluded from version control. Command: `<command>`.
- Thresholds: short window (<5 hours>) above <80>% before a task, except the last one; weekly above <90>% before and after a task.
- Source: <source>, checked on <YYYY-MM-DD>.
- Verification at creation: <results of the checks in the skill's usage-gate reference>.

| Time | Check point | Output |
| --- | --- | --- |

## Handoff prompt

<The exact prompt for the next chat: tracking path, task ID, model and effort to select, files to read first, permissions, and the stop condition.>
