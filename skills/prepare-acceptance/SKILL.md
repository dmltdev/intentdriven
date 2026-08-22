---
name: prepare-acceptance
domain: intentdriven
description: Use when an IntentDriven feature reaches final handoff and the human needs an evidence package with acceptance status, quality gates, screenshots or runtime proof, known risks, and a manual acceptance script.
depends-on: []
chains-to: null
suggests: []
---

# Prepare Acceptance

Make human acceptance fast and informed. The human should review evidence and product fit, not rediscover what to test.

## Boundary

- MUST NOT claim done without evidence.
- MUST NOT hide limitations, unverified criteria, or waived checks.
- MUST NOT ask the human to perform broad exploratory QA when a focused acceptance script can be provided.

## Process

1. Read final feature state, verification evidence, review verdict, drift report, conflict resolutions, docs reconciliation, and UI artifacts.
2. Produce a criterion-by-criterion status table.
3. Include quality gates with commands and observed outcomes.
4. Include UI evidence when applicable: screenshots or browser observations for default, error/loading/empty, responsive, and critical states.
5. List known limitations, accepted risks, and intentionally deferred non-goals.
6. Provide a short manual acceptance script with exact pages/commands/actions and expected observations.
7. State the requested human decision: accept, request changes, or choose among unresolved options.

## Output contract

```text
FEATURE COMPLETE / BLOCKED

Spec:
Acceptance criteria status:
Quality gates:
Review:
Drift/conflicts:
Documentation:
UI/runtime evidence:
Known limitations:
Manual acceptance script:
Human decision requested:
```

## Verification gate

The package is acceptance-ready only when every acceptance criterion is pass/fail/unverified with evidence or exact reason, and every requested human action is concrete.
