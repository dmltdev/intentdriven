---
name: record-decision
domain: intentdriven
description: Use when an IntentDriven feature involves a meaningful architectural, product-technical, persistence, API, rollout, or boundary decision with real alternatives and consequences.
depends-on: []
chains-to: null
suggests: ["plan-implementation"]
---

# Record Decision

Create or update decision evidence for non-obvious choices that future agents must not rediscover or silently reverse.

## Boundary

- MUST refuse ADRs for trivial implementation details.
- MUST NOT rewrite shipped ADR decisions; create a superseding ADR when history changes.
- MUST NOT decide business truth when `detect-drift` or `resolve-conflict` requires a human.

## ADR threshold

Record an ADR only when all are true:

1. Hard to reverse later.
2. Surprising without context.
3. Real alternatives were considered.

## Process

1. State the decision question.
2. List realistic options, including the boring/default option.
3. Compare tradeoffs: correctness, maintainability, cost, migration, rollback, operability, security/performance when relevant.
4. Choose one option and explain why now.
5. Record consequences, risks, and follow-up constraints.
6. Link the ADR or decision artifact in feature state.

## Output contract

```text
Decision question:
Options considered:
Decision:
Rationale:
Consequences:
Supersedes:
Artifact written:
```

## Verification gate

If the choice lacks real alternatives or future maintenance impact, do not write an ADR; record it as an implementation-plan note instead.
