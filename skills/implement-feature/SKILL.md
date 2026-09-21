---
name: implement-feature
domain: intentdriven
description: Use when an approved IntentDriven implementation plan should be executed end-to-end without reinterpreting the business spec or silently changing acceptance criteria.
depends-on: ["plan-implementation"]
chains-to: null
suggests: ["verify-feature"]
---

# Implement Feature

Execute the approved technical bridge through buildable, verified milestone commits. The agent owns routine engineering and pauses only for consequential deviations.

## Boundary

- MAY change code, tests, migrations, schemas, and version-coupled technical docs named by the plan.
- MUST NOT reinterpret the spec.
- MUST NOT silently redesign architecture.
- MUST NOT weaken tests or acceptance criteria to make implementation easier.
- MUST NOT ask the human to decide reversible local implementation details.

## Process

1. Read the approved implementation plan, feature state, normative specification IDs, domain context, glossary, and repository rules.
2. Confirm no unresolved semantic conflict blocks work.
3. Work in the repository's approved branch or isolated workspace. Preserve unrelated user changes.
4. Execute one planned milestone at a time. For each milestone:
   - implement one logical change;
   - run its focused checks;
   - inspect the diff for scope and risk;
   - remove accidental complexity without changing behavior;
   - review it against the approved plan and covered specification IDs;
   - commit it with the repository's message convention.
5. Keep every committed milestone buildable, verified, and reviewable. It need not be independently deployable. If incomplete work enters a shared release branch, use an approved exposure-control mechanism and record its removal condition.
6. Add or update tests for changed observable behavior, contracts, boundaries, and invariants. Follow repository test policy. Do not test implementation details or add tests only to increase test count.
7. If repository reality invalidates the plan or reveals a consequential choice, stop with a deviation packet:
   - plan assumption;
   - observed reality and evidence;
   - viable options and tradeoffs;
   - recommendation and reverse condition;
   - cost or risk of continuing.
8. For a rename, move, extraction, migration, public-contract cutover, caller migration, or compatibility layer, request `refactor-transaction` when available. Otherwise apply its minimum rules: inventory every reference, decide compatibility, migrate all callers, keep one canonical path, delete obsolete paths, and prove behavior.
9. Keep behavior changes and structural refactors in separate commits unless separation creates an invalid intermediate state.
10. Remove obsolete code in a clean cutover. Do not leave aliases, shims, re-exports, duplicate paths, or fallback names unless the approved plan owns their removal.
11. Run final end-to-end evidence after the last milestone.
12. Return a concise mental model: outcome, control/data flow, responsibility boundaries, decisions, invariants, failure paths, debugging entry points, and how to change or remove the feature.

## Output contract

```text
Implemented milestones:
Milestone commits:
Normative IDs implemented:
Files and contracts changed:
Tests/evidence added or updated:
Migrations/schemas changed:
Approved deviations:
Final verification:
Mental model:
Remaining risks:
How to change or remove:
Ready for verify-feature: yes/no
```

## Verification gate

Do not claim completion unless every milestone is committed and has observed verification, final evidence covers the approved specification IDs, obsolete paths are removed, and no unapproved deviation remains. A deviation is a valid stop; a silent reinterpretation is a failure.
