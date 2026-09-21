---
name: intentdriven
domain: intentdriven
description: Use when the user invokes /intentdriven, asks for Intent-Driven Development, AI-native SDLC, agentic feature delivery, or wants agents to carry a feature from human intent through spec, implementation, verification, semantic-drift handling, and acceptance evidence.
depends-on: []
chains-to: null
suggests: ["map-authority", "grill-feature", "write-spec", "reconcile-domain", "record-decision", "prototype-ui", "plan-implementation", "collaborative-implementation", "implement-feature", "verify-feature", "review-change", "detect-drift", "resolve-conflict", "reconcile-docs", "prepare-acceptance", "own", "own-report", "own-visual"]
user-invokable: true
---

# IntentDriven

Orchestrate Intent-Driven Development: humans own **what**, **why**, consequential decisions, and acceptance; agents own routine engineering, coding, proof, and milestone delivery.

## Core invariant

**Implementation must not silently redefine intent.** Drift between documented intent, tests, code, and runtime is information to classify and surface, not something the agent fixes by choosing a convenient source of truth.

Separate roles:

- `map-authority` decides where each kind of truth lives for this repository; it does not create product requirements.
- Skills that create intent (`grill-feature`, `write-spec`, `prototype-ui`) do not observe reality and rewrite it.
- Humans approve choices that change user-visible behavior, architecture, public contracts, persisted data, security, rollout, or substantial complexity.
- Agents resolve repository facts and own reversible local decisions, coding, verification, and milestone commits.
- Skills that observe reality (`verify-feature`, `review-change`, `detect-drift`) do not weaken or reinterpret acceptance criteria.
- Skills that surface conflicts (`detect-drift`, `resolve-conflict`) do not decide semantic business truth unless the decision is mechanical and evidence-backed.

## State artifact

Use the shared state shape in `references/feature-state.md`. If the project already has a state convention, adapt to it but preserve these fields: sources, stable specification IDs, traceability, conflicts, evidence, and current status.

## Human communication

Use simple technical English in human-facing output:

- Put the decision or result first.
- Use active voice, short sentences, and one main idea per sentence.
- Use one term for one meaning. Define an unfamiliar term once.
- Keep exact paths, symbols, commands, numbers, conditions, and uncertainty.
- Treat the human as a capable engineer. Simplify language, not technical meaning.

## Compact route

Run `collaborative-implementation` when accepted intent is clear and the developer wants joint technical decisions followed by agent-led implementation. It composes the planning and implementation phases. It does not remove specification, domain, traceability, verification, or acceptance obligations.

## Workflow

1. **Authority discovery** — run `map-authority` when the repo lacks an explicit source-of-truth boundary, the task crosses product/domain/repo knowledge, or an agent must know where to update intent. Use local conventions; do not assume Linear, Jira, Confluence, Notion, or repo docs are canonical.
2. **Discovery** — run `grill-feature` unless the user supplied a clear spec. Extract product intent, actors, states, permissions, edge cases, non-goals, acceptance criteria, and unresolved questions.
3. **Specification** — run `write-spec`. Write or reference the spec at the authority selected by `map-authority`; do not duplicate canonical business specs into repo docs for agent convenience. Give every normative item a stable feature-scoped ID.
4. **Knowledge update** — run `reconcile-domain` for changed domain concepts or vocabulary at the selected domain/vocabulary authority. Use the DDD-lite fallback when no domain authority exists. Request optional domain-modeling support when installed and deeper modeling is needed.
5. **Design gate** — run `prototype-ui` when UI is uncertain, interaction-heavy, expensive to reverse, or carries a product decision. Human selects/refines one option before implementation.
6. **Technical bridge** — run `plan-implementation`. It crosses from desired outcome through current repository reality into modules, APIs, schema/migrations, tests, rollout, observability, milestones, and known conflicts. It compares serious alternatives, recommends the simplest sufficient design, and waits for human approval.
7. **Implementation** — run `implement-feature` against the approved plan. The agent implements buildable, verified milestone commits. If reality invalidates the plan, it stops with a deviation packet instead of freelancing.
8. **Verification** — run `verify-feature`. Map every normative specification ID to executable or observed evidence.
9. **Adversarial review** — run `review-change` with spec, ADRs, diff, and test evidence. Reviewer attempts to disprove correctness.
10. **Drift gate** — run `detect-drift`. Compare the authorities recorded by `map-authority`: business intent, domain docs, glossary, ADRs, tests, code, schemas, and runtime evidence.
11. **Conflict handling** — if non-trivial semantic drift exists, run `resolve-conflict` and stop at a human gate when intended behavior cannot be inferred safely.
12. **Docs reconciliation** — run `reconcile-docs` only for decisions confirmed as intentional and only at the selected authority. Do not rewrite docs merely because code exists.
13. **Acceptance package** — run `prepare-acceptance`. Provide specification-ID status, commands, screenshots/states when UI exists, known limitations, a manual acceptance script, and a concise mental model.
14. **Ownership transfer** — optionally run `own`, `own-report`, or `own-visual` after acceptance when the human needs deeper understanding for explaining, defending, debugging, modifying, or extending the completed AI-assisted work.

## Gates

| Transition | Required proof |
|---|---|
| Authority -> Discovery | Truth authorities are explicit, irrelevant to this change, or accepted as missing risk. |
| Discovery -> Spec | Intent and acceptance meaning are explicit, or unresolved questions are surfaced. |
| Spec -> Plan | Business authority, domain authority, source locations, and stable normative IDs are recorded in feature state. |
| Plan -> Implement | Affected modules, alternatives, selected design, milestones, tests, risk areas, rollout, and known conflicts are explicit; the human approved consequential choices. |
| Implement -> Verify | Every milestone is buildable, verified, reviewed, and committed; deviations are approved or absent. |
| Verify -> Review | Relevant commands/probes ran; no claimed pass without output. |
| Review -> Drift | Blocking review findings resolved or explicitly escalated. |
| Drift -> Docs | No unresolved semantic conflict remains. |
| Docs -> Acceptance | Documentation changes reflect confirmed intent only. |
| Acceptance -> Done | The evidence package and concise mental model are complete. |
| Acceptance -> Ownership | Human wants a deeper working mental model, not only the mandatory concise handoff. |

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
Specification traceability:
Implementation summary:
Milestone commits:
Verification evidence:
Review findings:
Drift/conflicts:
Docs reconciled:
UI evidence:
Manual acceptance script:
Mental model:
Human decisions needed:
```
