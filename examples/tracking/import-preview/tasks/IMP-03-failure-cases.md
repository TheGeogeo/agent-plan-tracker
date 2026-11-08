# IMP-03 — Failure cases verified and work closed

Back to [TRACKING.md](../TRACKING.md).

- State: Planned
- Dependencies: IMP-02.
- Why: invalid input must produce useful errors ([scope.md](../scope.md#goal-and-acceptance)).
- Work: exercise invalid input, the relevant boundaries, and the failure paths identified in the contract; correct failures and recheck the affected behavior.
- Acceptance:
  1. The required scenarios have observed results tied to the tested revision.
  2. Acceptance gaps, explicit decisions, and delivery requirements are recorded.
- Verification: run the relevant existing checks and user-facing scenarios against the implementation; record the commands, inputs, observed results, and evidence locations under `evidence/imp-03/`.
- Evidence: Not run.
- Resume: start after the IMP-02 acceptance is supported by evidence.
