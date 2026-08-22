---
name: reconcile-domain
domain: intentdriven
description: Use when a feature introduces, renames, splits, or changes domain concepts, glossary terms, bounded contexts, or documented business rules before implementation planning.
depends-on: []
chains-to: null
suggests: ["record-decision", "plan-implementation"]
---

# Reconcile Domain

Keep domain language and documented meaning aligned with accepted intent before technical planning.

## Boundary

- MUST NOT write production code.
- MUST NOT silently rewrite docs to match current code.
- MUST NOT create parallel vocabulary when a glossary term already exists.

## Process

1. Locate the domain/vocabulary authority from the feature-state authority map or project convention. It may be local docs, an external wiki, a glossary service, or another project-defined source.
2. If no authority exists, recommend a lightweight map entry rather than inventing a fixed format or filename.
3. Compare proposed feature terms against existing vocabulary.
4. Detect collisions: same term with new meaning, synonym for existing term, context ownership ambiguity, or rule conflict.
5. Update glossary/domain docs only at the selected authority and only for accepted domain meaning, not technical implementation details.
6. If a conflict changes architecture, context boundaries, or an established rule, recommend `record-decision`.
7. Add changed docs and unresolved conflicts to feature state.

When the selected authority is DDD-shaped local docs, use `../intentdriven/references/docs-authority-profiles.md` for the glossary/domain/context-map split. Treat it as a profile chosen by `map-authority`, not a universal rule.

## Output contract

```text
Domain sources read:
Terms reused:
Terms added or changed:
Context ownership:
Rule conflicts:
Docs updated:
Decision candidates:
Human decisions needed:
```

## Verification gate

Every new or changed term has one owner and one definition in the relevant context. Unresolved semantic conflicts stop planning.
