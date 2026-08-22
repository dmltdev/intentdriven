---
name: detect-drift
domain: intentdriven
description: Use when documented intent, domain docs, ADRs, tests, code, schemas, or runtime behavior may diverge and semantic drift must be classified before docs reconciliation or acceptance.
depends-on: []
chains-to: null
suggests: ["resolve-conflict", "reconcile-docs"]
---

# Detect Drift

Find semantic divergence without deciding which truth wins.

## Boundary

- MAY identify contradictions.
- MUST NOT choose business truth for semantic conflicts.
- MUST NOT treat current code as automatically authoritative.
- MUST distinguish implementation-detail differences from business-behavior differences.

## Process

1. Gather authorities from feature state or project convention: business/spec authority, domain/vocabulary authority, decision records, implementation plan, tests, schemas, code, verification evidence, runtime/telemetry when relevant.
2. Compare by question:
   - What should happen?
   - Why was it designed this way?
   - What does this term mean?
   - How was it planned?
   - What actually happens?
   - What can be demonstrated?
3. Classify divergence:
   - **none** — sources agree.
   - **mechanical** — stale link/name/path, safe to reconcile.
   - **technical-detail** — docs omit implementation detail, no business impact.
   - **semantic** — expected business behavior differs from implementation/tests/runtime.
   - **unknown** — insufficient evidence.
4. For semantic/unknown conflicts, produce evidence and route to `resolve-conflict`.
5. For mechanical conflicts, list safe reconciliation actions.

## Output contract

```text
Sources compared:
Drift summary:
Mechanical drift:
Technical-detail drift:
Semantic conflicts:
Unknowns:
Evidence:
Recommended next skill:
```

## Verification gate

No semantic conflict may be auto-resolved. If intended business behavior cannot be inferred safely, stop at a human decision gate.
