# Contributing

Contributions should make Agent Plan Tracker better at turning substantial work into clear, verifiable tasks and maintaining an accurate record as that work proceeds.

## Propose a focused change

Describe the realistic request or failure your change addresses. Explain the current behavior, the proposed behavior, and why the existing instructions do not already cover the case.

Keep the skill portable across projects and coding agents. Put a workflow rule in SKILL.md only when it changes a useful decision. Put detailed guidance in the matching file under `references/`, starting files in `assets/templates/`, and installation and explanatory material in the README and `docs/`. Keep each file on one topic and link to related files instead of copying them.

Use English for repository content, comments, issues, and pull requests.

## When to change the skill

The skill is stable. Change its text only for one of these reasons:

- A failure reproduced in at least 2 of 3 fresh runs, with the model tier that the skill recommends for that kind of work.
- A host change that breaks installation or the skill format.
- A maintainer decision about the workflow itself.

A small fast model that skips a rule the skill already states is a model limit, not a gap in the text: record it with the test results and do not add wording for it. Prefer restructuring an existing rule, for example into numbered steps, over adding sentences.

## Stay model- and host-neutral

- Never name a model, a model version, or a model provider in `skills/` or `examples/`. Refer to the three tiers defined in `references/model-and-effort.md`: small fast model, balanced model, most capable model.
- Name hosts and their folders only in `README.md` and `docs/installation.md`, where installation needs them. The skill speaks of "the host" and "the folder where the host keeps its project configuration".
- Do not hard-code plan limits such as a window length; the usage gate reads them from the host.

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

## Update mirrored text together

Each rule has one owning file. A few summaries mirror it for readers; when the owner changes, update its mirrors in the same change:

| Topic | Owner | Mirrors |
| --- | --- | --- |
| Tracking layout | `references/tracking-folder.md` | `assets/templates/README.md`, `examples/tracking/README.md`, `README.md` |
| How a tracking works | `assets/templates/README.md` | `examples/tracking/README.md` (same text), `docs/how-it-works.md` |
| Task states and proof | `references/task-contract.md` | `assets/templates/TRACKING.md`, `docs/how-it-works.md` |
| Closure | `references/tracking-folder.md`, Close step | `SKILL.md` and `references/execution-modes.md` link to it |
| Model tiers | `references/model-and-effort.md` | `assets/templates/execution.md`, the example's `execution.md`, `docs/how-it-works.md`, `README.md` |
| Usage gate | `references/usage-gate.md` | `assets/templates/execution.md`; the summaries in `docs/how-it-works.md` and both tracking READMEs give no thresholds |
| Templates | `assets/templates/` | `examples/tracking/` |

Paths under `references/` and `assets/` are inside `skills/planning-and-progress-tracking/`.

## Validate your change

Review the whole affected workflow, not only the changed sentence. Confirm that the skill metadata still describes the intended triggers, that referenced files remain inside the installable skill directory, and that the `version` in the frontmatter is raised for any change to the skill.

Check Markdown links and heading anchors, check the mirrors above, and review the diff for unrelated changes, personal data, private project information, or model and host names outside the allowed files.

For behavior changes, run each affected scenario in a fresh agent on a disposable project, with a prompt that does not hint at the expected behavior:

- Judgment scenarios (closing a tracking, a Done task with invalid proof, resuming, a failed check, a blocker, an accepted limitation) run on a balanced model.
- Mechanical scenarios (creating a tracking, its language, verbatim quotes, keeping secrets out) run on a small fast model.
- Run each scenario once. After a failure, run it twice more; it passes at 2 of 3.

Distinguish manual review, static checks, and actual agent-run evaluation. Report unperformed checks honestly.

## Licensing

Contributions are provided under this repository's MIT license. Preserve existing copyright notices and identify the origin and license of adapted third-party material.
