# Contributing

Contributions should make the skills in this repository more useful and more reliable for coding agents. Each skill lives in its own directory under `skills/`, installs on its own, and has its reader documentation in `docs/<skill-name>/`.

The rules below apply to every skill. A skill with extra maintenance rules has its own section at the end of this file.

## Propose a focused change

Describe the realistic request or failure your change addresses. Explain the current behavior, the proposed behavior, and why the existing instructions do not already cover the case.

Keep each skill portable across projects and coding agents. Put a workflow rule in the skill's `SKILL.md` only when it changes a useful decision. Put detailed guidance in the skill's `references/`, starting files in its `assets/`, and installation and explanatory material in `docs/<skill-name>/`. Keep each file on one topic and link to related files instead of copying them.

Use English for repository content, comments, issues, and pull requests.

## Add a skill

1. Create `skills/<skill-name>/SKILL.md`. Its `name` matches the directory name, its `description` says what the skill does and when to use it, and its frontmatter sets `license: MIT` and, under `metadata`, a `version` and the `repository` URL.
2. Copy the repository's `LICENSE` into `skills/<skill-name>/` so that an installed copy carries it.
3. Keep everything the agent reads inside `skills/<skill-name>/`: `references/` for detailed guidance and `assets/` for templates and other starting files.
4. Add reader documentation in `docs/<skill-name>/`: at least a `README.md` overview, plus installation and usage pages when the skill needs them.
5. Add a row for the skill to the Skills table in the repository `README.md`.

## When to change a skill

The skills are meant to be stable. Change a skill's text only for one of these reasons:

- A failure reproduced in at least 2 of 3 fresh runs, with the model tier suited to that kind of work.
- A host change that breaks installation or the skill format.
- A maintainer decision about the workflow itself.

A small fast model that skips a rule the skill already states is a model limit, not a gap in the text: record it with the test results and do not add wording for it. Prefer restructuring an existing rule, for example into numbered steps, over adding sentences.

## Stay model- and host-neutral

- Never name a model, a model version, or a model provider in `skills/`. Refer to model tiers: small fast model, balanced model, most capable model.
- Name hosts and their folders only in `README.md` and in each skill's installation page under `docs/`, where installation needs them. A skill speaks of "the host" and "the folder where the host keeps its project configuration".
- Do not hard-code plan limits such as a window length; read them from the host.

## Keep skills lightweight and private

Additional dependencies, scripts, integrations, or host-specific features need a concrete benefit that justifies their maintenance cost.

Never add personal data to the repository: no credentials, tokens, keys, environment values, account identifiers, user-specific paths, or email addresses, including in templates and documentation.

## Validate your change

Review the whole affected workflow, not only the changed sentence. Confirm that the skill metadata still describes the intended triggers, that referenced files remain inside the installable skill directory, and that the `version` in the frontmatter is raised for any change to the skill.

Check Markdown links and heading anchors, check the skill's mirrored text if it has any, and review the diff for unrelated changes, personal data, private project information, or model and host names outside the allowed files.

For behavior changes, run each affected scenario in a fresh agent on a disposable project, with a prompt that does not hint at the expected behavior. Run each scenario once. After a failure, run it twice more; it passes at 2 of 3.

Distinguish manual review, static checks, and actual agent-run evaluation. Report unperformed checks honestly.

## Licensing

Contributions are provided under this repository's MIT license. Preserve existing copyright notices and identify the origin and license of adapted third-party material.

## planning-and-progress-tracking

### Model tiers

The three model tiers are defined in the skill's `references/model-and-effort.md`. A failure counts toward a text change only when it reproduces with the tier the skill recommends for that kind of work.

### Preserve the workflow's boundaries

- Reuse existing project plans and trackers rather than forcing a parallel structure.
- Preserve accepted decisions, incomplete work, and historical evidence.
- Keep task state separate from delivery state and keep expected results separate from observed evidence.
- Match planning effort to the work.
- Preserve the user's authorization, including the boundary between planning and implementation.
- Record a deliberate acceptance change without relabeling unexecuted checks as successful.
- Keep trackings in English by default and split into focused, linked files.

Do not ship executable scripts in the skill: describe a needed script as a specification that the agent builds for the current host, as the usage gate does. The usage gate reads plan limits from the host.

### Update mirrored text together

Each rule has one owning file. A few summaries mirror it for readers; when the owner changes, update its mirrors in the same change:

| Topic | Owner | Mirrors |
| --- | --- | --- |
| Tracking layout | `references/tracking-folder.md` | `assets/templates/README.md`, `docs/README.md` |
| How a tracking works | `assets/templates/README.md` | `docs/how-it-works.md` |
| Task states and proof | `references/task-contract.md` | `assets/templates/TRACKING.md`, `docs/how-it-works.md` |
| Closure | `references/tracking-folder.md`, Close step | `SKILL.md` and `references/execution-modes.md` link to it |
| Model tiers | `references/model-and-effort.md` | `assets/templates/execution.md`, `docs/how-it-works.md`, `docs/README.md` |
| Usage gate | `references/usage-gate.md` | `assets/templates/execution.md`; the summaries in `docs/how-it-works.md` and `assets/templates/README.md` give no thresholds |
| Install locations | Repository `README.md` | `docs/installation.md` |

In this table, paths under `references/` and `assets/` and `SKILL.md` are inside `skills/planning-and-progress-tracking/`, and paths under `docs/` are inside `docs/planning-and-progress-tracking/`.

### Test scenarios

- Judgment scenarios (closing a tracking, a Done task with invalid proof, resuming, a failed check, a blocker, an accepted limitation) run on a balanced model.
- Mechanical scenarios (creating a tracking, its language, verbatim quotes, keeping secrets out) run on a small fast model.
