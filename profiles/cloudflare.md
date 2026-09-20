# Cloudflare Provider Profile

**Status:** Active guidance

**Verified:** 2026-09-20 against the primary sources linked below

Use this profile after the core prompt has identified the application's required
capabilities. It is a decision aid, not permission to add every Cloudflare
product. Start with the smallest coherent set of services that satisfies current
requirements.

## Default posture

- Use Workers for request handling and Workers Static Assets for new static,
  SPA, and full-stack applications. Preserve an existing Pages deployment during
  unrelated maintenance; migration is its own change.
- Keep `wrangler.jsonc`, migrations, routes, domains, bindings, and compatibility
  settings in version control. Treat committed configuration as the source of
  truth instead of reproducing dashboard state by memory.
- Access Cloudflare resources through bindings when available. A binding avoids
  an application-held API credential and makes the dependency explicit.
- Pin Wrangler as a project development dependency. Use the project's pinned
  CLI, not a global installation.
- Put secret values in Workers secrets or Secrets Store. Commit only required
  secret names and a redacted local example.
- Verify current pricing, limits, availability, and plan requirements before
  committing to a service. Store the dated evidence in the generated project's
  architecture or deployment document, not in an always-loaded instruction file.

## Capability map

Choose only rows required by the product.

| Need                                      | Evaluate first          | Choose it when                                                                     | Do not use it as                                                       |
| ----------------------------------------- | ----------------------- | ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| Static site, SPA, or full-stack web app   | Workers + Static Assets | Static files and Worker logic should deploy as one unit                            | A reason to add server code to a static-only product                   |
| HTTP API or webhooks                      | Workers                 | The request fits the current CPU, duration, payload, and runtime constraints       | A home for unbounded or blocking work                                  |
| Lightweight relational records            | D1                      | SQL queries, managed migrations, and a read-heavy workload fit                     | Blob storage or a universal database default                           |
| Existing PostgreSQL/MySQL                 | Hyperdrive              | The existing database remains authoritative and connection acceleration is needed  | A reason to migrate data without a product requirement                 |
| Large files or object-addressed data      | R2                      | The product stores uploads, downloads, backups, or generated objects               | Searchable relational metadata; pair that with an appropriate database |
| Read-heavy distributed key/value data     | KV                      | Stale reads are acceptable and the access pattern is cache/config/session-like     | Strongly consistent invariants or rapid writes to one key              |
| Per-entity coordination or realtime state | Durable Objects         | A key needs one owner, strong coordination, WebSockets, alarms, or colocated state | Ordinary CRUD that needs none of those properties                      |
| Buffered background work                  | Queues                  | Producers and consumers should be decoupled and delivery/retry semantics fit       | A multi-step durable business process                                  |
| Durable multi-step orchestration          | Workflows               | Work must wait, retry, resume, or coordinate several steps                         | A single fast background action                                        |
| Scheduled trigger                         | Cron Triggers           | A recurring trigger is required                                                    | The work queue itself; hand off long or retryable work                 |
| Managed inference                         | Workers AI              | A supported model, schema, latency, and price meet the requirement                 | An assumed fit without model-specific evaluation                       |
| Custom semantic retrieval                 | Vectorize + Workers AI  | The project needs control of embeddings, indexing, and retrieval                   | A replacement for relational or transactional storage                  |
| Managed content search/answers            | AI Search               | Managed ingestion and retrieval fit better than a custom pipeline                  | A default dependency for any AI feature                                |
| Bot resistance                            | Turnstile               | A public form or action needs abuse friction and server-side verification          | Authentication or authorization                                        |
| Employee-only application access          | Access                  | Identity policies should sit in front of an internal application                   | In-application authorization for product users                         |
| Logs, traces, and request diagnostics     | Workers observability   | The project needs bounded operational evidence                                     | A place to emit credentials, payloads, filenames, or personal content  |

## Architecture questions

Before choosing a service, answer:

1. What consistency guarantee does the feature require?
2. What is the key, query, object, message, or coordination shape?
3. What operation drives cost under normal use and abuse?
4. What quota failure looks like to a user, and whether the application can
   degrade safely.
5. Whether local tests can use the real Workers runtime and representative
   bindings.
6. Whether the chosen service creates a material migration commitment. If so,
   record that decision rather than hiding it behind an artificial interface.

## Repository baseline

A deployable Worker project should normally include:

- a pinned runtime and package manager;
- a pinned project-local Wrangler dependency;
- `wrangler.jsonc` with its schema reference and current compatible date;
- generated binding types where the stack supports them;
- `.dev.vars.example` or equivalent with names and descriptions but no values;
- a gitignored local secret file;
- committed database and Durable Object migrations, where applicable;
- `dev`, `check`, `test`, `build`, `gate`, and canonical `deploy` scripts that
  actually exist;
- Workers-runtime unit tests and a production-build integration lane where the
  project's risk justifies it;
- a deployment document naming account-owned versus repository-owned resources;
- public-route smoke probes and a rollback procedure.

Do not scaffold unused bindings or placeholder resources. An empty database,
queue, or namespace is still an operational and cost-bearing decision.

## Deployment and rollback

- The canonical deploy command runs the credential-free gate before Wrangler.
- Authenticate and confirm the intended account/environment before the slow gate
  when account confusion is plausible.
- A dry run validates the candidate build and prints the target; it does not
  probe the currently live version and call that candidate verification.
- Record the Worker version/deployment identifier after publishing.
- Probe the real public entry route, important headers/assets, and one approved
  critical journey.
- Treat code rollback and state rollback separately. Workers versions do not
  version KV, R2, D1, or Durable Object data. A previous Worker version may be
  incompatible with a changed schema or missing binding.
- Use gradual deployment only with version-aware observability and a tested
  promotion/rollback decision. It is not a substitute for verification.

## Cost and failure posture

For every selected product, record in the generated project:

- the dated pricing and limits source;
- the unit that drives spend;
- expected normal, peak, and abusive usage;
- alerts and their owner;
- a hard or operational kill switch where unexpected spend is possible;
- useful degraded behavior after a limit is reached;
- resources that continue costing money while idle;
- teardown and retained-data behavior.

Cloudflare budget alerts are not automatically a product-level spend cap. Do not
describe an alert as enforcement unless the selected product and account setup
actually enforce it.

## Portability boundary

Keep product protocols and domain types free of Cloudflare service names. Natural
seams include configuration, object storage, message publication, email,
identity claims, and telemetry exporters. Do not build speculative alternative
adapters.

Durable Object coordination, Workers runtime constraints, KV consistency, D1
query behavior, and Queue/Workflow delivery semantics are architectural choices.
Document their migration consequences instead of pretending a renamed interface
makes them portable.

## Primary sources

- [Workers best practices](https://developers.cloudflare.com/workers/best-practices/workers-best-practices/)
- [Workers Static Assets](https://developers.cloudflare.com/workers/static-assets/)
- [Wrangler configuration](https://developers.cloudflare.com/workers/wrangler/configuration/)
- [Choose a storage product](https://developers.cloudflare.com/workers/platform/storage-options/)
- [Workers testing](https://developers.cloudflare.com/workers/testing/)
- [Workers secrets](https://developers.cloudflare.com/workers/configuration/secrets/)
- [Versions and deployments](https://developers.cloudflare.com/workers/versions-and-deployments/)
- [Rollbacks](https://developers.cloudflare.com/workers/versions-and-deployments/rollbacks/)
- [Cloudflare product directory](https://developers.cloudflare.com/directory/)
- [Cloudflare changelog](https://developers.cloudflare.com/changelog/)
