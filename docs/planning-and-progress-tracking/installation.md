# Installation

The installable skill is named **`planning-and-progress-tracking`**. It is part of the **`agent-skills`** repository. Back to the [overview](README.md).

## 1. Get the files

```sh
git clone https://github.com/TheGeogeo/agent-skills.git
```

Review [SKILL.md](../../skills/planning-and-progress-tracking/SKILL.md), its `references/`, and its `assets/templates/`, then copy the complete `skills/planning-and-progress-tracking/` directory to one of the locations below. Keep `references/`, `assets/`, and `LICENSE` together with `SKILL.md`.

## 2. Choose the scope

| Agent | Scope | Destination |
| --- | --- | --- |
| Claude Code | All your local projects | `~/.claude/skills/planning-and-progress-tracking/` |
| Claude Code | One repository | `<your-project>/.claude/skills/planning-and-progress-tracking/` |
| Codex | All your local projects | `~/.agents/skills/planning-and-progress-tracking/` |
| Codex | One repository | `<your-project>/.agents/skills/planning-and-progress-tracking/` |
| Another agent that supports Agent Skills | User or repository | The skills folder documented by that agent |

Here, `~` means your user home directory. On Windows, use the equivalent directory under your user profile. The destination should contain `SKILL.md` directly, with `references/` and `assets/` beside it.

A personal Claude Code installation on macOS or Linux:

```sh
mkdir -p ~/.claude/skills
cp -R agent-skills/skills/planning-and-progress-tracking ~/.claude/skills/
```

For a personal Codex installation, use `~/.agents/skills/` as the destination instead.

If the skill is already installed, compare the `version` in its `SKILL.md` frontmatter with this repository's, review the existing version before replacing it, and replace the whole directory so that removed files do not linger. If you use several agents, update every installed copy. Avoid installing multiple copies with the same name into overlapping scopes.

See the official [Claude Code skill documentation](https://code.claude.com/docs/en/skills) and [Codex skill documentation](https://learn.chatgpt.com/docs/build-skills) for discovery behavior and host-specific restrictions. These local directories apply to local agent sessions; account-hosted and cloud environments can use different distribution mechanisms.

## 3. Load the skill

Start a new session if the skill does not appear after installation.

In Claude Code, invoke it with:

```text
/planning-and-progress-tracking
```

In Codex CLI or the IDE extension, mention it with:

```text
$planning-and-progress-tracking
```

Both hosts can also select the skill when the task matches its description.

## Make it a standing project rule

Installation makes the skill discoverable. To make this workflow your default for substantial work, add a short rule to the instruction file your agent reads: the relevant `AGENTS.md` for Codex, or the relevant `CLAUDE.md` for Claude Code.

```markdown
For substantial multi-step work and work spanning sessions, use the
planning-and-progress-tracking skill before implementation and when resuming.
Maintain the existing tracking with task IDs, dependencies, acceptance,
verification evidence, and a concrete next action.
Update affected tasks at meaningful checkpoints and the resume record before
ending a session. Keep routine small changes lightweight.
```

Use a project instruction file for a team convention or the host's user-level instruction file for a personal default. Keep project-specific paths, delivery rules, and acceptance criteria in that project's own documents, or in the rules section of its `tracking/README.md`.
