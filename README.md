# Agent Plan Tracker

**Structured plans, evidence-based progress, and clear handoffs for coding agents.**

Agent Plan Tracker is an instruction-based Agent Skill for Claude Code and Codex. It helps an agent turn a broad request or an informal checklist into an actionable plan, maintain that plan as work proceeds, and leave a reliable starting point for the next session.

The skill works with the planning documents already in your project. It connects each task to a concrete result, its dependencies, a way to verify it, and the evidence needed to call it complete.

## Contents

- [What it helps you do](#what-it-helps-you-do)
- [What you get](#what-you-get)
- [How the workflow works](#how-the-workflow-works)
- [Install](#install)
- [Use the skill](#use-the-skill)
- [Make it a standing project rule](#make-it-a-standing-project-rule)
- [Task states and evidence](#task-states-and-evidence)
- [Example](#example)
- [Repository layout](#repository-layout)
- [Design and scope](#design-and-scope)
- [Contributing](#contributing)
- [License](#license)

## What it helps you do

Use the skill when a change needs several dependent steps, when a roadmap spans multiple sessions, or when an existing progress document is too loose to guide implementation.

It is especially useful for:

- Breaking a feature or refactor into tasks with observable acceptance.
- Ordering work by dependencies and surfacing important unknowns early.
- Keeping implementation, local checks, runtime validation, acceptance, and publication distinct.
- Recording which result was actually verified, against which revision or input.
- Resuming work from the current state instead of reconstructing it from a long conversation.
- Strengthening an existing tracker while preserving its decisions, history, and conventions.

Small, obvious changes can stay small. The skill scales the planning effort to the work.

## What you get

| Output | Information it preserves |
| --- | --- |
| Execution plan | Goal, scope, exclusions, acceptance, milestones, and material unknowns. |
| Task records | Stable IDs, concrete results, dependencies, states, verification, and evidence. |
| Decision record | What changed in the approach, why it changed, and the consequences. |
| Resume record | Current phase and task, last verified result, remaining work, and the exact next action. |
| Completion summary | Delivered behavior, supporting checks, and remaining limits. |

These outputs can live in one Markdown plan or in your existing collection of documents. If your project already uses a central status file, task sheets, or a designated issue tracker, the agent follows that structure and links to the detailed evidence.

The [task contract](skills/planning-and-progress-tracking/references/task-contract.md) defines the information the workflow maintains. The [example plan](examples/execution-plan.md) shows a compact application of that contract.

## How the workflow works

1. **Find the current state.** Read the existing plan, active task, recent evidence, relevant project instructions, and latest explicit decisions.
2. **Define the outcome.** Establish observable acceptance, scope, exclusions, and the architecture constraints that matter to the change.
3. **Build the task graph.** Give tasks stable IDs and clear results; order them by actual dependencies.
4. **Work and verify.** Execute authorized work, collect the relevant proof, and update the affected task at meaningful checkpoints.
5. **Keep the resume point current.** Record the active task, missing condition or remaining work, and a concrete next action before handing off.
6. **Close against acceptance.** Compare the delivered result with the agreed outcome and retain any remaining limitations.

Updates happen during the agent's active work. The workflow is carried by the skill instructions and your project documents.

## Install

The installable skill is named **`planning-and-progress-tracking`**. The repository is named **`agent-plan-tracker`**.

### 1. Get the files

```sh
git clone https://github.com/TheGeogeo/agent-plan-tracker.git
```

Review [SKILL.md](skills/planning-and-progress-tracking/SKILL.md) and its [task contract](skills/planning-and-progress-tracking/references/task-contract.md), then copy the complete `skills/planning-and-progress-tracking/` directory to one of the locations below. Keep its `references/` directory and `LICENSE` together with `SKILL.md`.

### 2. Choose the scope

| Agent | Scope | Destination |
| --- | --- | --- |
| Claude Code | All your local projects | `~/.claude/skills/planning-and-progress-tracking/` |
| Claude Code | One repository | `<your-project>/.claude/skills/planning-and-progress-tracking/` |
| Codex | All your local projects | `~/.agents/skills/planning-and-progress-tracking/` |
| Codex | One repository | `<your-project>/.agents/skills/planning-and-progress-tracking/` |

Here, `~` means your user home directory. On Windows, use the equivalent directory under your user profile. The destination should contain `SKILL.md` directly, with `references/` beside it.

For example, after cloning, a personal Claude Code installation on macOS or Linux is:

```sh
mkdir -p ~/.claude/skills
cp -R agent-plan-tracker/skills/planning-and-progress-tracking ~/.claude/skills/
```

For a personal Codex installation, use `~/.agents/skills/` as the destination instead.

If the skill is already installed, review the existing version before replacing it. Avoid installing multiple copies with the same name into overlapping scopes.

See the official [Claude Code skill documentation](https://code.claude.com/docs/en/skills) and [OpenAI skill documentation](https://developers.openai.com/codex/skills) for discovery behavior and host-specific restrictions. These local directories apply to local agent sessions; account-hosted and cloud environments can use different distribution mechanisms.

### 3. Load the skill

Start a new session if the skill does not appear after installation.

In Claude Code, invoke it with:

```text
/planning-and-progress-tracking
```

In Codex CLI or the IDE extension, mention it with:

```text
$planning-and-progress-tracking
```

Both hosts can also select a skill when the task matches its description.

## Use the skill

### Create a plan

```text
Use planning-and-progress-tracking to plan the import-preview feature.
Inspect the existing architecture and test commands first.
Create ordered tasks with acceptance criteria and verification methods.
Keep this request limited to planning.
```

### Improve an existing tracker

```text
Use planning-and-progress-tracking to strengthen the current roadmap.
Keep the existing files, completed work, and accepted decisions.
Add stable task IDs, dependencies, observable acceptance, and evidence fields.
Identify the current task and next concrete action.
```

### Execute authorized work

```text
Use planning-and-progress-tracking to carry out the active plan.
Start from the canonical state and check existing changes.
Update task status after meaningful results and keep the resume point current.
Follow the project's verification and delivery rules.
```

### Resume a session

```text
Resume the active plan with planning-and-progress-tracking.
Read the current status, active task, and latest evidence.
Check what changed since the handoff, then continue the next authorized action.
```

The prompts establish the task's scope. A request for a plan produces planning artifacts; a request to execute the plan authorizes implementation within the boundaries you provide.

## Make it a standing project rule

Installation makes the skill discoverable. To make this workflow your default for substantial work, add a short rule to the instruction file your agent reads.

For Codex, use the relevant `AGENTS.md`; for Claude Code, use the relevant `CLAUDE.md`:

```markdown
For substantial multi-step work and work spanning sessions, use the
planning-and-progress-tracking skill before implementation and when resuming.
Maintain the existing canonical plan with task IDs, dependencies, acceptance,
verification evidence, and a concrete next action.
Update affected tasks at meaningful checkpoints and the resume record before
ending a session. Keep routine small changes lightweight.
```

Use a project instruction file for a team convention or the host's user-level instruction file for a personal default. Keep project-specific paths, delivery rules, and acceptance criteria in that project's own documents.

## Task states and evidence

The skill preserves your project's vocabulary when it carries the same distinctions. Its default task model is:

| State | Meaning |
| --- | --- |
| Planned | Work has not started. Dependencies or required decisions may still be pending. |
| Active | Work is underway. |
| Awaiting verification | The intended result exists, but required acceptance proof is missing. |
| Done | The task's acceptance is supported by evidence or an explicit decision changing that acceptance, with its limits recorded. |
| Blocked | A specific missing condition prevents progress; the resumption action is recorded. |
| Deferred | Work has been deliberately postponed, with a reason. Deferral alone does not satisfy a dependency. |

A future test command belongs under **Verification**. An observed test result belongs under **Evidence**.

Useful evidence identifies the revision or input, applicable configuration, command or scenario, observed result, and an artifact or source location. Existing reports can be linked rather than copied into the plan.

If the owner accepts a limitation, the agent records that decision and the checks still unexecuted. If a later failure invalidates earlier acceptance, the agent reopens the affected task while preserving its earlier evidence.

## Example

An informal entry such as "add import preview" becomes a small dependency graph:

| Task | Result | Depends on | Acceptance |
| --- | --- | --- | --- |
| IMP-01 | Establish the preview contract and affected boundaries. | None | Input, output, error behavior, and limits are specified against the existing project. |
| IMP-02 | Produce preview results without applying the import. | IMP-01 | Valid input produces the expected preview and leaves stored data unchanged. |
| IMP-03 | Verify failure cases and record the handoff. | IMP-02 | Required scenarios have results tied to the tested revision; remaining limits and the next action are explicit. |

This is an illustrative plan, not a claim that the feature exists or has passed tests. The [full example](examples/execution-plan.md) includes task states, verification, evidence fields, and a resume record.

## Repository layout

```text
agent-plan-tracker/
  README.md
  LICENSE
  CONTRIBUTING.md
  examples/
    execution-plan.md
  skills/
    planning-and-progress-tracking/
      SKILL.md
      LICENSE
      references/
        task-contract.md
```

`SKILL.md` is the agent entry point. The reference holds the reusable task and resume contract. The example and contribution guide support readers of this repository; the installable skill is self-contained in its own directory.

## Design and scope

Agent Plan Tracker is a Markdown workflow with no additional runtime dependencies. It is designed to work across languages and project types by discovering the project's actual tooling and conventions.

The workflow emphasizes a single source of truth, proportional planning, evidence-backed state changes, preserved history, and useful handoffs. It includes architecture constraints and consequential decisions where they affect the plan, while keeping the plan focused on the requested outcome.

The agent remains responsible for following the user's permissions and delivery rules. The skill's instructions guide behavior; they are not a runtime enforcement mechanism. Host capabilities, context, and the quality of the project's evidence affect the result.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Focus changes on better planning decisions, clearer task contracts, and more reliable resumption. Include the concrete scenario a proposed change improves.

## License

Released under the [MIT License](LICENSE).

Agent Plan Tracker is a custom skill created and maintained by [TheGeogeo](https://github.com/TheGeogeo).
