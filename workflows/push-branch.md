# Branch Push Workflow

Push the current local branch to the remote repository.

## Pre-Push Validation

Before pushing:

1. Verify the current branch name.
2. Confirm that the branch is not `main`, `master`, `develop`, or any protected base branch.
3. Check that the working tree is clean.
4. Confirm that all intended changes are already committed.
5. Push the current branch to `origin`.

## First Push

If the branch does not yet exist on the remote, set the upstream tracking branch using:

```bash
git push -u origin <current-branch>
```

## Subsequent Pushes

If the branch already exists on the remote, use:

```bash
git push
```

## Important

Do not force push unless I explicitly request it.
