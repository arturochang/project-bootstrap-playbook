# Minimal Project Input

This example shows how to fill section 0 for a small local tool. It deliberately
selects no cloud provider, UI, CI deployment, database, or production operations.
The prompt should scale down rather than manufacture infrastructure.

```markdown
**Operating mode:** new project

**Product:** A command-line tool for renaming downloaded bank statements into a
consistent `YYYY-MM-bank-account.pdf` convention for one user.

**Target:** Local CLI; no domain.

**Primary infrastructure posture:** Provider undecided because no cloud
infrastructure is currently required.

**Portability requirement:** Provider-specific is acceptable if a future
requirement introduces hosting. Do not add a cloud abstraction now.

**Environments:** Local only.

**Constraints:** Runs on Windows and macOS; never uploads statement contents;
dry-run is the default; preserve originals; no telemetry.

**Availability and recovery target:** Best effort. Recovery is reinstalling from
source; originals remain untouched.

**Security, privacy, and compliance:** Filenames and statement contents are
financially sensitive. Never log contents or full paths. Process locally only.

**Prior art / prior implementation:** None.

**What a wrong answer costs here:** A wrong rename is recoverable; overwriting or
deleting an original is unacceptable.

**Who else touches this repository:** Me and coding agents.

**Where and how this is physically used:** On a personal laptop, usually from a
terminal, sometimes against hundreds of files at once.

**How much data will exist in two years:** A few thousand local files across
several directories.

**Delivery target:** Local vertical slice: scan one directory, show a deterministic
rename plan, handle collisions, and apply only after explicit confirmation, with
tests and packaged install instructions.

**Source of this prompt:**
`https://github.com/arturochang/project-bootstrap-playbook` at release `v2.1.0`.
```

Expected tailoring:

- No `docs/design-language.md` unless a UI is later added.
- Security and operations coverage may be combined with the product plan.
- The gate should test dry-run, collision handling, path portability, and the
  invariant that originals are never overwritten.
- Deployment commands, cloud bindings, and remote smoke probes should not exist.
