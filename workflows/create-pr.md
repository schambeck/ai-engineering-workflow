# Create Pull Request

## Objective

Open a reviewable pull request with clear scope, evidence, and risk.

## Prerequisites

- Branch is pushed and based on the intended target.
- Relevant checks pass.
- Diff contains one coherent change.

## Procedure

1. Review all commits and the complete diff against the target branch.
2. Reconcile the implementation with acceptance criteria.
3. Complete the repository pull-request template.
4. Include:

   - Problem and context
   - Solution summary
   - Validation evidence
   - Risks, migrations, and rollback
   - Screenshots or API examples when useful

5. Open as draft if significant work or verification remains.
6. Request reviewers based on ownership and risk.

## Guardrails

- Do not hide known failures or incomplete behavior.
- Avoid oversized PRs; split independent changes.
- Link issues and specifications instead of duplicating them.
- Mark breaking changes and operational requirements prominently.

## Completion Criteria

- A reviewer can understand why the change exists and how it was tested.
- Automated checks are running or complete.
- Known risks and follow-up work are explicit.
