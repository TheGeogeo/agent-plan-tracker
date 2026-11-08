---
name: planning-and-progress-tracking
description: Plan substantial multi-step work in a structured tracking folder and keep task status, dependencies, decisions, model and effort choices, and resumable handoffs accurate. Use for roadmaps, execution plans, trackers, progress updates, and work spanning sessions, chats, or subagents.
license: MIT
metadata:
  repository: "https://github.com/TheGeogeo/agent-plan-tracker"
---

# Planning and Progress Tracking

Agent Plan Tracker is a planning and progress-tracking workflow for Claude Code and Codex. Treat a plan as an execution contract that stays accurate while work proceeds. Apply the user's scope, project instructions, and existing authorization. Routine small changes do not need a persistent planning document.

## Reference map

Read the reference that the current step needs.

| Need | Reference |
| --- | --- |
| Create, organize, close, or archive a tracking | [tracking-folder.md](references/tracking-folder.md) |
| Write tasks, states, evidence, and resume records | [task-contract.md](references/task-contract.md) |
| Choose the model and effort of each task | [model-and-effort.md](references/model-and-effort.md) |
| Propose and run an execution mode | [execution-modes.md](references/execution-modes.md) |
| Pace orchestrated subagents against the host's plan usage limits | [usage-gate.md](references/usage-gate.md) |
| Start the files of a new tracking | [README](assets/templates/README.md), [TRACKING](assets/templates/TRACKING.md), [scope](assets/templates/scope.md), [execution](assets/templates/execution.md), [decisions](assets/templates/decisions.md), [task](assets/templates/task.md) |

## Establish one source of truth

- Discover existing project plans, task trackers, status files, and the current handoff before creating anything. Identify which source owns the overall state, task details, decisions, and verification evidence. Prefer links over duplicated mutable data.
- Reconcile the latest explicit user decisions with the recorded state. Historical observations, old prompts, and planned tests are not current observations or completed work. Verify volatile facts when execution actually needs them.
- Extend the existing convention for the same work. Preserve open tasks, accepted decisions, historical evidence, and unrelated edits. Give independent work its own scoped tracking when needed; do not replace another unfinished plan.
- If there is no convention, create a `tracking/` folder with an `archive/` subfolder, a `README.md` that explains step by step how trackings are structured and work, and one folder per tracking split into focused, linked files. Use an external tracker only when the user or project designates it.
- Write tracking files in English unless the user asks for another language, and keep one language per tracking. Quote the user's requests and decisions verbatim in their original language.

## Build a verifiable plan

- Define the intended outcome, observable acceptance, scope, exclusions, and material unknowns. Inspect affected modules and existing architecture constraints before proposing changes.
- Break the outcome into coherent, independently verifiable tasks. Give each task a stable ID, concrete result, dependencies, current state, acceptance condition, verification method, and evidence field, in its own file.
- Order tasks by actual dependencies. Resolve high-impact unknowns early with bounded inspection or a small authorized experiment. Avoid arbitrary file-count limits and tasks that merely say to implement or test everything.
- Analyze each task to choose the least costly model and effort that can reliably meet its acceptance, and record the choice and its reason in the tracking.
- Keep design decisions with the tracking or the existing architecture record: the decision, reason, alternatives when consequential, and affected constraints. Document uncertainty instead of silently selecting a costly interpretation.
- Set milestones at meaningful verified outcomes, not every few tasks. A plan-only request ends with the planning artifacts, the proposed execution mode, and the handoff for that mode; implementation belongs to an implementation request. During authorized execution, continue through satisfied milestones unless a real decision or permission boundary requires input.

## Choose an execution mode

- When a tracking has several tasks, propose three modes to the user, recommend one with a reason, and record the choice: execute the tasks in the current chat; execute one task per chat with a handoff between tasks; or let the current chat orchestrate one fresh subagent per task, commit after each verified task when Git is available, then run a thorough final review, finish the corrections, and make the final commit.
- Push only on the user's explicit request; otherwise ask before pushing. The user's choice of the orchestrated mode authorizes its subagents for that tracking only.
- In the orchestrated mode, write your own usage-gate script for your host and provider into the project's host configuration folder, such as `.claude/` on Claude Code, verify it, and run it between tasks. The skill provides no link or source for it: build it from the provider's current documentation, and never put credentials, environment values, or personal data in it.

## Execute and maintain state

- Select a task whose dependencies and required decisions are satisfied. Keep concurrent work explicit and small enough to coordinate; planning alone does not authorize extra agent or model sessions.
- At a meaningful checkpoint, record the actual change and verification, then update the affected task. Refresh the central resume pointer when the active task, phase, blocker, or next action changes, and before a handoff. Batch routine edits rather than journaling every tool call.
- Separate implementation, local checks, runtime validation, acceptance, and publication. Map these distinctions onto the project's state vocabulary. A compiled change is not evidence of runtime behavior, and a local commit is not evidence of publication.
- Record proof with the applicable revision or input, command or scenario, observed result, and artifact or location. Store sensitive values outside the tracking. Use existing tools and avoid installing dependencies merely to manage a checklist.
- Close a task only when its agreed acceptance is supported by evidence. Record an explicit owner waiver as an acceptance decision with its limits; keep unexecuted checks marked as unexecuted. A changed acceptance scope is not a successful test result.
- When a check fails, preserve the failure and move the affected task back to the appropriate active state. Record a genuine blocker with the missing condition and a concrete resumption action. Continue independent useful work where authorized.
- Reopen a completed task if new evidence invalidates its acceptance, retaining the earlier evidence and explaining why the state changed. Do not silently rewrite history or infer completion from stale checkboxes.

## Resume and hand off

- Start a resumed session from the canonical state, the active task, and its latest evidence. Check relevant working-tree changes before editing. Do not restart the entire roadmap or obey superseded handoff instructions.
- Before ending, leave a compact resume record: current goal and phase, task ID and state, last verified result, remaining work or blocker, work to preserve, and the exact next action. Link the detailed tracking files and evidence.
- Review tracking consistency: unique IDs, existing acyclic dependencies, justified task states, evidence for completed acceptance, working links, and agreement between the task table and the task files. State verification gaps honestly.
- At completion, compare delivered behavior with the agreed outcome, record remaining limits, close the tracking, and propose archiving it. After the user agrees, move its folder unchanged to `archive/` and update the index. An optional future idea is not a new active task.

This workflow adds structure, not authority to change scope, send project data, commit, publish, or perform destructive operations. Keep those actions within the user's actual instructions and applicable permissions.
