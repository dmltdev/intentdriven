---
name: prototype-ui
domain: intentdriven
description: Use when UI is uncertain, interaction-heavy, product-significant, expensive to reverse, or the user asks for prototypes, UI variants, screens, flows, screenshots, or visual exploration before implementation.
depends-on: []
chains-to: null
suggests: ["write-spec", "plan-implementation"]
---

# Prototype UI

Generate materially different interaction models before implementation commits to a product shape.

## Boundary

- MUST NOT build production UI as the prototype deliverable.
- MUST NOT present color/font skins as separate variants when the interaction model is identical.
- MUST stop for human selection/refinement before implementation when the UI choice affects product behavior.

## Process

1. Read intent, acceptance criteria, users, constraints, and existing design conventions.
2. Decide if UI branch is required: uncertain, high-friction, multi-step, dense data, destructive action, permissions, or expensive reversal.
3. Generate 3-5 variants with different interaction models.
4. Cover important states: default, loading, empty, error, permission-denied, success, and mobile/responsive where relevant.
5. Compare variants by cognitive load, speed, error recovery, accessibility, implementation complexity, and fit to existing product language.
6. Ask the human to select/refine one variant.
7. Convert selected variant into UI acceptance criteria and evidence requirements.

## Output contract

```text
Prototype variants:
Comparison matrix:
Recommended variant:
States covered:
Accessibility notes:
Implementation implications:
UI acceptance criteria:
Human selection needed:
```

## Verification gate

Do not proceed to production implementation until the selected interaction model and its acceptance criteria are explicit.
