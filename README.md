# Agent Skills

**Custom skills for coding agents such as Claude Code and Codex.**

This repository collects instruction-based skills in the Agent Skills format. Each skill lives in its own directory under [`skills/`](skills/), carries its own license, and installs on its own: pick only the skills you need.

## Contents

- [Skills](#skills)
- [Installation](#installation)
- [Using a skill](#using-a-skill)
- [Repository layout](#repository-layout)
- [Design principles](#design-principles)
- [Contributing](#contributing)
- [License](#license)

## Skills

| Skill | What it does | Documentation |
| --- | --- | --- |
| [`planning-and-progress-tracking`](skills/planning-and-progress-tracking/SKILL.md) | Turns substantial multi-step work into a tracking folder of verifiable tasks, keeps it accurate while work proceeds, and leaves a reliable handoff for the next chat or agent. | [Overview](docs/planning-and-progress-tracking/README.md) · [Installation](docs/planning-and-progress-tracking/installation.md) · [Usage](docs/planning-and-progress-tracking/usage.md) · [How it works](docs/planning-and-progress-tracking/how-it-works.md) |

## Installation

Clone the repository, review the skill you want, and copy its complete directory into your agent's skills folder. A skill directory contains `SKILL.md` and its `LICENSE`, plus any `references/` or `assets/` it uses; keep them together.

```sh
git clone https://github.com/TheGeogeo/agent-skills.git
```

| Agent | Scope | Destination |
| --- | --- | --- |
| Claude Code | All your local projects | `~/.claude/skills/<skill-name>/` |
| Claude Code | One repository | `<your-project>/.claude/skills/<skill-name>/` |
| Codex | All your local projects | `~/.agents/skills/<skill-name>/` |
| Codex | One repository | `<your-project>/.agents/skills/<skill-name>/` |
| Another agent that supports Agent Skills | User or repository | The skills folder documented by that agent |

For example, a personal Claude Code installation of one skill on macOS or Linux:

```sh
mkdir -p ~/.claude/skills
cp -R agent-skills/skills/planning-and-progress-tracking ~/.claude/skills/
```

Here, `~` means your user home directory. On Windows, use the equivalent directory under your user profile. The destination should contain `SKILL.md` directly.

To update an installed skill, compare the `version` in its `SKILL.md` frontmatter with this repository's, review the new version, and replace the whole directory so that removed files do not linger. If you use several agents, update every installed copy.

Each skill's installation page covers anything specific to that skill, such as making it a standing project rule.

## Using a skill

Start a new session if a skill does not appear after installation. Invoke it by name, with `/<skill-name>` in Claude Code or `$<skill-name>` in Codex, or let the agent select it when your request matches the skill's description. Each skill's usage page has example prompts.

## Repository layout

```text
agent-skills/
  README.md                 This catalog
  LICENSE
  CONTRIBUTING.md
  docs/
    <skill-name>/           Documentation for readers, one folder per skill
  skills/
    <skill-name>/           One installable skill
      SKILL.md              Agent entry point
      LICENSE
      references/           Detailed guidance, read when needed
      assets/               Templates and other starting files
```

## Design principles

- **Self-contained:** each skill directory installs on its own and carries its own license.
- **Portable:** skills work across projects and agents that support the format, and name no model or model provider.
- **Proportional:** a skill scales its process to the work, so small, obvious changes stay small.
- **Lightweight:** skills are Markdown instructions; any dependency or script needs a concrete benefit that justifies its maintenance cost.
- **Guidance, not enforcement:** a skill shapes how the agent works; your agent's permissions and your delivery rules still apply.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Describe the concrete scenario a proposed change improves. A new skill follows the checklist in [Add a skill](CONTRIBUTING.md#add-a-skill).

## License

Released under the [MIT License](LICENSE). Each skill directory includes a copy of the license.

Created and maintained by [TheGeogeo](https://github.com/TheGeogeo).
