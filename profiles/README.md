# Provider Profiles

Provider profiles are dated decision aids used after the core prompt identifies
required capabilities. They contain volatile product guidance that should not be
embedded permanently in the provider-neutral workflow.

Available profiles:

- [`cloudflare.md`](cloudflare.md) — Workers application architecture, storage
  selection, bindings, testing, deployment, rollback, cost, and portability.

An AWS profile should be added only after the same capability questions have
been researched against current AWS primary documentation. Do not create a
service-name translation of the Cloudflare profile.

Every profile must:

- state when it was last verified;
- link primary sources;
- distinguish recommendations from requirements;
- omit or date volatile prices, quotas, and availability claims;
- name consistency, cost, failure, deployment, and migration consequences;
- recommend only products bought by a concrete requirement.
