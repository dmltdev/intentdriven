---
name: reconcile-docs
domain: intentdriven
description: Use when implementation, verification, review, and drift handling are complete and specs, domain docs, glossary, ADR links, or implementation plans must be updated only for confirmed intentional changes.
depends-on: []
chains-to: null
suggests: ["prepare-acceptance"]
---

# Reconcile Docs

Update documentation to match confirmed intent, not merely current code.

## Boundary

- MAY update docs after a confirmed decision.
- MUST NOT treat current code as automatically authoritative.
- MUST NOT paper over unresolved drift.
- MUST NOT duplicate canonical business specs into repo docs for convenience, regardless of platform.

## Process

1. Read feature state, stable specification IDs, domain term/rule IDs, central traceability, drift report, conflict resolutions, review findings, and implementation report.
2. Confirm every documentation change is backed by accepted intent or an explicit human decision.
3. Update only the selected authority from the feature-state map:
   - business/product spec at its configured authority;
   - vocabulary at the selected glossary/ubiquitous-language authority;
   - domain meaning, rules, and invariants at the selected domain authority;
   - context ownership at the selected context-map authority;
   - design rationale in ADRs or equivalent decision records;
   - implementation plan for technical bridge history when retained.
4. Preserve stable IDs. Mark changed meaning as superseded or withdrawn. Do not renumber or reuse IDs.
5. Update central traceability only for confirmed meaning and observed implementation/evidence.
6. Delete or replace stale local docs when they would create two authorities for one truth.
7. Update authority links in feature state.

## Output contract

```text
Confirmed decisions used:
Stable IDs changed:
Traceability changed:
Docs changed:
Docs intentionally unchanged:
Canonical sources referenced:
Deleted duplicate/stale docs:
Remaining drift:
Ready for prepare-acceptance: yes/no
```

## Verification gate

No docs reconciliation is complete while semantic conflicts remain unresolved or while two editable sources claim the same business truth.
