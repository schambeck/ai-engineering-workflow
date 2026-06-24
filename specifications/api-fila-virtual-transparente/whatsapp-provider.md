# WhatsApp Provider

## Status

Draft integration contract.

## Objective

Provide a replaceable WhatsApp messaging boundary with reliable delivery tracking and safe handling of customer data.

## Interface

The application-facing port should support:

```text
sendMessage(recipient, template, parameters, idempotencyKey) -> messageReference
getStatus(messageReference) -> deliveryStatus
handleCallback(payload, signature) -> acknowledgment
```

## Requirements

1. Provider-specific payloads remain inside the adapter.
2. Recipient numbers use a canonical international format.
3. Only approved templates and validated parameters may be sent.
4. Every send uses an application-generated idempotency key.
5. Timeouts, throttling, and transient provider failures are retryable with bounded exponential backoff.
6. Permanent failures are recorded without endless retry.
7. Callback signatures are verified before processing.
8. Callback events are idempotent and may arrive out of order.
9. Logs redact phone numbers, message content, tokens, and provider secrets.

## Delivery Status

- `PENDING`
- `ACCEPTED`
- `DELIVERED`
- `READ`
- `FAILED`

Status may advance but must not regress due to an older callback.

## Configuration

Credentials, sender identifiers, endpoints, timeout values, and retry policy must come from external configuration. Secrets must never be committed.

## Verification

- Adapter contract tests
- Timeout, throttling, and retry tests
- Duplicate and out-of-order callback tests
- Invalid-signature tests
- Redaction tests
- Sandbox-provider integration test
