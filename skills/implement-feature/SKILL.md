---
name: implement-feature
domain: intentdriven
description: Use when an approved IntentDriven implementation plan should be executed end-to-end without reinterpreting the business spec or silently changing acceptance criteria.
depends-on: ["plan-implementation"]
chains-to: null
suggests: ["verify-feature"]
---

# Implement Feature

Execute the approved technical bridge. Boring, complete, and evidence-oriented.

## Boundary

- MAY change code, tests, migrations, schemas, and version-coupled technical docs named by the plan.
- MUST NOT reinterpret the spec.
- MUST NOT silently redesign architecture.
- MUST NOT weaken tests or acceptance criteria to make implementation easier.

## Process

1. Read the implementation plan and feature state.
2. Confirm no unresolved semantic conflict blocks work.
3. Implement the smallest complete slice set that satisfies the plan.
4. Add or update tests for new observable behavior and changed contracts.
5. If the repo reality invalidates the plan, stop and return a deviation packet:
   - plan assumption,
   - observed reality,
   - evidence,
   - options,
   - recommended next gate.
6. Remove obsolete code in a clean cutover when replacing behavior; do not leave aliases/shims unless the plan explicitly requires compatibility.
7. Report changed files and local evidence produced.

## Output contract

```text
Implemented slices:
Files changed:
Tests added/updated:
Migrations/schemas changed:
Plan deviations:
Acceptance criteria touched:
Self-verification run:
Ready for verify-feature: yes/no
```

## Verification gate

Do not claim completion if implementation diverged from plan or spec. A deviation is a valid stop; a silent reinterpretation is a failure.
