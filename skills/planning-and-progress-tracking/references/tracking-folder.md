# Tracking folder

Use this layout when the project has no planning convention or when the user asks for it. If the project already has trackers for the same work, extend them instead of creating a parallel structure.

## Location and version control

- Create `tracking/` at the repository root, or in the project's documentation directory when the project keeps planning documents there.
- Follow the project's rules on versioning plans. If those rules keep plans out of versioned paths, add `tracking/` to `.git/info/exclude`, which stays local. If no rule exists, ask the user once and record the answer in `tracking/README.md`.
- Without Git, the folder is simply local.

## Layout

```text
tracking/
  README.md                How trackings work here, and the active and archived index
  archive/                 Closed trackings, moved unchanged
    <name>/
  <name>/                  One folder per tracking, kebab-case name
    TRACKING.md            Entry point: resume record and task table
    scope.md               Requests, goal, acceptance, scope, exclusions, work limits
    execution.md           Mode, model and effort per task, commits, usage gate, handoff
    decisions.md           User decisions and their consequences
    tasks/
      <ID>-<slug>.md       One record per task
    evidence/
      <id>/                Logs, outputs, and screenshots cited by tasks
    tools/                 Optional helper scripts, with a README for their use
```

Create `evidence/` and `tools/` only when they receive content.

## What each file owns

| File | Owns | Leaves to other files |
| --- | --- | --- |
| `tracking/README.md` | How trackings work, the layout, project-specific tracking rules, and one line per active or archived tracking | Any tracking's details |
| `TRACKING.md` | Resume record and task table | Task details, evidence, rationale |
| `scope.md` | Verbatim requests with dates, goal, observable acceptance, scope, exclusions, constraints, work limits, unknowns | Task states |
| `execution.md` | Chosen mode, model and effort per task, commit and push rules, usage gate, handoff prompt | Task results |
| `decisions.md` | User decisions verbatim, their consequences, and reversible choices the agent made | Rules that do not come from a decision |
| `tasks/<ID>-<slug>.md` | The full record of one task, including its next action | Other tasks' details |
| `evidence/` | Logs, outputs, and the usage-gate log cited by tasks | Conclusions, which go in the task record |

## Keep files light

- One topic per file, so a reader finds each fact in the one file that owns it.
- Link to the owning file instead of copying its text. Summaries in `TRACKING.md` and `tracking/README.md` stay at one line per item.
- Start every file of a tracking other than `TRACKING.md` with its title and a link back to `TRACKING.md`.
- When a file mixes concerns or grows long enough to slow a reader, move the detail into a new file in the same tracking, such as `audit.md` or `notes.md`, and link it from the file that needs it.
- Put long logs and outputs in `evidence/` and cite them; do not paste them into task records.

## Links that survive archiving

- Link files inside a tracking with relative paths such as `tasks/T1-setup.md` or `../TRACKING.md`. They stay valid when the folder moves to `archive/`.
- Refer to project files as repository-relative paths in code formatting, such as `src/app.ts:42`, rather than relative links whose depth changes when the tracking moves.
- Refer to another tracking by name and let `tracking/README.md` hold its location.

## Lifecycle

1. **Create.** If `tracking/README.md` is missing, create it from the template, keeping its explanation of how a tracking works and adding only project-specific rules. Create `tracking/<name>/` from the templates and list it under Active.
2. **Plan.** Fill `scope.md`, the task files, and the task table. Choose a model and effort for each task ([model-and-effort.md](model-and-effort.md)). Propose the execution mode and record the user's choice ([execution-modes.md](execution-modes.md)).
3. **Execute.** Follow the chosen mode and the [task contract](task-contract.md). Keep the resume record current.
4. **Close.** When every task is Done, or Deferred with a recorded decision, compare the delivered result with the acceptance in `scope.md` and record remaining limits. Then, before archiving, rewrite every resume field so none describes the state before closure: goal and phase, closed on <YYYY-MM-DD> with the comparison's outcome; active task, none; last verified result, the final comparison with its revision and evidence path; remaining work, one line per item, with its task ID when it has one: each Deferred task, each task file's `Limits`, and each limit the comparison found, or none; changes to preserve, any uncommitted or unpushed work, or none; next action, none.
5. **Archive.** Propose archiving. After the user agrees, move `tracking/<name>/` unchanged to `tracking/archive/<name>/`, move its index entry to Archived with a one-line outcome, and check that its links still resolve.

## Templates

Start files from the templates in `assets/templates/`: [README.md](../assets/templates/README.md) for the tracking root, then [TRACKING.md](../assets/templates/TRACKING.md), [scope.md](../assets/templates/scope.md), [execution.md](../assets/templates/execution.md), [decisions.md](../assets/templates/decisions.md), and [task.md](../assets/templates/task.md), copied once per task and renamed `tasks/<ID>-<slug>.md`. Replace every placeholder and delete optional sections that do not apply.
