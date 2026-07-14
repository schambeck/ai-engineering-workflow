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
prompts/
skills/
templates/
workflows/
```

Each folder has its own `README.md` with the full file list, design principles, and typical usage order — the sections below are a summary.

### agents/

Specialized AI engineering roles, used as plain role prompts. See [agents/README.md](agents/README.md).

```
agents/
├── 01-architect.md
├── 02-backend-developer.md
├── 03-code-reviewer.md
├── 04-docs-engineer.md
├── 05-performance-engineer.md
├── 06-security-reviewer.md
└── 07-test-engineer.md
```

---

### skills/

The same engineering roles packaged as Claude Skills (`SKILL.md` with frontmatter) for automatic, tool-native invocation, plus an orchestrator that aggregates review findings into a merge decision. See [skills/README.md](skills/README.md).

```
skills/
├── 01a-feature-analysis-architect/
├── 01b-healthcare-queue-architect/
├── 02-senior-java-backend-engineer/
├── 03-senior-qa-automation-engineer/
├── 04a-staff-backend-code-reviewer/
├── 04b-staff-application-security-risk-analyzer/
├── 04c-staff-performance-bottleneck-analyzer/
├── 05-staff-documentation-impact-analyzer/
└── 06-ai-pr-gate-orchestrator/
```

---

### workflows/

Reusable engineering workflows covering the git and release lifecycle, with explicit approval gates before irreversible actions. See [workflows/README.md](workflows/README.md).

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

Reusable document templates. See [templates/README.md](templates/README.md).

```
templates/
├── pr-template.md
├── issue-template.md
└── adr-template.md
```

---

### checklists/

Verification checklists used as a gate at each delivery stage. See [checklists/README.md](checklists/README.md).

```
checklists/
├── code-review.md
├── pull-request.md
├── release.md
└── production-readiness.md
```

---

### prompts/

One-off, project-specific prompts that don't fit the reusable folders above. See [prompts/README.md](prompts/README.md).

```
prompts/
├── api-gateway.md
├── arch-doc.md
├── cleanarch-ddd-edd.md
└── create-readme.md
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
