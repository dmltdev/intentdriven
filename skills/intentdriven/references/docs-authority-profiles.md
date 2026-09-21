# Docs Authority Profiles

IntentDriven stays platform-neutral. `map-authority` first respects explicit project authorities and conventions. When domain or vocabulary authority is missing and local repository docs are viable, recommend the DDD local-docs profile below as the default fallback.

The project can replace this profile. Record the chosen authority in feature state.

## DDD local-docs fallback

```text
Vocabulary -> docs/glossary.md -> stable term slugs -> update accepted terms -> reject parallel terms
Domain meaning -> docs/domain/<context>.md -> stable rule/invariant IDs -> update accepted meaning -> surface conflicts before writing
Context relationships -> docs/context-map.md -> create only for multiple relevant contexts -> human decides boundary ambiguity
Decision rationale -> docs/adr/NNNN-*.md -> create only for hard-to-reverse, surprising tradeoffs -> append/supersede
Feature behavior -> selected specification authority -> stable feature-scoped normative IDs -> human approves meaning
Implementation plan -> project-selected plan authority -> map normative IDs to code and proof -> code can invalidate the route, not intent
Behavioral proof -> tests, schemas, and runtime probes -> map evidence to normative IDs -> failing proof blocks acceptance
Actual behavior -> code/schemas/config -> implementation change -> runtime truth, not automatically business truth
```

## DDD language rules

- Bounded contexts locate vocabulary and domain ownership.
- Ubiquitous language prevents synonyms from leaking into specs, plans, code, tests, commits, and reports.
- Glossary entries use stable slugs. Normative domain rules and invariants use stable context-scoped IDs.
- Domain docs carry meaning, boundaries, relationships, and invariants. They do not restate obvious code or schemas.
- ADRs record only hard-to-reverse, surprising choices with real alternatives.
- If docs and implementation disagree, surface the drift before editing either side.
- Request optional `domain-modeling` support for active term, scenario, relationship, or context-boundary work when it is installed.

## Limits

- Do not replace an explicit project authority with this fallback.
- Do not force `docs/domain`, `docs/glossary.md`, or `docs/adr` when local docs are not viable.
- Do not reject external business specs by default.
- Do not make docs follow code automatically.
- Do not infer tactical DDD architecture from the language and context discipline.

## Skill mapping

- `map-authority` chooses whether this profile applies.
- `reconcile-domain` applies the vocabulary/domain/context parts.
- `record-decision` applies the ADR threshold and append-only decision policy.
- `detect-drift` enforces the docs/code conflict rule.
- `reconcile-docs` updates only the selected authority after confirmed intent.
