# Code Review Checklist

## Correctness

- [ ] The change satisfies the stated requirements.
- [ ] Boundary and failure cases are handled.
- [ ] State changes and side effects are atomic where required.
- [ ] Existing public behavior is preserved unless intentionally changed.

## Design and Maintainability

- [ ] The implementation follows repository conventions.
- [ ] Responsibilities and dependencies are clear.
- [ ] Complexity and abstractions are justified.
- [ ] The diff contains no unrelated refactoring.

## Security and Data

- [ ] Inputs are validated at trust boundaries.
- [ ] Authorization is enforced for affected resources.
- [ ] Secrets and sensitive data are protected and redacted.
- [ ] Queries and persistence changes preserve data integrity.

## Tests and Operations

- [ ] Tests cover the behavior and credible regressions.
- [ ] Tests are deterministic and meaningful.
- [ ] Logs, metrics, and errors support diagnosis.
- [ ] Performance and deployment impact are acceptable.

## Review Outcome

- [ ] Blocking findings are specific and actionable.
- [ ] Optional suggestions are clearly marked.
- [ ] Approval is based on the final diff and passing checks.
