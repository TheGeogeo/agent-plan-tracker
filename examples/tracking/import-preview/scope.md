# Scope: import preview

Back to [TRACKING.md](TRACKING.md).

## Requests

Verbatim, in their original language, with dates.

1. 2026-01-15: "Add an import preview so users can check their data before importing it. Plan it with the tracking skill first."

## Goal and acceptance

Let a user preview the records and validation errors of an import before applying it. Previewing must leave persisted application data unchanged.

Acceptance: supported valid input produces the expected preview, invalid input produces useful errors, and evidence shows that previewing does not apply the import.

## In scope

- The preview path, built on the application's existing importer, validation rules, and test setup.
- The limits and error behavior of the preview, defined against the actual project.

## Out of scope

- Applying an import.
- Changing the storage architecture.
- Adding a new file format.

## Constraints

- Reuse the existing importer and validation behavior ([D1](decisions.md)).
- Release and publication requirements come from the project's current instructions.

## Work limits

- Stay on the requested tasks and stop when their acceptance is proven.
- Report a major problem outside the tasks to the user before fixing it.
- Note smaller observations in one line in the affected task, without a fix or a new task.
- Add no task without the user's request.

## Unknowns

- Supported input limits: resolved by IMP-01.
- Current focused test commands: resolved by IMP-01.
