---
name: own-report
domain: intentdriven
description: Use when completed AI-written, AI-led, or AI-assisted engineering work needs a self-contained Markdown ownership report for async reading, PR discussion, debugging, future modification, or knowledge transfer.
depends-on: []
chains-to: null
suggests: ["own"]
user-invokable: true
---

# Own Report

Create a Markdown ownership report that lets an engineer reconstruct the completed work's mental model without depending on the original agent.

## Boundary

- MUST NOT be interactive. Use `own` for conversational walkthroughs.
- MUST NOT produce a narrated diff.
- MUST NOT review correctness. Use `review-change` for adversarial review.
- MUST NOT replace verification evidence. Use `verify-feature` and `prepare-acceptance` for proof.
- MUST NOT create permanent repo docs unless the user gives a path or the authority map says ownership reports belong there.
- MUST distinguish implementation fact, documented decision, architectural inference, and speculation.

## Ownership model

Before writing, inspect the actual work. Prefer source, diff, tests, specs, plans, ADRs, review notes, and verification evidence over agent summaries.

Analyze the relevant subset:

- intent and requirements;
- previous vs new behavior;
- architecture, responsibilities, and boundaries;
- control flow and entry points;
- state, data, schemas, persistence, caching, and config;
- consequential decisions and realistic alternatives;
- trade-offs, costs, and reconsideration conditions;
- enforced invariants and relied-upon assumptions;
- failure modes, fallback, retry, partial failure, and concurrency;
- blast radius across modules, APIs, users, data, jobs, infra, perf, security, and compatibility;
- observability and debugging paths;
- extension points and boundaries future work must preserve;
- intentionally unsupported behavior and unknowns.

Do not force irrelevant dimensions into the report.

## Adaptive depth

Scale by risk and conceptual complexity, not lines changed.

Small low-risk work should produce a small report. Consequential work in auth, persistence, migrations, money, concurrency, caching, public APIs, infra, rollout, external dependencies, or high-blast-radius areas deserves deeper treatment.

## Report rules

- Organize by concepts, decisions, flows, boundaries, and risks.
- Use files and symbols as navigation anchors.
- Explain why important responsibilities live where they do.
- Include realistic alternatives only when they could reasonably have been chosen.
- State when reasoning is inferred from the current architecture rather than documented.
- Omit sections that add no meaningful ownership value.

## Output contract

Use this structure as a flexible default:

```md
# Ownership Report - <task>

## Executive Mental Model

## Context and Intent

## Ownership Map

## Architecture

## Control Flow

## Meaningful Changes

## Decisions and Trade-offs

## Invariants and Assumptions

## State and Data

## Failure Modes

## Blast Radius

## Risk and Technical Debt

## Observability and Debugging

## Extension Guide

## Things to Know Before Touching This

## Unknowns
```

For each meaningful change, prefer:

```md
### <Conceptual change>

**What changed**

**Why**

**How**

**Consequences**

**Important code**
```

For each consequential decision, prefer:

```md
### <Decision>

**Chosen approach**

**Reasoning**

**Alternatives**

**Why not**

**Cost**

**Reconsider when**
```

## Verification gate

The report is complete only when a reader can explain the implementation to colleagues, trace important flows, identify key decisions and invariants, debug likely failures, estimate blast radius, and know where future extensions belong.
