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

- Execute the tasks in dependency order in this chat, with the model tier and effort recorded for it.
- Update the task file, the task table, and the resume record at each meaningful checkpoint.
- Commit only as the user's instructions and the project's rules allow, and record that rule in `execution.md`.

## Mode 2: one task per chat

- Each task runs in a fresh chat that starts from `TRACKING.md`.
- Before a chat ends, update the task, the table, and the resume record, check the next task's setting as [Apply and revise](model-and-effort.md#apply-and-revise) describes, then write the handoff prompt for the next chat in `execution.md`: tracking path, task ID, the model tier and effort to select with the host model that matches the tier when the prompt is written, files to read first, permissions such as commits and pushes, and the stop condition (the end of that task).
- Give the user that prompt verbatim.
- Commit at the end of each task when the user chose to.

## Mode 3: orchestrated subagents

The main chat orchestrates. It does not do the tasks' work itself, except small corrections that it states in the task record.

Before the first task, check the working tree, then write and verify your own usage gate for the host, as described in [usage-gate.md](usage-gate.md).

For each task, in order:

1. **Launch one fresh subagent**, after checking its setting as [Apply and revise](model-and-effort.md#apply-and-revise) describes, with the agent type and effort recorded for the task, on the host's current model for its model tier. Its prompt points to the task file only, restates the acceptance, states that the State, Evidence, and Resume fields belong to the orchestrator, and forbids commits, pushes, and edits to the tracking files other than the task's evidence. Write the task file so that it is enough on its own: work, acceptance, verification, and the constraints that apply, citing any other file the subagent must read.
2. **Wait for its completion notice.** Do not assume the result.
3. **Verify personally.** Read the diff, cross-check its claims against the code, read the logs, and check every acceptance point. A subagent report is not evidence.
4. **Correct or stop.** If the result is insufficient, send corrections to the same subagent or fix a small error yourself and say so. If the acceptance cannot be reached, mark the task Blocked, stop, and ask the user.
5. **Record** the task file, the task table, the evidence, and the resume record.
6. **Commit the task** when Git is available: one commit per task, following the project's and the user's commit rules. Include tracking files only when the tracking is versioned.
7. **Gate after the task.** Unless this was the last task, run the usage gate. On STOP or UNAVAILABLE, follow the stop procedure below.

After the last task, without a gate, so that the tracking finishes:

1. **Final review.** First check each Done task's proof, as in step 1 of the [Close step](tracking-folder.md#lifecycle). Then review the whole change range against the acceptance in `scope.md`: full diff, the relevant full checks, documentation consistency, interactions between tasks, and leftover debugging code.
2. **Finish the corrections** that the review finds within scope and record them with evidence. Report out-of-scope problems to the user instead of fixing them.
3. **Final commit** when there are changes.
4. **Push** only if the user explicitly asked for it; otherwise ask. After a push, record the remote revision as evidence.
5. **Report** to the user what actually ran and what did not, then propose archiving.

### Stop procedure

Used when the usage gate returns STOP, or UNAVAILABLE after one retry. The gate runs after a task is recorded and committed, so no work is lost. The session ends here, even when the reset is near:

1. Do not launch another task.
2. Update the resume record with the gate output (percentages and reset times) and the next step.
3. Write into `execution.md` the exact prompt that resumes the orchestration in a new chat, including the orchestrating chat's model tier and effort to select with the matching host model. It gives the reset times as facts and repeats that a later STOP follows this procedure; it never tells the next chat to wait for a reset.
4. Commit the tracking changes when Git is available and the tracking is versioned.
5. Give the prompt to the user and end the session. Never wait for the reset inside the session: no sleep, scheduled wake-up, timer, or repeated gate run. The user resumes by pasting the prompt in a new chat.

## Without Git

Skip the commits, record in the evidence that the changes are uncommitted, and list the files to preserve in the resume record.

## Host support

Mode 3 needs a host that can launch subagents with a chosen model. The usage gate needs a host whose plan usage can be read; when it cannot, record that no gate is available and agree on pacing with the user.
