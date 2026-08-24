---
name: intentdriven
domain: intentdriven
description: Use when the user invokes /intentdriven, asks for Intent-Driven Development, AI-native SDLC, agentic feature delivery, or wants agents to carry a feature from human intent through spec, implementation, verification, semantic-drift handling, and acceptance evidence.
depends-on: []
chains-to: null
suggests: ["map-authority", "grill-feature", "write-spec", "reconcile-domain", "record-decision", "prototype-ui", "plan-implementation", "implement-feature", "verify-feature", "review-change", "detect-drift", "resolve-conflict", "reconcile-docs", "prepare-acceptance", "own", "own-report", "own-visual"]
user-invokable: true
---

# IntentDriven

Orchestrate Intent-Driven Development: humans own **what**, **why**, ambiguous decisions, and acceptance; agents own the engineering cycle and proof.

## Core invariant

**Implementation must not silently redefine intent.** Drift between documented intent, tests, code, and runtime is information to classify and surface, not something the agent fixes by choosing a convenient source of truth.

Separate roles:

- `map-authority` decides where each kind of truth lives for this repository; it does not create product requirements.
- Skills that create intent (`grill-feature`, `write-spec`, `prototype-ui`) do not observe reality and rewrite it.
- Skills that observe reality (`verify-feature`, `review-change`, `detect-drift`) do not weaken or reinterpret acceptance criteria.
- Skills that surface conflicts (`detect-drift`, `resolve-conflict`) do not decide semantic business truth unless the decision is mechanical and evidence-backed.

## State artifact

Use the shared state shape in `references/feature-state.md`. If the project already has a state convention, adapt to it but preserve these fields: sources, acceptance criteria, conflicts, evidence, current status.

## Workflow

1. **Authority discovery** — run `map-authority` when the repo lacks an explicit source-of-truth boundary, the task crosses product/domain/repo knowledge, or an agent must know where to update intent. Use local conventions; do not assume Linear, Jira, Confluence, Notion, or repo docs are canonical.
2. **Discovery** — run `grill-feature` unless the user supplied a clear spec. Extract product intent, actors, states, permissions, edge cases, non-goals, acceptance criteria, and unresolved questions.
3. **Specification** — run `write-spec`. Write or reference the spec at the authority selected by `map-authority`; do not duplicate canonical business specs into repo docs for agent convenience.
4. **Knowledge update** — run `reconcile-domain` for changed domain concepts or vocabulary at the selected domain/vocabulary authority. Run `record-decision` only for meaningful, hard-to-reverse tradeoffs.
5. **Design gate** — run `prototype-ui` when UI is uncertain, interaction-heavy, expensive to reverse, or carries a product decision. Human selects/refines one option before implementation.
6. **Technical bridge** — run `plan-implementation`. It crosses from business intent into repo reality: modules, APIs, schema/migrations, tests, rollout, observability, and known conflicts.
7. **Implementation** — run `implement-feature` against the approved plan. If reality invalidates the plan, stop with a deviation packet instead of freelancing.
8. **Verification** — run `verify-feature`. Map every acceptance criterion to executable or observed evidence.
9. **Adversarial review** — run `review-change` with spec, ADRs, diff, and test evidence. Reviewer attempts to disprove correctness.
10. **Drift gate** — run `detect-drift`. Compare the authorities recorded by `map-authority`: business intent, domain docs, glossary, ADRs, tests, code, schemas, and runtime evidence.
11. **Conflict handling** — if non-trivial semantic drift exists, run `resolve-conflict` and stop at a human gate when intended behavior cannot be inferred safely.
12. **Docs reconciliation** — run `reconcile-docs` only for decisions confirmed as intentional and only at the selected authority. Do not rewrite docs merely because code exists.
13. **Acceptance package** — run `prepare-acceptance`. Provide AC status, commands, screenshots/states when UI exists, known limitations, and manual acceptance script.
14. **Ownership transfer** — optionally run `own`, `own-report`, or `own-visual` after acceptance when the human needs to explain, defend, debug, modify, or extend the completed AI-assisted work without relying on the original agent.

## Gates

| Transition | Required proof |
|---|---|
| Authority -> Discovery | Truth authorities are explicit, irrelevant to this change, or accepted as missing risk. |
| Discovery -> Spec | Intent and acceptance criteria are explicit, or unresolved questions are surfaced. |
| Spec -> Plan | Business authority and source locations are recorded in feature state. |
| Plan -> Implement | Affected modules, tests, risk areas, rollout, and known conflicts are explicit. |
| Implement -> Verify | Implementation reports changed files and tests/evidence added. |
| Verify -> Review | Relevant commands/probes ran; no claimed pass without output. |
| Review -> Drift | Blocking review findings resolved or explicitly escalated. |
| Drift -> Docs | No unresolved semantic conflict remains. |
| Docs -> Acceptance | Documentation changes reflect confirmed intent only. |
| Acceptance -> Done | Human acceptance evidence package is complete. |
| Acceptance -> Ownership | Human wants a working mental model of completed AI-assisted work, not only acceptance evidence. |

## Source-of-truth split

Use the question to choose authority. The answer comes from local project conventions, not this plugin:

- **What should the product mean?** Selected business/product/domain authority.
- **What does this term mean?** Selected vocabulary authority.
- **Why this design?** Selected decision authority.
- **How this version will implement it?** Implementation plan / technical design.
- **What actually happens now?** Code, schemas, config, tests, runtime.

When no boundary exists, recommend `map-authority` and a minimal local authority map. Do not enforce a format. The useful minimum is: truth type -> authority -> location/link -> write policy -> conflict policy.

## Output contract

Return one operational report:

```text
Feature:
State:
Sources:
Acceptance criteria status:
Implementation summary:
Verification evidence:
Review findings:
Drift/conflicts:
Docs reconciled:
UI evidence:
Manual acceptance script:
Ownership transfer:
Human decisions needed:
```
