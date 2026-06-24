# Release Checklist

## Readiness

- [ ] Version and scope are confirmed.
- [ ] Target commit and included changes are identified.
- [ ] Required reviews and CI checks pass.
- [ ] Release notes are complete.

## Compatibility and Data

- [ ] Breaking changes are communicated.
- [ ] Database migrations are reviewed and rehearsed.
- [ ] Backups or recovery points exist where required.
- [ ] Configuration and secret changes are available in the target environment.

## Deployment

- [ ] Artifacts are reproducible and traceable to the commit.
- [ ] Deployment order and ownership are clear.
- [ ] Smoke tests are defined.
- [ ] Rollback steps and stop conditions are explicit.

## Verification

- [ ] Health, errors, latency, traffic, and saturation are monitored.
- [ ] Critical user journeys pass after deployment.
- [ ] The released commit is tagged.
- [ ] Release outcome and incidents are recorded.
