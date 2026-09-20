# Product Plan Readiness Checklist

Use this checklist before scaffolding or writing product code. Its purpose is to
find decisions that materially change the project, not to force every product
into a heavyweight planning format.

## Verdicts

- **Ready:** The plan supports the selected delivery target without unresolved
  shape-changing decisions.
- **Ready with recorded assumptions:** Missing answers have safe, reversible
  defaults with consequences and revisit triggers.
- **Needs clarification:** At least one unanswered or contradictory decision
  could materially change scope, architecture, security/privacy, data lifecycle,
  cost, operations, or deployment authority.

## Product and users

- [ ] The product, intended users, problem, outcome, and central claim are clear.
- [ ] At least one end-to-end user workflow includes failure and recovery.
- [ ] Physical use and network conditions are described beyond device labels.
- [ ] The first useful release is bounded.
- [ ] Explicit non-goals prevent attractive but unwanted scope expansion.
- [ ] Shelved items say what future option must not be foreclosed.

## Requirements and completion

- [ ] Important behavior is observable or testable rather than aspirational.
- [ ] The cost of a wrong answer is stated for consequential behavior.
- [ ] The delivery target is one of design-ready, local vertical slice, preview,
      or production.
- [ ] Completion names expected artifacts, commands, evidence, and human checks.
- [ ] Success measures and guardrails are proportionate to the product.

## Data and security

- [ ] Data classes, owners, sensitivity, expected two-year scale, and lifecycle
      are described—or the no-storage invariant is explicit.
- [ ] Authentication and authorization requirements are clear or explicitly not
      required.
- [ ] Trust boundaries, secret ownership, forbidden logs/telemetry, and likely
      abuse cases are identified.
- [ ] Retention, deletion, export, backup, and restore expectations match the
      product's promises.
- [ ] Compliance and residency requirements are stated or recorded as unknown.
- [ ] Public security/privacy claims do not imply an audit or guarantee that has
      not occurred.

## Architecture and provider

- [ ] Architecture is labeled Proposed, Approved, or Locked.
- [ ] Required capabilities are described before provider products are selected.
- [ ] State choices match query shape, consistency, coordination, and lifecycle.
- [ ] Slow, unreliable, scheduled, or multi-step work has an execution model.
- [ ] Each selected provider product has a concrete requirement that buys it.
- [ ] Volatile availability, pricing, quota, or recommendation claims are marked
      for live primary-source verification.
- [ ] Meaningful migration commitments are recorded; speculative multi-cloud
      implementations are not mistaken for portability.

## Delivery and operations

- [ ] Local, preview/staging, and production environments are selected or marked
      not applicable.
- [ ] Deployment authority and prohibited remote actions are explicit.
- [ ] Availability, acceptable data loss, and recovery time are stated, even if
      all are best effort.
- [ ] Primary cost drivers, budget posture, alerts, kill switches, and useful
      degradation are identified.
- [ ] Observability has an owner and excludes sensitive content.
- [ ] Production verification can use safe test identities and reversible,
      non-customer-visible probes—or is explicitly human-only.
- [ ] Rollback distinguishes code/config rollback from state/schema recovery.

## Repository adoption

For an existing repository:

- [ ] Current instructions, git status, manifest, commands, runtime pins, entry
      points, deployment configuration, and generated artifacts were inspected.
- [ ] Unrelated dirty work has an owner and will be preserved.
- [ ] Existing decisions and conventions were discovered before proposing a new
      structure.
- [ ] The current gate was run or its blocker recorded before changing it.

## Question batch

Ask one consolidated batch only for failed items that change the project shape.
For every question provide:

1. the decision required;
2. the recommended default;
3. a one-sentence consequence;
4. whether work can proceed elsewhere before the answer;
5. the assumption that will be recorded if the user delegates the decision.

Do not ask the user to repeat facts already present in the plan. Decide naming,
formatting, file layout, and other reversible implementation details unless they
interact with a stated constraint.

## Hard stops

Do not proceed into affected implementation when any of these is unresolved:

- contradictory product purpose or mutually exclusive core workflows;
- unknown authority to handle sensitive or regulated data;
- authentication/authorization ambiguity that changes the trust boundary;
- no safe storage/lifecycle path for promised durable data;
- a delivery target requiring remote mutation without an authorized environment
  and owner;
- a locked architecture that conflicts with a verified platform limitation;
- a production probe that may be destructive, customer-visible, externally
  messaged, or chargeable without explicit approval.

The checklist is complete when it produces a verdict, a short assumption list,
and either one question batch or an explicit statement that no clarification is
needed.
