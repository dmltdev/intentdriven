---
name: verify-feature
domain: intentdriven
description: Use when an implemented feature must be proven against stable specification IDs with tests, builds, runtime probes, browser evidence, CLI smoke checks, or other executable evidence.
depends-on: []
chains-to: null
suggests: ["review-change", "test-with-browser"]
---

# Verify Feature

Prove the implementation against the approved specification, not against the implementer's intent.

## Boundary

- MAY fail the implementation.
- MUST NOT weaken normative specification items.
- MUST NOT mark an item passing without executed or observed evidence.
- MUST NOT substitute code review for behavioral proof.

## Process

1. Read the normative specification items, central traceability map, implementation report, and repository test rules.
2. Select the narrowest commands or probes that prove changed behavior, contracts, boundaries, and invariants. Use type checks, lint, unit, integration, E2E, builds, migration checks, CLI/TUI smoke checks, or browser verification when they fit.
3. Execute the relevant checks.
4. Map every normative ID to status:
   - `pass` with implementation and evidence anchors;
   - `fail` with evidence;
   - `unverified` with exact reason;
   - `not-applicable` with justification;
   - `superseded` with the replacement ID or decision.
5. For UI, capture runtime and visual evidence for applicable default, error, loading, empty, responsive, and critical states.
6. Update the central traceability map and feature-state evidence.

## Output contract

```text
Quality gates:
Specification traceability:
Failed IDs:
Unverified IDs:
UI/runtime evidence:
Known limitations:
Ready for review-change: yes/no
```

## Verification gate

A specification item is PASS only when its evidence would fail if the item were broken. A command name, code location, or test existence without observed behavior is not evidence.
