# Queue Flow

## Status

Draft domain contract.

## Objective

Define deterministic lifecycle rules for customers moving through a transparent virtual queue.

## States

- `WAITING`: customer is queued and eligible for ordering.
- `CALLED`: customer has been invited for service.
- `IN_SERVICE`: service has started.
- `COMPLETED`: service finished successfully.
- `CANCELLED`: entry was withdrawn.
- `EXPIRED`: customer did not respond within the allowed time.

## Allowed Transitions

```text
WAITING -> CALLED | CANCELLED
CALLED -> IN_SERVICE | EXPIRED | CANCELLED
IN_SERVICE -> COMPLETED | CANCELLED
COMPLETED, CANCELLED, EXPIRED -> terminal
```

## Requirements

1. A customer may have at most one active entry per queue.
2. Queue position is derived from explicit priority and enqueue order.
3. State transitions are atomic and reject stale versions.
4. Repeated equivalent requests are idempotent.
5. Every transition records timestamp, actor, previous state, and new state.
6. Notifications occur only after the state transaction commits.
7. Public status responses must not expose another customer's private data.

## Failure Behavior

- Invalid transitions return a domain conflict.
- Missing entries return not found.
- Concurrent updates allow one winner; stale updates fail without partial effects.
- Notification failure does not roll back an already committed transition and must be retryable.

## Verification

- Transition matrix tests
- Duplicate active-entry test
- Stable ordering test
- Concurrent call and cancellation tests
- Notification retry and idempotency tests
- Authorization and data-isolation tests
