# Skills

Claude Skills (`SKILL.md` with YAML frontmatter) that implement the same specialized engineering roles found in [agents](../agents) as auto-invocable, tool-native skills. Each skill is self-contained: a `name`, a `description` used for automatic discovery, and a strict behavioral specification.

Skills are more prescriptive than agents — they define hard constraints, prioritization rules, and "final rule" statements that bias the model toward saying **no** (no bottleneck, no vulnerability, no doc update) unless evidence justifies otherwise.

---

## Available Skills

| Folder                                                                                                | Role                                             | Responsibility                                                                                                                                |
|-------------------------------------------------------------------------------------------------------|--------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| [01a-feature-analysis-architect](01a-feature-analysis-architect/SKILL.md)                             | Senior Business Analyst / Software Architect     | General-purpose pre-implementation analysis: business rules, edge cases, data model, API contract, rollout plan. Never writes code.           |
| [01b-healthcare-queue-architect](01b-healthcare-queue-architect/SKILL.md)                             | Business Analyst + Distributed Systems Architect | Domain-specialized variant of 01a for virtual queue / medical scheduling systems — state machine, slot reservation, concurrency, LGPD.        |
| [02-senior-java-backend-engineer](02-senior-java-backend-engineer/SKILL.md)                           | Senior Java Backend Engineer                     | Implements features (Spring Boot, JPA, Liquibase) by extending existing patterns instead of redesigning the system.                           |
| [03-senior-qa-automation-engineer](03-senior-qa-automation-engineer/SKILL.md)                         | Staff QA Automation Engineer                     | Test-strategy engine: decides what deserves unit/integration/Testcontainers coverage and skips low-value tests.                               |
| [04a-staff-backend-code-reviewer](04a-staff-backend-code-reviewer/SKILL.md)                           | Staff Software Engineer (Code Reviewer)          | Skeptical, evidence-based review across architecture, SOLID, concurrency, transactions, and maintainability.                                  |
| [04b-staff-application-security-risk-analyzer](04b-staff-application-security-risk-analyzer/SKILL.md) | Staff Application Security Engineer              | Attacker-mindset review; reports only realistically exploitable vulnerabilities, not theoretical risk.                                        |
| [04c-staff-performance-bottleneck-analyzer](04c-staff-performance-bottleneck-analyzer/SKILL.md)       | Staff Performance Engineer                       | Flags only bottlenecks with measurable impact; explicitly avoids micro-optimization advice.                                                   |
| [05-staff-documentation-impact-analyzer](05-staff-documentation-impact-analyzer/SKILL.md)             | Staff Software Documentation Engineer            | Decides *if*, *what*, and *where* documentation must change; defaults to "unnecessary" unless justified.                                      |
| [06-ai-pr-gate-orchestrator](06-ai-pr-gate-orchestrator/SKILL.md)                                     | AI PR Gate Orchestrator                          | Not a reviewer itself — aggregates findings from the 04x skills into a weighted risk score and an Approve / Request Changes / Block decision. |

---

## Design Principles

### Discoverable by Description

The `description` field in each skill's frontmatter is written for automatic matching — it states the trigger conditions so the assistant can select the right skill without manual invocation.

### Deny-by-Default

Skills default to *not* flagging an issue, *not* updating docs, and *not* adding a test unless there is concrete evidence it adds value. This keeps output signal-heavy and avoids noisy, low-value findings.

### Severity-Aware and Weighted

The 04x review skills classify findings as CRITICAL/HIGH/MEDIUM/LOW. The orchestrator (06) converts those classifications into a weighted score (Security 30%, Correctness 25%, Data Integrity 20%, Performance 10%, Tests 10%, Documentation 5%) to reach a single merge decision.

### General vs. Domain-Specialized

01a is the general-purpose analysis skill; 01b is a domain-specific specialization (healthcare queueing) of the same role. When adapting this collection to a new domain, prefer cloning the `01a` pattern rather than editing it in place.

---

## Typical Pipeline

```
01a/01b — Feature Analysis
        ↓
02 — Backend Implementation
        ↓
03 — Test Generation
        ↓
04a/04b/04c — Code / Security / Performance Review (parallel)
        ↓
06 — AI PR Gate Orchestrator (score + decision)
        ↓
05 — Documentation Impact Analysis
```

See [06-ai-pr-gate-orchestrator/SKILL.md](06-ai-pr-gate-orchestrator/SKILL.md) for the full scoring model and an example CI pipeline wiring these skills together as automated PR gates.

---

## Contributing

When adding a new skill:

* Write the `description` field as a trigger condition, not a summary — it drives automatic selection.
* State a `CORE PRINCIPLE` that biases the skill toward the safe default (e.g., "assume secure unless proven otherwise").
* Define a strict, structured `OUTPUT FORMAT` section.
* Include an `UNCERTAINTY HANDLING` section instructing the skill to state assumptions rather than invent behavior.
* If specializing an existing skill for a domain, create a new sibling folder instead of overwriting the general version.
