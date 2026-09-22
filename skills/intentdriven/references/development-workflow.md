# IDD Development Workflow

This reference explains how Intent-Driven Development handles a feature, technical task, bugfix, or refactor. The parent `intentdriven` skill owns the required workflow and route selection. Use this document when explaining the lifecycle, choosing a route, or showing how the process scales.

## Core invariant

**Implementation must not silently redefine intent.**

The desired outcome comes first. The current repository shows actual behavior, constraints, and the safe implementation route. When documented intent and actual behavior disagree, classify and surface the conflict. Do not choose the convenient source as product truth.

## Ownership

### Human ownership

The human owns:

- the problem and desired outcome;
- user-visible behavior;
- business and domain meaning;
- consequential choices;
- acceptance of the result.

A choice is consequential when it changes architecture, public contracts, persisted data, security, rollout, user-visible behavior, or substantial complexity.

### Agent ownership

The agent owns:

- repository investigation;
- reversible technical choices;
- implementation and focused refactoring;
- test and verification mechanics;
- milestone commits;
- review and drift evidence;
- documentation reconciliation;
- the concise mental-model handoff.

The agent asks for a human decision only when tools and project authorities cannot resolve a consequential choice safely.

## Route selection

Select the lightest route that preserves explicit intent and sufficient proof.

| Route | Use when | Intent artifact | Delivery shape |
|---|---|---|---|
| Small-work | One bounded, local, reversible milestone with clear behavior and low risk | Embedded intent contract in the plan | Plan, implement, verify, commit, hand off |
| Collaborative | Accepted intent is clear, but implementation has non-trivial approaches or consequential choices | Existing or concise specification | Compare routes, approve once, deliver verified milestones |
| Full IDD | Intent, domain meaning, UI, authority, or semantic consistency needs discovery | Durable specification and feature state | Full discovery through acceptance lifecycle |
| Conflict resolution | Code, tests, docs, or runtime disagree about intended behavior | Conflict packet linked to existing authorities | Human resolves meaning before reconciliation |

Route selection is an agent-owned reversible decision. Select the small-work route automatically when all eligibility conditions hold. Expand the route when new evidence crosses a boundary.

## Small-work route

### Eligibility

Use the small-work route only when all conditions hold:

- The desired outcome is explicit.
- The change fits one bounded milestone.
- The change is local and reversible.
- The relevant behavior has no unresolved ambiguity.
- The change does not introduce or change domain meaning.
- The change does not alter a public API or shared contract.
- The change does not require a schema or data migration.
- The change does not change security, permissions, or privacy behavior.
- The change does not require a risky rollout.
- The change does not require cross-repository coordination.
- The expected blast radius is small.

A small bugfix can change user-visible behavior when the intended behavior is already explicit. An unclear behavior choice disqualifies the shortcut.

### Embedded intent contract

The plan starts with this minimum contract:

```text
Outcome:
Preserved behavior:
Done when:
Plan:
Verification:
```

The contract is the small-work specification. It does not require a separate specification file or a separate specification phase.

Number multiple `Done when` items so verification can map evidence to each item. A single item can remain unnumbered. Keep the plan in chat unless the project requires another authority.

When the user already supplied these facts, reference their wording instead of rewriting it.

### Execution

1. Read the request, repository rules, affected code, and relevant tests or runtime evidence.
2. Confirm that every eligibility condition holds.
3. Write the embedded intent contract and technical plan together.
4. If the user requested implementation and no consequential choice remains, proceed without a second approval round.
5. Implement the change.
6. Exercise the changed behavior.
7. Run focused verification and map the evidence to `Done when`.
8. Inspect the diff and remove accidental complexity.
9. Commit the verified milestone when commits are authorized.
10. Return the outcome, evidence, remaining risk, and concise mental model.

### Expansion conditions

Expand to collaborative or full IDD when investigation reveals any of these conditions:

- more than one milestone;
- multiple viable user behaviors;
- architecture or large blast-radius impact;
- a public contract change;
- persisted-data or migration work;
- security, privacy, or permission impact;
- changed domain language or rules;
- cross-repository coordination;
- risky rollout or compatibility work;
- a conflict between documented intent and actual behavior;
- focused verification cannot prove the result.

State the evidence and the route change. Preserve completed investigation. Do not force the work through the shortcut.

## Collaborative route

Use `collaborative-implementation` when intent is accepted and the developer wants agent-led delivery after approving consequential choices.

1. Ground the change in accepted intent and repository reality.
2. Compare the recommendation with at least one serious alternative for each non-trivial decision.
3. Present one approval packet with the outcome, gap, approaches, recommendation, milestones, proof, and human decisions.
4. Implement buildable, verified, reviewable milestone commits.
5. Pause only when evidence invalidates the approved route or reveals a new consequential choice.
6. Complete verification and return a concise mental model.

The collaborative route can keep a bounded one-milestone plan in chat. Persist plans for multi-milestone, architectural, migration, public-contract, or cross-repository work.

## Full IDD route

### 1. Map authority

Identify where each truth type lives:

| Question | Typical authority |
|---|---|
| What should happen? | Product workspace, ticket, or local feature specification |
| What does this term mean? | Glossary or domain documentation |
| Why this design? | ADR or equivalent decision record |
| How will this version implement it? | Implementation plan |
| What happens now? | Code, schema, configuration, and runtime |
| Can the behavior be demonstrated? | Tests, executable scenarios, and runtime probes |

Code is authoritative for actual behavior. It is not automatically authoritative for intended behavior.

### 2. Discover intent

Clarify the actor, desired outcome, states, permissions, edge cases, constraints, non-goals, and acceptance meaning. Skip broad discovery when the user supplied a clear accepted specification.

### 3. Specify behavior

Write or reference a concise behavior contract at the selected authority. Assign stable feature-scoped IDs to normative items:

- `BR`, business rule;
- `INV`, invariant;
- `AC`, acceptance criterion;
- `CON`, constraint;
- `NG`, non-goal;
- `EDGE`, required edge case;
- `DEC`, accepted consequential decision.

The specification states what must be true. It does not prescribe implementation structure.

### 4. Reconcile domain knowledge

Update accepted terms, rules, invariants, context ownership, and relationships when the change affects domain meaning. Use the DDD-lite fallback when no domain authority exists: glossary, domain context documents, context map, and ADRs. Tactical DDD patterns remain optional.

### 5. Resolve product-significant UI

Prototype UI when interaction choices are uncertain, expensive to reverse, or product-significant. The human selects the behavior before implementation planning.

### 6. Plan against repository reality

Inspect the current system and produce:

- the current state and gap;
- affected modules and contracts;
- serious implementation alternatives;
- the simplest sufficient recommendation;
- reverse conditions;
- milestones and commits;
- verification for each milestone;
- relevant quality risks;
- rollout and observability when relevant.

Simplicity means the fewest necessary concepts, states, branches, abstractions, dependencies, configuration points, and integration boundaries. Line count is not a simplicity measure.

### 7. Approve consequential choices

The human approves choices that change behavior, architecture, contracts, data, security, rollout, or substantial complexity. The agent resolves local reversible choices without asking.

### 8. Implement milestones

Each milestone is one logical change. It must be buildable, verified, reviewable, and committed when commits are authorized. Keep behavior changes and structural refactors in separate commits unless separation creates an invalid intermediate state.

### 9. Verify normative items

Maintain a central mapping:

```text
Specification item -> implementation anchor -> evidence -> status
```

Evidence can include tests, API probes, browser interaction, screenshots, CLI output, migration probes, database state, logs, or telemetry. A passing suite does not prove requirements that have no mapped evidence.

### 10. Review and detect drift

Adversarial review tries to disprove correctness, requirement coverage, and relevant quality claims. Drift detection compares business intent, domain knowledge, ADRs, plans, tests, code, schemas, and runtime behavior.

### 11. Resolve semantic conflicts

When authorities disagree about intended meaning, return documented intent, actual behavior, evidence, viable explanations, a recommendation, and the exact human decision. Do not rewrite intent to match implementation.

### 12. Reconcile documentation

Update only confirmed intent, accepted decisions, approved deviations, traceability, and obsolete material. Keep the selected authority canonical.

### 13. Prepare acceptance

Return specification status, implementation summary, milestone commits, verification evidence, review findings, drift status, known limitations, UI evidence when relevant, a manual acceptance script, and a concise mental model.

### 14. Transfer ownership

The concise mental model is mandatory. Use `own`, `own-report`, or `own-visual` when the human needs a deeper model for explaining, defending, debugging, modifying, or extending the result.

## Work-type recipes

### Feature

Use discovery and specification to make user behavior explicit. Reconcile changed domain meaning. Prototype consequential UI. Plan and deliver the smallest observable milestones. Verify every accepted behavior.

### Bugfix

Record actual behavior, intended behavior, and a reliable reproduction. Identify the violated rule or invariant. Keep the reproduction as regression evidence when it protects a plausible future failure. Confirm the original symptom no longer occurs.

### Technical task

Define the structural outcome, preserved behavior, and completion evidence. Use the small-work route for one local reversible change. Expand when contracts, architecture, data, or multiple milestones appear.

### Refactor

Define preserved observable behavior, the desired structural result, and clean-cutover conditions. Separate structural commits from behavior changes when possible. Remove obsolete paths instead of leaving unapproved aliases or shims.

## Human interaction model

A normal implementation should feel like this:

1. The human states the problem and desired outcome.
2. The agent asks only about missing product meaning.
3. The agent selects the lightest safe route and investigates the repository.
4. The human approves only consequential choices.
5. The agent implements and verifies the work.
6. The agent interrupts only when evidence invalidates the route.
7. The human receives evidence, an acceptance path, and a concise mental model.
8. The human accepts the result or resolves a clearly stated semantic conflict.

Small work stays small. Consequential work leaves durable intent, decisions, traceability, evidence, and ownership.