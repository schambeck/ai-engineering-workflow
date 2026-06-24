# Branch Creation Workflow

Before starting the implementation:

## Preparation

1. Sync with the latest `main` branch.
2. Create a new branch from `main`.
3. Generate a Conventional Commits–style branch name that best describes the requested work.

## Branch Naming Format

```text
<type>/<short-kebab-case-description>
```

## Branch Type Selection

Use the most appropriate type:

* `feat`
* `fix`
* `refactor`
* `perf`
* `test`
* `docs`
* `chore`

## Naming Requirements

The branch name should be:

* concise;
* descriptive;
* aligned with the primary objective of the changes;
* written in kebab-case.

## Examples

```text
refactor/migrate-jdbcclient-to-jpa
```

```text
refactor/replace-jdbcclient-with-spring-data-jpa
```

```text
feat/add-querydsl-support
```

```text
fix/queue-entry-locking
```

## Approval Workflow

Before creating a branch:

* display the proposed branch name;
* briefly explain why that branch name was chosen;
* wait for my explicit approval.

## Important
Do not execute `git checkout -b ` until I explicitly approve the proposed branch name.
