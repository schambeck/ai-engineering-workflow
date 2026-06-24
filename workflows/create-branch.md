# Create Branch

## Objective

Create a focused branch from an up-to-date base without disturbing local work.

## Inputs

- Base branch, normally `main`
- Work type and concise description
- Issue identifier, when available

## Procedure

1. Check repository status and preserve unrelated local changes.
2. Fetch remote references.
3. Confirm the selected base branch and update it safely.
4. Create a branch using:

   ```text
   <type>/<issue>-<short-description>
   ```

   Common types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`.

5. Verify the branch name and starting commit.

## Example

```bash
git fetch origin
git switch main
git pull --ff-only
git switch -c feat/123-add-queue-status
```

## Guardrails

- Do not discard or overwrite uncommitted work.
- Do not branch from a stale or unintended commit.
- Keep one coherent objective per branch.

## Output

- New local branch
- Confirmed base commit
- Clean or intentionally dirty working-tree status
