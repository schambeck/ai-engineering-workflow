# Workflows

Reusable, tool-agnostic engineering workflows that govern how changes move from a local branch to a released, reviewed artifact. Each workflow describes a procedure an AI assistant should follow — including validation steps and explicit approval gates before any irreversible or externally visible action.

---

## Available Workflows

| File | Purpose |
|---|---|
| [create-branch.md](create-branch.md) | Creates a Conventional-Commits-style branch name from `main` and waits for explicit approval before running `git checkout -b`. |
| [create-commit.md](create-commit.md) | Drafts a Conventional Commits message for staged changes and waits for approval before running `git commit`. |
| [push-branch.md](push-branch.md) | Validates the branch is not a protected branch and the tree is clean, then pushes to `origin` (never force-pushes without explicit request). |
| [create-pr.md](create-pr.md) | Validates the branch state, drafts a PR title and description, and waits for approval before opening the pull request. |
| [review-pr.md](review-pr.md) | Reviews a pull request end-to-end (diff, tests, CI) and reports findings ordered by severity using a fixed Problem/Impact/Evidence/Suggestion format. |
| [resolve-review-comments.md](resolve-review-comments.md) | Backend-developer workflow for triaging and resolving PR review comments — critically evaluates each suggestion instead of applying it blindly, and justifies any rejection. |
| [release.md](release.md) | Publishes a traceable, tested release with release notes, progressive deployment, smoke tests, and rollback conditions. |

---

## Design Principles

### Approval Gates

Any workflow that performs an irreversible or externally visible action (branch creation, commit, push, PR creation) stops and shows the proposed action for explicit approval first. No workflow force-pushes or skips this gate on its own.

### Validation Before Action

Workflows verify state before acting: the current branch isn't `main`/protected, the working tree is clean, changes are committed, CI is green. Failing validation blocks the workflow rather than working around it.

### Evidence-Based Review

`review-pr.md` and `resolve-review-comments.md` require findings and rejections to be backed by a concrete code path or technical justification — never a bare opinion.

### Behavior-Preserving by Default

`resolve-review-comments.md` explicitly permits pushing back on a reviewer suggestion when it would break compatibility, weaken security, or introduce regressions — as long as the rejection is justified in the output.

---

## Typical Sequence

```
create-branch
    ↓
(implementation)
    ↓
create-commit
    ↓
push-branch
    ↓
create-pr
    ↓
review-pr
    ↓
resolve-review-comments  (loop until approved)
    ↓
release
```

Pairs with the [agents](../agents) and [skills](../skills) that perform the actual implementation and review work, and the [checklists](../checklists) used to validate each stage.

---

## Contributing

When adding a new workflow:

* Define a clear `Objective` or `Procedure` up front.
* List explicit pre-conditions/validation steps before any action.
* Add an approval gate before any git operation that pushes, rewrites history, or is otherwise hard to reverse.
* Include concrete examples (branch names, commit messages, comment formats) rather than abstract descriptions.
* State guardrails explicitly (e.g., "never force push unless explicitly requested").
