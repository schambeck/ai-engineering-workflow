# Review Pull Request

## Objective

Determine whether a pull request is correct, safe, maintainable, and ready to merge.

## Procedure

1. Read the linked requirement, issue, and PR description.
2. Inspect the complete diff and affected call paths.
3. Verify behavior, error handling, data integrity, security, and compatibility.
4. Evaluate whether tests cover requirements and credible regressions.
5. Check CI results and reproduce high-risk behavior when practical.
6. Submit actionable findings ordered by severity.
7. Approve only when no blocking issue remains.

## Review Comment Format

```text
Problem: what can fail
Impact: who or what is affected
Evidence: code path or reproducible scenario
Suggestion: smallest practical correction
```

## Guardrails

- Review the change, not the author.
- Distinguish blocking defects from optional suggestions.
- Avoid expanding scope without a concrete risk.
- Re-check updated code before resolving a finding.
