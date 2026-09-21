# IntentDriven

Composable agent skills for **Intent-Driven Development (IDD)**: humans own product intent, ambiguous decisions, and acceptance; agents own planning, implementation, verification, review, evidence, and documentation reconciliation.

Core invariant:

> Implementation must not silently redefine intent.

The plugin turns a feature request into a gated chain:

```text
Intent -> Spec -> Domain Knowledge -> Decisions -> Implementation -> Evidence -> Human Acceptance -> Ownership
```
For clear intent and agent-led coding, use `collaborative-implementation`. The human approves consequential technical choices. The agent owns routine engineering, milestone commits, verification, and the concise mental-model handoff.

IntentDriven uses DDD as a language and context discipline. Specifications stay concise, assign stable IDs to normative items, and use one central map from each ID to implementation and evidence.


## Skills

| Group | Skills | Purpose |
|---|---|---|
| Intent | `intentdriven`, `map-authority`, `grill-feature`, `write-spec`, `prototype-ui` | Discover which local or external artifact owns each truth type, clarify product intent, write business contract, branch into UI prototypes when interaction choices matter. |
| Decisions / Bridge | `reconcile-domain`, `record-decision`, `plan-implementation` | Keep ubiquitous language, domain context, ADRs, and technical plans aligned with accepted intent. |
| Collaborative Delivery | `collaborative-implementation` | Compare real approaches, obtain one risk-based approval, implement autonomously through verified milestone commits, and pause only for consequential deviations. |
| Execution / Evidence | `implement-feature`, `verify-feature`, `review-change`, `prepare-acceptance` | Execute the approved plan, map stable specification IDs to evidence, review the result, and package acceptance evidence. |
| Consistency | `detect-drift`, `resolve-conflict`, `reconcile-docs` | Detect semantic or traceability drift, surface human decision packets, and update docs only after confirmed intent. |
| Human Ownership | `own`, `own-report`, `own-visual` | Build a mental model for explaining, defending, debugging, modifying, and extending completed AI-assisted work. |
| Plugin Operations | `intentdriven-install-skills` | Reinstall this local plugin into Pi, OMP, Claude Code, and Codex with separate evidence for each harness. |

## Install

### skills.sh

Install the whole skill pack:

```bash
npx skills add dmltdev/intentdriven
```

Install only the root workflow skill:

```bash
npx skills add dmltdev/intentdriven --skill intentdriven
```

Replace `intentdriven` with any skill from the table above to install a narrower phase skill.

### Claude Code

Install from GitHub as a Claude Code plugin marketplace:

```text
/plugin marketplace add dmltdev/intentdriven
/plugin install intentdriven@intentdriven
```

For local development, pass the path to your local clone:

```text
/plugin marketplace add /path/to/intentdriven
/plugin install intentdriven@intentdriven
```

### pi

Install from GitHub with pi's package installer:

```bash
pi install git:github.com/dmltdev/intentdriven
```

Install project-locally, writing the package entry to `.pi/settings.json`:

```bash
pi install -l git:github.com/dmltdev/intentdriven
```

Run a one-off pi session with the package loaded:

```bash
pi -e git:github.com/dmltdev/intentdriven
```

### omp

Install from GitHub as an omp plugin marketplace. See `https://omp.sh/docs/plugins` for omp's plugin marketplace workflow.

```bash
omp plugin marketplace add dmltdev/intentdriven
omp plugin install intentdriven@intentdriven
```

For local development, pass the path to your local clone:

```bash
omp plugin marketplace add /path/to/intentdriven
omp plugin install intentdriven@intentdriven --force
```

### Codex

Install from GitHub as a Codex plugin marketplace:

```bash
codex plugin marketplace add dmltdev/intentdriven --ref main
codex plugin add intentdriven@intentdriven
```

For local development, pass the path to your local clone:

```bash
codex plugin marketplace add /path/to/intentdriven
codex plugin add intentdriven@intentdriven
```

## Use

Invoke `/intentdriven` for the full lifecycle. Invoke `/collaborative-implementation` when accepted intent is clear and the agent should perform the coding after the human approves consequential technical choices. Invoke a narrower phase skill when entering a known phase.

Every completed implementation includes a concise mental-model handoff. Use `own`, `own-report`, or `own-visual` when deeper ownership transfer is useful.

The shared state and central traceability format are described in `skills/intentdriven/references/feature-state.md`.

## Boundary

- Platform-neutral by default. Linear, Jira, Confluence, Notion, local Markdown, ADRs, tests, schemas, and code can own different kinds of truth.
- Local project docs or agent instructions define each authority: truth type -> authority -> location/link -> write policy -> conflict policy.
- When domain or vocabulary authority is missing and local docs are viable, the plugin recommends a replaceable DDD-lite fallback with a glossary, domain context, and context map.
- Feature specifications stay separate from technical plans. Stable normative IDs connect the specification to implementation and evidence through one central traceability map.
- Drift between documented intent and implemented behavior is information. Agents classify and surface it; they do not silently choose a winner.
