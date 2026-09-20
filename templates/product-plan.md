# Product Plan

**Status:** Draft input

**Owner:** [name or role]

**Last updated:** [YYYY-MM-DD]

**Authority:**

- Product purpose, approved scope, constraints, and non-goals are authoritative.
- Architecture is provisional unless a decision is explicitly marked `Locked`.
- Open questions require resolution or a recorded assumption before affected
  implementation begins.
- When this plan conflicts with a more focused approved specification, surface
  the conflict instead of silently choosing one.

## 1. Product summary

**Product:** [one or two sentences]

**For:** [primary users]

**Problem:** [what is painful, risky, slow, or impossible today]

**Outcome:** [what becomes observably better]

**Central claim:** [the most important promise the product makes]

## 2. Users and usage environment

### Primary users

| User or role | Goal   | Current workaround | Important limitation |
| ------------ | ------ | ------------------ | -------------------- |
| [user]       | [goal] | [workaround]       | [limitation]         |

### Physical and network context

[Where and how the product is used: device posture, lighting, connectivity,
interruptions, accessibility needs, one-handed or hands-busy use, and whether
both people/screens can be present. Describe the environment, not only a device.]

## 3. Core workflows

Describe the smallest end-to-end jobs, including failure and recovery.

1. **[Workflow name]**
   - Trigger: [what starts it]
   - Happy path: [observable steps]
   - Failure/recovery: [what the user sees and can do]
   - Completion evidence: [how we know it worked]

## 4. Requirements

Use stable IDs so plans, tests, and reviews can refer to the same property.

### Functional

| ID  | Requirement         | Priority          | Acceptance evidence              |
| --- | ------------------- | ----------------- | -------------------------------- |
| F-1 | [testable behavior] | Must/Should/Could | [test, observation, or artifact] |

### Quality attributes

| ID  | Attribute     | Measurable target or explicit discipline         | Verification |
| --- | ------------- | ------------------------------------------------ | ------------ |
| Q-1 | Performance   | [for example, P95 target under named conditions] | [method]     |
| Q-2 | Availability  | [SLO or best-effort statement]                   | [method]     |
| Q-3 | Accessibility | [standard and applicable surfaces]               | [method]     |
| Q-4 | Privacy       | [data minimization/retention property]           | [method]     |

## 5. Scope

### In scope for the first useful release

- [capability]

### Explicitly out of scope

- [item and why it will not be proposed again]

### Shelved, not rejected

- [item, why it is deferred, and what must not be foreclosed]

## 6. Data and lifecycle

| Data class | Source/owner | Sensitivity      | Expected two-year scale | Retention/deletion | Export/restore |
| ---------- | ------------ | ---------------- | ----------------------- | ------------------ | -------------- |
| [data]     | [source]     | [classification] | [size/count/rate]       | [policy]           | [method]       |

State whether the product intentionally stores nothing. For durable data, cover
schema evolution, migration, backup, restore testing, deletion, and ownership.

## 7. Security, privacy, and abuse

- Actors and trust boundaries: [users, administrators, services, third parties]
- Authentication: [required mechanism or none]
- Authorization: [roles/resources/invariants]
- Secrets: [owners, storage, rotation, revocation]
- Forbidden logs/telemetry: [credentials, payloads, personal data, URLs, etc.]
- Abuse cases: [automation, enumeration, spam, resource exhaustion, fraud]
- Regulatory/residency constraints: [or none known]
- Security claims the public product may and may not make: [claims]

## 8. Proposed architecture

**Decision status:** Proposed / Approved / Locked

Describe components and data flow in plain language before naming services.

### Capability map

| Capability          | Requirement/invariant | Proposed primitive | Why      | Cost/quota failure | Migration seam     |
| ------------------- | --------------------- | ------------------ | -------- | ------------------ | ------------------ |
| Compute             | [need]                | [candidate]        | [reason] | [behavior]         | [boundary or none] |
| Static delivery     | [need]                | [candidate]        | [reason] | [behavior]         | [boundary or none] |
| Transactional state | [need]                | [candidate]        | [reason] | [behavior]         | [boundary or none] |
| Objects/files       | [need]                | [candidate]        | [reason] | [behavior]         | [boundary or none] |
| Coordination        | [need]                | [candidate]        | [reason] | [behavior]         | [boundary or none] |
| Async work          | [need]                | [candidate]        | [reason] | [behavior]         | [boundary or none] |
| Identity/secrets    | [need]                | [candidate]        | [reason] | [behavior]         | [boundary or none] |
| Observability       | [need]                | [candidate]        | [reason] | [behavior]         | [boundary or none] |
| DNS/TLS             | [need]                | [candidate]        | [reason] | [behavior]         | [boundary or none] |

### Provider posture

- Primary provider: [Cloudflare / AWS / another / undecided]
- Portability requirement: [provider-specific / isolate likely seams / active
  multi-cloud, with justification]
- Existing mandated services: [or none]
- Rejected alternatives: [option and reason]
- Volatile claims requiring live verification: [limits, pricing, availability]

## 9. Environments and operations

| Environment | Purpose                   | Data class        | Deployment authority | External dependencies |
| ----------- | ------------------------- | ----------------- | -------------------- | --------------------- |
| Local       | [purpose]                 | [synthetic/local] | [owner]              | [dependencies]        |
| Preview     | [purpose or not required] | [data]            | [owner]              | [dependencies]        |
| Production  | [purpose or not required] | [data]            | [owner]              | [dependencies]        |

- Availability posture: [best effort or target]
- Recovery point objective: [acceptable data loss]
- Recovery time objective: [acceptable recovery time]
- Observability and alert owner: [signals and owner]
- Deployment/rollback expectation: [process]
- Human-only verification: [devices, browsers, physical conditions]

## 10. Cost constraints

- Monthly target and hard ceiling: [amount or “not yet set”]
- Primary cost drivers: [requests, storage, egress, compute, third parties]
- Expected normal/peak/abusive usage: [estimates]
- Alerts and owner: [mechanism]
- Kill switch or degradation: [behavior]
- Idle resources with nonzero cost: [or none]

## 11. Dependencies and integrations

| Dependency/integration | Purpose   | Data shared | Failure behavior        | Exit strategy        |
| ---------------------- | --------- | ----------- | ----------------------- | -------------------- |
| [system]               | [purpose] | [data]      | [user-visible behavior] | [replacement/export] |

## 12. Risks and assumptions

| ID  | Type       | Statement   | Consequence if wrong | Resolution/evidence |
| --- | ---------- | ----------- | -------------------- | ------------------- |
| A-1 | Assumption | [statement] | [impact]             | [how to test]       |
| R-1 | Risk       | [statement] | [impact]             | [mitigation]        |

## 13. Open questions

| ID  | Question   | Recommended default | Consequence | Blocking? |
| --- | ---------- | ------------------- | ----------- | --------- |
| O-1 | [question] | [default]           | [impact]    | Yes/No    |

## 14. Success measures

- Product outcome: [observable measure]
- Reliability/quality: [measure]
- Adoption or usage: [measure, if relevant]
- Guardrail: [what must not worsen]

## 15. Delivery target

Choose one for the bootstrap session:

- [ ] Design-ready
- [ ] Local vertical slice
- [ ] Preview deployment
- [ ] Production deployment

Define completion in observable terms, including required artifacts, commands,
URLs, automated evidence, and human-only evidence.

## 16. Decision log

| Date   | Decision   | Status                   | Rejected alternatives | Revisit trigger |
| ------ | ---------- | ------------------------ | --------------------- | --------------- |
| [date] | [decision] | Proposed/Approved/Locked | [alternatives]        | [trigger]       |

## 17. Approval

- Product intent and scope owner: [name/date or pending]
- Security/privacy owner: [name/date, not applicable, or pending]
- Architecture owner: [name/date or pending]
- Delivery authority: [who may approve preview/production]
