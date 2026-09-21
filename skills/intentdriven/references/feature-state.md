# Feature State Contract

IntentDriven skills exchange a shared feature state. Keep it small, explicit, and source-linked. YAML is preferred when persisted; prose-only handoff is allowed only for tiny work.

```yaml
feature:
  id: APPT-142
  title: Reschedule appointment
  status: plan-ready
  owner: human

authority_map:
  business_intent:
    authority: product workspace
    location: "external://product-doc-or-ticket"
    write_policy: update there; repository references stable ID/link
    conflict_policy: human/domain-owner decision for semantic drift
  vocabulary:
    authority: repository glossary
    location: docs/glossary.md
    write_policy: update accepted terms with stable slugs
    conflict_policy: reject parallel terms unless accepted by domain owner
  domain_meaning:
    authority: repository domain docs
    location: docs/domain/appointments.md
    write_policy: update accepted rules and invariants with stable IDs
    conflict_policy: human/domain-owner decision for semantic drift
  context_relationships:
    authority: repository context map
    location: docs/context-map.md
    write_policy: update when context ownership or flow changes
    conflict_policy: human decides boundary ambiguity
  decisions:
    authority: repository ADRs
    location: docs/adr/
    write_policy: append new ADR; supersede rather than rewrite shipped decisions
    conflict_policy: newest accepted ADR wins for design rationale
  implementation_plan:
    authority: repository implementation plan
    location: docs/implementation/APPT-142.md
    write_policy: update while planning; record approved deviations
    conflict_policy: code reality can invalidate the route, but cannot change business intent
  actual_behavior:
    authority: code/schemas/config
    location: src/, schema/, config/
    write_policy: change through implementation commits
    conflict_policy: observed behavior is runtime truth, not automatically business truth
  behavioral_proof:
    authority: tests and runtime probes
    location: test suites, e2e specs, smoke commands
    write_policy: update with changed observable behavior
    conflict_policy: failing proof blocks acceptance unless explicitly waived

sources:
  spec: "external://product-doc-or-local-doc-defined-by-authority-map"
  domain:
    - docs/domain/appointments.md
  glossary: docs/glossary.md
  context_map: docs/context-map.md
  adrs:
    - docs/adr/0042-appointment-conflicts.md
  implementation_plan: docs/implementation/APPT-142.md

specification_items:
  - id: APPT-BR-01
    kind: business-rule
    statement: An appointment can move only to an available slot.
    source: "external://product-doc#availability"
    status: accepted
  - id: APPT-AC-01
    kind: acceptance-criterion
    statement: User can drag an appointment to an available slot.
    source: "external://product-doc#reschedule"
    status: accepted
  - id: APPT-AC-02
    kind: acceptance-criterion
    statement: Conflicts show an error and do not persist.
    source: "external://product-doc#conflicts"
    status: accepted

traceability:
  APPT-BR-01:
    implementation:
      - kind: symbol
        path: src/appointments/availability.ts#isSlotAvailable
    evidence:
      - kind: integration-test
        path: test/appointments/reschedule.test.ts
    status: verified
  APPT-AC-01:
    implementation:
      - kind: ui-flow
        path: apps/web/src/appointments/RescheduleDialog.tsx
    evidence:
      - kind: e2e-test
        path: apps/web/e2e/reschedule.spec.ts:42
    status: verified
  APPT-AC-02:
    implementation: []
    evidence: []
    status: unverified

milestones:
  - id: M1
    outcome: Enforce slot availability in the reschedule flow.
    commit: abc1234
    covered_ids: [APPT-BR-01, APPT-AC-01]
    verification:
      - command: pnpm test --filter appointments
        status: pass

conflicts:
  - id: CONFLICT-01
    type: semantic
    requires_human: true
    documented_intent: Cancelled appointments cannot be restored.
    implemented_behavior: POST /appointments/:id/restore restores cancelled appointments.
    evidence:
      - src/appointments/controller.ts:184
      - test/restore-appointment.e2e-spec.ts
    options:
      - Implementation is stale; remove restore behavior.
      - Business rule changed; update spec and docs.
      - Restore is an intentional exception; document exception and tests.

evidence_package:
  quality_gates:
    - command: pnpm test --filter appointments
      status: pass
      output: artifact://...
  ui_evidence:
    - path: .test-results/reschedule/desktop-default.png
      state: desktop default
  manual_acceptance_script:
    - Open /appointments/123.
    - Drag appointment to 14:30.
    - Confirm persisted state after refresh.
  mental_model:
    flow: Reschedule action -> availability rule -> persistence -> refreshed appointment.
    change_points:
      - src/appointments/availability.ts
      - apps/web/src/appointments/RescheduleDialog.tsx
```

## Status values

```text
discovery -> spec-ready -> knowledge-ready -> design-ready -> plan-ready -> implemented -> verified -> reviewed -> drift-cleared -> docs-reconciled -> acceptance-ready -> done
```

Use `blocked` only when the next action requires a human/domain-owner decision that tools cannot infer safely.

## Authority hierarchy

Authority is project-local and platform-neutral. `map-authority` discovers or recommends the mapping; it does not force one platform.

| Question | Typical authority |
|---|---|
| What should happen? | Product workspace, local feature docs, domain docs, or another project-defined business authority |
| What does this term mean? | Glossary / ubiquitous language authority |
| Which context owns this meaning? | Domain docs and context map |
| Why was it designed this way? | ADR or equivalent decision record |
| How will this version implement it? | Implementation plan / technical design |
| Where is each normative item represented? | Central traceability map |
| What actually happens now? | Code, schemas, config |
| Can behavior be demonstrated? | Tests / executable scenarios / runtime probes |
| What happens in production? | Runtime / telemetry |

Recommended minimum map: truth type -> authority -> location/link -> write policy -> conflict policy. Never resolve a semantic conflict by silently choosing one authority as globally dominant. Surface documented intent, implemented behavior, evidence, likely explanations, a recommendation, and the exact human decision needed.

## ID and status rules

- Normative IDs are feature-scoped and stable. Do not reuse or renumber them.
- Specification item status is `accepted`, `withdrawn`, or `superseded`.
- Traceability status is `planned`, `implemented`, `verified`, `fail`, `unverified`, `not-applicable`, or `superseded`.
- A superseded item records its replacement ID or accepted decision.
- Production code does not need a literal ID when the central map gives a clear implementation anchor.
