---
name: own-visual
domain: intentdriven
description: Use when completed AI-written, AI-led, or AI-assisted engineering work needs a scan-friendly MDX ownership report with visual maps for architecture, control flow, decisions, risks, blast radius, debugging paths, and extension points.
depends-on: []
chains-to: null
suggests: ["own-report", "own"]
user-invokable: true
---

# Own Visual

Create an MDX ownership report optimized for fast mental-model reconstruction.

## Boundary

- MUST NOT generate prettier Markdown. Use `own-report` for dense linear Markdown.
- MUST NOT review correctness. Use `review-change` for adversarial review.
- MUST NOT replace verification evidence. Use `verify-feature` and `prepare-acceptance` for proof.
- MUST NOT invent arbitrary JSX components.
- MUST NOT turn prose into diagrams unless the concept has useful shape.
- MUST NOT prioritize visual density over correctness.
- MUST distinguish implementation fact, documented decision, architectural inference, and speculation.

## Component discipline

Use the project's real MDX ownership-report component library when available. Read its docs or examples before choosing props.

If component docs are unavailable, stay within this conservative vocabulary and use child content instead of guessing complex props:

```mdx
<OwnershipReport />
<Summary />
<OwnershipMap />
<ArchitectureDiagram />
<Flow />
<Component />
<Decision />
<Tradeoff />
<Invariant />
<Assumption />
<RiskMatrix />
<Risk />
<BlastRadius />
<FailureMode />
<DebugPath />
<ExtensionPoint />
<CodeReference />
<Callout />
<Section />
```

## Ownership model

Before writing, inspect the actual work. Prefer source, diff, tests, specs, plans, ADRs, review notes, and verification evidence over agent summaries.

Analyze the relevant subset:

- intent and requirements;
- architecture, responsibilities, and boundaries;
- control flow and entry points;
- state, data, schemas, persistence, caching, and config;
- consequential decisions and realistic alternatives;
- invariants and assumptions;
- failure modes and fallback behavior;
- blast radius and risk;
- observability and debugging paths;
- extension points and boundaries future work must preserve;
- intentionally unsupported behavior and unknowns.

## Visual priority

Primary visual weight:

- architecture;
- core flow;
- key decisions;
- dangerous invariants;
- high-impact risks.

Secondary visual weight:

- failure paths;
- debugging;
- extension points;
- configuration;
- state/data lifecycle.

Reference visual weight:

- file/symbol locations;
- minor assumptions;
- implementation details.

## Visualization rules

Visualize concepts with shape:

- control flow;
- component relationships;
- dependency boundaries;
- state ownership;
- precedence rules;
- lifecycle;
- before/after architecture;
- blast radius;
- failure propagation;
- decision alternatives.

Keep text for concepts without useful shape:

- nuanced trade-offs;
- reasoning;
- caveats;
- architectural intent;
- technical debt.

## Output contract

Use this structure as a flexible default:

```mdx
<OwnershipReport title="<task>">

<Summary>
Shortest useful mental model of the change.
</Summary>

<OwnershipMap topics={[
  "Core model",
  "Control flow",
  "Key decisions",
  "Failure behavior",
  "Blast radius",
  "Extension points"
]} />

## Architecture

<ArchitectureDiagram>
...
</ArchitectureDiagram>

<Callout type="important">
The most important architectural consequence.
</Callout>

## Core Flow

<Flow>
...
</Flow>

## Key Decisions

<Decision title="...">
...
</Decision>

## Invariants and Risks

<RiskMatrix>
  <Risk impact="high" likelihood="medium" area="...">
    ...
  </Risk>
</RiskMatrix>

## Debugging

<DebugPath>
...
</DebugPath>

## Extension Points

<ExtensionPoint title="...">
...
</ExtensionPoint>

## Code References

<CodeReference path="..." symbol="..." />

</OwnershipReport>
```

## Verification gate

The MDX report is complete only when a reader can scan it to reconstruct the core architecture, flow, decisions, risks, debugging strategy, and extension points faster than reading a linear Markdown report.
