# Conventional Commit Generator

Create a commit for the staged changes using the Conventional Commits specification.

## Commit Type Selection

Choose the most appropriate commit type based on the staged changes:

* `feat`
* `fix`
* `refactor`
* `perf`
* `test`
* `docs`
* `build`
* `ci`
* `chore`
* `style`

## Commit Message Requirements

The commit message should:

* accurately describe the primary purpose of the changes;
* be concise and specific;
* use the following format:

```text
<type>: <short description>
```

## Examples

```text
refactor: migrate JdbcClient queries to Spring Data JPA
```

```text
feat: add QueryDSL support for dynamic filtering
```

```text
fix: prevent race condition when calling next patient
```

```text
test: add integration tests for queue locking
```

## Approval Workflow

Before committing:

* display the proposed commit message;
* briefly explain why that commit type was chosen;
* wait for my explicit approval.

## Important

Do not execute `git commit` until I explicitly approve the proposed message.
