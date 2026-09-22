---
name: collaborative-implementation
domain: intentdriven
description: Use when a developer wants agent-led implementation with human approval of consequential technical decisions, especially for non-trivial repository changes with multiple viable approaches, risk-based gates, or autonomous milestone delivery.
depends-on: ["plan-implementation", "implement-feature"]
chains-to: null
suggests: ["reconcile-domain", "verify-feature", "own", "own-report"]
user-invokable: true
---

# Collaborative Implementation

Let the human own consequential decisions while the agent owns routine engineering, more than 99% of coding, verification, and milestone commits.

## Contract

- Define the desired outcome first. Inspect the current state to find the safe route, blast radius, and risks.
- Ask the human only when a choice changes user-visible behavior, architecture, public contracts, persisted data, security, rollout, or substantial complexity.
- Resolve repository facts with tools. The agent owns local names, helper structure, test mechanics, and other reversible choices.
- Use simple technical English in every human-facing message. Use short sentences, active voice, one meaning per term, and one main idea per sentence. Keep exact identifiers and technical facts.

## Workflow

1. **Ground the change.** Read accepted intent, specification IDs, domain context, glossary, repository rules, current code, tests, and runtime evidence when relevant.
2. **Design the route.** Run `plan-implementation`. Compare the recommendation with at least one serious alternative for every non-trivial decision. Include a change-safe option for architecture, hot paths, migrations, and large blast-radius work.
3. **Approve once.** Present the outcome, gap, approaches, recommendation, milestones, proof, and consequential decisions. Wait for approval before edits.
4. **Implement autonomously.** Run `implement-feature`. Complete buildable and verified milestones. For each milestone: implement, run focused checks, inspect the diff, remove accidental complexity, review against the plan, and commit.
5. **Pause only for deviation.** Stop when repository evidence invalidates the approved design or reveals a new consequential choice. Return the evidence, viable options, recommendation, and cost of continuing.
6. **Prove and transfer.** Run final verification. Return a concise mental model. Use `own-report` when deeper ownership transfer is useful.

## Design rules

**Simplicity:** choose the fewest concepts, states, branches, abstractions, dependencies, configuration points, and integration boundaries that meet current requirements and repository conventions. Line count is not a simplicity measure. Do not omit errors, validation, security, tests, or useful boundaries.

**Alternatives:** do not invent fake options for canonical or convention-set choices. Normal planning needs one serious alternative. Mention ADHD exploration as an optional wider method for open-ended or high-cost decisions. Use it only when its own gate passes or the user requests it.

**Changeability:** prefer local change and low coupling. A thin port, adapter, or dependency injection seam is valuable when it contains unstable or foreign details, protects domain logic, improves testing, or matches repository conventions. It is not mandatory for every dependency. Assume no delivery budget for framework or provider independence unless current evidence earns it.

**Relevant quality:** assess security, privacy, performance, scale, reliability, concurrency, compatibility, operations, accessibility, and data integrity. Show only relevant areas. Add one short exclusion line when a plausible high-risk area is intentionally excluded.

**Optional support:** request compatible pragmatic engineering, domain-modeling, or refactor-transaction capabilities when installed and their triggers match. The workflow must remain complete without them.

## Plan and milestone rules

- Keep a bounded one-milestone plan in chat.
- Persist the plan for multi-milestone, architectural, migration, public-contract, or cross-repository work at the project-selected authority.
- A milestone is one logical change. It must be buildable, verified, reviewable, and committed.
- A milestone does not need to be independently deployable. If incomplete work enters a shared release branch, hide it through an approved exposure-control mechanism with a removal condition.
- Keep behavior changes and structural refactors in separate commits unless separation creates an invalid intermediate state.

## Output contracts

Before implementation:

```text
Desired outcome:
Current state and gap:
Approaches and trade-offs:
Recommendation and reverse condition:
Relevant quality risks:
Milestones and commits:
Verification:
Human decisions needed:
Ready for approval: yes/no
```

After implementation:

```text
Outcome:
Mental model:
Milestone commits:
Verification evidence:
Approved deviations:
Remaining risks:
How to change or remove:
Ready for acceptance: yes/no
```
