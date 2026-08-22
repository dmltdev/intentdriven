---
name: resolve-conflict
domain: intentdriven
description: Use when detect-drift reports semantic or unknown divergence and a human-readable decision packet is needed before changing code, tests, specs, domain docs, or ADRs.
depends-on: ["detect-drift"]
chains-to: null
suggests: ["reconcile-docs", "implement-feature"]
---

# Resolve Conflict

Turn semantic drift into a concrete decision packet. The human/domain owner decides when intent is ambiguous.

## Boundary

- MUST NOT silently choose docs over code or code over docs.
- MUST NOT ask abstractly "what should I do?"
- MAY recommend a resolution, but only with evidence and blast radius.

## Process

1. Restate the conflict in business terms.
2. Show documented intent, implemented behavior, tests/runtime behavior, and evidence anchors.
3. Explain likely interpretations:
   - implementation is stale/incorrect,
   - business requirement changed but docs were not updated,
   - intentional exception missing from spec,
   - test/verification artifact is wrong.
4. Estimate blast radius for each option: code, tests, docs, data, users, rollout.
5. Recommend one option when evidence supports it; otherwise state uncertainty.
6. Ask for a precise human decision with 2-4 options.
7. Update feature state with conflict status and chosen resolution when provided.

## Output contract

```text
Conflict ID:
Documented intent:
Implemented behavior:
Behavioral evidence:
Likely explanations:
Options:
Blast radius:
Recommendation:
Human decision needed:
```

## Verification gate

Do not proceed to implementation or docs reconciliation for semantic conflicts until the decision is explicit.
