# Push Branch

## Objective

Publish the current branch safely and establish remote tracking.

## Procedure

1. Confirm the current branch is not the protected base branch.
2. Inspect local status and recent commits.
3. Verify required checks have passed.
4. Fetch remote references and identify divergence.
5. Push while setting the upstream:

   ```bash
   git push -u origin HEAD
   ```

6. Confirm the remote branch and commit SHA.

## Guardrails

- Do not force-push shared branches by default.
- If history rewriting is explicitly required, use `--force-with-lease`.
- Do not publish secrets, debug artifacts, or unintended commits.
- Stop if the remote branch has unexpected commits.

## Output

- Updated remote branch
- Configured upstream tracking
- Confirmed remote commit
