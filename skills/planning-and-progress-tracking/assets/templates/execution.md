# Execution: <title>

Back to [TRACKING.md](TRACKING.md).

## Mode

- Chosen: <current chat | one task per chat | orchestrated subagents>, by the user on <YYYY-MM-DD>.
- Reason: <why this mode fits the tracking>.
- Main or orchestrating chat: <model tier>, <effort>.

## Model and effort per task

| Task | Executor | Model tier | Effort | Why |
| --- | --- | --- | --- | --- |
| T1 | <subagent type, this chat, or new chat> | <small fast, balanced, or most capable> | <effort> | <reason> |

## Commits and push

- Commits: <after each verified task | at the end | not allowed>, on <branch>, following <commit rules>.
- Tracking files in commits: <yes, the tracking is versioned | no, the tracking is local>.
- Push: <only on the user's explicit request | requested on YYYY-MM-DD: "<quote>">.

## Usage gate

<!-- Orchestrated mode only. Otherwise, or when the host's usage cannot be read, replace this section with: "Not used: <reason>." -->

- Host and provider: <host>, <provider>.
- Script: `<host configuration folder>/scripts/usage-gate.<extension>`, excluded from version control. Command: `<command>`.
- Thresholds: short window (<duration>) at <80>% or more, weekly at <90>% or more, checked after each task except the last.
- Source: <source>, checked on <YYYY-MM-DD>.
- Verification at creation: <results of the checks in the skill's usage-gate reference>.
- Log: `evidence/usage-gate.log`, written by the gate.

## Handoff prompt

<The exact prompt for the next chat: tracking path, task ID, model tier and effort to select with the matching host model, files to read first, permissions, and the stop condition.>
