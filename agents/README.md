# Agents

Specialized AI engineering roles used across the software delivery lifecycle, from analysis to implementation, testing, review, and documentation.

Each agent defines a single responsibility, an explicit scope, and a structured output format so results are predictable and easy to reuse across AI coding assistants.

---

## Available Agents

| File                                                     | Role                                           | Responsibility                                                                                                                         |
|----------------------------------------------------------|------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| [01-architect.md](01-architect.md)                       | Senior Business Analyst and Software Architect | Analyzes a requested feature and produces an implementation plan. Does not write code.                                                 |
| [02-backend-developer.md](02-backend-developer.md)       | Senior Java Backend Engineer                   | Implements features (Java 25, Spring Boot 4, PostgreSQL) following the provided specification and existing project conventions.        |
| [03-code-reviewer.md](03-code-reviewer.md)               | Staff Software Engineer (Code Reviewer)        | Reviews a pull request for architecture, security, performance, and maintainability issues, and can convert findings into PR comments. |
| [04-docs-engineer.md](04-docs-engineer.md)               | Senior Software Documentation Engineer         | Determines what documentation (README, ADRs, API docs, diagrams) should be created or updated after a change.                          |
| [05-performance-engineer.md](05-performance-engineer.md) | Performance Engineer                           | Identifies performance bottlenecks, scalability risks, and resource inefficiencies.                                                    |
| [06-security-reviewer.md](06-security-reviewer.md)       | Application Security Engineer                  | Identifies security vulnerabilities, privacy risks, and OWASP Top 10 concerns.                                                         |
| [07-test-engineer.md](07-test-engineer.md)               | Senior QA Automation Engineer                  | Designs and implements automated tests (unit, integration, Testcontainers) without touching production code.                           |

---

## Design Principles

### Single Responsibility

Each agent has one clearly defined job and explicit boundaries on what it must **not** do (e.g., the architect never writes code, the test engineer never implements features).

### Structured Output

Every agent produces output in a fixed set of sections (e.g., Findings Summary, Deliverables, Implementation Plan), making results consistent and easy to hand off to the next agent in the workflow.

### Evidence-Based

Agents are instructed to state assumptions explicitly, avoid inventing requirements, and base findings on observable code rather than speculation.

### Severity-Aware Review

The reviewer agents (code, security, performance) classify every finding as CRITICAL, HIGH, MEDIUM, or LOW to prioritize what must be fixed before merge.

---

## Typical Usage Order

```
01-architect
    ↓
02-backend-developer
    ↓
03-code-reviewer / 06-security-reviewer / 05-performance-engineer
    ↓
07-test-engineer
    ↓
04-docs-engineer
```

Agents can be used independently or chained together as part of a larger [workflow](../workflows).

---

## Contributing

When adding a new agent:

* Give it a single, well-defined responsibility.
* State explicitly what it should and should not do.
* Define a structured output format.
* Include guidance for handling uncertainty and ambiguity.
* Prefix the filename with the next available two-digit number to indicate suggested execution order.
