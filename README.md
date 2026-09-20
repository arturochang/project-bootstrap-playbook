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

1. Open [`project-setup-prompt.md`](project-setup-prompt.md).
2. Replace the bracketed fields in section 0.
3. Give the complete prompt to your coding agent in the target repository.
4. Review irreversible or high-cost decisions when the prompt asks you to.
5. Keep the generated status and handoff documents current as the project grows.

Reference an immutable release tag or commit when using the prompt from another
project. Record that source and version in the generated project's setup
provenance document.

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
