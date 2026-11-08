# Usage gate

Coding-agent subscription plans limit usage over time windows, for example a rolling 5-hour window and a weekly window. In the [orchestrated mode](execution-modes.md#mode-3-orchestrated-subagents), a usage gate keeps the orchestrator from launching work that the remaining usage may not cover, and leaves the finished work committed with a handoff.

## No provided source

This reference is a specification only. It deliberately gives no link, endpoint, file location, or command for reading usage: those depend on the host and its provider, and they change over time.

The model running the orchestration writes its own detection script for its own host and provider, for example Claude Code by Anthropic, Codex by OpenAI, or Grok by xAI. It builds the script from that provider's current documentation and tools when the user chooses the orchestrated mode, verifies it, and only then relies on it. Rewrite the script when the host or its usage source changes. Never reuse a script written for another host.

## Rules

These defaults apply unless the user sets other thresholds; record any change in `decisions.md`.

| Check point | Rule | Exception |
| --- | --- | --- |
| Before launching each task | Short-window usage above 80%: STOP | Not applied before the last task. That task, the final review, the final commit, and an authorized push proceed. |
| Before launching each task | Weekly usage above 90%: STOP | None |
| After the last task, before the final review | Weekly usage above 90%: STOP | None |

- The check before a task runs once the previous task is verified and committed, so it also covers the end of that task. One check per boundary is enough.
- The short window is the host's shortest rolling limit, such as 5 hours. Weekly usage is the highest of the weekly limits that the source reports, across all models and model-specific limits. If the host's windows differ, record in `execution.md` how they map onto these rules.
- The gate runs only between tasks, so it never interrupts a subagent. On STOP, follow the [stop procedure](execution-modes.md#stop-procedure).
- If usage cannot be read, retry once after a short wait, or after the delay the source asks for when it reports a rate limit. If it is still unreadable, treat it as STOP and tell the user why.
- Usage sources can rate-limit frequent calls: call the gate only at its check points, and space the verification calls at creation.

## Find the usage source

Before writing the gate:

1. Read the host provider's current official documentation for a way that a local process can read plan usage and reset times.
2. Prefer a documented source that works in the session's actual environment: terminal, IDE extension, desktop app, or cloud.
3. If only an undocumented source exists, such as the one behind the host's own usage command, tell the user and get their agreement first. Confirm its current request and response shape with one call before relying on it.
4. If no source can be read, do not write a gate: record "Not available: <reason>" in `execution.md` and agree on pacing with the user.

## Credentials and privacy

- If the source needs credentials, read them at run time from where the host already stores them, so that no secret is typed into the chat or the script. Resolve user-specific locations at run time.
- Send credentials only to the provider's own service over HTTPS. Never print, log, store, or commit them, and keep them out of error messages.
- The gate hard-codes no keys, tokens, account identifiers, environment values, email addresses, or user-specific paths; it reads what it needs at run time. Use a generic User-Agent.

## Location

- Write the gate to a `scripts/` folder inside the host's project configuration folder, such as `.claude/scripts/` on Claude Code, and record its path and command in `execution.md`.
- Keep it out of version control: add its path to `.git/info/exclude` unless the user asks to version it, so that task commits cannot pick it up.
- Use a runtime that already exists in the environment, such as the Python standard library, PowerShell, or a POSIX shell with common tools. Install nothing.

## Interface

- `--point before-task|after-last`: required check point. `after-last` applies the weekly rule only.
- `--last-task`: with `before-task`, the task to launch is the last one, so the short-window rule is skipped.
- `--short-stop <percent>`: default 80. `--weekly-stop <percent>`: default 90.
- `--log <file>`: also append the output line to this file.
- Output, one line: `<UTC time> <point> short=<percent> weekly=<percent> resets=<short reset>,<weekly reset> verdict=<CONTINUE | STOP: reasons | UNAVAILABLE: reason>`. An UNAVAILABLE reason includes the wait the source requested, if any.
- Exit code: 0 to continue, 10 to stop, 2 when usage is unavailable.

## Verify at creation

Space the calls that read usage. Record the results in `execution.md`, without any secret:

1. `--point before-task` with the default thresholds reads both percentages and both reset times. When the user can check, they match what the host's own usage display shows.
2. `--point before-task --short-stop 0 --weekly-stop 0` returns STOP with both reasons and exit code 10.
3. The same command with `--last-task` returns STOP with the weekly reason only.
4. With credentials or the source unavailable, for example the host's configuration directory pointed at an empty temporary directory, the gate returns UNAVAILABLE with exit code 2, and its output contains no secret.
5. The gate file contains no secret, user path, or other personal data.

## Use during orchestration

- Before each task launch, run it at `before-task`, adding `--last-task` for the last task.
- After the last task is verified and committed, run it at `after-last`.
- Pass `--log <tracking>/evidence/usage-gate.log` on every run. The gate keeps the log, so the orchestrator does not edit it; only a STOP or UNAVAILABLE result goes into the resume record.
