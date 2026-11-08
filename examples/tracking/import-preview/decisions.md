# Decisions: import preview

Back to [TRACKING.md](TRACKING.md). One row per decision. Never rewrite a past row: add a new one that supersedes it.

| ID | Date | Question or topic | User's answer, verbatim | Consequence for this tracking |
| --- | --- | --- | --- | --- |
| D1 | 2026-01-15 | Build the preview on the existing importer, or write a separate parser? | "Reuse the importer." | IMP-02 reuses the existing importer and validation rules. Revisit only if IMP-01 demonstrates a concrete incompatibility. |

## Choices made while planning

Choices the agent made without a user decision, reported to the user and reversible:

- The tracking stays local and out of commits, following the project's rule against plans in versioned paths.
