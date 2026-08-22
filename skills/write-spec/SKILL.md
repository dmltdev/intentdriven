---
name: write-spec
domain: intentdriven
description: Use when clarified product intent must become or update a business feature spec with behavior, acceptance criteria, non-goals, constraints, and source links before technical planning.
depends-on: []
chains-to: null
suggests: ["reconcile-domain", "plan-implementation"]
---

# Write Spec

Create the business contract the rest of the workflow must prove against.

## Boundary

- MUST NOT infer current behavior from code without marking it as implementation evidence.
- MUST NOT include implementation details unless they are business constraints.
- MUST NOT duplicate a canonical business spec into repo docs for convenience, regardless of platform.

## Source rule

Use the authority map selected by `map-authority` or the project's existing local convention. The spec authority may be an external product system, local Markdown, an issue tracker, a wiki, or another project-defined source. If the authority is absent or conflicting, recommend a minimal authority map and ask for a human decision only when the boundary affects product meaning.

## Process

1. Read the clarified intent, feature-state authority map, and the selected business source.
2. Normalize the spec into discrete, testable behavior statements.
3. Capture business rules, invariants, actors, permissions, edge cases, failure behavior, and non-goals.
4. Assign stable acceptance criterion IDs (`AC-01`, `AC-02`, ...).
5. Link each criterion to source text, source location, or decision context.
6. Mark unresolved ambiguity explicitly; do not bury it in broad wording.
7. Update feature state with spec authority, source location, and acceptance criteria.

## Output contract

```text
Spec source:
Feature summary:
Business rules:
Acceptance criteria:
Non-goals:
Constraints:
Edge cases:
Open questions:
Next gate:
```

## Verification gate

The spec is ready only when each acceptance criterion is observable, falsifiable, and independent enough to map to evidence later.
