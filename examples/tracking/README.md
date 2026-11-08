# Tracking

Execution trackings for this project, maintained with the `planning-and-progress-tracking` skill.

This is an illustrative example. It does not describe an existing project, implementation, or test result.

Version control: this folder is local only, excluded through `.git/info/exclude`.

## Layout

```text
tracking/
  README.md               This file: how trackings work, and the index
  archive/<name>/         Closed trackings, moved unchanged
  <name>/
    TRACKING.md           Start here: resume record and task table
    scope.md              Requests, goal, acceptance, scope, work limits
    execution.md          Mode, model and effort per task, commits, usage gate, handoff
    decisions.md          User decisions and their consequences
    tasks/<ID>-<slug>.md  One file per task
    evidence/<id>/        Proof cited by the tasks
```

Each file owns one topic and links to the others instead of copying them.

## How a tracking works

1. **Create.** Work with several dependent steps gets its own folder, `<name>/`, created from the skill's templates and listed under Active below.
2. **Scope.** `scope.md` quotes the requests verbatim and fixes the goal, the observable acceptance, the exclusions, and the work limits.
3. **Plan the tasks.** Each task gets a stable ID and its own file in `tasks/` with its dependencies, acceptance, verification, and evidence. `TRACKING.md` lists the tasks in execution order.
4. **Choose models and effort.** Each task is analyzed for the least costly model and effort that can reliably meet its acceptance. The choice and its reason go in `execution.md`.
5. **Choose the execution mode.** The user picks one, and `execution.md` records it:
   - all tasks in the current chat;
   - one task per chat, with a handoff prompt between tasks;
   - an orchestrating chat that runs one subagent per task, commits after each verified task when Git is available, then performs a final review, the last corrections, and the final commit. Pushing needs the user's explicit request.
6. **Execute and verify.** A task starts when its dependencies are met. It becomes Done only when evidence, stored in `evidence/` or cited by reference, supports its acceptance.
7. **Pace usage.** In the orchestrated mode, a usage gate that the agent writes for its own host into the project's host configuration folder (`.claude/` on Claude Code) runs between tasks. It stops before a new task when short-window usage, such as 5 hours, passes its threshold, except before the last task, and before any task or after the last one when weekly usage passes its threshold. The thresholds are in `execution.md`. The finished work is then committed and a handoff is written.
8. **Hand off.** Before a chat ends, the resume record at the top of `TRACKING.md` states the active task, the last verified result, what to preserve, and the exact next action.
9. **Close and archive.** When every task is Done, or Deferred by a recorded decision, the result is compared with the acceptance. After the user agrees, the folder moves unchanged to `archive/<name>/` and its entry moves to Archived.

## Rules for this project

- Trackings are written in English unless the user asks for another language.
- Commits follow the project's commit conventions and never include tracking files.

## Active

- [import-preview](import-preview/TRACKING.md): preview an import without applying it. 3 tasks, all Planned; execution mode proposed, awaiting the user's choice.

## Archived

None.
