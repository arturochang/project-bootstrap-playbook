# Cloudflare Web Application Input

This example fills section 0 for a small production application. It expresses
requirements and risk without preselecting D1, KV, Durable Objects, or another
state product before the capability analysis.

```markdown
**Operating mode:** new project

**Product:** A mobile-first equipment checkout tracker for a small photography
studio. Staff can see availability, check an item out to a member, return it, and
resolve overdue equipment without maintaining spreadsheets.

**Target:** `gear.example.com` after a preview environment is verified.

**Primary infrastructure posture:** Cloudflare-first. Workers and Static Assets
are preferred if current requirements fit.

**Portability requirement:** Isolate natural migration seams for identity,
relational data export, email, and telemetry. Do not implement a second provider.

**Environments:** Local + preview + production. Only the owner deploys production;
preview uses separate state and test identities.

**Constraints:** Stay within a documented monthly budget; TypeScript strict;
mobile-first; accessible keyboard and screen-reader flows; timezone-aware dates;
no native app; no offline writes in the first release.

**Availability and recovery target:** Best-effort service with a four-hour
recovery target and at most one hour of acceptable data loss until real restore
evidence supports a stronger promise.

**Security, privacy, and compliance:** Staff authentication is required. Member
name, contact information, and checkout history are personal data. Never log
contact details, free text, session credentials, or complete request bodies.
Document retention and deletion before production data is accepted.

**Prior art / prior implementation:** A shared spreadsheet. Preserve its useful
fields, but do not reproduce unrestricted editing or ambiguous availability.

**What a wrong answer costs here:** Double-booking equipment disrupts paid work;
exposing member data is high impact; a short read-only outage is tolerable.

**Who else touches this repository:** Me, coding agents, and eventually one
additional maintainer.

**Where and how this is physically used:** Staff use phones in a busy studio,
often one-handed and sometimes on weak Wi-Fi while standing beside equipment.

**How much data will exist in two years:** Hundreds of items, thousands of
members, and tens of thousands of checkout events. All list surfaces need a
declared pagination/search strategy.

**Delivery target:** Preview deployment containing one vertical slice: sign in
as a test staff member, list equipment, perform an idempotent checkout, observe
the audit event without personal data in logs, return the item, and verify the
public route and security headers. Production deployment requires explicit
approval after preview evidence.

**Source of this prompt:**
`https://github.com/arturochang/project-bootstrap-playbook` at release `v2.1.0`.
```

Expected capability analysis:

- Workers + Static Assets for the application shell and API, if verified against
  current Cloudflare guidance.
- Relational, consistent checkout state; evaluate D1 and transaction design
  rather than choosing KV.
- No Durable Object unless a concrete coordination/contention requirement cannot
  be held by the selected database design.
- Separate preview and production bindings, secrets, identities, and data.
- A credential-free gate plus a production-build browser lane.
- Preview smoke probes may use the dedicated test identity. Production probes
  must not create member-visible messages or uncontrolled records.
- Cost model, backup/export, restore exercise, retention, and rollback must be
  resolved before production.
