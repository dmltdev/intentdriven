---
name: map-authority
domain: intentdriven
description: Use when a repository lacks a clear source-of-truth boundary, an IntentDriven feature crosses product/domain/repo knowledge, or agents must know which local or external artifact owns each kind of truth.
depends-on: []
chains-to: null
suggests: ["grill-feature", "write-spec", "reconcile-domain"]
---

# Map Authority

Locate or define the project's truth boundary before agents create specs, rewrite docs, or interpret drift.

## Core invariant

The plugin is platform-agnostic. Linear, Jira, Confluence, Notion, local Markdown, ADRs, tests, schemas, and code are all possible authorities for different truths. The local project must say which authority owns which truth. If it does not, produce a lightweight recommendation and ask for a decision only when the missing boundary affects product meaning.

## Boundary

- MUST NOT assume Linear, Jira, Confluence, or repo docs are canonical by default.
- MUST NOT enforce a fixed file name, YAML schema, docs tool, or product-management platform.
- MUST NOT create business requirements.
- MAY recommend a minimal authority map in the project's existing docs or agent instructions.

## Process

1. Read existing local conventions before proposing anything: README, docs index, domain/glossary/ADR docs, product links, project agent instructions already in context, and feature state if present.
2. Identify authorities by truth type, not by platform:
   - should happen / business intent,
   - vocabulary / domain meaning,
   - why designed,
   - implementation plan,
   - actual behavior,
   - behavioral proof,
   - observed runtime behavior.
3. Classify each authority:
   - **explicit** — documented in local conventions,
   - **implicit** — strongly implied by repo layout or linked artifacts,
   - **missing** — no reliable authority found,
   - **conflicting** — two editable sources claim the same truth.
4. If missing/conflicting authority affects a non-trivial feature, ask for a precise human decision with recommended options.
5. If the project lacks an authority map, recommend adding one to an existing local source of instructions/docs. Do not invent a new format unless the user asks.
6. Record the selected authority map in feature state.

## Recommended minimum shape

Use prose, a table, YAML, frontmatter, or whatever the project already accepts. Minimum content:

```text
Truth type -> authority -> location/link -> write policy -> conflict policy
```

Example:

```text
Business intent -> Product workspace -> linked issue/doc -> update there -> human decides semantic drift
Vocabulary -> docs/glossary.md -> repo -> update in PR -> reject parallel terms
Architecture decisions -> docs/adr/ -> repo -> append ADR -> supersede, don't rewrite
Actual behavior -> code/schemas/config -> repo -> implementation PR -> tests prove behavior
```

Optional profile: if the repository uses DDD-shaped local docs, apply `references/docs-authority-profiles.md` as a recommendation, not a mandate.

## Output contract

```text
Authority sources inspected:
Authority map:
Explicit authorities:
Implicit authorities:
Missing authorities:
Conflicting authorities:
Recommended local documentation point:
Human decisions needed:
Feature-state update:
```

## Verification gate

Before proceeding to `write-spec`, the feature state must record at least the authority for business intent, vocabulary/domain meaning, decisions, actual behavior, and behavioral proof. Missing authority can remain only when it is irrelevant to the current change or explicitly accepted as a risk.
