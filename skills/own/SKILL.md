---
name: own
domain: intentdriven
description: Use when completed AI-written, AI-led, or AI-assisted engineering work must be transferred into the engineer's working mental model through an interactive ownership walkthrough of decisions, control flow, risks, trade-offs, and extension points.
depends-on: []
chains-to: null
suggests: ["own-report", "own-visual"]
user-invokable: true
---

# Own

Transfer implementation ownership from agent to engineer. The engineer should be able to explain, defend, debug, modify, and extend the completed work without relying on the original agent.

## Boundary

- MUST NOT review whether the implementation is good. Use `review-change` for adversarial correctness review.
- MUST NOT replace verification or acceptance evidence. Use `verify-feature` and `prepare-acceptance` for proof.
- MUST NOT narrate the diff file-by-file.
- MUST NOT dump the full explanation at once unless the user explicitly asks.
- MUST NOT explain obvious syntax unless it has design or runtime consequences.
- MUST distinguish implementation fact, documented decision, architectural inference, and speculation.

## Ownership model

Before teaching, inspect the actual work. Prefer source, diff, tests, specs, plans, ADRs, review notes, and verification evidence over agent summaries.

Build the relevant subset:

- **Intent** — problem solved, previous behavior, desired behavior, constraints, non-goals.
- **Architecture** — components, responsibilities, boundaries, abstractions, integrations.
- **Control flow** — entry points, adapters, orchestration, domain logic, persistence, outputs, async behavior.
- **State and data** — sources of truth, transformations, schemas, precedence, caching, lifecycle.
- **Decisions and trade-offs** — chosen approach, realistic alternatives, costs, reconsideration conditions.
- **Invariants and assumptions** — what is enforced vs merely relied upon.
- **Failure modes** — triggers, propagation, fallback, retry, partial failure, concurrency, recognition.
- **Blast radius** — consumers, modules, APIs, users, data, jobs, infra, perf, security, compatibility.
- **Observability and debugging** — logs, metrics, traces, identifiers, state to inspect, investigation order.
- **Extension points** — where future behavior belongs and what boundaries should not be bypassed.

Do not force irrelevant dimensions into the walkthrough.

## Adaptive depth

Scale by risk and conceptual complexity, not lines changed.

Use more depth for security, auth, persistence, migrations, money, concurrency, caching, public APIs, infra, rollout, external dependencies, or high blast radius.

Use less depth for localized low-risk edits, routine generated UI, and obvious mechanical changes.

## Process

1. Inspect the work and surrounding architecture enough to teach from reality, not only from the diff.
2. Present a concise ownership map: target, complexity/risk, and topics.
3. Teach exactly one meaningful topic at a time.
4. Stop for questions after that topic.
5. Continue only when the user asks `next`, asks a follow-up, or asks to skip ahead.
6. For consequential topics, ask one realistic ownership check.
7. If the answer exposes a gap, correct the mental model and stay on the topic.
8. End with a short ownership recap.

## Topic rules

Organize by concepts, decisions, flows, boundaries, and risks. Files and symbols are evidence and navigation aids, not the structure.

Prefer:

```text
1. Resolution model
2. Override precedence
3. Request-time control flow
4. Failure/fallback behavior
5. Caching boundary
6. Blast radius
7. Extension points
```

Avoid:

```text
1. Changes to resolver.ts
2. Changes to service.ts
3. Changes to controller.ts
```

## Ownership checks

Use checks sparingly. Test application of understanding, not memorization.

Good checks:

- A colleague asks why this abstraction exists instead of calling the dependency directly. How would you answer?
- Production reports the wrong value for one tenant/user/request. Where do you start debugging?
- A new requirement adds another precedence layer. Where should it enter the architecture?
- What breaks if this invariant stops being true?

The user may always skip with `next`. Never hold progress hostage to a correct answer.

## Output contract

Initial orientation:

```text
Ownership target:
Complexity/risk:
Ownership map:
How to proceed:
```

Per topic:

```text
Topic N/M:
Mental model:
Important code:
Why this shape:
Trade-offs:
Invariants/risks:
How to debug/modify:
Question / ownership check:
```

Final recap:

```text
Ownership recap:
Core mental model:
Key decisions:
Key invariants:
Debug starting points:
Modification risks:
Unresolved unknowns:
```

## Verification gate

Complete only when the walkthrough has covered enough for the engineer to explain, defend, debug, modify, extend, and discuss the work with colleagues without relying on the original agent.
