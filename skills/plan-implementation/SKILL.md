---
name: plan-implementation
domain: intentdriven
description: Use when a confirmed spec, domain context, ADRs, and optional UI decision must be translated into a technical implementation plan against the current repository.
depends-on: []
chains-to: null
suggests: ["detect-drift", "implement-feature"]
---

# Plan Implementation

Cross from the desired product outcome through current repository reality into one approved, change-safe implementation route.

## Boundary

- MAY propose technical changes and compare real alternatives.
- MUST NOT change business requirements.
- MUST NOT implement.
- MUST identify spec/code conflicts before implementation starts.
- MUST wait for human approval of consequential technical choices.

## Process

1. Read feature state: authority map, normative specification IDs, domain context, glossary, ADRs, selected UI prototype, constraints, and accepted intent.
2. State the desired outcome. Inspect the current state only far enough to define the gap, affected flow, blast radius, risks, and safe route. Reuse a clear Actual Result / Expected Result for a documented bug; do not create a current-state snapshot for a new feature without a proof need.
3. Inspect current code, schemas, APIs, tests, migrations, configuration, runtime evidence, and repository conventions.
4. Map every normative specification ID to planned code paths and planned evidence. Keep the feature specification free of implementation details.
5. Compare the recommendation with at least one serious alternative for each non-trivial decision. Do not invent alternatives for canonical or convention-set choices.
6. Always include a change-safe alternative for architecture, hot-path, migration, public-contract, or large blast-radius work. Ask whether fewer changed boundaries, callers, or breaking changes can reach the same outcome.
7. Mention ADHD exploration as an optional wider method when the decision is open-ended or expensive. Use it only when installed and its own gate passes, or when the user requests it.
8. Recommend one approach. State its tradeoff, confidence, and the condition that would make the alternative better.
9. Apply the simplicity test: count new concepts, states, branches, abstractions, dependencies, configuration points, and integration boundaries. Require a current need for each. Line count is not a simplicity measure.
10. Prefer local change and low coupling. Consider the thinnest useful port, adapter, or dependency injection seam when it contains foreign details, protects domain logic, improves testing, or follows repository conventions. Assume no budget for framework or provider independence unless current evidence earns it.
11. Scan security/privacy, performance/scale, reliability, concurrency, compatibility/migration, operations/observability, accessibility, and data integrity. Show only relevant areas. Add one short exclusion line when a plausible high-risk area is intentionally excluded.
12. Derive the test and evidence method from repository rules, existing patterns, and changed behavior. Name the exact behavior and command or observation. Ask the human only when the choice changes delivery time, fidelity, production risk, or acceptance scope.
13. Decompose work into logical milestone commits. Each milestone must be buildable, verified, reviewable, and small enough to stop or resume safely. It need not be independently deployable.
14. Keep a bounded one-milestone plan in chat. Persist multi-milestone, architectural, migration, public-contract, or cross-repository plans at the project-selected authority.
15. Identify semantic conflicts using the selected authorities. Route semantic conflicts to `detect-drift` / `resolve-conflict`.
16. Present the plan in simple technical English and wait for explicit approval before implementation.
17. Update feature state to `plan-ready` only when no semantic conflict blocks work and the human approved consequential choices.

## Output contract

```text
Plan source:
Desired outcome:
Current state and gap:
Normative IDs covered:
Approaches and trade-offs:
Recommendation, confidence, and reverse condition:
Conceptual complexity:
Relevant quality risks:
Intentionally excluded high-risk area:
Affected modules and contracts:
Data/migration plan:
Milestone commits:
Verification methods and commands:
Risks and rollback:
Detected conflicts:
Human decisions needed:
Ready for approval: yes/no
```

## Verification gate

No plan is ready unless every normative specification ID has a planned implementation and evidence path, the recommendation has a real alternative when required, milestone commits are buildable and verifiable, known semantic conflicts are resolved or blocked, and the human approved consequential choices.
