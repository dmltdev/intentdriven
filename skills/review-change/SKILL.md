---
name: review-change
domain: intentdriven
description: Use when a verified change needs adversarial review against the spec, ADRs, domain docs, diff, tests, security/performance risks, and requirement coverage.
depends-on: []
chains-to: null
suggests: ["detect-drift"]
---

# Review Change

Attempt to disprove correctness. Review receives requirements and diff, not the implementer's self-justifying reasoning.

## Boundary

- MAY reject the implementation.
- MUST NOT silently fix business ambiguity.
- MUST NOT accept weak tests because code looks reasonable.
- MUST NOT expand scope beyond the accepted plan except to flag risk.

## Process

1. Read normative specification items, central traceability, domain docs/glossary, ADRs, approved implementation plan, milestone commits, diff, and verification evidence.
2. Review coverage ID by ID. Check that each implementation anchor and evidence item proves the stated meaning.
3. Inspect for incorrect assumptions, architecture violations, missing edge cases, accidental scope expansion, security/privacy issues, performance hazards, migration/rollback risk, weak tests, and unnecessary complexity.
4. Classify findings:
   - **BLOCKER** — specification violation, broken behavior, unsafe change, missing required evidence.
   - **CONCERN** — should fix or consciously accept.
   - **NIT** — low-risk polish.
5. Require evidence anchors: normative IDs, file paths, symbols, test names, command output, or runtime observations.
6. Update feature state with blockers and concerns. Do not change accepted specification meaning.

## Output contract

```text
Verdict: pass/block
Specification coverage:
Blockers:
Concerns:
Test quality findings:
Security/performance findings:
Architecture/complexity findings:
Evidence anchors:
Ready for detect-drift: yes/no
```

## Verification gate

No PASS if any active normative specification ID lacks credible implementation and evidence anchors, or if any blocker remains unresolved.
