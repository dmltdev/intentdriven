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

1. Read spec, acceptance criteria, domain docs/glossary, ADRs, implementation plan, diff, and verification evidence.
2. Review requirement coverage criterion by criterion.
3. Inspect for incorrect assumptions, architecture violations, missing edge cases, accidental scope expansion, security/privacy issues, performance hazards, migration/rollback risk, and weak tests.
4. Classify findings:
   - **BLOCKER** — spec violation, broken behavior, unsafe change, missing required evidence.
   - **CONCERN** — should fix or consciously accept.
   - **NIT** — low-risk polish.
5. Require evidence anchors: file paths, test names, command output, or spec criteria.
6. Update feature state with blockers and concerns.

## Output contract

```text
Verdict: pass/block
Requirement coverage:
Blockers:
Concerns:
Test quality findings:
Security/performance findings:
Architecture findings:
Evidence anchors:
Ready for detect-drift: yes/no
```

## Verification gate

No PASS if any acceptance criterion lacks credible evidence or any blocker remains unresolved.
