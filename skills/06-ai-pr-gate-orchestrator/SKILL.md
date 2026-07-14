---
name: 06-ai-pr-gate-orchestrator
description: "Orchestrates multiple AI engineering reviews to evaluate pull requests. Aggregates architecture, code quality, security, performance, testing, and documentation analysis into a unified risk assessment and merge decision."
---

# 3. Skill Responsibility

It does NOT review code.

It:

* receives results from the other Skills
* normalizes findings
* calculates risk
* applies policy
* decides

---

# 4. Expected Inputs

Each Skill returns something structured.

Example:

## Code Reviewer

```json
{
  "category": "CODE_QUALITY",
  "findings": [
    {
      "severity": "HIGH",
      "title": "Missing transaction boundary",
      "impact": "Possible inconsistent database state"
    }
  ]
}
```

---

## Security

```json
{
  "category": "SECURITY",
  "findings": [
    {
      "severity": "CRITICAL",
      "title": "Broken authorization",
      "impact": "Unauthorized data access"
    }
  ]
}
```

---

## Performance

```json
{
  "category": "PERFORMANCE",
  "findings": []
}
```

---

# 5. Score Model (0-100)

I would avoid a simple average.

I would use **risk weighted scoring**.

---

## Weight per category

| Category                | Weight |
| ----------------------- | ---: |
| Security                |  30% |
| Correctness             |  25% |
| Database/Data Integrity |  20% |
| Performance             |  10% |
| Tests                   |  10% |
| Documentation           |   5% |

---

## Weight per severity

| Severity | Points |
| ---------- | -----: |
| CRITICAL   |    -40 |
| HIGH       |    -20 |
| MEDIUM     |     -8 |
| LOW        |     -2 |

---

Example:

```
Base Score: 100

Security:
- CRITICAL
-40

Code:
- HIGH
-20

Performance:
- MEDIUM
-8


Final Score:

100 - 40 -20 -8

= 32
```

Result:

```
BLOCK
```

---

# 6. Decision Policy

## 🟢 APPROVE

Conditions:

```
Score >= 85

AND

No CRITICAL findings

AND

No HIGH security findings
```

---

## 🟡 REQUEST CHANGES

```
60 <= Score < 85
```

Example:

* poor performance
* missing test
* technical debt

---

## 🔴 BLOCK

```
Score < 60

OR

Any CRITICAL finding

OR

Security HIGH+
```

---

# 7. Orchestrator Output

Example:

```json
{
  "decision": "REQUEST_CHANGES",

  "score": 72,

  "summary": {
    "critical": 0,
    "high": 2,
    "medium": 3,
    "low": 5
  },

  "blockingReasons": [
    "Missing integration test for payment flow",
    "Potential N+1 query"
  ]
}
```

---

# 8. Automatic Comment on the PR

The bot generates something like this:

---

## 🤖 AI Engineering Review

### Risk Score

```
72/100
```

### Decision

🟡 REQUEST CHANGES

---

## Findings

### 🔴 Security

No critical issues found.

### 🟠 Code Quality

**HIGH**

Transaction boundary may cause inconsistent persistence state.

Recommendation:

Move transaction boundary to service layer.

---

### 🟠 Performance

**MEDIUM**

Possible N+1 query when loading appointments.

Recommendation:

Review fetch strategy.

---

### 🟢 Tests

Coverage added:

* happy path ✅
* validation ✅
* persistence ⚠️

Missing:

* concurrent booking scenario

---

## Final Recommendation

Changes recommended before merge.

---

# 9. Ideal Pipeline

Example:

```
Developer
   |
   v
Open PR
   |
   v
CI Pipeline
   |
   +--> Unit Tests
   |
   +--> Integration Tests
   |
   +--> AI Feature Analysis
   |
   +--> AI Code Review
   |
   +--> AI Security Review
   |
   +--> AI Performance Review
   |
   +--> AI QA Review
   |
   +--> AI Documentation Review
   |
   v
AI PR Gate
   |
   +--> Approve
   |
   +--> Request Changes
   |
   +--> Block
```

---

# 10. Future Evolution (enterprise level)

Later you can add:

## Quality history

Database:

```
pull_request_review

id
repository
pr_number
score
decision
created_at
```

---

## Metrics

Dashboard:

```
Average PR Score

Security Trend

Most Common Findings

Regression Rate

AI Approval Rate
```

---

## Learning per project

Example:

Project A:

```
Always uses Kafka
Always uses PostgreSQL
Always uses Spring Events
```

The AI learns context.

---

# My Suggestion for Your Current Ecosystem

I would create this sequence:

```
1. feature-analysis-architect
        |
        v
2. senior-java-backend-engineer
        |
        v
3. senior-qa-automation-engineer
        |
        v
4. staff-backend-code-reviewer
        |
        +---- security
        |
        +---- performance
        |
        v
5. AI PR Gate Orchestrator
```
