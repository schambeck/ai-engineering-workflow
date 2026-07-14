# AI Supervisor Platform

A curated collection of reusable AI engineering workflows, agents, templates, and project specifications for software development.

## Motivation

Modern AI coding assistants are powerful, but their effectiveness depends heavily on context, constraints, and well-defined workflows.

This repository aims to capture proven engineering workflows that can be reused across projects and AI tools, improving consistency, quality, and developer productivity.

The workflows are designed to be AI-agnostic and can be used with:

* OpenAI Codex
* Claude Code
* GitHub Copilot
* Cursor
* Continue
* Cline
* Other AI coding assistants

---

## Goals

* Standardize common software engineering workflows.
* Improve code quality and maintainability.
* Reduce repetitive prompt engineering.
* Encourage behavior-preserving refactoring.
* Promote best practices for architecture, testing, and code reviews.
* Provide reusable project specifications.

---

## Repository Structure

```
ai-engineering-workflows/

agents/
checklists/
skills/
templates/
workflows/
```

### agents/

Specialized AI engineering roles.

Examples:

```
agents/
├── architect.md
├── backend-developer.md
├── test-engineer.md
├── code-reviewer.md
├── security-reviewer.md
├── performance-engineer.md
├── docs-engineer.md
```

---

### workflows/

Reusable engineering workflows.

Examples:

```
workflows/
├── create-branch.md
├── create-commit.md
├── push-branch.md
├── create-pr.md
├── review-pr.md
├── resolve-review-comments.md
└── release.md
```

---

### templates/

Reusable templates.

Examples:

```
templates/
├── pr-template.md
├── issue-template.md
└── adr-template.md
```

---

### checklists/

Engineering checklists.

Examples:

```
checklists/
├── code-review.md
├── pull-request.md
├── release.md
└── production-readiness.md
```

---

## Principles

The workflows in this repository follow a few core principles:

### Reusable

Avoid project-specific assumptions whenever possible.

### AI-Agnostic

Work with different AI coding assistants.

### Behavior-Preserving

Prefer minimal, safe changes over large rewrites.

### Incremental

Encourage small, reviewable changes.

### Evidence-Based

Avoid unnecessary refactoring and speculative improvements.

### Test-Driven

Promote automated testing and regression prevention.

---

## Example Workflow

A typical feature implementation may involve:

```
Architect
    ↓
Backend Developer
    ↓
Reviewer
    ↓
Backend Developer
    ↓
QA Engineer
    ↓
Performance Engineer
    ↓
Pull Request
```

Each step can use one or more workflows and specialized agents from this repository.

---

## Contributing

Contributions are welcome.

When adding a new workflow or agent:

* Keep it reusable.
* Avoid tool-specific assumptions.
* Prefer clear constraints over lengthy instructions.
* Document the intended use case.
* Include examples when appropriate.

---

## License

MIT
