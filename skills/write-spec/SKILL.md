---
name: write-spec
domain: intentdriven
description: Use when clarified product intent must become or update a business feature spec with behavior, acceptance criteria, non-goals, constraints, and source links before technical planning.
depends-on: []
chains-to: null
suggests: ["reconcile-domain", "plan-implementation"]
---

# Write Spec

Create a concise business contract with stable IDs that the rest of the workflow can trace and prove.

## Boundary

- MUST NOT infer current behavior from code without marking it as implementation evidence.
- MUST NOT include implementation details unless they are product or business constraints.
- MUST NOT duplicate a canonical business spec into repo docs for convenience, regardless of platform.
- MUST NOT assign IDs to explanatory prose. IDs belong to normative items that downstream work must preserve or prove.

## Source rule

Use the authority map selected by `map-authority` or the project's existing local convention. The spec authority may be an external product system, local Markdown, an issue tracker, a wiki, or another project-defined source. If the authority is absent or conflicting, recommend a minimal authority map and ask for a human decision only when the boundary affects product meaning.

## Process

1. Read clarified intent, feature-state authority map, selected business source, domain context, and glossary.
2. Keep four concerns separate: domain meaning, feature behavior, technical implementation, and traceability.
3. Write the desired outcome first. Use current behavior only as evidence that helps define the gap, compatibility needs, or change route.
4. Normalize accepted intent into concise normative items:
   - `BR` business rule;
   - `INV` invariant;
   - `AC` observable acceptance criterion;
   - `CON` constraint;
   - `NG` non-goal;
   - `EDGE` required edge case;
   - `DEC` unresolved or resolved product decision.
5. Give every normative item a stable feature-scoped ID, such as `APPT-AC-01`. Never reuse or renumber an ID. Mark removed meaning as withdrawn or superseded.
6. Write one meaning per item. Make acceptance criteria observable and falsifiable. Keep explanatory prose short and unnumbered.
7. Use accepted domain terms. Link to the glossary and domain context instead of redefining them. Route new or changed terms to `reconcile-domain`.
8. Link every item to source text, source location, or accepted decision context.
9. Record unresolved ambiguity as a `DEC` item. Do not hide it in broad wording.
10. Update feature state with the spec authority, source location, normative items, and an empty traceability entry for each ID.

## Output contract

```text
Spec source:
Feature ID and objective:
Actors:
Domain sources:
Business rules and invariants:
Acceptance criteria:
Constraints:
Non-goals:
Required edge cases:
Open/resolved decisions:
Source links:
Traceability target:
Next gate:
```

## Verification gate

The spec is ready only when every normative item has one stable feature-scoped ID, one meaning, a source link, and a central traceability entry. Acceptance criteria must be observable and falsifiable. Technical implementation remains in the implementation plan.
