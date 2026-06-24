# Production Readiness Checklist

## Reliability

- [ ] Timeouts, retries, and idempotency are defined.
- [ ] Failure modes degrade safely.
- [ ] Dependencies have clear availability assumptions.
- [ ] Recovery and rollback procedures are tested.

## Observability

- [ ] Structured logs support diagnosis without exposing sensitive data.
- [ ] Metrics cover traffic, errors, latency, and saturation.
- [ ] Alerts are actionable and have owners.
- [ ] Dashboards and runbooks exist for critical paths.

## Security and Compliance

- [ ] Authentication and authorization are verified.
- [ ] Secrets are externally managed and rotatable.
- [ ] Sensitive data retention and access are appropriate.
- [ ] Abuse, injection, and dependency risks are assessed.

## Capacity and Performance

- [ ] Expected and peak workloads are defined.
- [ ] Load testing covers representative data and concurrency.
- [ ] Resource limits and scaling behavior are configured.
- [ ] Bottlenecks and capacity thresholds are known.

## Operations

- [ ] Deployment is automated and traceable.
- [ ] Configuration is validated before startup.
- [ ] On-call ownership and escalation paths are documented.
- [ ] Business continuity and data recovery requirements are met.
