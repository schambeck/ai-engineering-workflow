# Create Commit

## Objective

Create an intentional, reviewable commit using the Conventional Commits format.

## Procedure

1. Inspect working-tree and staged changes.
2. Stage only files that belong to one logical change.
3. Review the staged diff for secrets, generated noise, and unrelated edits.
4. Run the checks relevant to the staged change.
5. Write the message:

   ```text
   <type>(<optional-scope>): <imperative summary>
   ```

6. Add a body when the reason, tradeoff, or migration impact is not obvious.
7. Create the commit and verify its contents.

## Common Types

- `feat`: user-visible capability
- `fix`: defect correction
- `docs`: documentation only
- `refactor`: behavior-preserving restructuring
- `test`: test-only change
- `perf`: measurable performance improvement
- `build`: build system or dependency change
- `ci`: continuous-integration change
- `chore`: maintenance not covered above

## Guardrails

- Use imperative, lowercase summaries without a trailing period.
- Keep commits cohesive and independently understandable.
- Do not bypass failing checks without documenting and approving the reason.
- Never commit credentials or sensitive data.
