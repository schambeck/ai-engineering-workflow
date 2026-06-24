# Release

## Objective

Publish a traceable, tested release with explicit operational and rollback steps.

## Inputs

- Release version and target environment
- Included changes
- Compatibility and migration requirements

## Procedure

1. Confirm the release scope and version according to project policy.
2. Verify the target commit, CI status, and required approvals.
3. Review dependency, schema, configuration, and infrastructure changes.
4. Prepare release notes covering:

   - Features and fixes
   - Breaking changes
   - Migration steps
   - Known limitations

5. Execute the documented build and artifact-signing process.
6. Deploy progressively when supported.
7. Run smoke tests and inspect health, errors, latency, and saturation.
8. Tag the exact released commit and publish release metadata.
9. Roll back if predefined stop conditions are met.

## Guardrails

- Never release from an unverified local-only state.
- Back up or rehearse irreversible data migrations.
- Do not combine deployment troubleshooting with unrelated changes.
- Record who released what, when, and to which environment.
