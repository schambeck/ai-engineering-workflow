# Prompts

One-off, project-specific prompts. Unlike [agents](../agents), [skills](../skills), [workflows](../workflows), [templates](../templates), and [checklists](../checklists), these are not meant to be reused as-is across projects — each one targets a specific system, stack, or one-time deliverable and would need to be adapted before reuse.

---

## Available Prompts

| File | Purpose |
|---|---|
| [api-gateway.md](api-gateway.md) | Implementation brief for an API Gateway (Spring Cloud Gateway) centralizing access to a backend service ecosystem. |
| [arch-doc.md](arch-doc.md) | Generates a single interactive HTML "Architecture Explorer" page visualizing flows between packages/layers/components for a specific fleet-management system. |
| [cleanarch-ddd-edd.md](cleanarch-ddd-edd.md) | Extended variant of `arch-doc.md` — a more detailed Architecture Explorer brief for the same Clean Architecture / DDD / Event-Driven system, covering more modules and flows. |
| [create-readme.md](create-readme.md) | Generic prompt that analyzes a repository and generates a complete `README.md` from the actual codebase, structure, and detected stack. |

---

## Why These Are Separate From templates/

[templates/](../templates) holds structural documents meant to be filled in for *any* project (a PR description, an ADR, an issue). The prompts here are tied to a specific system, domain, or stack (e.g., a named "Fleet Control" SaaS, a specific backend ecosystem) — they're kept for reference and as a starting point, not as drop-in reusable content.

`create-readme.md` is the exception — it's stack-agnostic — but it's still a one-shot generation prompt rather than a structural template, so it lives here rather than in `templates/`.

---

## Contributing

When adding a new prompt here:

* Confirm it doesn't fit an existing reusable folder (agent, skill, workflow, template, or checklist) before adding it here.
* Keep any project-specific names, stack details, or domain assumptions explicit rather than implying general reuse.
* Prefer a short filename without a redundant `prompt-` prefix — the folder name already conveys that.
