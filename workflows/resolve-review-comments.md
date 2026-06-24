# Resolve Review Comments

## Objective

Address review feedback with traceable changes and clear responses.

## Procedure

1. Collect unresolved review threads and group related findings.
2. Validate each finding against current code and requirements.
3. For valid feedback:

   - Implement the smallest complete fix.
   - Add or update regression tests.
   - Run relevant checks.
   - Reply with what changed and the evidence.

4. For feedback that should not be implemented:

   - Explain the technical reason.
   - Provide evidence or an alternative.
   - Leave the thread open until agreement.

5. Re-review the final diff for interactions between fixes.
6. Resolve threads only after the concern is addressed or explicitly closed.

## Guardrails

- Do not resolve comments silently.
- Do not weaken tests or contracts merely to satisfy a suggestion.
- Keep unrelated cleanup out of the feedback cycle.
- Request clarification when a comment permits materially different outcomes.
