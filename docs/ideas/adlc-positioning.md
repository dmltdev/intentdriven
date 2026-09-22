# Position IntentDriven within the Agent Development Lifecycle

## Source

- Cloudflare, [The Agent Development Lifecycle has arrived on Cloudflare](https://blog.cloudflare.com/agent-development-lifecycle/), published August 4, 2026.
- Discussion after defining the IntentDriven full, collaborative, and small-work routes.

Cloudflare presents the Agent Development Lifecycle (ADLC) as a model for software factories. An input such as a feature idea, customer bug, or production error can trigger agents that plan, build, test, deploy, observe, maintain, and retire software.

The article identifies seven properties required for safe autonomous software factories:

1. Programmatic operations.
2. Horizontal scale.
3. Reproducible environments and failures.
4. Real-time, push-based triggers.
5. Atomic changes.
6. Permissioned actions and escalation.
7. Self-improvement from experience.

## Problem

IntentDriven and ADLC have strong conceptual overlap. Both move agents beyond code generation, reduce human babysitting, require evidence, and reserve human time for judgment.

They are not equivalent. Treating them as synonyms would blur their strongest responsibilities:

- IntentDriven protects intent, domain meaning, consequential decisions, traceability, semantic consistency, acceptance, and human ownership.
- ADLC describes the operational system that lets agents execute the complete software lifecycle at scale, including deployment, observation, maintenance, and retirement.

IntentDriven currently reaches acceptance and ownership. It considers rollout and observability during planning, but it does not own a complete autonomous deploy-maintain-retire loop.

ADLC explains infrastructure and operational autonomy. The Cloudflare article does not define a detailed method for preserving product meaning or resolving semantic conflicts between specifications, code, tests, and runtime behavior.

A software factory can therefore be programmatic, reproducible, observable, and reversible while still building the wrong thing.

## Direction

Position IntentDriven as the intent, decision, evidence, and semantic-drift layer for an ADLC software factory.

Use this concise statement:

> IntentDriven preserves what software should mean while agents build it. It can govern a human-supervised repository workflow or operate as the intent and acceptance layer inside an autonomous Agent Development Lifecycle.

The complementary responsibilities are:

| Layer | Primary responsibility |
|---|---|
| IntentDriven | Define desired behavior, map authorities, preserve domain meaning, govern consequential decisions, trace requirements, detect semantic drift, prepare acceptance, and transfer ownership. |
| ADLC orchestration | Trigger and coordinate agents, workflows, containers, browsers, CI, previews, deployment, rollout, production observation, maintenance, and retirement. |
| Platform primitives | Provide artifacts, isolated environments, APIs, permissions, feature flags, telemetry, rollback, and durable workflow state. |
| Human authority | Supply product judgment, taste, semantic decisions, high-risk permission grants, and final accountability. |

IntentDriven should remain platform-neutral. Cloudflare can be one ADLC platform, not a required dependency or the definition of ADLC.

## Difference between IDD and ADLC

| Dimension | IntentDriven | Cloudflare ADLC direction |
|---|---|---|
| Center of gravity | Semantic correctness and human intent | Operational autonomy and software-factory scale |
| Primary input | Desired outcome, task, bugfix, specification, or semantic conflict | Feature idea, bug report, production event, or maintenance signal |
| Human role | Own intent, consequential choices, semantic conflicts, and acceptance | Focus on inspiration, taste, judgment, and permission escalation |
| Agent role | Investigate, plan, implement, verify, review, reconcile, and hand off | Drive the lifecycle from trigger through deployment, maintenance, and retirement |
| State | Sources, specification items, decisions, traceability, conflicts, evidence, and status | Durable workflow state, artifacts, traces, events, deployments, and operational signals |
| Safety | Authority boundaries, approval gates, evidence, adversarial review, and semantic drift detection | Isolation, reproducibility, atomic release units, permissions, previews, observability, and rollback |
| Current endpoint | Acceptance and ownership transfer | Deployment, observation, maintenance, improvement, and retirement |
| Distinctive strength | Prevents implementation from silently redefining intent | Makes full-lifecycle autonomous execution technically possible |

## Important design tension

IntentDriven currently allows a milestone to be buildable, verified, reviewable, and committed without being independently deployable.

Cloudflare argues that factory changes should be independently testable, releasable, observable, and reversible.

Keep the current IntentDriven rule for normal repository delivery. Add the stronger requirement only to an autonomous-factory route. Requiring every ordinary milestone to be independently deployable would add unnecessary rollout and isolation machinery to small work.

## How IntentDriven can absorb ADLC

Absorb ADLC as an optional operational extension, not as a rename or replacement of the IDD core.

### 1. Add an ADLC alignment reference

Document the seven factory properties and map each property to project capabilities, evidence, and gaps. Keep the assessment platform-neutral.

Example shape:

```text
Property:
Current capability:
Evidence:
Gap:
Required authority:
```

### 2. Extend feature state after acceptance

Add optional lifecycle states for projects where IntentDriven owns release and operations:

```text
acceptance-ready
-> release-ready
-> deployed
-> observing
-> stable
-> maintaining
-> retired
```

Do not require these states when the repository workflow ends at a PR or handoff.

### 3. Extend traceability into production

Evolve the evidence map when operational ownership exists:

```text
Specification item
-> implementation anchor
-> pre-release evidence
-> deployment
-> production signal
-> operational status
```

This makes production behavior evidence for the requirement without allowing runtime behavior to redefine business intent.

### 4. Add release authority and permissions

Map operational authority separately from product authority:

- who can create previews;
- who can deploy;
- who can enable a feature flag;
- who can increase rollout percentage;
- which permissions an agent can obtain automatically;
- which permissions require a human grant;
- which conditions require immediate rollback.

The authority map should record policy and escalation, not credentials.

### 5. Add rollout and rollback gates

For autonomous-factory work, require:

- an independently releasable delivery unit;
- preview or equivalent isolated validation;
- exposure control when risk requires it;
- production signals linked to acceptance meaning;
- automatic stop or rollback conditions;
- a removal condition for temporary flags and compatibility paths.

### 6. Add operational drift detection

Permit events to reopen an accepted feature when production evidence reveals a material gap:

- deployment failure;
- error-rate or latency regression;
- trace anomaly;
- support report;
- changed usage pattern;
- unmet business outcome;
- obsolete or unused behavior.

Classify the result before acting. Mechanical failures can route to autonomous repair. Semantic uncertainty returns to human authority.

### 7. Add learning receipts

Capture why autonomy stopped or failed:

- failed assumption;
- missing tool or permission;
- insufficient reproduction;
- verification gap;
- unclear authority;
- semantic conflict;
- rollout or observability gap;
- useful workflow change.

Promote a receipt into a test, gate, repository rule, domain document, or reusable skill only when the lesson is repeatable and belongs there.

### 8. Preserve route scaling

The ADLC extension must not make every change use factory-scale ceremony.

- Small-work route: embedded intent contract, focused proof, one local milestone.
- Collaborative route: accepted intent, one consequential approval, autonomous milestone delivery.
- Full IDD route: durable specification, domain and authority work, traceability, acceptance.
- ADLC operational route: full lifecycle through release, observation, maintenance, and retirement.

The agent selects the lightest route that covers the authority, risk, and operational ownership of the change.

## Non-goals

- Do not rename IntentDriven to ADLC.
- Do not claim that IntentDriven implements the complete ADLC today.
- Do not make Cloudflare a required runtime or vendor dependency.
- Do not require production permissions for repository-only work.
- Do not force every milestone to be independently deployable.
- Do not let production behavior silently override accepted intent.
- Do not turn the skill plugin into a CI/CD or orchestration platform.

## Desired outcome

IntentDriven keeps its distinct value: preserving intent and semantic correctness across agent-led delivery.

Projects can use IntentDriven alone for repository work, planning, implementation, review, and acceptance. Software factories can compose IntentDriven with an ADLC orchestrator and platform primitives for deployment and operations.

The combined model becomes:

```text
Trigger
-> IntentDriven intent and authority
-> specification and consequential decisions
-> ADLC orchestration
-> build, verify, preview, and deploy
-> production observation
-> IntentDriven drift classification
-> autonomous repair or human semantic decision
-> maintenance, learning, and retirement
```

## Open questions

- Should the operational extension be a new top-level skill, a set of lifecycle skills, or a reference used by the existing orchestrator?
- Where should human acceptance end and release authority begin?
- Which production signals can verify a specification item without turning telemetry into product authority?
- Which failures are mechanical enough for autonomous repair?
- What is the minimum permission model that remains platform-neutral?
- When should an operational failure update the workflow, and when should it remain incident-specific evidence?
- Should the autonomous-factory route require every delivery unit to be independently deployable, or allow approved multi-unit release groups?