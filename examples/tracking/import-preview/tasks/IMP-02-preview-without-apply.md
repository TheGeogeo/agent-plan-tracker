# IMP-02 — Preview produced without applying the import

Back to [TRACKING.md](../TRACKING.md).

- State: Planned
- Dependencies: IMP-01.
- Why: the core of the requested feature ([scope.md](../scope.md#goal-and-acceptance)).
- Work: implement the agreed preview path with the existing validation rules and conventions ([D1](../decisions.md)).
- Acceptance:
  1. Supported valid input produces the expected records and validation information.
  2. Persisted data is unchanged after a preview.
- Verification: use the focused checks identified in IMP-01; observe the preview and compare the relevant persisted data before and after the operation.
- Evidence: Not run.
- Limits: None.
- Accepted deviations: None.
- Resume: wait for the IMP-01 contract and verification method before choosing an implementation.
