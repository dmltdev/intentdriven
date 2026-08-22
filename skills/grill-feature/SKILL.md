---
name: grill-feature
domain: intentdriven
description: Use when a feature idea, bugfix intent, product request, or agentic SDLC task is fuzzy and needs assumptions challenged before a spec or implementation plan is written.
depends-on: []
chains-to: null
suggests: ["write-spec", "prototype-ui"]
---

# Grill Feature

Turn a fuzzy idea into spec-ready intent by challenging assumptions before the agent ecosystem starts producing code that confirms the wrong thing.

## Boundary

- MUST NOT implement.
- MUST NOT write final business specs, ADRs, or repo docs.
- MAY propose candidate acceptance criteria and unresolved questions.

## Process

1. Extract the user's stated goal, actors, affected workflows, current pain, and desired outcome.
2. Challenge assumptions: missing actors, permissions, states, edge cases, failure modes, rollback, data ownership, and non-goals.
3. Split compound requirements into testable statements.
4. Identify UI/product decisions that would be expensive to reverse.
5. Classify questions:
   - **Blocker** — implementation could build the wrong product.
   - **Design choice** — a human/product decision is needed before UI/API shape.
   - **Can infer** — local convention or code/docs can answer later.
6. Produce spec-ready intent, not a plan.

## Output contract

```text
Intent summary:
Actors:
Behavior candidates:
Acceptance criteria candidates:
Edge cases:
Non-goals:
Constraints:
UI/design decisions:
Unresolved blocker questions:
Recommended next skill: write-spec or prototype-ui
```

## Verification gate

Before completion, confirm every acceptance criterion candidate is observable and every blocker question is concrete. Do not ask vague "what should I do?" questions; provide options and consequences.
