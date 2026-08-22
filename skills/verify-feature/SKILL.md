---
name: verify-feature
domain: intentdriven
description: Use when an implemented feature must be proven against acceptance criteria with tests, builds, runtime probes, browser evidence, CLI smoke checks, or other executable evidence.
depends-on: []
chains-to: null
suggests: ["review-change", "test-with-browser"]
---

# Verify Feature

Prove the implementation against the spec, not against the implementer's intent.

## Boundary

- MAY fail the implementation.
- MUST NOT weaken acceptance criteria.
- MUST NOT mark criteria passing without executed or observed evidence.
- MUST NOT substitute code review for behavioral proof.

## Process

1. Read acceptance criteria and implementation report.
2. Select the narrowest commands/probes that prove changed contracts: typecheck, lint, unit, integration, E2E, build, migration checks, CLI/TUI smoke, browser verification for UI.
3. Execute the relevant checks.
4. Map every criterion to status:
   - `pass` with evidence,
   - `fail` with evidence,
   - `unverified` with exact reason,
   - `not-applicable` with justification.
5. For UI, capture visual evidence for default, error/loading/empty, responsive, and critical states when applicable.
6. Update feature state evidence.

## Output contract

```text
Quality gates:
Acceptance evidence map:
Failed criteria:
Unverified criteria:
UI/runtime evidence:
Known limitations:
Ready for review-change: yes/no
```

## Verification gate

A criterion is PASS only when the evidence would fail if the criterion were broken. Command names without observed output are not evidence.
