# Project Setup Prompt

**Template version:** 2.1.0

**Last updated:** 2026-09-20

Use this with a capable coding agent to start a new project or harden an existing
one. Replace the bracketed parts in §0, choose an operating mode, and delete this
introductory paragraph. The prompt is toolchain-neutral: adapt instruction,
skill, and agent paths to the active harness instead of assuming Claude Code,
Codex, Copilot, or another tool uses the same layout.

This prompt's job is not merely to generate a source tree. It must leave behind
a project another human or agent can understand, verify, operate, deploy, and
recover without reconstructing the original conversation.

---

## 0. What I want to build

**Operating mode:** [new project / adopt an existing repository / assess only].
For a new project, establish the foundation and proceed only to the selected
delivery target. For an existing repository, discover its real commands and
conventions before proposing changes, preserve unrelated work, and produce an
adoption/migration plan before rewriting structure. For assess-only, write the
evidence-backed documents and stop before changing product code.

**Product:** [one or two sentences — what it is, who it is for, what the central
claim is]

**Target:** [domain, or "undecided"]

**Primary infrastructure posture:** [Cloudflare-first / AWS-first / another
provider / provider undecided]. Name any service already mandated. A primary
provider is a present deployment decision, not a promise never to move.

**Portability requirement:** [provider-specific is acceptable / isolate the
likely migration seams / active multi-cloud]. Do not default to active
multi-cloud: it multiplies operating cost and usually produces a lowest-common-
denominator design. If future migration is only a possibility, identify the
hard-to-reverse choices and isolate those boundaries instead.

**Environments:** [local only / local + production / local + preview + staging +
production]. State who may deploy to each and which one owns real data.

**Constraints:** [e.g. free tier, monthly spend ceiling, closed source, i18n
from day one, mobile primary — or "none stated, propose some"]

**Availability and recovery target:** [best effort / target SLO; acceptable data
loss (RPO); acceptable recovery time (RTO)]. "Small project" is not an answer:
it still needs an explicit failure posture, even if that posture is best effort
and restore from source.

**Security, privacy, and compliance:** [data classes, authentication needs,
regulated data, residency, retention/deletion promises, or "none known — threat
model and propose"]. Include what must never enter logs, analytics, URLs, or
third-party services.

**Prior art / prior implementation:** [path to an old version, links to
competitors, or "none"]

**What a wrong answer costs here:** [users act on it / it is embarrassing / it is
recoverable in a redeploy]. This drives how much verification each layer gets.
Say it plainly, because "everything is critical" produces the same result as
"nothing is."

**Who else touches this repository:** [just me / me and other humans / me and
other agent toolchains / eventually a team]. This decides how much of what I
know has to be written down rather than remembered, and whether the instruction
files need a drift test (§4).

**Where and how this is physically used:** [at a desk on good wifi / on a phone
outdoors / in a gym basement with no signal / hands busy / one-handed /
interrupted every ninety seconds]. Answer this even if it feels obvious, and do
not let me answer it with a device name — "mobile" is not an environment. In the
project I am modelling this on, the single richest vein of real defects came from
one gap: every screen was built for a user looking at it on a good connection,
and the product is used by someone glancing at a phone between sets in a building
with bad signal. Nothing was wrong with the code. The whole failure class —
invisible save failures, an expired session that looked like a network blip, no
offline tolerance, a status region that scrolled off-screen — came from an
environment nobody had written down. Hold each design against this line
specifically, and say when a design assumes something better than what I wrote.

**How much data will exist in two years:** [a few dozen rows / thousands /
unbounded]. Single-user does not mean small-data. A list capped at 100 with no
pagination is invisible truncation once the cap is reached, and it is discovered
by the user, not by a test.

**Delivery target:** [design-ready / local vertical slice / preview deployment /
production deployment]. Define "ready" in observable terms: exact checks that
pass, URLs or artifacts that exist, and any human-only evidence still required.

**Source of this prompt:** [repository URL + immutable tag or commit, or "local
copy"]. Record this and template version 2.1.0 in the generated project so a
future update can compare versions instead of guessing what changed.

---

## 1. How to work with me

**Inventory reality before designing.** In an existing repository, start with
`git status`, the instruction files, the manifest, and the smallest current-state
or handoff document. Enumerate actual scripts, runtime versions, entry points,
deployment configuration, generated artifacts, and uncommitted work. Do not
infer a command or component from convention. In a new repository, write down
that these things do not exist yet so later agents do not imagine them.

**Do the research before writing anything.** If I named prior art or a previous
implementation, read it first and write down what it got wrong. If I named a
platform, verify its current limits against live primary documentation rather
than training data or a third-party summary — free tiers, product status, and
quotas move. Cite the source and the date verified. Label an inference as an
inference. Keep volatile facts out of always-loaded instruction files.

**Keep an assumption and decision ledger.** For every missing input, either ask
once if it changes the product's shape or record the safe default, its consequence,
and what would cause it to be revisited. Distinguish a requirement, an assumption,
a reversible preference, and an irreversible decision. Silence is not consent.

**Decisions get made, with reasons, and then they stop being re-opened.** State
what was considered and what was rejected. A decision recorded without its
rejected alternatives will be re-litigated in three weeks by both of us.

**Write constraints as testable properties, not aspirations.** "Fast" is not a
constraint. "P95 under 200ms, asserted in a test" is. If a rule cannot be
expressed as something that fails, say so explicitly and mark it as held by
discipline rather than pretending it is enforced.

**Verify before you assert, and correct the record when you were wrong.** Do not
tell me a capability is missing because a status command did not list it — test
the operation. Do not tell me a duplicated file is accidental drift before
checking whether something documents it. When you find you were wrong, say so in
one sentence, fix it, and move on; do not narrate the mistake at length, and do
not quietly let the wrong version stand.

**Ask before assuming on anything that changes the shape of the product.** Make
routine calls yourself. If two readings would produce materially different work,
ask — but do everything that does not depend on the answer first.

**Tell me what is not done.** A partial implementation described as complete
costs more than one described honestly. When you defer something, say what and
why, and put it somewhere durable rather than in a sentence I will scroll past.

**Converge; do not regenerate.** After the initial artifacts exist, refine them
in place and reconcile contradictions. Do not repeatedly replace whole plans or
specifications: that destroys decisions, evidence links, stable finding IDs, and
review history. Completion means the implementation, tests, current docs, and
deployment record agree.

**Retry budget.** Read the whole error and name the failing layer — shell,
executable discovery, dependency, configuration, application, network, provider
— before changing code. Never run an unchanged failing command a second time.
Change a condition or gather evidence first. Prefer one focused diagnostic over
a broad log dump. If a failure recurs, fix the shared script or configuration
rather than working around it again, and write the diagnosis down.

**Push back on my requests when the premise is wrong.** If I question a
dependency, a design, or an approach, treat it as a real question and check.
Twice in the project I am modelling this on, my challenge to a decision turned
out to be right and the fix was better than the original. If I reaffirm
something after you have raised a concern, that is my call — say so and proceed
with the full request.

---

## 2. Documents to produce, in this order

Do not write product code until the §2 foundation exists and its internal
conflicts are resolved. Pause for approval when an irreversible or high-cost
decision remains, or when the delivery target is `design-ready`; otherwise
continue without manufacturing a checkpoint. These decisions are cheap to
change now and expensive later, and several constrain each other.

Everything goes in `docs/`. Every document is dated at the top and states its
status.

Create **`docs/setup-provenance.md`** as a small metadata record containing the
prompt source and version, setup mode, primary provider, runtime and package-
manager pins, chosen environments, canonical gate, deployment command, and paths
to current status and handoff. Record answers, not secrets. If this prompt is
later distributed with a maintained setup CLI and published schema, it may use a
validated `.project-setup.yml` instead; do not invent a generic updater or YAML
schema merely to satisfy this prompt.

**When two documents disagree, prefer the more focused one, then the newer
explicit decision — and surface the conflict rather than silently picking.** Six
documents that constrain each other will contradict each other eventually; the
failure mode is not the contradiction, it is resolving it quietly in a direction
I never agreed to.

**a. `docs/prior-art.md`** — what comparable products do, filtered to what
serves _this_ product rather than the category. A summary table, then what to
take and what to leave, each with a reason. Note that version numbers and terms
change and should be re-checked.

**b. `docs/reviews/`** — a directory, not a file, from day one. The initial entry
is the review of the previous implementation if there is one: what it got right,
and every defect, each with a stable ID (`S-1` for security, `B-1` for
correctness/behaviour, `P-1` for product decisions). Every later independent
review lands here too, one dated file each.

Three rules make this directory earn its place:

- **IDs are permanent.** They get referenced from the rules file, from the
  implementation plan, and from test names for the life of the project. Number
  them once and never renumber.
- **Every review closes out with a disposition table** — what fixed each finding,
  or which stage it is scheduled into, and what would fail if someone undid the
  fix. An open finding with no scheduled home is a finding that will be
  rediscovered by the next review at full price.
- **A review is a dated snapshot, never current state.** Say so in the file's own
  header. A review that sits in the docs table advertised as "current findings"
  is describing an app that stopped existing three stages ago, and the next
  reader will believe it. Point the rules file at the directory and at the
  ledger, not at one review that will silently expire.

**c. `docs/product-plan.md`** — the reasoning. Platform choice with the rejected
options and why they lose. Scope decisions. What is explicitly out of scope and
will not be argued again. What is shelved rather than rejected, with the analysis
that shelved it and the note about what not to foreclose. A build order,
correctness-first. Include a capability map before naming services: compute,
static delivery, transactional state, object storage, cache/config, coordination,
asynchronous work, identity, secrets, observability, DNS/TLS, and infrastructure
as code. For every required capability, record the chosen provider primitive,
why it fits, its quota/cost failure mode, and the migration seam if one is worth
buying now.

**d. `docs/design-language.md`** — normative, if the thing has a UI. Tokens with
actual values in a table. The complete component set, named. Breakpoints, named
and countable. Accessibility rules as absolutes. Anti-goals stated explicitly so
they are not proposed again. Voice and copy rules — sentence case, no exclamation
marks, buttons are verbs, name the consequence rather than the mechanism.

**e. `docs/implementation-plan.md`** — written to be picked up cold, but kept
small: active-stage scope/closure, the next-stage entry gate and candidates,
finding routing, and universal verification rules. When a stage closes, move
its detailed build steps, file list, tests, and original done criteria into
`docs/implementation-history.md`. Agents read that archive only when a task
needs completed-stage rationale or provenance. Where a current decision is
still open, say so and recommend a default rather than leaving it silent.

Two structural habits worth building in from the start:

- **After the first implementation of a shared surface, insert an `N.5`
  consolidation checkpoint before a second surface copies it.** The modelled
  project added a "Stage 3.5" after the first logging screen and before the
  second, purely to fix the conventions the second would otherwise inherit —
  recovery semantics, destructive-action treatment, focus, tokens. It was the
  highest-leverage stage in the plan, because every fix landed once instead of
  twice. Do the same after the first real deployment: production teaches things
  staging cannot.
- **Every review finding gets routed to a stage, by ID, in the current plan.** A
  finding that lives only in the review document is a finding nobody is going to
  do. Move closed detail to implementation history without renumbering the ID.

**f. `docs/status.md`** — the living ledger, and the file a new session reads
first to answer "what now?" Put a compact current focus and active handoff at the
top; keep completed-stage evidence below an explicit on-demand boundary. The
plan says what we intend; status says what is actually true.

- A fixed status vocabulary and nothing else: `Done`, `In progress`, `Pending`,
  `Blocked` (naming the blocker), `Deferred` (naming who deferred it and why).
- **Every `Done` carries evidence** — a link to the code, the test, or the
  command output that proves it. A status claim with no evidence link is a
  wish. This one rule does more than the other five.
- A "current focus" queue, kept short, with obsolete items deleted rather than
  accumulated. This is a ledger, not a changelog; git already has the changelog.
- A verification record: the last broad run, its result, and **which gates were
  intentionally skipped and why.** A green summary that hides a skipped browser
  lane is worse than no summary.
- Known-but-unassigned work, so that a defect found during review has somewhere
  to go that is not "fix it now" or "forget it."
- Updated _in the same change_ that advances a deliverable, never as a
  follow-up.

**g. `docs/security-model.md`** — compact but concrete. Assets, actors, trust
boundaries, data classification, abuse cases, authentication/authorization,
secret ownership, logging/telemetry exclusions, dependency and supply-chain
posture, and the checks that hold each claim shut. If the product handles tokens,
cryptography, uploads, webhooks, user-generated content, or regulated data, add
misuse cases and rotation/revocation procedures. Never claim an audit unless one
actually occurred.

**h. `docs/deployment-setup.md`** — the reproducible path from a clean account
and clean clone to each environment. Include prerequisites, infrastructure as
code or committed provider config, bindings, migrations, secrets workflow,
domain/DNS/TLS ownership, preflight, deploy, smoke probes against the real public
route, rollback, and teardown. Separate repository-owned resources from account-
or organization-owned resources. Dashboard-only state is drift unless the
provider offers no declarative mechanism; document every unavoidable exception.

**i. `docs/operations.md`** — proportionate to the product, never ceremonial.
Name health signals, structured log fields and forbidden fields, dashboards,
alerts and owners, cost budgets/kill switches, backup and restore where data is
durable, incident triage, rollback, and post-deploy verification. For a best-
effort hobby service this can be one page, but it cannot be implicit.

**j. `docs/handoff.md`** — a deliberately short active-session handoff: current
stage, exact next task in order, tree state, last verification, known traps, and
anything that must not be overwritten. Historical detail belongs in status or
implementation history, not here.

**k. `AGENTS.md`** — see §3. Written last, from the others.

Do not create empty documents to satisfy this list. If two adjacent documents
would each be a few paragraphs, combine them and record the mapping in
`docs/setup-provenance.md`. The requirement is durable coverage and
discoverability, not a sacred file count.

---

## 3. AGENTS.md

The single entry point for anyone, human or agent, changing this repository.

**This file is loaded into every session, so every line has a permanent token
cost.** That is the discipline that keeps it good: if a line does not change
what someone does, it does not belong. Prefer imperative rules over explanation.
When I trimmed this file by a third in the modelled project, nothing was lost
except restatement — the same instruction had been given in three sections.

**Division of labour, and hold it strictly:** `AGENTS.md` holds the _operative
rules_, in imperative form — what to do. `docs/` holds the _reasoning_ — what was
considered, what was rejected, why. A recurring diagnostic procedure goes in a
skill (§4), not here. When a rule and its rationale would both need stating, the
rule goes in `AGENTS.md` and the rationale in `docs/`. Do not copy paragraphs
between them; a duplicated paragraph is a paragraph that will drift.

Sections, roughly in this order:

- **What this is** — two sentences, plus what this repo is _not_ responsible for,
  plus what does not exist yet. State plainly which scripts, frameworks, and
  services are not present, and say: do not assume a command exists until it is
  in the working tree. Half of an agent's wasted turns are spent running scripts
  that were imagined.
- **Read first** — a table of the `docs/` files and what each carries, with the
  instruction to read the relevant section rather than the whole tree. State the
  rule: if a change contradicts one of these, update it in the same change.
  Silent divergence between docs and code is worse than either being wrong.
- **Architecture** — the decisions, and the explicit `Do not use X` rules with
  the one-line reason. Negative rules are more valuable than positive ones; they
  are the ones that get violated by someone being helpful.
- **Stack and layout** — an annotated directory tree where the annotation says
  what belongs there and what does not.
- **Non-negotiable constraints** — the section that earns the file. Each rule
  imperative, each carrying the finding ID it encodes where one exists. Where a
  rule is subtle, state the mechanism concretely: not "this is atomic" but "there
  is no `await` between the read and the delete; the absence of a suspension
  point _is_ the atomicity."
- **Product constraints**, and an explicit **out of scope** list.
- **Failure handling and retry budget** — §1's version, in imperative form.
- **Token and context discipline** — search before reading; read targeted
  sections, not whole trees; never paste lockfiles, generated files, or logs
  into chat; keep durable facts in documents and procedures in skills; do not
  restate the same instruction across plans, comments, and reports.
- **Before finishing a change** — a numbered checklist ending in "if this change
  touches a decision recorded in `docs/`, update that document in the same
  change." Include any check a machine cannot do, and say why it exists.
- **When to delegate a review** — see §4. Give concrete triggers, not "when it
  seems risky."
- **Operational** — how to deploy, what the gate is, what is managed outside the
  repo, and every environment trap that has cost time. Long diagnostics go in a
  skill; leave a pointer.
- **Volatile facts** — quotas, limits, third-party recommendations. Dated, with
  the instruction to re-verify rather than quote from memory, _including from
  this file_.

**Anything that cost more than an hour to discover goes in this file or a skill,
in the place where someone would be about to make the same mistake.** Not in a
commit message, not in a comment.

---

## 4. Agent tooling

Set this up early. It is the difference between an assistant that re-derives the
same context every session and one that does not.

**Skills** (for example `.claude/skills/<name>/SKILL.md`, or the active
harness's equivalent) — a procedure loaded on demand rather than carried in
every session. Each has a `name` and a `description` that says _when to use it
and when not to_, because the description is all that is matched against. Keep
the canonical substance in one place and generate or test harness-specific
wrappers where formats differ.

Write one for each of these, if they apply:

- **Verification and environment diagnosis.** The gate order, and a
  `Known failures` section: the exact error text, the real cause, and the fix.
  This is the highest-value skill by a distance. In the modelled project it
  turned a recurring twenty-minute toolchain rabbit hole into a thirty-second
  lookup, because the error text was verbatim-searchable.
- **The design system**, if there is a UI.
- **The domain rules** that are easy to get subtly wrong.
- **The deployment platform's constraints.**

A trap belongs in a skill rather than `AGENTS.md` when it is long, conditional,
and only needed when something has already gone wrong.

**Subagents** (in the active harness's supported location) — bounded by default,
with one question or implementation packet each.

- Give each an explicit question, scope, allowed tools, and expected output
  shape.
- Prefer read-only for discovery and review. Give write access only for a
  mechanical change with exclusive file ownership. The primary agent owns
  integration, consequential decisions, deployment, and final verification.
- Never let two agents edit the same files. Cap concurrency at about three.
- Require evidence-backed returns. An agent that reports a defect must give the
  file, line, and the failure scenario, so the claim can be checked rather than
  believed. **Do not accept a subagent's findings at face value** — in the
  modelled project a reviewer was right three times and a planner was wrong once,
  and both needed checking.

Write implementation packets so a smaller model can execute them safely. Each
packet must contain: purpose; non-goals; owned files; required context and skill;
preconditions; numbered edits; invariants that must remain true; exact tests;
an adversarial or mutation check when a new guard is added; documentation/status
updates; stop conditions; and the required return format. If a packet still asks
the worker to make an architectural, protocol, security, migration, or public-
claim decision, it is not complete enough to delegate.

**Pick the model by the cost of a wrong answer, not the size of the task.** Use
capability tiers rather than hard-coding a vendor's current model names; model
catalogues age quickly. Where the harness permits, pin the selected model and
reasoning level in its configuration and document the dated mapping.

| Work                                                                                  | Minimum tier                |
| ------------------------------------------------------------------------------------- | --------------------------- |
| Locating files, enumerating call sites, deterministic formatting                      | Fast/low-cost               |
| Bounded mechanical edits from a complete packet, with exact tests                     | Standard implementation     |
| Structured research, extraction, comparisons, a plan the primary will verify          | Standard reasoning          |
| Reviewing a diff, accessibility judgment, security, protocol, migrations, public copy | Strong independent reviewer |

Two things make a cheap model a false economy: a mistake that is _silent_, and a
mistake nothing downstream catches. A reviewer's failure mode is a false clear
that ships, so reviewers do not get cheapened.

**Make review delegation trigger on facts, not vibes.** "Review the diff" reads
as self-review, and self-review misses what the author already believes. Name
the conditions — more than ~5 files, or touching correctness-critical logic,
auth, data migration, a public route, or a user-visible surface. In the modelled
project, adding this trigger paid for itself on its first two uses: once it
caught a test that had quietly become a parallel reimplementation of the code it
was supposed to guard, and once it caught a data-loss bug whose own misleading
justification was already sitting in the code as a comment.

**Hooks** (where supported by the active harness) — use a session-start hook to
make the environment correct rather than documenting how to correct it. Fix the
cause once in the hook instead of writing the workaround in three places. Keep
hooks fast, deterministic, local, and safe when run repeatedly.

**If you use more than one agent toolchain** (say Claude Code and Codex), they
will each want their own instruction directory. That duplication is legitimate,
but it _will_ drift, and the copy that drifts is the one you are not looking at.
Add a test that asserts both carry the same substance — match on meaning, not
exact text, since the wordings differ deliberately.

---

## 5. Repository setup

**Scaffold**

- `README.md` — what it is, how it works in three sentences, the stack, the
  development commands with a note on what each is _for_, and a pointer to
  `AGENTS.md` and the `docs/` table. It is not a duplicate of `AGENTS.md`, and
  **it does not restate project status** — link to the ledger instead. A README
  that says which stage is current is a README that will be wrong within a week,
  and it is the first file a stranger trusts. In the modelled project it sat four
  stages out of date, next to a deploy command that had been superseded.
- `.gitignore` — dependencies, build output, tool caches, secrets (with the
  `!*.example` negations), local agent config, logs, OS files. Group with
  comments. The secrets group gets a comment pointing at the AGENTS.md section
  that explains the real workflow.
- Version pin file for the runtime, and `engines` for the real floor. They are
  different questions: raise the pin freely, changing the floor is a
  compatibility decision.
- A `.env.example` (or equivalent) committed, with every variable named and
  described, and the real one gitignored.
- Shared agent/harness settings committed where safe; personal settings,
  credentials, machine paths, and local approvals gitignored. Document the
  exact harness-specific filenames chosen.
- A file-size gate with soft warnings and hard failures, per file category. Soft
  warnings are advisory and may stay; hard failures block. It catches the file
  that has quietly become unreviewable before a reviewer has to say so.
- **Any gate that walks the repository must ignore exactly what git ignores.**
  Give it one ignore list and derive both from it, or it will eventually fail on
  something that is not part of the deliverable. The modelled project's file-size
  gate did not exclude the local database-backup directory, so the first
  production backup over the hard limit would have failed the gate — and
  therefore blocked deployment — from a gitignored file. A gate that can be
  broken by an artifact nobody ships teaches people to bypass gates.

**Scripts** — one command per intent, and one gate:

- `doctor` for fast environment/config preflight without changing remote state;
  `dev`; `check` (types/lint, no emit); `test`; `build`; and `preview` where the
  stack supports it.
- Separate expensive or environment-dependent lanes such as `test:browser`,
  `test:e2e`, `test:integration`, and `test:live`. Document whether each is in
  the normal gate and what credentials, browsers, devices, or network it needs.
- **`gate` is the complete credential-free release check**, in the order that
  actually works. If ordering matters — build before tests because tests read
  build output, for example — state that in the script's documentation, because
  someone will "optimise" it otherwise.
- **`deploy` runs preflight, the full gate, the provider deploy, and post-deploy
  smoke probes.** Never call the underlying provider deploy tool alone. Support
  a dry run. Dry-run mode must not mutate remote state or probe the currently
  live release as if it were the candidate; it validates/renders the deployment
  plan and prints the target and intended probe plan. Add `rollback` and
  `teardown` only when they can be made safe and exact; otherwise document the
  provider procedure and required approval.
- **Check every script name against the package manager's own built-in
  commands.** `pnpm deploy` is a real pnpm command for workspace package
  deployment, so a script named `deploy` must be invoked as `pnpm run deploy` and
  the bare form quietly does something else entirely. This cost the modelled
  project a documentation fix in three files and would have cost a bad deploy.
  Check the collision at the moment you name the script, not after.
- **Auto-fix what can be auto-fixed; only gate on what cannot.** If the first
  link in the release chain is cosmetic, releases will be blocked for cosmetic
  reasons at the worst possible moment. Run the formatter as a write step in the
  local loop and in a pre-commit hook, and keep `format:check` in the gate as the
  backstop rather than the primary mechanism. The modelled project shipped five
  correct review fixes and left the release path red on whitespace.
- **Do not invent scripts that do not exist yet.** Until it is in the manifest,
  it is not a command.

**Default to a read-only CI verification workflow** on pull requests and pushes:
install from the lockfile, run the canonical gate, use least-privilege permissions,
pin third-party actions to immutable revisions, and use no production secrets or
deploy step. Deployment authority stays explicit and separate. If there is no
CI, say so in `AGENTS.md`, name what the only gate is, and name who runs it,
because an unrun gate is not a gate. A green CI result is verification, not proof
of deployment or of human-only behavior.

Treat pull-request code as untrusted. On GitHub Actions, use the ordinary
unprivileged `pull_request` event with explicit minimal permissions (normally
`contents: read`); never use `pull_request_target` to check out and execute the
pull request's code. Expose no repository, registry, cloud, or inherited secret
to untrusted code beyond what public dependency installation strictly requires.

**A platform wrapper script if my platform needs one** (Windows/PowerShell
here). It _calls_ the gate rather than reimplementing it — two copies of an
order-sensitive sequence will drift. What it adds is a preflight that runs
_before_ the slow gate: auth first, so an expired login does not fail only after
build and test have both run; and probe every external binary before use,
because version managers put tools on PATH through a per-shell hook and any
shell that never ran the profile has none of them. Better still, have the
wrapper _repair_ the common breakage itself rather than printing instructions.
Support a dry run. Collect all problems and report them together rather than
failing on the first.

**Make repeated setup safe.** A second bootstrap run must not blindly overwrite
user changes: inspect and present a diff first. Record the source prompt version
in `docs/setup-provenance.md`. If a maintained CLI/template system exists, use
its published ownership, dry-run, and migration contract; otherwise do not
invent one inside the generated project. Version changes to this prompt and
publish a concise migration note for breaking updates.

**Dependencies: check the platform first.** Before adding a library, check
whether the platform's own CLI or primitive already does the job. In the
modelled project a signing library was added to reach an S3-compatible API, and
the platform's own CLI turned out to do the same work while reusing the existing
login — which removed the dependency _and_ the entire credential-storage
problem. Adding a dependency is also adding its supply chain, its lockfile
churn, and its secrets. When you do add one, state the reason in `AGENTS.md`,
and verify the package's real size, licence, and transitive dependencies rather
than recalling them.

**But do not hand-roll protocol or cryptographic verification to avoid a
dependency.** "Prefer the platform primitive" means prefer the platform's
_capability_, not reimplement someone else's _specification_ on top of it. The
modelled project wrote a JWT verifier directly against the platform's Web Crypto
API — signature check, key selection, claim validation, all of it — and it passed
its own tests, because the tests were written from the same understanding as the
code. It failed against the real identity provider on the first production
request, and was replaced by the standard library. Signature verification, token
parsing, canonicalisation, date-format handling, and anything with a published
spec and a widely used implementation are where a dependency is _cheaper_ than
the code you would write. The tell is that you are implementing a document rather
than calling one.

**Choose capabilities before products.** Do not begin with a provider logo and
then search for services to use. Build this table in `docs/product-plan.md` and
leave rows out when the capability is not needed:

| Capability          | Requirement/invariant          | Chosen primitive | Why      | Quota/cost failure | Migration seam     |
| ------------------- | ------------------------------ | ---------------- | -------- | ------------------ | ------------------ |
| Compute             | [latency, runtime, duration]   | [service]        | [reason] | [behavior]         | [boundary or none] |
| Static delivery     | [cache/routing needs]          | [service]        | [reason] | [behavior]         | [boundary or none] |
| Transactional state | [consistency/query shape]      | [service]        | [reason] | [behavior]         | [boundary or none] |
| Objects/files       | [size, retention, egress]      | [service]        | [reason] | [behavior]         | [boundary or none] |
| Coordination        | [single writer/locks/realtime] | [service]        | [reason] | [behavior]         | [boundary or none] |
| Async work          | [retry/delay/duration]         | [service]        | [reason] | [behavior]         | [boundary or none] |
| Identity/secrets    | [actors/rotation]              | [service]        | [reason] | [behavior]         | [boundary or none] |
| Observability       | [signals/retention]            | [service]        | [reason] | [behavior]         | [boundary or none] |
| DNS/TLS             | [zones/certificates]           | [service]        | [reason] | [behavior]         | [boundary or none] |

Keep domain logic independent of provider SDK types when the boundary is natural:
configuration, object storage, message publication, email, identity claims, and
telemetry exporters are common seams. Do not wrap a provider primitive merely to
claim portability. A distributed coordination model, consistency guarantee,
runtime limit, or database query model cannot be made portable by renaming its
methods; record it as an architectural commitment and a migration plan instead.

Keep provider configuration in a focused adapter/IaC area and keep product
protocols free of provider service names. Test adapters against a shared
behavior contract only where two implementations actually exist or near-term
migration justifies one. A speculative second implementation is not portability;
it is twice the maintenance.

**Cloudflare profile, if Cloudflare is primary.** These are starting
positions, not conclusions — put the ones that survive §0's constraints into
`AGENTS.md` under Architecture, each as a rule with its one-line reason, and
record any you reject in `docs/product-plan.md` with why. Re-verify the
product-status claims before relying on them; this list is dated below. When
using this prompt from its source repository, also consult the dated companion
[`profiles/cloudflare.md`](profiles/cloudflare.md) at the same tag or commit.

- Start new applications on **Workers + Static Assets**, not Pages. Pages
  continues to work and remains supported, but Cloudflare's feature work and
  optimisation now go to Workers, so choosing Pages is choosing the branch that
  stops gaining. Migrating later is real work.
- **For lightweight, read-heavy relational workloads, evaluate D1 first.** Its
  binding avoids connection management and application-held database credentials,
  but verify current database-size, query, write, replication, migration, and
  compatibility needs. Use external Postgres/MySQL or another store when the
  workload requires it; do not force a product into D1 to satisfy a template.
- **R2 stores files; D1 stores metadata about those files.** Binary content in
  D1 wastes the row limit and cannot be served directly; query-shaped metadata
  in R2 cannot be filtered without listing the bucket.
- **KV is a cache or config layer, not a source of truth** — it is eventually
  consistent, so a write is not guaranteed visible to the next read. Anything
  that must read-your-writes or hold an invariant belongs in D1 or a Durable
  Object.
- **Durable Objects are for coordination** — locks, single-writer state,
  WebSocket fan-out, rate limiting — **not ordinary CRUD.** The property they
  sell is that exactly one instance owns a key at a time; if a feature does not
  need that, it does not need a Durable Object.
- **Queues take anything slow, unreliable, or AI-shaped** off the request path,
  because a Worker request has a wall-clock and CPU budget and a third-party
  call can exceed it. Queues also give retries you would otherwise hand-roll.
- **Keep Cloudflare resources behind bindings, not public service URLs.** A
  binding is private by construction and carries no credential to leak or
  rotate; the same resource behind a public URL is an access-control surface
  you now own forever. This is the rule most often broken by someone being
  helpful during debugging.
- **Cache deterministic and public responses aggressively**, keyed on what
  actually varies the response — and never cache a per-user or per-household
  response on a shared key. A cache key missing a dimension that changes the
  body is a cross-user data leak, not a performance bug.
- **Commit D1 migrations and the Wrangler config to Git.** They are part of the
  deployable artifact, not local state; a schema that exists only in a
  developer's account cannot be reproduced or reviewed.
- **Start simple, and make the platform earn each addition.** Worker + Static
  Assets + D1 is a genuinely capable application. Add KV, Durable Objects, or
  Queues when a concrete requirement demands it — not a hypothetical scale —
  and say in `AGENTS.md` which requirement bought it.

_Verified 2026-09-20 against Cloudflare's
[Workers best practices](https://developers.cloudflare.com/workers/best-practices/workers-best-practices/)
and [storage selection guide](https://developers.cloudflare.com/workers/platform/storage-options/):
Workers Static Assets is recommended for new static, SPA, and full-stack projects;
Pages remains supported while new features and optimizations focus on Workers;
and storage choice is workload-specific. Re-check before quoting._

**AWS profile, if AWS is primary or a credible migration target.** Do not make a
service-by-name translation from Cloudflare. Re-run the capability table against
current AWS primary documentation, pricing, quotas, regions, and the team's
operational ability. Decide deliberately among edge/CDN and origin compute,
Lambda/API Gateway or container compute, DynamoDB or relational storage, S3,
SQS/EventBridge, Step Functions, Cognito or an external identity provider,
Secrets Manager/Parameter Store, CloudWatch/X-Ray, Route 53/ACM, and CDK,
CloudFormation, Terraform, or Pulumi. These are candidates, not defaults. Record:

- the account/organization and region model;
- IAM roles and least-privilege boundaries for humans, CI, and workloads;
- tagging, budgets, anomaly detection, and resources whose idle cost is nonzero;
- VPC/NAT and cross-region/cross-AZ data-transfer costs before introducing them;
- deployment packaging, rollback, retained resources, and deletion protection;
- whether local tests exercise a real-compatible runtime or only a mock;
- the exact portability boundary, especially for stateful and event-driven
  semantics that do not map one-to-one to Cloudflare.

If Cloudflare is primary today and AWS is merely possible later, create no AWS
resources and add no AWS SDK. The useful preparation is a provider-neutral
capability record, narrow integration seams, portable data export formats, and
an explicit migration trigger — not paying the complexity tax in advance.

---

## 6. Commits

**Subject line: `type: what changed, in lower case, as a phrase.`** Conventional
prefixes (`feat`, `fix`, `docs`, `test`, `chore`, `build`, `a11y`, `perf`). Not
a restatement of the diff — say what is now true:

```
feat: rate limiting, in two mechanisms for two different attacks
fix: cap the secret in bytes, and say so before it is too late
a11y: audit reduced motion, and fix what the reset was missing
docs: the prior deployment is decommissioned, and the item that described it was wrong
```

**Body: what was wrong, what is now true, and what would break if someone undid
it.** Prose paragraphs, not bullet lists of files. If the change fixes something
subtle, say specifically what was subtle about it. If a test now holds a
property shut, name the property. If the change corrects an earlier claim, say
what the earlier claim was.

Length follows substance: a version bump gets one line, a decision gets five
paragraphs.

Co-author trailer on agent-assisted commits.

---

## 7. Testing and verification

- Tests run in the **real runtime**, not a simulation of it, wherever the
  platform makes that possible. A harness that exercises a code path production
  does not take is worse than no test, because it reads as coverage.
- Browser/end-to-end tests exercise the **shipped entry point and built assets**,
  not a test-only reimplementation. Inspect generated output for properties that
  source tests cannot prove: forbidden inline code, secret strings, the intended
  source-map publication/access policy, bootstrap ordering, stale asset
  references, security headers, and bundle-size ceilings.
- **Name the test after the property**, not the function. `20 concurrent reveals
produce exactly one winner` is a test name.
- **Where a test asserts a finding from the design review, put the finding ID in
  the test name** so a failure leads back to the defect it exists to prevent.

- **A test that has never failed is a hypothesis.** Before believing a guard,
  break the thing it guards and watch that specific test fail. This is the
  single highest-value habit here, and it is cheap — revert the fix, run, restore.
  In the modelled project it caught a test that duplicated the logic it was
  meant to protect: it passed happily while the real function was broken, because
  it never called it. Green was meaningless and had been for weeks.

- **A test must not call a parallel implementation of the thing it tests.** If
  the assertion re-derives what the code derives, it will agree with itself
  forever. Call the real exported function.

- **Verify on a clean clone.** Tests that read files produced by a local run —
  anything gitignored, cached, or generated — pass on the machine that made them
  and fail everywhere else. Actually clone into a temp directory and run, or
  temporarily move the artifact aside. An absent artifact is usually a legitimate
  state that should assert nothing; a _present_ one should be asserted fully.
  And if a check must skip, add a companion test asserting that it skips only
  when it should, or the coverage will retire itself silently.

- **Do not pin generated filenames that embed a hash or timestamp.** Scan the
  directory. A pinned name vanishes the moment the input changes — which is
  exactly when the check mattered.

- **Probe the real thing once, then encode what you learned in the fake.** Fakes
  test your logic; they cannot discover how the outside world actually behaves.
  One real round trip in the modelled project surfaced two behaviours no
  reasonable fake would have had: the runtime refused to spawn a wrapper script
  on Windows, and the download tool created its output file _even when the
  download failed_ — which would have left empty files posing as real data.
  Both became fake behaviour and both are now regression-tested offline.

- **Keep credentials and network out of the normal gate.** Inject the transport.
  The gate must pass on a machine that has never logged in.

- **Treat production verification as a separate evidence layer.** A dry build is
  not a deploy, a deploy command exiting zero is not a healthy release, and a
  `/health` endpoint does not prove the public HTML, JavaScript, cache behavior,
  authentication boundary, or security headers. After deployment, probe the
  real user entry route and one critical journey. Any production write probe
  requires an explicitly approved environment plus a dedicated test identity or
  tenant; it must be marked, idempotent, reversible, and cleaned up. By default,
  prohibit destructive, customer-visible, externally messaged, or chargeable
  probes. Record the deployed version, probes, cleanup result, and rollback point.

- **Flakes are findings.** A test that fails a few percent of runs, only under
  load, always in the same direction, is a real defect wearing a costume.
  Diagnose it; do not retry it.

- **Say which properties nothing tests.** Some things are held by architecture,
  and some only by discipline. Both should be written down as such.

- If any check requires a human — a physical device, a real browser, a camera —
  put it in the `Before finishing a change` checklist with the reason it cannot
  be automated. Give it a stable case ID, setup, steps, expected result, evidence
  field, and retest rule in a human-testing workbook. Self-consistent round-trip
  tests are wrong in both directions at once and pass.

**Gate order**, cheapest and most localising first, so a failure points at
itself. Include integration and browser lanes in the canonical gate only when
they are deterministic, credential-free, and available from a clean toolchain;
otherwise keep them as explicitly required external lanes:

```
format → lint → file limits → schema/static checks → typecheck → unit → [integration] → [browser] → build
```

Run the narrowest relevant check while working, and the full gate before
declaring done. **Never weaken or skip a check to make it green** without
saying so explicitly and getting agreement.

Before a production deploy, write a compact release record containing the exact
commit, clean/dirty tree status, gate result, out-of-gate browser/integration
lanes, dependency audit, applicable human cases, migrations/config changes,
known open findings, smoke plan, and rollback target. After deployment, append
the provider deployment identifier and probe results. Never reconstruct this
from memory after an incident.

**Run the full gate again after applying review fixes.** A batch of fixes
answering a review feels like the end of a process, so it is the change most
likely to skip the process. In the modelled project the gate ran before the
review and not after it, and five correct fixes left the release path red.

**Assert the exact set, not the presence of members.** A test that checks each
expected item is present passes just as happily when an unexpected sixth item
appears. If the property is "exactly these five read-only tools and no write
tool," the assertion is a sorted deep-equal on the whole list. The looser version
reads as coverage of an invariant it does not actually hold.

---

## 8. Defaults I want unless I say otherwise

- TypeScript, strict.
- Minimal dependencies. Prefer the platform primitive; if you add a library,
  state the reason in `AGENTS.md`.
- Static by default; ship client-side JavaScript only where it is required, and
  say where.
- Accessibility is not a phase: semantic HTML, visible focus, contrast, reduced
  motion, keyboard-only, from the first component.
- Mobile-first literally — author at the narrow width and add `min-width`
  queries upward, not the reverse.
- i18n from day one if it will ever be needed. Retrofitting it is painful. Every
  user-visible string is a key; a missing or stale key fails the build.
- Every design value comes from a token. A literal colour or spacing value
  outside the token file is a defect.
- Nothing inline — no inline styles, no inline script, no inline handlers — and
  a Content Security Policy that forbids it, with a test that fails the build
  output before a browser would.
- Never log credentials, payloads, or user content. Log IDs and outcomes.
- Define structured event names and bounded fields before adding telemetry.
  Redact at the source; a dashboard filter is not a privacy boundary. Correlation
  IDs must not become stable user identifiers accidentally.
- Model cost as a failure mode. Record the unit that drives spend, free/paid
  thresholds, projected normal and abusive usage, alerts, a hard or operational
  kill switch, and the degraded behavior after the limit. Prefer fail-safe and
  still-useful over fail-open and unexpectedly expensive.
- **Separate mutation success from revalidation failure** in any autosaving UI.
  Once the write has succeeded, a failed follow-up read must never re-offer the
  write as the retry — that is how a retry button becomes a duplicate-record
  button, or a permanent failure loop against an already-deleted row. Two states,
  two retries. This was the first blocker found in the modelled project's UI
  review and it would have been free to get right at the start.
- **Classify authentication failure distinctly at the client HTTP boundary,
  from the first request wrapper you write.** A wrapper that throws one generic
  error on every non-`ok` response makes an expired session indistinguishable
  from a transient blip, and offers a retry that can never succeed. Worse, an
  identity proxy that answers with a redirect to its login page yields a `200`
  full of HTML, so the failure arrives as a JSON parse error and the status code
  never appears at all. Detect the auth cases, and offer a reload — which lets
  the redirect complete — rather than a retry.
- **Anything holding a cache must outlive the request.** Constructing a client
  per request throws away the cache, cooldown, and connection reuse that the
  client exists to provide, while looking correct in every test. The modelled
  project built its JWKS resolver inside the per-request handler and refetched
  signing keys on every single API call.
- **Three auth lanes, and the local one must be impossible to activate in
  production:** the real production mechanism, injected test identity, and an
  interactive local-development identity. Gate the local lane on something
  production cannot present — a loopback hostname _and_ the absence of production
  configuration — never on a header or query parameter, which is a bypass wearing
  a development costume.
- **A status region that scrolls away is not a status region.** If a surface can
  be taller than the viewport, its save state and its recovery action must be
  reachable from wherever the user actually is. Off-screen is worse than
  transient: transient was at least rendered once.
- Secrets via the platform's secret store and a gitignored local file. Never
  committed. Never in a config file — check the config files, they are where
  they actually hide.
- Prefer an approach that needs no stored credential at all over one that stores
  one safely.
- **Separate permission to acquire from permission to publish** for any
  third-party data, and track it per resource. Fetching something is not a right
  to redistribute it, and conflating the two is discovered late and expensively.
- **Make derived output immutable and content-addressed** where it is
  practical — the digest in the identifier makes re-running idempotent for free
  and makes corruption detectable rather than silent.
- Prefer choices a stranger could reproduce on a fresh free-tier account.
- Pin runtimes, package managers, and lockfiles. Separate the version used by
  maintainers from the minimum version the project promises to support.
- Generate an SBOM or at minimum keep an auditable dependency inventory; enable
  automated vulnerability/update alerts, but batch toolchain upgrades deliberately
  rather than mixing them into feature work.
- For durable data, define ownership, schema migration, export, backup, restore,
  deletion, and retention before the first production write. Test restore, not
  merely backup creation. For products that intentionally store nothing, state
  that as an invariant and test that no storage binding or persistence path is
  introduced.

---

## 9. Start here

1. Identify the operating mode. In an existing repository, inventory actual
   state and preserve the user's dirty tree before doing anything else.
2. Ask whatever is genuinely unresolved in §0 — but only what would change the
   work, and ask it all at once. Record safe assumptions for everything else.
3. Research prior art and verify provider claims against primary sources, with
   URLs and dates. Produce the capability table before selecting products.
4. Create `docs/setup-provenance.md` and the smallest complete `docs/` set from
   §2. Run a consistency pass across scope, architecture, security, operations,
   delivery stages, and deployment.
5. For assess-only mode, stop with a decision and next-step options. Otherwise,
   present the irreversible/high-cost decisions for approval. If none remain,
   continue without manufacturing a checkpoint.
6. If the delivery target is `design-ready`, stop after the approved foundation
   and readiness report. Otherwise scaffold the repository, canonical gate,
   read-only CI, `AGENTS.md`, and only the agent skills/tooling the project
   actually needs. Run the gate on the empty/skeleton project so setup defects
   surface before product complexity.
7. For `local vertical slice`, `preview deployment`, or `production deployment`,
   build one thin vertical slice through the real runtime and deployment shape:
   user entry, core domain action, persistence or explicit no-storage path,
   error state, observability, tests, and deploy artifact. Do not build every
   feature before proving the architecture can ship. Stop locally when that is
   the selected target.
8. Update `docs/status.md` and `docs/handoff.md` in the same change as reality.
   Run the full gate, applicable external lanes, independent review triggers,
   and clean-clone verification.
9. Only for `preview deployment` or `production deployment`, use the canonical
   deploy command for the named environment, run its approved public-route smoke
   probes, record the deployment and rollback point, and say which human-only
   checks remain. Never promote preview to production implicitly.

At handoff, return a concise readiness report with:

- what now exists and the first command a new contributor runs;
- the chosen architecture and primary provider, with the important rejected
  alternatives;
- exact local, gate, preview, deploy, smoke, and rollback commands that actually
  exist;
- verification evidence, including skipped lanes and human-only work;
- open findings, risks, assumptions, and the next three tasks in order;
- the source prompt version and any deliberate deviations from it.

**If research contradicts something I asserted in §0, stop and tell me before
writing the documents.** A constraint I gave from memory — a free-tier limit, a
competitor's behaviour, what the old implementation did — is exactly the kind of
thing research overturns, and it is cheap to correct now and expensive once the
project foundation has been written on top of it. This is the most likely useful
outcome of step 3; treat it as a success, not an obstacle.
