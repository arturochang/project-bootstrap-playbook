# Migrate a Version 1 Project to Version 2

Version 2 changes the setup output contract. Apply it as a documentation and
workflow migration, not by rerunning the prompt over the repository.

## Before changing anything

1. Record `git status` and preserve unrelated work.
2. Read the project's current instruction, architecture, implementation, status,
   handoff, security, and deployment documents.
3. Inventory commands from the real manifest. Do not copy command names from the
   new prompt unless they are implemented.
4. Run the existing canonical gate and record its baseline result.

## Required changes

1. Add `docs/setup-provenance.md` with the original prompt source if known,
   `version: 1.x`, the migration target `2.2.0`, setup mode, provider, runtime,
   package manager, environments, canonical gate, deployment command, status
   path, and handoff path. Use prose or a small table; do not invent a parser.
2. Classify the repository as new-project continuation, existing-project
   adoption, or assess-only maintenance. Record its current delivery state
   separately from its desired target.
3. Add a provider capability table to the architecture/product plan. Map only
   capabilities the application actually needs. Record consistency, cost/quota
   failure, and meaningful migration seams.
4. Ensure the current documentation covers security boundaries, deployment from
   a clean account/clone, operations, and a short active handoff. Combine small
   documents when that is clearer.
5. Split verification evidence into credential-free gate, external browser or
   integration lanes, human-only cases, and deployed public-route probes.
6. Make production probes safe: dedicated test identity/tenant, idempotent and
   reversible operations, cleanup evidence, and no customer-visible, destructive,
   externally messaged, or chargeable action by default.
7. Review CI handling of untrusted pull requests. Do not execute pull-request
   code through a privileged event or expose repository/cloud secrets.
8. Update agent delegation guidance so a smaller implementation model receives
   owned files, non-goals, invariants, numbered edits, exact tests, stop
   conditions, documentation changes, and a return contract.
9. Reconcile status, handoff, implementation plan, deployment truth, and README.
   Every completed claim needs current evidence.

## Do not change automatically

- Provider services solely to match version 2 examples.
- Existing Pages deployments during an unrelated migration.
- Runtime, package-manager, or dependency major versions.
- Database or Durable Object migrations.
- Authentication, protocol, cryptography, public claims, or production routing.
- Deployment authority or environment ownership.

Treat each as a separate decision and verified change when the project actually
needs it.

## Verification

Run the repository's existing gate, not an imagined version 2 command. Then run
applicable browser/integration lanes and inspect the generated/deployed artifact
where the project already supports them. Record what remains human-only.

The migration is complete when current documents agree, the existing gate is
green, no project-specific decision was silently replaced, and the next task is
clear to a new session.
