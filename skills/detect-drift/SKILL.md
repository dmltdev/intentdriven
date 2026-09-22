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

1. Gather authorities from feature state or project convention: business/spec authority, normative IDs, glossary term slugs, domain rule IDs, context ownership, decision records, implementation plan, traceability, tests, schemas, code, verification evidence, and runtime/telemetry when relevant.
2. Compare by stable ID and question:
   - What should happen?
   - What does this term mean, and which context owns it?
   - Why was it designed this way?
   - How was it planned?
   - Where is it implemented?
   - What can be demonstrated?
   - What happens at runtime?
3. Classify divergence:
   - **none** — sources agree;
   - **mechanical** — stale link/name/path, safe to reconcile;
   - **technical-detail** — docs omit implementation detail, no product impact;
   - **semantic** — accepted meaning differs from implementation, tests, or runtime;
   - **traceability-gap** — an active normative ID lacks a clear implementation or evidence anchor;
   - **unknown** — insufficient evidence.
4. For semantic or unknown conflicts, produce evidence and route to `resolve-conflict`.
5. For a traceability gap, return the missing implementation or evidence obligation. Do not change the specification to match code.
6. For mechanical conflicts, list safe reconciliation actions.

## Output contract

```text
Sources compared:
Drift summary:
Mechanical drift:
Technical-detail drift:
Semantic conflicts:
Traceability gaps:
Unknowns:
Evidence:
Recommended next skill:
```

## Verification gate

No semantic conflict may be auto-resolved. If intended business behavior cannot be inferred safely, stop at a human decision gate.
