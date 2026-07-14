# Templates

Reusable document templates that standardize how decisions, issues, and pull requests are written up across projects. Each template uses HTML comments (`<!-- -->`) to prompt for content without polluting the rendered document.

---

## Available Templates

| File                                   | Used For                                                                                                                    |
|----------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| [adr-template.md](adr-template.md)     | Architecture Decision Records — context, decision drivers, considered options, decision, consequences, and validation plan. |
| [issue-template.md](issue-template.md) | Bug reports and feature requests — problem, desired outcome, acceptance criteria, non-goals, risks/dependencies.            |
| [pr-template.md](pr-template.md)       | Pull request descriptions — summary, related work, validation performed, risk/impact, deployment and rollback notes.        |

---

## Design Principles

### Outcome-Focused, Not Solution-Prescribing

`issue-template.md` explicitly asks for the "Desired Outcome" rather than a preferred implementation, keeping the solution space open for whoever picks up the work.

### Risk and Rollback Are First-Class

Both `pr-template.md` and `adr-template.md` require explicit sections for risk, compatibility, and — for PRs — deployment/rollback steps. A change isn't fully described until its failure mode is.

### Evidence Over Assertion

`pr-template.md` requires validation to be listed as concrete checks (unit tests, integration tests, static analysis, manual verification) plus an "Evidence" section for logs, screenshots, or benchmark results.

---

## Usage

Copy the relevant template's content into the target platform (GitHub issue/PR body, ADR file in your `docs/adr/` directory, etc.) and fill in each section. Leave a section explicitly empty or marked "N/A" rather than deleting it — that preserves the checklist value for reviewers.

Pairs with the [checklists](../checklists) (e.g., `pull-request.md`) used to verify a filled-out template before merge, and the [workflows](../workflows) (`create-pr.md`) that generate PR descriptions following this template's structure.

---

## Contributing

When adding a new template:

* Use HTML comments to guide the author on what belongs in each section, not filler prose.
* Include a risk/impact section — compatibility, security, performance, or operational.
* Keep placeholders generic (no project-specific names, tools, or paths).
* Add a checklist section at the end only if the template represents a gated document (like a PR).
