---
name: plan-implementation
domain: intentdriven
description: Use when a confirmed spec, domain context, ADRs, and optional UI decision must be translated into a technical implementation plan against the current repository.
depends-on: []
chains-to: null
suggests: ["detect-drift", "implement-feature"]
---

# Plan Implementation

Cross the boundary from business intent into repository reality without changing what the product is supposed to mean.

## Boundary

- MAY propose technical changes.
- MUST NOT change business requirements.
- MUST NOT implement.
- MUST identify spec/code conflicts before implementation starts.

## Process

1. Read feature state: authority map, spec source, acceptance criteria, domain/vocabulary sources, ADRs, selected UI prototype, constraints.
2. Inspect current code, schemas, APIs, tests, migrations, configuration, and relevant runtime conventions.
3. Map each acceptance criterion to planned code paths and planned evidence.
4. Identify affected modules, public surfaces, data model changes, migration strategy, events, permissions, observability, rollout, and rollback.
5. Detect conflicts between documented intent and current implementation using the selected authorities. If semantic, route to `detect-drift` / `resolve-conflict` before implementation.
6. Decompose tasks into safe implementation slices with verification commands.
7. Update feature state to `plan-ready` only when no unresolved semantic conflict blocks implementation and authority gaps are irrelevant or accepted.

## Output contract

```text
Plan source:
Affected modules:
Public/API/schema changes:
Data/migration plan:
Permission/security impact:
Telemetry/observability:
Acceptance-to-evidence map:
Implementation slices:
Verification commands:
Risks and rollback:
Detected conflicts:
Ready for implement-feature: yes/no
```

## Verification gate

No plan is ready unless every acceptance criterion has a planned evidence path and every known docs/code semantic conflict is either resolved or explicitly blocked for human decision.
