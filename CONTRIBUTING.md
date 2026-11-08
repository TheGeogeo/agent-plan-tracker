# Contributing

Contributions should make Agent Plan Tracker better at turning substantial work into clear, verifiable tasks and maintaining an accurate record as that work proceeds.

## Propose a focused change

Describe the realistic request or failure your change addresses. Explain the current behavior, the proposed behavior, and why the existing instructions do not already cover the case.

Keep the skill portable across projects and coding agents. Put a workflow rule in SKILL.md only when it changes a useful decision. Put detailed guidance in the matching file under `references/`, starting files in `assets/templates/`, and installation and explanatory material in the README and `docs/`. Keep each file on one topic and link to related files instead of copying them.

Use English for repository content, comments, issues, and pull requests.

## Preserve the workflow's boundaries

- Reuse existing project plans and trackers rather than forcing a parallel structure.
- Preserve accepted decisions, incomplete work, and historical evidence.
- Keep task state separate from delivery state and keep expected results separate from observed evidence.
- Match planning effort to the work.
- Preserve the user's authorization, including the boundary between planning and implementation.
- Record a deliberate acceptance change without relabeling unexecuted checks as successful.
- Keep trackings in English by default and split into focused, linked files.

Additional dependencies, scripts, integrations, or host-specific features need a concrete benefit that justifies their maintenance cost. Do not ship executable scripts in the skill: describe a needed script as a specification that the agent builds for the current host, as the usage gate does.

Never add personal data to the repository: no credentials, tokens, keys, environment values, account identifiers, user-specific paths, or email addresses, including in examples.

## Validate your change

Review the whole affected workflow, not only the changed sentence. Confirm that the skill metadata still describes the intended triggers and that referenced files remain inside the installable skill directory.

Check Markdown links and heading anchors, keep the templates and the example tracking consistent with the task contract, and review the diff for unrelated changes, personal data, or private project information.

For behavior changes, describe a representative scenario and the evidence you actually collected. Useful cases include improving a loose tracker, resuming after interruption, handling a failed check, preserving an existing plan, completing a task with an explicitly accepted limitation, handing off between chats, and an orchestration stopped by the usage gate.

Distinguish manual review, static checks, and actual agent-run evaluation. Report unperformed checks honestly.

## Licensing

Contributions are provided under this repository's MIT license. Preserve existing copyright notices and identify the origin and license of adapted third-party material.
