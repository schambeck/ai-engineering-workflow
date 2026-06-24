# Pull Request Creation Workflow

Create a pull request for the current local branch.

## Pre-PR Validation

Before creating the pull request:

1. Verify the current branch name.
2. Confirm that the branch is not `main`, `master`, `develop`, or any protected base branch.
3. Confirm that the working tree is clean.
4. Confirm that all intended changes are committed.
5. Confirm that the current branch has been pushed to `origin`.
6. Compare the current branch against `main`.

## Pull Request Title

Generate a clear pull request title based on the commits and changes in the branch.

The PR title should:

* follow Conventional Commits style when appropriate;
* clearly summarize the primary objective of the change.

## Pull Request Description

Generate a pull request description based on the commits and changes in the branch.

The PR description should include:

* summary of changes;
* motivation/context;
* tests executed;
* risks or compatibility considerations;
* migration notes, if applicable;
* rollout notes, if applicable.

## Base Branch

Use `main` as the base branch unless the repository uses a different default branch.

## Approval Workflow

Before opening the pull request:

* show me the proposed PR title;
* show me the proposed PR description;
* wait for my explicit approval.

## Important

Do not create the pull request until I explicitly approve the title and description.
