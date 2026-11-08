# IMP-01 — Preview contract fits the existing importer

Back to [TRACKING.md](../TRACKING.md).

- State: Planned
- Dependencies: None.
- Why: the input limits, error behavior, and test commands are unknown ([scope.md](../scope.md#unknowns)).
- Work: inspect the importer, its callers, validation rules, and available test commands. Define the preview's input, output, errors, limits, and the boundary that prevents applying an import.
- Acceptance:
  1. The contract identifies the affected modules, the observable behavior, and the important constraints.
  2. The verification needed by IMP-02 and IMP-03 is defined with the project's actual commands.
- Verification: trace the relevant entry points and callers; record the focused test commands and the scenarios that establish the acceptance conditions.
- Evidence: Not run.
- Limits: None.
- Accepted deviations: None.
- Resume: start by finding the existing importer entry point and its tests.
