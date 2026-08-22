# IntentDriven

Composable agent skills for **Intent-Driven Development (IDD)**: humans own product intent, ambiguous decisions, and acceptance; agents own planning, implementation, verification, review, evidence, and documentation reconciliation.

Core invariant:

> Implementation must not silently redefine intent.

The plugin turns a feature request into a gated chain:

```text
Intent -> Spec -> Domain Knowledge -> Decisions -> Implementation -> Evidence -> Human Acceptance
```

## Skills

| Group | Skills | Purpose |
|---|---|---|
| Intent | `intentdriven`, `map-authority`, `grill-feature`, `write-spec`, `prototype-ui` | Discover which local or external artifact owns each truth type, clarify product intent, write business contract, branch into UI prototypes when interaction choices matter. |
| Decisions / Bridge | `reconcile-domain`, `record-decision`, `plan-implementation` | Keep vocabulary/domain/ADRs aligned and translate business intent into a technical plan. |
| Execution / Evidence | `implement-feature`, `verify-feature`, `review-change`, `prepare-acceptance` | Execute the approved plan, prove acceptance criteria, adversarially review, package evidence. |
| Consistency | `detect-drift`, `resolve-conflict`, `reconcile-docs` | Detect semantic divergence, surface human decision packets, update docs only after confirmed intent. |

## Install

### Individual skills with skills.sh

Install the whole skill pack:

```bash
npx skills add dmltdev/intentdriven
```

Install only one skill:

```bash
npx skills add dmltdev/intentdriven --skill intentdriven
npx skills add dmltdev/intentdriven --skill map-authority
npx skills add dmltdev/intentdriven --skill verify-feature
```

Replace the skill name with any skill from the table above.

### Local development with omp

From the parent `plugins/` workspace:

```bash
omp plugin marketplace add ./intentdriven
omp plugin install intentdriven@intentdriven-dev --force
```

## Use

Invoke `/intentdriven` for an end-to-end feature lifecycle, or invoke a narrower skill directly when entering a known phase.

The expected state artifact is described in `skills/intentdriven/references/feature-state.md`.

## Boundary

- Platform-agnostic by default. Linear, Jira, Confluence, Notion, local Markdown, ADRs, tests, schemas, and code are possible authorities for different truths.
- Local project docs or agent instructions should define the source-of-truth boundary: truth type -> authority -> location/link -> write policy -> conflict policy.
- The plugin recommends a minimum authority map when none exists, but does not enforce a file name, schema, docs platform, or product-management tool.
- Drift between documented intent and implemented behavior is information. Agents must classify and surface it; they must not silently choose a winner.
