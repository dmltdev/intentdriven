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
    write_policy: update there; repo references stable ID/link
    conflict_policy: human/domain-owner decision for semantic drift
  vocabulary:
    authority: repo glossary
    location: docs/glossary.md
    write_policy: update in the implementation PR when terms change
    conflict_policy: reject parallel terms unless accepted by domain owner
  decisions:
    authority: repo ADRs
    location: docs/adr/
    write_policy: append new ADR; supersede rather than rewrite shipped decisions
    conflict_policy: newest accepted ADR wins for design rationale
  implementation_plan:
    authority: repo implementation plan
    location: docs/implementation/APPT-142.md
    write_policy: update while planning; preserve final plan if project convention keeps plans
    conflict_policy: code reality can invalidate plan, but cannot change business intent
  actual_behavior:
    authority: code/schemas/config
    location: src/, schema/, config/
    write_policy: change through implementation PR
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
  adrs:
    - docs/adr/0042-appointment-conflicts.md
  implementation_plan: docs/implementation/APPT-142.md

acceptance_criteria:
  - id: AC-01
    statement: User can drag an appointment to an available slot.
    status: pass
    evidence:
      - kind: e2e-test
        path: apps/web/e2e/reschedule.spec.ts:42
  - id: AC-02
    statement: Conflicts show an error and do not persist.
    status: unverified
    evidence: []

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
```

## Status values

```text
discovery -> spec-ready -> knowledge-ready -> design-ready -> plan-ready -> implemented -> verified -> reviewed -> drift-cleared -> docs-reconciled -> acceptance-ready -> done
```

Use `blocked` only when the next action requires a human/domain-owner decision that tools cannot infer safely.

## Authority hierarchy

Authority is project-local and platform-agnostic. `map-authority` discovers or recommends the mapping; it does not enforce a specific platform or file format.

| Question | Typical authority |
|---|---|
| What should happen? | Product workspace, local feature docs, domain docs, or another project-defined business authority |
| Why was it designed this way? | ADR or equivalent decision record |
| What does this term mean? | Glossary / ubiquitous language authority |
| How are we planning to implement it? | Implementation plan / technical design |
| What actually happens now? | Code, schemas, config |
| Can behavior be demonstrated? | Tests / executable scenarios / runtime probes |
| What happens in production? | Runtime / telemetry |

Recommended minimum map: truth type -> authority -> location/link -> write policy -> conflict policy. Never resolve a semantic conflict by silently choosing one authority as globally dominant. Surface documented intent, implemented behavior, evidence, likely explanations, a recommendation, and the exact human decision needed.
