# Setup Provenance

**Status:** Current metadata

**Last updated:** [YYYY-MM-DD]

This document records how the repository foundation was produced. It contains no
credentials, secret values, private URLs, personal access tokens, or copied
environment files.

## Source

| Field                | Value                                                       |
| -------------------- | ----------------------------------------------------------- |
| Playbook repository  | `https://github.com/arturochang/project-bootstrap-playbook` |
| Release/tag          | `v2.2.0`                                                    |
| Resolved commit SHA  | [SHA or unavailable]                                        |
| Canonical prompt     | `project-setup-prompt.md`                                   |
| Provider profile(s)  | [path + tag/SHA, or none]                                   |
| Example(s) consulted | [path + tag/SHA, or none]                                   |
| Bootstrap date       | [YYYY-MM-DD]                                                |
| Agent/harness        | [name and version if known]                                 |

## Input authority

| Field                 | Value                                                      |
| --------------------- | ---------------------------------------------------------- |
| Product-plan path     | `docs/product-plan.md`                                     |
| Product-plan commit   | [commit SHA or uncommitted]                                |
| Approved intent owner | [name/role]                                                |
| Architecture status   | Proposed / Approved / Locked                               |
| Setup mode            | New project / Existing repository / Assess only            |
| Delivery target       | Design-ready / Local vertical slice / Preview / Production |

## Environment and toolchain

| Field                   | Value                                                     |
| ----------------------- | --------------------------------------------------------- |
| Primary provider        | [provider or none]                                        |
| Portability posture     | [provider-specific / isolated seams / active multi-cloud] |
| Environments            | [local, preview, staging, production]                     |
| Runtime and pin         | [runtime/version/file]                                    |
| Package manager and pin | [manager/version/file]                                    |
| Canonical gate          | [exact command or not yet implemented]                    |
| Canonical deploy        | [exact command or not applicable/not yet implemented]     |
| Status document         | [path]                                                    |
| Active handoff          | [path]                                                    |

Only list commands confirmed in the working tree. “Planned” is not a command.

## Artifact mapping

Record combined or renamed playbook outputs so a later session can find their
content without assuming the default path.

| Playbook artifact       | Repository path             | Notes   |
| ----------------------- | --------------------------- | ------- |
| Product plan            | `docs/product-plan.md`      | [notes] |
| Design language         | [path or not applicable]    | [notes] |
| Implementation plan     | [path]                      | [notes] |
| Status ledger           | [path]                      | [notes] |
| Security model          | [path or combined location] | [notes] |
| Deployment setup        | [path or not applicable]    | [notes] |
| Operations              | [path or combined location] | [notes] |
| Handoff                 | [path]                      | [notes] |
| Repository instructions | [path]                      | [notes] |

## Assumptions and deviations

| ID  | Assumption or deviation | Reason   | Consequence | Revisit trigger |
| --- | ----------------------- | -------- | ----------- | --------------- |
| P-1 | [statement]             | [reason] | [impact]    | [trigger]       |

State `None` explicitly when there are no deliberate deviations.

## Baseline evidence

| Check                    | Command/evidence               | Result   | Date   |
| ------------------------ | ------------------------------ | -------- | ------ |
| Repository inventory     | [evidence]                     | [result] | [date] |
| Format/lint/types        | [command or not yet available] | [result] | [date] |
| Tests                    | [command or not yet available] | [result] | [date] |
| Build/dry run            | [command or not applicable]    | [result] | [date] |
| Browser/integration lane | [command or outside gate]      | [result] | [date] |
| Human-only checks        | [workbook/cases]               | [result] | [date] |
| Deployment/public probes | [evidence or not authorized]   | [result] | [date] |

## Remote actions

List every remote mutation performed during setup, including repository settings,
cloud resources, secrets by name only, DNS, preview/production deployments, and
their identifiers. If none occurred, write: `None — local repository changes
only.`

## Updating the foundation

Before adopting a later playbook release:

1. Read its changelog and matching migration guide.
2. Preserve current project decisions and dirty work.
3. Present a diff; never regenerate mature documents wholesale.
4. Update this provenance record with the old and new release/commit.
5. Run the repository's real gate and applicable external checks.
