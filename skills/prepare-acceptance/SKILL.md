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
2. Produce a normative-ID status table from the central traceability map.
3. Include quality gates with commands and observed outcomes.
4. Include UI evidence when applicable: screenshots or browser observations for default, error/loading/empty, responsive, and critical states.
5. List known limitations, accepted risks, intentionally deferred non-goals, and superseded IDs.
6. Provide a short manual acceptance script with exact pages, commands, actions, and expected observations.
7. Include the concise mental model from implementation: outcome, main flow, responsibilities, decisions, invariants, failure paths, debugging entry points, and change/removal points.
8. State the requested human decision: accept, request changes, or choose among unresolved options.

## Output contract

```text
FEATURE COMPLETE / BLOCKED

Spec:
Specification traceability:
Quality gates:
Review:
Drift/conflicts:
Documentation:
UI/runtime evidence:
Known limitations:
Manual acceptance script:
Mental model:
Human decision requested:
```

## Verification gate

The package is acceptance-ready only when every normative specification ID has a pass/fail/unverified/not-applicable/superseded status with evidence or exact reason, the concise mental model is present, and every requested human action is concrete.
