---
name: practical-testing
description: Design, write, review, consolidate, or remove software tests and test gates. Use to preserve meaningful behavior coverage while keeping the test suite focused and affordable.
---

# Practical Testing

Protect observable behavior with the smallest sufficient body of evidence. Follow the repository's specifications, test requirements, and safety rules. Preserve tests for required behavior when reducing a suite.

Treat test count, execution time, fixture complexity, and maintenance as costs. Add tests for specified behavior that needs better evidence. Use coverage reports only to find gaps in tests for specified behavior.

## Choose what to test

- Derive every test from behavior required by the program's spec files. Assert the observable result the spec guarantees. For a bug, reproduce the defect before the fix when practical.
- Find existing coverage before adding a test. Extend an existing owner or consolidate equivalent assertions when that preserves the evidence. Give each behavior one primary owner in the cheapest sufficient lane; add another only for a distinct property or boundary. Do not remove independently meaningful checks simply because they share setup or touch the same endpoint.
- Test through a public function, registered handler, or other meaningful entry point that exercises several layers of real functions together. Use mocks, fixtures, or fakes to set up scenarios or control dependencies where useful.
- Keep distinct, applicable checks for authorization, validation, privacy, failure behavior, and denied operations without side effects. Shared setup or table cases must not hide which behavior failed. Follow any required endpoint or domain regression matrix.

## Choose where it runs

- Use deterministic in-process tests for business decisions, contract behavior, and error mapping when they can prove the result. Keep test state isolated and run independent cases in parallel where supported.
- Use a real database for properties a fake cannot establish, such as query semantics, constraints, migrations, transactions, and isolation. Use browser, multi-service, or live-provider tests for properties that require those environments. Do not repeat lower-lane assertions without a distinct reason.
- Keep normal gates bounded and deterministic. Put load, throughput, and unusually expensive resource tests in explicit on-demand lanes unless a repository requirement or the task calls for them in the normal gate. Document how to select them and what they need. Measure or investigate material test-cost increases rather than masking them with retries, larger timeouts, or skipped coverage.
- Make selectors, inventories, and prerequisites visible. Keep them aligned with runnable tests and fail clearly on stale or missing required selections. Verify changed selectors execute the intended tests in the intended lane, including exclusions and on-demand cases. Avoid starting the same package repeatedly for overlapping cases in one lane.

## Review and report

- Batch related changes before validation. Run the smallest relevant checks once and run independent checks in parallel when safe. After a routine fix, rerun only the failed checks. Follow any separate validation gates required by the governing workflow.
- When removing or consolidating tests, identify the surviving owner for each protected behavior. Retain or replace assertions that have no equivalent owner. Review the final diff for lost boundaries, redundant evidence, unnecessary fixtures, and hidden cost.
- For a large test audit, record each test's protected behavior, actual lane, and disposition: retain, consolidate, remove, or make on demand. Record the replacement owner or reason. For ordinary changes, use the diff and review rather than creating a permanent inventory.
- Run focused checks appropriate to the change and report what ran, what it proves, and required evidence that remains unavailable. Do not imply that source tests, database tests, image builds, browser checks, or live acceptance prove the same thing.
