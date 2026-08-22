# Docs Authority Profiles

`docs-source-of-truth` is useful as an **authority profile**, not as a standalone workflow competing with IntentDriven.

IntentDriven stays platform-agnostic: `map-authority` decides which sources own each truth type in the current repository. A repository may choose a DDD-shaped local-docs profile when that matches its product/team reality.

## DDD local-docs profile

Use this profile only when local docs intentionally own domain meaning.

```text
Vocabulary -> docs/glossary.md -> update when accepted terms change -> reject parallel terms
Domain meaning -> docs/domain/<context>.md -> update accepted invariants/contracts -> surface conflicts before writing
Context relationships -> docs/context-map.md -> update cross-context ownership/flow -> human decides boundary ambiguity
Decision rationale -> docs/adr/NNNN-*.md -> append/supersede ADRs -> never rewrite shipped decisions
Behavioral proof -> tests and schemas -> update with changed observable behavior -> failing proof blocks acceptance
Actual behavior -> code/schemas/config -> implementation PR -> runtime truth, not automatically business truth
```

## What to preserve from docs-source-of-truth

- Bounded contexts help locate vocabulary and domain ownership.
- Ubiquitous language prevents synonyms from leaking into code, tests, commits, and PRs.
- ADRs are the right place for hard-to-reverse, surprising tradeoffs.
- Domain docs should carry meaning, boundaries, and invariants; they should not restate obvious code or schemas.
- If docs and implementation disagree, surface the drift before editing either side.

## What not to preserve

- Do not assume repo docs are canonical in every repository.
- Do not force `docs/domain`, `docs/glossary.md`, or `docs/adr` if the project uses another authority.
- Do not reject external business specs by default.
- Do not make docs follow code automatically. Confirm whether the implementation changed intent or regressed from it.

## Skill mapping

- `map-authority` chooses whether this profile applies.
- `reconcile-domain` applies the vocabulary/domain/context parts.
- `record-decision` applies the ADR threshold and append-only decision policy.
- `detect-drift` enforces the docs/code conflict rule.
- `reconcile-docs` updates only the selected authority after confirmed intent.
