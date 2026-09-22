# IntentDriven

Composable agent skills for **Intent-Driven Development (IDD)**: humans own product intent, ambiguous decisions, and acceptance; agents own planning, implementation, verification, review, evidence, and documentation reconciliation.

Core invariant:

> Implementation must not silently redefine intent.

The plugin turns a feature request into a gated chain:

```text
Intent -> Spec -> Domain Knowledge -> Decisions -> Implementation -> Evidence -> Human Acceptance -> Ownership
```

## Skills

| Group | Skills | Purpose |
|---|---|---|
| Intent | `intentdriven`, `map-authority`, `grill-feature`, `write-spec`, `prototype-ui` | Discover which local or external artifact owns each truth type, clarify product intent, write business contract, branch into UI prototypes when interaction choices matter. |
| Decisions / Bridge | `reconcile-domain`, `record-decision`, `plan-implementation` | Keep vocabulary/domain/ADRs aligned and translate business intent into a technical plan. |
| Execution / Evidence | `implement-feature`, `verify-feature`, `review-change`, `prepare-acceptance` | Execute the approved plan, prove acceptance criteria, adversarially review, package evidence. |
| Consistency | `detect-drift`, `resolve-conflict`, `reconcile-docs` | Detect semantic divergence, surface human decision packets, update docs only after confirmed intent. |
| Human Ownership | `own`, `own-report`, `own-visual` | Transfer completed AI-assisted work into the engineer's mental model for explaining, defending, debugging, modifying, extending, and discussing trade-offs without depending on the agent. |
| Operations | `install-intentdriven` | Install or verify this local plugin across Pi, OMP, Claude Code, and Codex with per-target evidence. |

## Install

After changing skills or manifests in a local checkout, invoke `install-intentdriven` to validate aligned versions, install each available harness, and report source, version, and activation evidence.

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

Invoke `/intentdriven` for an end-to-end feature lifecycle, or invoke a narrower skill directly when entering a known phase. Use `own`, `own-report`, or `own-visual` after acceptance when the human needs to understand completed AI-assisted work well enough to maintain it.

The expected state artifact is described in `skills/intentdriven/references/feature-state.md`.

## Boundary

- Platform-agnostic by default. Linear, Jira, Confluence, Notion, local Markdown, ADRs, tests, schemas, and code are possible authorities for different truths.
- Local project docs or agent instructions should define the source-of-truth boundary: truth type -> authority -> location/link -> write policy -> conflict policy.
- The plugin recommends a minimum authority map when none exists, but does not enforce a file name, schema, docs platform, or product-management tool.
- Drift between documented intent and implemented behavior is information. Agents must classify and surface it; they must not silently choose a winner.
