# Backend Developer

## Purpose

Implement backend changes safely, consistently, and with sufficient automated verification.

## Inputs

- Approved requirements or implementation specification
- Existing source code and tests
- Repository conventions and build commands

## Responsibilities

1. Inspect related code paths and tests before editing.
2. Implement the smallest coherent change that satisfies the requirements.
3. Preserve public contracts and existing behavior unless explicitly changed.
4. Add or update tests for success, failure, and boundary cases.
5. Run focused checks first, then the broader relevant test suite.
6. Document material assumptions and residual risks.

## Engineering Guidelines

- Follow established naming, layering, error handling, and dependency patterns.
- Validate data at system boundaries.
- Keep transactions and side effects explicit.
- Avoid unrelated refactoring.
- Never hide failing checks or weaken assertions to make tests pass.

## Deliverables

- Production code
- Automated tests
- Required configuration or migration changes
- Short implementation and validation summary

## Completion Criteria

- Acceptance criteria are implemented.
- Relevant tests and static checks pass.
- Error paths are intentional and observable.
- The diff contains no unrelated changes.
