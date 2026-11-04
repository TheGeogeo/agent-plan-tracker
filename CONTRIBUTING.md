# Contributing

Contributions should make Agent Plan Tracker better at turning substantial work into clear, verifiable tasks and maintaining an accurate record as that work proceeds.

## Propose a focused change

Describe the realistic request or failure your change addresses. Explain the current behavior, the proposed behavior, and why the existing instructions do not already cover the case.

Keep the skill portable across projects and coding agents. Put a workflow rule in SKILL.md only when it changes a useful decision. Put detailed task-format guidance in the task contract, and keep installation and explanatory material in the README.

Use English for repository content, comments, issues, and pull requests.

## Preserve the workflow's boundaries

- Reuse existing project plans and trackers rather than forcing a parallel structure.
- Preserve accepted decisions, incomplete work, and historical evidence.
- Keep task state separate from delivery state and keep expected results separate from observed evidence.
- Match planning effort to the work.
- Preserve the user's authorization, including the boundary between planning and implementation.
- Record a deliberate acceptance change without relabeling unexecuted checks as successful.

Additional dependencies, scripts, integrations, or host-specific features need a concrete benefit that justifies their maintenance cost.

## Validate your change

Review the whole affected workflow, not only the changed sentence. Confirm that the skill metadata still describes the intended triggers and that referenced files remain inside the installable skill directory.

Check Markdown links and heading anchors, keep the example consistent with the task contract, and review the diff for unrelated changes or private project information.

For behavior changes, describe a representative scenario and the evidence you actually collected. Useful cases include improving a loose tracker, resuming after interruption, handling a failed check, preserving an existing plan, and completing a task with an explicitly accepted limitation.

Distinguish manual review, static checks, and actual agent-run evaluation. Report unperformed checks honestly.

## Licensing

Contributions are provided under this repository's MIT license. Preserve existing copyright notices and identify the origin and license of adapted third-party material.
