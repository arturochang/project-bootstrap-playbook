# Bootstrap From an Existing Product Plan

Use this prompt after committing a draft `docs/product-plan.md` to a new or
existing repository. Replace the bracketed delivery target before sending it to
the coding agent.

```text
Bootstrap this repository using the existing docs/product-plan.md and Project
Bootstrap Playbook v2.2.0:

https://github.com/arturochang/project-bootstrap-playbook/tree/v2.2.0

Read these files from that release:

- project-setup-prompt.md
- checklists/product-plan-readiness.md
- templates/setup-provenance.md
- profiles/cloudflare.md if Cloudflare remains a candidate
- relevant examples or migration guidance only when applicable

If you cannot retrieve the pinned release, stop and ask me to attach it. Do not
silently substitute main, another version, or remembered instructions.

Treat docs/product-plan.md as authoritative for approved product purpose, scope,
constraints, and non-goals. Treat proposed architecture and provider choices as
hypotheses to verify unless the plan explicitly marks a decision as locked.

Before changing files:

1. Inspect repository instructions, git status, the real manifest, existing
   commands, runtime pins, deployment configuration, and current documentation.
   Do not assume a command, module, environment, or cloud resource exists.
2. Evaluate docs/product-plan.md with checklists/product-plan-readiness.md.
3. Extract everything the plan already answers. Do not ask me to repeat it.
4. Identify contradictions, unsafe assumptions, missing decisions, and volatile
   provider claims that require primary-source verification.
5. Ask one consolidated batch of only the questions whose answers materially
   change product scope, architecture, security/privacy, data lifecycle, cost,
   operations, or delivery. For every question, include your recommended default
   and one-sentence consequence. Decide routine implementation details yourself.
6. Do not write product code, create or modify remote resources, configure
   repository settings, handle real secrets, or deploy before the foundation
   decisions are resolved.

After I answer:

1. Follow project-setup-prompt.md in existing-plan mode through this delivery
   target: [design-ready / local vertical slice / preview deployment / production
   deployment].
2. Refine docs/product-plan.md in place. Preserve approved intent and history;
   distinguish requirements, verified decisions, assumptions, reversible
   preferences, locked decisions, and open questions.
3. Create docs/setup-provenance.md from the pinned template. Record release
   v2.2.0 and, if available, its resolved commit SHA. Never put secrets in it.
4. Use capability-first provider selection. If Cloudflare is selected, apply the
   pinned Cloudflare profile and reverify volatile facts against current primary
   documentation. Do not add AWS resources or speculative multi-cloud adapters.
5. Create the smallest complete documentation and repository foundation. Combine
   small documents when clearer; do not create empty ceremonial files.
6. Keep remote actions inside the selected delivery target. Local setup does not
   authorize DNS, cloud resources, GitHub settings, secrets, preview deployment,
   or production deployment. Ask before any required remote action not already
   explicit in the target and plan.
7. Use only commands that actually exist. Establish and run the credential-free
   gate before product complexity, then build one thin vertical slice when the
   selected target requires implementation.
8. Preserve unrelated work. Never overwrite a dirty file without reconciling its
   current contents.

At handoff, report:

- readiness verdict and assumptions used;
- files and operational surfaces created or changed;
- important accepted and rejected architecture decisions;
- commands that actually exist for setup, development, gate, preview, deployment,
  smoke verification, and rollback;
- verification evidence, skipped lanes, and human-only checks;
- remote actions taken, with identifiers, or an explicit statement that none
  were taken;
- open findings, risks, and blockers;
- the next three tasks in dependency order;
- deviations from Project Bootstrap Playbook v2.2.0.
```

For an existing mature repository, replace “bootstrap” with “adopt the playbook
without reorganizing unrelated code,” and review the relevant migration guide
before changing the documentation layout.
