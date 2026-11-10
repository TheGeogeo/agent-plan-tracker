# How it works

An overview for readers of this repository. The exact rules the agent follows are in the skill's references, linked from each section. Back to the [overview](README.md).

## The workflow

1. **Find the current state.** Read the existing plan, the active task, recent evidence, relevant project instructions, and the latest explicit decisions.
2. **Define the outcome.** Establish observable acceptance, scope, exclusions, and the architecture constraints that matter to the change.
3. **Build the task graph.** Give tasks stable IDs and clear results, order them by actual dependencies, and choose a model tier and effort for each.
4. **Choose the execution mode.** Propose the modes, record your choice, and prepare its handoff.
5. **Work and verify.** Execute authorized work, collect the relevant proof, and update the affected task at meaningful checkpoints.
6. **Keep the resume point current.** Record the active task, the missing condition or remaining work, and a concrete next action before handing off.
7. **Close against acceptance.** Compare the delivered result with the agreed outcome, keep the remaining limits, and archive the tracking once you agree.

## Tracking folder

Without an existing convention, the agent creates `tracking/` with a `README.md`, an `archive/` folder, and one folder per tracking. The README explains, step by step, how a tracking is structured and how it works, and lists the active and archived trackings.

A tracking is split into small files that each own one topic: `TRACKING.md` for the resume record and task table, `scope.md`, `execution.md`, `decisions.md`, one file per task in `tasks/`, and proof in `evidence/`. Files link to each other instead of copying text, with links that stay valid when the folder moves to `archive/`.

The folder follows your project's rules on versioning plans; when plans must stay out of Git, the agent excludes it locally through `.git/info/exclude`.

Rules: [tracking-folder.md](../../skills/planning-and-progress-tracking/references/tracking-folder.md). Starting files: [assets/templates/](../../skills/planning-and-progress-tracking/assets/templates/).

## Execution modes

| Mode | How it runs |
| --- | --- |
| Current chat | The agent executes the tasks in order in the same chat. |
| One task per chat | Each task runs in a fresh chat; the agent writes the handoff prompt for the next one. |
| Orchestrated subagents | The chat launches one fresh subagent per task with the recorded model tier and effort, verifies the result itself, and commits each verified task when Git is available. After the last task, it reviews the whole change, finishes the corrections, and makes the final commit. |

Pushing happens only on your explicit request; otherwise the agent asks.

Rules: [execution-modes.md](../../skills/planning-and-progress-tracking/references/execution-modes.md).

## Model and effort

While planning, the agent analyzes each task for the least costly model tier and effort that can reliably meet its acceptance, weighing reasoning depth, the cost of a wrong result, the breadth of context, the verification load, and how mechanical the work is. The tiers are the small fast model, the balanced model, and the most capable model; the tracking records the tier, and the agent maps it onto the host's current model when the task starts, so the tracking stays valid when new models are released. The choice and its reason are recorded in `execution.md` and passed to each subagent. Before each task starts, the agent compares its setting with what the tracking recorded since the setting was chosen: when a recorded fact contradicts the setting's reason, it may raise the tier, the effort, or both by one level each, lowers them only with your approval, and never changes them to save usage.

Rules: [model-and-effort.md](../../skills/planning-and-progress-tracking/references/model-and-effort.md).

## Usage gate

In the orchestrated mode, a usage gate checks the plan's short-window and weekly usage after each task except the last, once the task is verified and committed, never while a subagent runs. When usage reaches a threshold, the orchestration stops before the next task. After the last task it never stops, so the tracking finishes. The default thresholds and their exceptions are in the [rules of usage-gate.md](../../skills/planning-and-progress-tracking/references/usage-gate.md#rules), and each tracking records its own in `execution.md`. When the gate stops, the finished task is already verified and committed, and the agent writes a handoff prompt that resumes the orchestration in a new chat and names the model tier and effort to select for it. The session then ends: the agent never waits for the reset itself. The gate keeps its own log in the tracking's `evidence/`.

The skill ships no script and gives no link or source for reading usage. When you choose this mode, the model writes its own detection script for the host and provider it runs on, from that provider's current documentation. It places the script in the folder where the host keeps its project configuration and verifies it before use. If you already have your own script, the agent uses it instead once it passes the same checks; if a reading equal to a threshold would not stop it, the agent points that out and has it fixed, with your agreement, before the first task. If the source needs credentials, the gate reads them at run time from where the host stores them and sends them only to the provider's own service; it contains no credentials, environment values, or personal paths, and it stays out of version control. If the host's usage cannot be read, the agent agrees on pacing with you instead.

Rules: [usage-gate.md](../../skills/planning-and-progress-tracking/references/usage-gate.md).

## Task states and evidence

The skill keeps your project's vocabulary when it carries the same distinctions. Its default task model is:

| State | Meaning |
| --- | --- |
| Planned | Work has not started. Dependencies or required decisions may still be pending. |
| Active | Work is underway. |
| Awaiting verification | The intended result exists, but required acceptance proof is missing. |
| Done | The task's acceptance is supported by evidence or an explicit decision changing that acceptance, with its limits recorded. |
| Blocked | A specific missing condition prevents progress; the resumption action is recorded. |
| Deferred | Work has been deliberately postponed, with a reason. Deferral alone does not satisfy a dependency. |

A future test command belongs under **Verification**. An observed test result belongs under **Evidence**, with the revision or input, the command or scenario, the observed result, and an artifact or source location.

If you accept a limitation, the agent records that decision and the checks still unexecuted. If a Done task's proof turns out missing, contradicted, or invalidated by a later failure, the agent returns the task to Awaiting verification while preserving its earlier evidence.

Rules: [task-contract.md](../../skills/planning-and-progress-tracking/references/task-contract.md).
