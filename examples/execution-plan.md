# Example: Import Preview

This illustrative plan demonstrates the task contract. Every task is planned and every verification is unexecuted. It does not describe an existing implementation or claim test results.

## Goal and acceptance

Let a user preview the records and validation errors in an import before applying it. Previewing must leave persisted application data unchanged.

Acceptance requires the expected preview for supported valid input, useful errors for invalid input, and evidence that previewing does not apply the import.

## Scope and constraints

Reuse the application's existing importer, validation rules, and test setup. Define limits and error behavior against the actual project before implementation.

Applying an import, changing storage architecture, and adding a new file format are outside this example's scope.

## Canonical records

This document owns task states, acceptance, and the resume point. Link existing test reports or decision documents from Evidence when the work is actually performed.

If adopted into a project with an existing tracker, move these records into that convention instead of maintaining two active copies.

## Milestones

1. The preview contract fits the existing importer and its constraints.
2. The preview behavior is implemented and independently verified.
3. Required failure scenarios are verified and the final state is recorded.

## Tasks

### IMP-01 - Establish the preview contract

- State: Planned
- Dependencies: None.
- Work: Inspect the importer, its callers, validation rules, and available test commands. Define preview input, output, errors, limits, and the boundary that prevents applying an import.
- Acceptance: The contract identifies the affected modules, observable behavior, important constraints, and the verification required for the next tasks.
- Verification: Trace the relevant entry points and callers. Record the project's actual focused test commands and the scenarios needed to establish the acceptance conditions.
- Evidence: Not run.
- Resume: Start by finding the existing importer entry point and its tests.

### IMP-02 - Produce the preview without applying the import

- State: Planned
- Dependencies: IMP-01.
- Work: Implement the agreed preview path using the existing validation rules and conventions.
- Acceptance: Supported valid input produces the expected records and validation information while leaving persisted data unchanged.
- Verification: Use the focused checks identified in IMP-01. Observe the preview and compare relevant persisted data before and after the operation.
- Evidence: Not run.
- Resume: Wait for IMP-01's contract and verification method before choosing an implementation.

### IMP-03 - Verify failure cases and close the work

- State: Planned
- Dependencies: IMP-02.
- Work: Exercise invalid input, relevant boundaries, and failure paths identified in the contract; correct failures and recheck affected behavior.
- Acceptance: The required scenarios have observed results tied to the tested revision. Acceptance gaps, explicit decisions, and delivery requirements are recorded.
- Verification: Run the relevant existing checks and user-facing scenarios against the implementation. Record the commands, inputs, observed results, and evidence locations.
- Evidence: Not run.
- Resume: Start after IMP-02's acceptance is supported by evidence.

## Decisions and unknowns

- Decision: Reuse the existing importer and validation behavior to preserve project conventions. Revisit this only if inspection demonstrates a concrete incompatibility.
- Unknown: The supported input limits and current test commands must be established during IMP-01.
- Unknown: Any project-specific release or publication requirement must be read from the project's current instructions.

## Resume record

- Active goal and phase: Define the import-preview contract.
- Active task and state: IMP-01, Planned.
- Last verified result and evidence: None; this is an illustrative starting plan.
- Remaining work: Inspect the importer and replace the stated unknowns with findings from the actual project.
- Existing changes and artifacts to preserve: Check the working tree and current project records before editing.
- Next concrete action: Find the existing importer entry point, then identify its callers and focused tests.
- Canonical plan and evidence links: This document; link actual evidence after execution.
