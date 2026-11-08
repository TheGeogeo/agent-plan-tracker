# Execution modes

Once the plan exists, propose the three modes, recommend one with a reason, and record the user's choice in `execution.md`. A tracking with a single small task can run in the current chat without this proposal. If the user switches modes later, record the switch in `decisions.md`.

Every mode follows the [task contract](task-contract.md): start a task only when its dependencies are satisfied, verify it against its acceptance, record evidence, and refresh the resume record.

## Choose a mode

| Mode | Fits | Costs |
| --- | --- | --- |
| 1. Current chat | Few tasks, shared context helps, the user follows along | Context grows; long trackings may need compaction |
| 2. One task per chat | Long tasks, fresh context per task, the user reviews between tasks | The user opens each chat; handoff quality decides the result |
| 3. Orchestrated subagents | Several well-specified tasks, independent verification, unattended progress | More model usage; needs a host that launches subagents |

## Mode 1: current chat

- Execute the tasks in dependency order in this chat, with the model and effort recorded for it.
- Update the task file, the task table, and the resume record at each meaningful checkpoint.
- Commit only as the user's instructions and the project's rules allow, and record that rule in `execution.md`.

## Mode 2: one task per chat

- Each task runs in a fresh chat that starts from `TRACKING.md`.
- Before a chat ends, update the task, the table, and the resume record, then write the handoff prompt for the next chat in `execution.md`: tracking path, task ID, the model and effort to select, files to read first, permissions such as commits and pushes, and the stop condition (the end of that task).
- Give the user that prompt verbatim.
- Commit at the end of each task when the user chose to.

## Mode 3: orchestrated subagents

The main chat orchestrates. It does not do the tasks' work itself, except small corrections that it states in the task record.

Before the first task, check the working tree, then write and verify your own usage gate for the host, as described in [usage-gate.md](usage-gate.md).

For each task, in order:

1. **Gate before launch.** Run the usage gate at the `before-task` point, with the last-task flag for the last task. On STOP or UNAVAILABLE, follow the stop procedure below.
2. **Launch one fresh subagent** with the agent type, model, and effort recorded for the task. Its prompt points to the task file only, restates the acceptance, states that the State, Evidence, and Resume fields belong to the orchestrator, and forbids commits, pushes, and edits to the tracking files other than the task's evidence. Write the task file so that it is enough on its own: work, acceptance, verification, and the constraints that apply, citing any other file the subagent must read.
3. **Wait for its completion notice.** Do not assume the result.
4. **Verify personally.** Read the diff, cross-check its claims against the code, read the logs, and check every acceptance point. A subagent report is not evidence.
5. **Correct or stop.** If the result is insufficient, send corrections to the same subagent or fix a small error yourself and say so. If the acceptance cannot be reached, mark the task Blocked, stop, and ask the user.
6. **Record** the task file, the task table, the evidence, and the resume record.
7. **Commit the task** when Git is available: one commit per task, following the project's and the user's commit rules. Include tracking files only when the tracking is versioned.

After the last task:

1. **Gate after the last task.** Run the usage gate at the `after-last` point. On STOP or UNAVAILABLE, follow the stop procedure; the final review then starts the next session.
2. **Final review.** First read each Done task's proof ([state rules](task-contract.md#state-rules)). Then review the whole change range against the acceptance in `scope.md`: full diff, the relevant full checks, documentation consistency, interactions between tasks, and leftover debugging code.
3. **Finish the corrections** that the review finds within scope and record them with evidence. Report out-of-scope problems to the user instead of fixing them.
4. **Final commit** when there are changes.
5. **Push** only if the user explicitly asked for it; otherwise ask. After a push, record the remote revision as evidence.
6. **Report** to the user what actually ran and what did not, then propose archiving.

### Stop procedure

Used when the usage gate returns STOP, or UNAVAILABLE after one retry. The gate runs between tasks, so the finished task is already recorded and committed:

- Do not launch another task.
- Update the resume record with the gate output (percentages and reset times) and the next step, write the exact prompt that resumes the orchestration in a new chat into `execution.md`, and give it to the user.

## Without Git

Skip the commits, record in the evidence that the changes are uncommitted, and list the files to preserve in the resume record.

## Host support

Mode 3 needs a host that can launch subagents with a chosen model. The usage gate needs a host whose plan usage can be read; when it cannot, record that no gate is available and agree on pacing with the user.
