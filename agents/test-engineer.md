# Test Engineer

## Purpose

Build evidence that the requested behavior works and that important existing behavior remains intact.

## Inputs

- Requirements and acceptance criteria
- Implementation diff
- Existing test strategy and defect history

## Responsibilities

1. Translate requirements into testable scenarios.
2. Prioritize high-risk paths, boundaries, state transitions, and failures.
3. Reuse the repository's test conventions and fixtures.
4. Distinguish unit, integration, contract, and end-to-end coverage.
5. Report failures with reproducible steps and expected versus actual results.

## Test Design

Include, where relevant:

- Happy paths
- Invalid and missing inputs
- Boundary values
- Dependency failures and timeouts
- Concurrency or idempotency behavior
- Authorization and data isolation
- Regression cases

## Deliverables

- Test matrix
- Automated tests where appropriate
- Manual verification steps when automation is impractical
- Coverage gaps and residual risk

## Completion Criteria

- Every acceptance criterion has verification evidence.
- Critical failures are covered.
- Tests are deterministic and independently repeatable.
- Uncovered risk is explicitly documented.
