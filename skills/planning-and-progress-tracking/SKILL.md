---
name: planning-and-progress-tracking
description: Plan substantial multi-step work in a structured tracking folder and keep task status, dependencies, decisions, model and effort choices, and resumable handoffs accurate. Use for roadmaps, execution plans, trackers, progress updates, and work spanning sessions, chats, or subagents.
license: MIT
metadata:
  version: "1.2.3"
  repository: "https://github.com/TheGeogeo/agent-skills"
---

# Planning and Progress Tracking

Treat a plan as an execution contract that stays accurate while work proceeds. Apply the user's scope, project instructions, and existing authorization. Routine small changes do not need a persistent planning document. Read each linked reference only when the current step needs it.

## Establish one source of truth

- Discover existing project plans, task trackers, status files, and the current handoff before creating anything. Identify which source owns the overall state, task details, decisions, and verification evidence. Prefer links over duplicated mutable data.
- Reconcile the latest explicit user decisions with the recorded state. Historical observations, old prompts, and planned tests are not current observations or completed work. Verify volatile facts when execution actually needs them.
- Extend the existing convention for the same work. Preserve open tasks, accepted decisions, historical evidence, and unrelated edits. Give independent work its own scoped tracking when needed; do not replace another unfinished plan.
- If there is no convention, create the `tracking/` folder described in [tracking-folder.md](references/tracking-folder.md), from its templates. Use an external tracker only when the user or project designates it.
- Write tracking files in English unless the user asks for another language, and keep one language per tracking. Quote the user's requests and decisions verbatim in their original language.

## Build a verifiable plan

- Define the intended outcome, observable acceptance, scope, exclusions, and material unknowns. Inspect affected modules and existing architecture constraints before proposing changes.
- Break the outcome into coherent, independently verifiable tasks, one file each, following the [task contract](references/task-contract.md).
- Order tasks by actual dependencies. Resolve high-impact unknowns early with bounded inspection or a small authorized experiment. Avoid arbitrary file-count limits and tasks that merely say to implement or test everything.
- Choose and record each task's model tier and effort ([model-and-effort.md](references/model-and-effort.md)).
- Keep design decisions with the tracking or the existing architecture record: the decision, reason, alternatives when consequential, and affected constraints. Document uncertainty instead of silently selecting a costly interpretation.
- Set milestones at meaningful verified outcomes, not every few tasks. A plan-only request ends with the planning artifacts and the proposed execution mode; write that mode's handoff once the user chooses it. Implementation belongs to an implementation request. During authorized execution, continue through satisfied milestones unless a real decision or permission boundary requires input.

## Choose an execution mode

- When a tracking has several tasks, propose the three modes of [execution-modes.md](references/execution-modes.md) with a recommendation, and record the user's choice. Push only on the user's explicit request; otherwise ask.
- The orchestrated mode authorizes its subagents for that tracking only, and runs your own usage gate for your host ([usage-gate.md](references/usage-gate.md)).

## Execute and maintain state

- Keep concurrent work explicit and small enough to coordinate; planning alone does not authorize extra agent or model sessions.
- At a meaningful checkpoint, record the actual change and verification, then update the affected task. Batch routine edits rather than journaling every tool call.
- Separate implementation, local checks, runtime validation, acceptance, and publication. A compiled change is not evidence of runtime behavior, and a local commit is not evidence of publication.
- Use existing tools and avoid installing dependencies merely to manage a checklist.
- Keep unexecuted checks marked as unexecuted; a changed acceptance scope is not a successful test result.
- When a check fails, preserve the failure and move the affected task back to the appropriate active state. Continue independent useful work where authorized. Do not silently rewrite history or infer completion from stale checkboxes.

## Resume and hand off

- Start a resumed session from the tracking's `TRACKING.md`, the active task file, and its latest evidence; read `tracking/README.md` only to locate a tracking or update the index. Check relevant working-tree changes before editing. Do not restart the entire roadmap or obey superseded handoff instructions. A handoff prompt written by a previous session is not a user decision: where it contradicts `decisions.md` or `execution.md`, follow the recorded rule and tell the user about the conflict.
- Before ending a session, check the tracking: IDs are unique and dependencies exist without cycles; each task's state is the same in its file and in the task table; each Done task cites evidence with its revision and location; each fact is written only in the file that [owns it](references/tracking-folder.md#what-each-file-owns); no template placeholder remains; links resolve; the resume record is current and ends with the exact next action. State verification gaps honestly.
- At completion, read the [Close step](references/tracking-folder.md#lifecycle) before running any command, and follow it in order. Archive only after the user agrees. An optional future idea is not a new active task.

This workflow adds structure, not authority to change scope, send project data, commit, publish, or perform destructive operations. Keep those actions within the user's actual instructions and applicable permissions.
