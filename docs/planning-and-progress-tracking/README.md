# Planning and Progress Tracking

**Structured trackings, evidence-based progress, and clear handoffs for coding agents.**

`planning-and-progress-tracking` is an instruction-based skill in the Agent Skills format, for coding agents such as Claude Code and Codex. It turns a broad request or an informal checklist into a tracking folder of verifiable tasks, keeps that tracking accurate while work proceeds, and leaves a reliable starting point for the next chat or agent.

The skill works with the planning documents already in your project. When there are none, it creates a `tracking/` folder with an index, an archive, and one folder per piece of work.

Back to the [skill catalog](../../README.md).

## Contents

- [What it helps you do](#what-it-helps-you-do)
- [What you get](#what-you-get)
- [How it works](#how-it-works)
- [Quick start](#quick-start)
- [Documentation](#documentation)
- [Design and scope](#design-and-scope)

## What it helps you do

Use the skill when a change needs several dependent steps, when a roadmap spans multiple sessions, or when an existing progress document is too loose to guide implementation. It helps you:

- Break a feature or refactor into tasks with observable acceptance, ordered by their dependencies.
- Keep each piece of work in its own tracking folder, split into small linked files, with an index and an archive.
- Choose a model tier (small fast, balanced, or most capable) and an effort for each task, recorded with the reason, so a tracking stays valid when model names change.
- Run the tasks in the current chat, one chat per task, or through an orchestrating chat that drives subagents and commits after each verified task.
- Pause orchestrated work before the plan's short-window or weekly usage limits run out, with the finished work committed and a handoff written.
- Record which result was actually verified, against which revision or input, and resume from the current state instead of a long conversation.

Small, obvious changes can stay small. The skill scales the planning effort to the work.

## What you get

```text
tracking/
  README.md               How trackings work, and the active and archived index
  archive/<name>/         Closed trackings, moved unchanged
  <name>/
    TRACKING.md           Start here: resume record and task table
    scope.md              Requests, goal, acceptance, scope, work limits
    execution.md          Mode, model tier and effort per task, commits, usage gate, handoff
    decisions.md          User decisions and their consequences
    tasks/<ID>-<slug>.md  One file per task
    evidence/<id>/        Proof cited by the tasks
```

Trackings are written in English unless you ask for another language. If your project already uses a central status file, task sheets, or a designated issue tracker, the agent follows that structure instead. The [templates](../../skills/planning-and-progress-tracking/assets/templates/) show the starting content of each file.

## How it works

1. **Find the current state:** existing plans, the active task, recent evidence, and your latest decisions.
2. **Define the outcome:** observable acceptance, scope, exclusions, and the constraints that matter.
3. **Build the task graph:** stable IDs, one file per task, ordered by actual dependencies, with a model tier and effort chosen per task.
4. **Choose the execution mode:** you pick how the tasks run; pushing always needs your explicit request.
5. **Work and verify:** each task closes only when evidence supports its acceptance.
6. **Hand off and close:** the resume record names the exact next action; a finished tracking moves to `archive/` once you agree.

[How it works](how-it-works.md) covers each step, the execution modes, and the usage gate.

## Quick start

Clone the repository, review the skill, and copy the complete skill directory. For a personal Claude Code installation on macOS or Linux:

```sh
git clone https://github.com/TheGeogeo/agent-skills.git
mkdir -p ~/.claude/skills
cp -R agent-skills/skills/planning-and-progress-tracking ~/.claude/skills/
```

Then ask for a tracking:

```text
Use planning-and-progress-tracking to plan the import-preview feature.
Inspect the existing architecture and test commands first.
Keep this request limited to planning.
```

[Installation](installation.md) covers Codex, per-project scopes, Windows, and making the workflow a standing rule. [Usage](usage.md) has prompts for every stage.

## Documentation

| Page | Contents |
| --- | --- |
| [Installation](installation.md) | Install locations, loading the skill, standing project rule |
| [Usage](usage.md) | Prompts to plan, strengthen a tracker, execute in each mode, resume, and archive |
| [How it works](how-it-works.md) | Tracking folder, execution modes, model and effort, usage gate, task states and evidence |

The agent itself reads [SKILL.md](../../skills/planning-and-progress-tracking/SKILL.md), which links to one reference per topic.

## Design and scope

The skill is a Markdown workflow with no runtime dependencies and no shipped scripts. It discovers the project's actual tooling and conventions, so it works across languages and project types. The one script it uses, the usage gate, is written by the agent itself for its own host and provider when you choose the orchestrated mode; the skill provides no link or source for it, and the script never contains credentials or personal data.

The workflow emphasizes a single source of truth, proportional planning, evidence-backed state changes, preserved history, and useful handoffs. The agent remains responsible for following your permissions and delivery rules: the skill guides behavior, it does not enforce it at run time.
