# Usage gate

Claude Code subscription plans limit usage over a rolling 5-hour window and over a week. In the [orchestrated mode](execution-modes.md#mode-3-orchestrated-subagents), a usage gate keeps the orchestrator from launching work that the remaining usage may not cover, and leaves the finished work committed with a handoff.

This reference is a specification. The skill ships no script: when the user chooses the orchestrated mode on Claude Code, write the gate fresh for the current host, verify it, and only then rely on it. Rewrite it if a later run shows that its source has changed.

## Rules

These defaults apply unless the user sets other thresholds; record any change in `decisions.md`.

| Check point | Rule | Exception |
| --- | --- | --- |
| Before launching a task | 5-hour usage above 80%: STOP | Not applied when the task to launch is the last one. That task, the final review, the final commit, and an authorized push proceed. |
| Before launching a task | Weekly usage above 90%: STOP | None |
| After a task ends, once its subagent has finished | Weekly usage above 90%: STOP | None, including after the last task |

- Weekly usage is the highest of the weekly limits that the source reports, across all models and model-specific limits.
- STOP never interrupts a running subagent. Follow the [stop procedure](execution-modes.md#stop-procedure).
- If usage cannot be read, retry once after a short wait. If it is still unreadable, treat it as STOP and tell the user why.

## Location

- Write the gate to `.claude/scripts/usage-gate.<extension>` in the project, and record its path and command in `execution.md`.
- Keep it out of version control: add its path to `.git/info/exclude` unless the user asks to version it, so that task commits cannot pick it up.
- Use a runtime that already exists in the environment, such as the Python standard library, PowerShell, or a POSIX shell with common tools. Install nothing.

## Source of usage data

Before writing the gate, check the current Claude Code documentation and choose the source:

1. **A documented source that the gate can read from this host**, if one exists. At the time of writing, the status line input includes `rate_limits.five_hour.used_percentage` and `rate_limits.seven_day.used_percentage`, but only status line commands receive it, not hooks, and IDE integrations may not run a status line.
2. **Otherwise, the usage endpoint behind Claude Code's `/usage` command.** At the time of writing it is `GET https://api.anthropic.com/api/oauth/usage`, called with `Authorization: Bearer <OAuth access token>` and `anthropic-beta: oauth-2025-04-20`. It is undocumented: confirm the URL, the headers, and the response fields with one call before relying on them. Two response shapes have been seen: a `limits` list, where the 5-hour entry has the `session` kind and weekly entries belong to the `weekly` group with a `percent` value; and top-level `five_hour` and `seven_day*` objects with a `utilization` value and `resets_at`.

## Credentials and privacy

- Read the OAuth access token at run time from where Claude Code stores it: the `.credentials.json` file in the Claude configuration directory (`CLAUDE_CONFIG_DIR` when set, otherwise `.claude` in the user's home directory), or the system keychain on macOS. Resolve the home directory at run time.
- Send the token only to the usage endpoint over HTTPS. Never print, log, store, or commit it, and keep it out of error messages.
- The gate hard-codes no keys, tokens, account identifiers, environment values, email addresses, or user-specific paths; it reads what it needs at run time. Use a generic User-Agent.

## Interface

- `--point before-step|after-step`: required check point.
- `--final-step`: with `before-step`, the task to launch is the last one.
- `--five-hour-stop <percent>`: default 80. `--weekly-stop <percent>`: default 90.
- Output, one line: `five_hour=<percent> weekly=<percent> resets=<5-hour reset>,<weekly reset> verdict=<CONTINUE | STOP: reason | UNAVAILABLE: reason>`.
- Exit code: 0 to continue, 10 to stop, 2 when usage is unavailable.

## Verify at creation

Record the results in `execution.md`, without the token:

1. With the default thresholds, both percentages and both reset times are read. When the user can check, they match what `/usage` shows.
2. `--point before-step --five-hour-stop 0` returns STOP with exit code 10. Adding `--final-step` returns CONTINUE while weekly usage is below its threshold.
3. `--point after-step --weekly-stop 0` returns STOP with exit code 10.
4. With credentials unavailable, for example `CLAUDE_CONFIG_DIR` pointing to an empty temporary directory on a host that stores credentials in a file, the gate returns UNAVAILABLE with exit code 2, and its output contains no token.
5. The gate file contains no token, user path, or other personal data.

## Use during orchestration

- Before each task launch, run it at `before-step`, adding `--final-step` for the last task.
- After each task's subagent finishes and the task is recorded, run it at `after-step`.
- Add each result to the gate log in `execution.md`: time, check point, and output line.
