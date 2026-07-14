# Checklists

Verification checklists used as the final gate at each stage of the delivery lifecycle: reviewing code, opening a pull request, promoting a service to production, and cutting a release. Each item is phrased as a verifiable yes/no condition (`- [ ]`), not a vague guideline.

---

## Available Checklists

| File                                               | Used When                                                                                                                       |
|----------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| [code-review.md](code-review.md)                   | Reviewing a diff — correctness, design/maintainability, security/data, tests/operations.                                        |
| [pull-request.md](pull-request.md)                 | Opening or reviewing a PR — scope, quality, risk, and delivery readiness.                                                       |
| [production-readiness.md](production-readiness.md) | Promoting a new service or major feature to production — reliability, observability, security/compliance, capacity, operations. |
| [release.md](release.md)                           | Cutting a release — readiness, compatibility/data, deployment, post-deploy verification.                                        |

---

## Design Principles

### Verifiable, Not Aspirational

Every item is a concrete, checkable condition ("Tests are deterministic and meaningful") rather than a principle to keep in mind ("write good tests").

### Layered, Not Redundant

`code-review.md` covers the diff itself; `pull-request.md` covers the PR as a delivery unit (scope, risk, docs); `production-readiness.md` and `release.md` cover operational and rollout concerns. Use the narrowest checklist that fits the task rather than one all-purpose list.

### Risk-Aware

Every checklist has a section dedicated to security/data/compatibility risk — none of them treat correctness as the only concern.

---

## Typical Usage Order

```
code-review          (per diff, during review)
    ↓
pull-request         (before requesting merge)
    ↓
production-readiness (before first production rollout of a new service/feature)
    ↓
release               (every release going forward)
```

Pairs with [workflows/review-pr.md](../workflows/review-pr.md) and [workflows/release.md](../workflows/release.md), which describe the *procedure*; the checklists here are the *gate* applied at the end of that procedure.

---

## Contributing

When adding a new checklist:

* Group items into a small number of labeled sections (e.g., Correctness, Security, Operations).
* Phrase every item as a single verifiable condition using `- [ ]`.
* Avoid duplicating items already owned by another checklist in this folder — link to it instead.
* Keep it short enough to actually be used at the point of decision, not skimmed and ignored.
