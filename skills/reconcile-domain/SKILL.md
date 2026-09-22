---
name: reconcile-domain
domain: intentdriven
description: Use when a feature introduces, renames, splits, or changes domain concepts, glossary terms, bounded contexts, or documented business rules before implementation planning.
depends-on: []
chains-to: null
suggests: ["record-decision", "plan-implementation"]
---

# Reconcile Domain

Keep ubiquitous language, domain context, and documented meaning aligned with accepted intent before technical planning.

## Boundary

- MUST NOT write production code.
- MUST NOT silently rewrite docs to match current code.
- MUST NOT create parallel vocabulary when a glossary term already exists.
- MUST NOT force tactical DDD patterns such as aggregates, repositories, CQRS, or domain events without evidence.

## DDD-lite contract

Use DDD first for language, context, and reasoning:

- identify the relevant bounded context and owner;
- give each term one definition within that context;
- reject accidental synonyms and overloaded terms;
- test unclear rules with concrete scenarios;
- keep domain terms aligned across specs, plans, code, tests, commits, and human discussion;
- state mappings when technical names cannot match domain terms.

Ports, adapters, dependency injection, entities, value objects, repositories, and domain events remain design choices. Repository conventions and current needs decide them.

## Process

1. Locate the domain/vocabulary authority from feature state or project convention.
2. If no authority exists, recommend the DDD local-docs fallback in `../intentdriven/references/docs-authority-profiles.md`. Existing project conventions still win.
3. Request optional `domain-modeling` support when it is installed and terms, relationships, context boundaries, or business rules need active exploration. Apply its method through the selected authority.
4. Compare proposed feature terms against existing vocabulary.
5. Detect collisions: same term with new meaning, synonym for an existing term, context ownership ambiguity, or rule conflict.
6. Test unclear relationships and rules with concrete scenarios before accepting them.
7. Give glossary terms stable slugs. Give normative domain rules and invariants stable context-scoped IDs. Do not renumber or reuse them.
8. Update glossary/domain docs only at the selected authority and only for accepted domain meaning, not technical implementation details.
9. Compare accepted language with code and tests. Record intentional technical-name mappings and surface naming drift.
10. If a conflict changes architecture, context boundaries, or an established rule, recommend `record-decision`.
11. Add changed docs, stable IDs, mappings, and unresolved conflicts to feature state.

## Output contract

```text
Domain sources read:
Bounded context and owner:
Terms reused:
Terms added or changed:
Rule/invariant IDs:
Concrete scenarios checked:
Technical-name mappings:
Context relationships:
Rule conflicts:
Docs updated:
Decision candidates:
Human decisions needed:
```

## Verification gate

Every new or changed term must have one owner, one definition, and one stable slug in its context. Every normative domain rule or invariant must have a stable ID. Unresolved semantic conflicts stop planning.
