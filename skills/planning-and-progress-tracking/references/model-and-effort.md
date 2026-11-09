# Model and effort

For every tracking, choose the executor, model tier, and effort of each task while planning, and record them in `execution.md` with the reason. Aim for the least costly setting that can reliably meet the task's acceptance: an under-powered risky task costs more in rework than it saves.

## Model tiers

Record a tier, not a model name: model names change with each release, and each host offers its own.

- **Small fast model:** the host's cheapest and fastest model.
- **Balanced model:** the host's everyday model for implementation work.
- **Most capable model:** the host's strongest reasoning model.

When a task starts, use the host's current model for its tier, and record the model actually used with the task's evidence.

## Analyze each task

Weigh these factors:

- **Reasoning depth.** An unclear root cause, concurrency, security, architecture, or design trade-offs need stronger reasoning; dictated edits need little.
- **Cost of a wrong result.** Data loss, crashes, broken releases, or regressions that are hard to detect call for a stronger setting.
- **Breadth of context.** How much code and documentation the executor must read and keep consistent.
- **Verification load.** Long-running checks, runtime scenarios, or tools that the executor must drive and interpret.
- **How mechanical the work is.** Exact edits fully specified in the task suit the small fast model.

## Typical settings

| Task profile | Model tier | Effort |
| --- | --- | --- |
| Mechanical edits fully specified in the task | Small fast | Low |
| Implementation with a clear contract and existing tests | Balanced | Medium |
| Cross-cutting change, tricky state or concurrency, ambiguous failure | Most capable | High |
| Design decisions, or a task that already failed at a lower setting | Most capable | Highest available |

Use the effort levels that the host offers; do not name a model or effort level that it does not provide.

## Record the choice

Use this table in `execution.md`:

```markdown
| Task | Executor | Model tier | Effort | Why |
| --- | --- | --- | --- | --- |
| T1 | <subagent type, this chat, or new chat> | <small fast, balanced, or most capable> | <effort> | <reason> |
```

- **Executor:** the subagent type in the orchestrated mode, `this chat` in the current-chat mode, or `new chat` in the one-task-per-chat mode, where the user selects the model and effort when opening the chat and the handoff prompt states them.
- Also record the model tier and effort of the main or orchestrating chat. Its final review needs the strongest reasoning that the tracking justifies.

## Apply and revise

- Once the user approves the tracking, the recorded settings are the instruction for launching each subagent: pass the host's current model for the tier and the effort explicitly.
- If the host cannot set a model or effort per subagent, record the setting actually used.
- When evidence shows that a setting failed, for example repeated wrong results or missed acceptance, report it, record the new setting and its reason in `decisions.md`, and update the table.
