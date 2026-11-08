# Usage

Prompts for each stage of a tracking. Back to the [README](../README.md).

The prompts establish the task's scope. A request for a plan produces the tracking, a proposed execution mode, and its handoff; a request to execute authorizes implementation within the boundaries you give.

## Create a tracking

```text
Use planning-and-progress-tracking to plan the import-preview feature.
Inspect the existing architecture and test commands first.
Create ordered tasks with acceptance criteria and verification methods.
Keep this request limited to planning.
```

The agent creates `tracking/import-preview/` from the skill's templates, chooses a model and effort for each task, and proposes an execution mode for you to choose.

Trackings are written in English by default. To use another language, say so: `Write the tracking in French.`

## Strengthen an existing tracker

```text
Use planning-and-progress-tracking to strengthen the current roadmap.
Keep the existing files, completed work, and accepted decisions.
Add stable task IDs, dependencies, observable acceptance, and evidence fields.
Identify the current task and next concrete action.
```

## Execute the tracking

Pick the mode that fits; the agent records your choice in `execution.md`.

All tasks in the current chat:

```text
Execute the import-preview tracking in this chat.
Update each task after meaningful results and keep the resume record current.
Commit after each verified task; do not push.
```

One task per chat:

```text
Execute task IMP-01 of tracking/import-preview, then stop.
Update the tracking and give me the handoff prompt for the next task.
```

Orchestrated subagents:

```text
Orchestrate the import-preview tracking with one subagent per task,
using the models and effort recorded in execution.md.
Verify each task yourself and commit it, run the usage gate between tasks,
then do the final review and the final commit. Push at the end.
```

Leave out `Push at the end.` if you want the agent to ask before pushing.

## Resume a session

```text
Resume tracking/import-preview with planning-and-progress-tracking.
Read the resume record, the active task, and its latest evidence.
Check what changed since the handoff, then continue the next authorized action.
```

When the usage gate stopped an orchestration, paste the resume prompt that the agent wrote in `execution.md`.

## Close and archive

```text
Close the import-preview tracking: compare the result with its acceptance,
record the remaining limits, and archive it.
```
