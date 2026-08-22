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

1. Read feature state, drift report, conflict resolutions, review findings, and implementation report.
2. Confirm every documentation change is backed by accepted intent or explicit human decision.
3. Update only the selected authority from the feature-state map:
   - business/product spec at its configured authority,
   - vocabulary at the selected glossary/ubiquitous-language authority,
   - domain meaning/invariants at the selected domain authority,
   - design rationale in ADRs or equivalent decision records,
   - implementation plan for technical bridge history when retained.
4. Delete or replace stale local docs when they would create two authorities for one truth.
5. Update links in feature state.

## Output contract

```text
Confirmed decisions used:
Docs changed:
Docs intentionally unchanged:
Canonical sources referenced:
Deleted duplicate/stale docs:
Remaining drift:
Ready for prepare-acceptance: yes/no
```

## Verification gate

No docs reconciliation is complete while semantic conflicts remain unresolved or while two editable sources claim the same business truth.
