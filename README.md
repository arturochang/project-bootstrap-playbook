# Project Bootstrap Playbook

An agent-friendly playbook for turning a product idea into a documented,
tested, secure, operable, and deployment-ready project.

This repository is not an application template and does not prescribe one cloud
or coding agent. Its primary artifact is a reusable setup prompt that helps a
human and a coding agent establish:

- product scope, constraints, non-goals, and delivery target;
- evidence-backed architecture and provider decisions;
- security, deployment, operations, and cost controls;
- repository instructions, status, handoff, and review records;
- executable development, verification, CI, deployment, and rollback paths;
- implementation packets that smaller models can follow safely.

## Use it

For the product-plan-first workflow:

1. Create `docs/product-plan.md` from
   [`templates/product-plan.md`](templates/product-plan.md), or bring an existing
   plan with equivalent content.
2. Commit the plan as a clean checkpoint.
3. Give your coding agent
   [`prompts/bootstrap-from-product-plan.md`](prompts/bootstrap-from-product-plan.md)
   and select a delivery target.
4. Answer its one consolidated clarification batch.
5. Review irreversible or high-cost decisions, then let it execute through the
   selected target.
6. Keep the generated status and handoff documents current as the project grows.

For a project without an existing plan, open
[`project-setup-prompt.md`](project-setup-prompt.md), replace the bracketed fields
in section 0, and give the complete prompt to your coding agent.

Reference an immutable release tag or commit when using the prompt from another
project. Record that source and version in the generated project's setup
provenance document.

## Repository contents

- [`project-setup-prompt.md`](project-setup-prompt.md) — the canonical,
  provider-neutral setup workflow.
- [`prompts/`](prompts/) — copy-ready entry prompts, including bootstrap from an
  existing product plan.
- [`templates/`](templates/) — product-plan and setup-provenance starting points.
- [`checklists/`](checklists/) — readiness checks that determine whether the
  agent can proceed, record assumptions, or must ask for clarification.
- [`profiles/`](profiles/) — dated provider decision guidance, currently
  including Cloudflare product
  selection, configuration, testing, cost, and deployment guidance.
- [`migrations/`](migrations/) — changes existing consumers must make when the
  prompt's output contract changes.
- [`examples/`](examples/) — filled project intakes for a small local-only tool
  and a production-oriented Cloudflare web application.

Profiles and examples inform the canonical prompt; they do not silently override
it. Recheck volatile provider facts against the linked primary documentation.

## What makes this different

Most project starters copy files. Most agent frameworks prescribe a coding
workflow. This playbook concentrates on the project foundation that must remain
true after the first generation step: decisions, invariants, verification,
deployment safety, operational ownership, and honest completion evidence.

Cloudflare is the most developed provider profile in the current prompt. The
core process remains provider-neutral, and AWS or another provider must be
selected from required capabilities rather than by translating service names
one-to-one.

## Versioning

The prompt uses semantic versions:

- Patch: clarification with no intended workflow change.
- Minor: backward-compatible capability or guidance.
- Major: a changed output contract, required artifact, or setup workflow.

See [`CHANGELOG.md`](CHANGELOG.md) before adopting a newer version in an
existing project.

## Contributing

Issues and pull requests should describe the failure mode the proposed rule
prevents. Prefer a focused, testable instruction over general advice. Volatile
cloud limits and product recommendations require a dated primary source.

## License

MIT. See [`LICENSE`](LICENSE).
