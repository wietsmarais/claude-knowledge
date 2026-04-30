# Build OS — SCOPING.md
# Version: 1.1 — 30 April 2026
# Status: WORKING STANDARD — Patch 02 absorbed; ready for founder confirmation and commit
# Produced in: Developer OS — Build OS scoping session (Session 4, 27 April 2026)
# Independent review: ChatGPT (two rounds, same session)
# Canonical location when committed: wietsmarais/docs/build-os/BUILD_OS_SCOPING.md
# Live Claude reference copy: claude-knowledge/build-os/BUILD_OS_SCOPING.md
# This document governs: every Build OS build session, every assembly run
# This document is read before: every Build OS session, every module selection step
# This document is updated when: any architectural decision changes, any new module class is added, Build Plan schema changes, Build Manifest schema changes, or Build OS approval gates change

---

## Stage 1 Scoping — Status

| Blocker | Status |
|---------|--------|
| Stack confirmed by founder | ✅ Confirmed |
| Multi-tenant architecture confirmed | ✅ Confirmed — external-safe from day one |
| Executor scope defined | ✅ Confirmed — out of v1 execution |
| Build Plan schema defined | ✅ Confirmed — human-readable + Build Manifest |
| Module Readiness Matrix gate defined | ✅ Confirmed — structure locked, population pre-first-assembly |
| Approval tier model defined | ✅ Confirmed — five tiers |
| assembly_logs schema defined | ✅ Confirmed — audit/usage/execution grade |
| External-readiness trigger defined | ✅ Confirmed — measurable criteria |
| AI assistant delivery mode declared | ✅ Phase 1 — Path A (Claude Project) |
| Component library modules identified | ✅ Seven modules, classified |
| Security and white-label approach confirmed | ✅ Confirmed |
| RLS on every table from creation | ✅ Confirmed |


---

## Patch 02 Absorption Note — 30 April 2026

`PATCH_02_JOINT_DEFINITION_IN_BUILD_PLAN_28042026.md` has been absorbed into this Build OS scoping standard.

This version includes:

- the `Joint definition` row in the human-readable Build Plan schema;
- the `stage_label` Build Manifest field;
- the `joint_definition_required` Build Manifest field;
- the `joint_definition_status` Build Manifest field;
- the `contracts_status` Build Manifest object; and
- the Build Plan approval gate requiring Joint definition and `contracts/` status confirmation before ORGAN or COMPOSITE sessions open.

The patch file is now historical reference only once this document is committed and the live `claude-knowledge/build-os/BUILD_OS_SCOPING.md` copy is updated.

---

## Section 1 — Build OS v1 Definition

Build OS v1 is an internal proving harness with external-safe architecture posture.
It is not yet an external product.

Build OS is a governed build pipeline. It takes a high-level project specification,
selects relevant modules from the component library, applies tenant config, draws on
governed system prompts, enriches the Cursor/Claude Code prompt to architectural
depth, and produces a structured Build Plan for founder approval before any build
session opens.

Build OS v1 does not execute. The founder reviews the Build Plan and opens Cursor
against it manually. The Build Manifest inside the Build Plan defines the contract
the Executor will later consume in v2.

Build OS v1 is not a prompt relay tool. It is not a chatbot that helps write Cursor
prompts. It is a factory intake process: specification in, governed build artefact
out, human approval gate between them.

**What Build OS v1 is:**
- A governed Claude Project with structured inputs and outputs
- A module selector drawing on the component library
- A governed system prompt recommender (human-confirmed selection)
- A Build Plan producer (human-readable + machine-readable manifest)
- An assembly logger (every session logged to assembly_logs in Supabase)

**What Build OS v1 is not:**
- A build execution environment
- A prompt relay tool
- An Executor (v2)
- A client-facing product
- A replacement for Cursor, Claude Code, or the Developer OS

---

## Section 2 — Build Plan Schema

Every Build OS assembly session produces one Build Plan. The Build Plan has two
mandatory parts. Neither part is optional. A Build Plan without a Build Manifest
is incomplete and must not be approved.

### Part 1 — Human-Readable Build Plan

Sections in this order:

| Section | Contents |
|---------|----------|
| Project | Project name, repo, branch, active Claude project |
| Session goal | One sentence — what this build session will produce |
| Modules selected | List of component library modules in scope, with rationale |
| Joint definition | For each Level 2 organ or Level 3 composite in scope: input types, output types, dependencies, side effects — confirmed against contracts/interfaces/. Required when STAGE is ORGAN or COMPOSITE. Not required for CONTRACTS, PRIMITIVE, APP, or GOVERNANCE sessions. |
| Modules referenced but not assembled | Modules noted for context, not included in this session |
| Governed prompt used | Prompt name, version, source — confirmed by founder |
| Scope boundaries | What is explicitly in scope and out of scope for this session |
| Pre-session reads | Files Cursor or Claude Code must read before beginning |
| Risk classification | Overall risk class for this session (see Approval Tier Model) |
| Approval actions required | List of approval events required during execution |
| PLAN.md updates required | Tasks to be added before session opens |
| DECISIONS.md entries required | Decisions to be logged before or during session |
| Known gaps or unknowns | Dependencies not yet resolved — flagged, not ignored |
| Handover note | What the session handover must capture at close |

### Part 2 — Build Manifest (machine-readable)

Mandatory. Included in every Build Plan. Format: JSON.
The Executor will consume this format in v2. Defining it in v1 means no retrofitting.

```json
{
  "build_manifest_version": "1.0",
  "session_id": "<uuid>",
  "project_name": "<string>",
  "repo_url": "<string>",
  "branch_name": "<string>",
  "stage_label": "CONTRACTS | PRIMITIVE | ORGAN | COMPOSITE | APP | GOVERNANCE",
  "joint_definition_required": true,
  "joint_definition_status": "not_required | confirmed_existing | must_be_created_before_cursor",
  "contracts_status": {
    "interfaces_checked": true,
    "types_checked": true,
    "missing_contracts_block_session": true
  },
  "modules": [
    {
      "module_name": "<string>",
      "module_version": "<string>",
      "action": "assemble | adapt | reference",
      "files_affected": ["<path>"],
      "dependencies": ["<module_name>"]
    }
  ],
  "files_to_create": [
    {
      "path": "<string>",
      "source": "module | template | new",
      "risk_class": "low | medium | high | critical"
    }
  ],
  "files_to_modify": [
    {
      "path": "<string>",
      "change_description": "<string>",
      "risk_class": "low | medium | high | critical"
    }
  ],
  "governed_prompt": {
    "prompt_name": "<string>",
    "prompt_version": "<string>",
    "source": "<string>",
    "confirmed_by_founder": true
  },
  "approval_events": [
    {
      "event_id": "<uuid>",
      "action_description": "<string>",
      "tier": "1 | 2 | 3 | 4 | 5",
      "requires_second_model": true,
      "status": "pending"
    }
  ],
  "risk_class_overall": "low | medium | high | critical",
  "test_commands": ["<string>"],
  "rollback_plan": "<string>",
  "assembly_log_ref": "<uuid>"
}
```

---

## Section 3 — Module Readiness Matrix

### Purpose

No module is selectable by Build OS until it has passed the Module Readiness Matrix
gate. This is a hard gate. Build OS must not assemble from a module whose readiness
is unknown.

The completed matrix does not need to exist before Stage 1 closes.
The matrix structure and gate rule must exist before the first Build OS assembly session.
Populating the matrix is a pre-first-assembly task — it is not deferred to v2.

### Gate Rule

A module may be used in a Build OS assembly session only if:
- Its matrix row exists
- `reusable_as_is` is YES or `reuse_with_adaptation` is YES
- `test_status` is VERIFIED or TESTED
- `last_verified` is within the past 90 days

If a module fails the gate: it is listed as Referenced but not assembled in the
Build Plan, and the gap is flagged in the Known gaps section.

### Matrix Structure

| Column | Type | Description |
|--------|------|-------------|
| module_name | TEXT | Exact folder name from component library |
| version | TEXT | Semantic version — e.g. 1.0, 1.2 |
| status | TEXT | ACTIVE / DEPRECATED / DRAFT |
| reusable_as_is | BOOL | Can be assembled without modification |
| reuse_with_adaptation | BOOL | Can be assembled with documented adaptation |
| dependencies | TEXT | Comma-separated list of dependent modules |
| required_config | TEXT | Env vars, tenant config, or Supabase tables required |
| test_status | TEXT | VERIFIED / TESTED / UNTESTED |
| known_limits | TEXT | Any known constraints or incompatibilities |
| compatible_stack | TEXT | Next.js 14 App Router / plain HTML / both |
| tenant_aware | BOOL | Every query filters by tenant_id |
| toggle_ready | BOOL | Activatable per tenant by subscription tier |
| last_verified | DATE | Date of last confirmed working integration |
| owner | TEXT | Who maintains this module |
| notes | TEXT | Free text — anything not captured above |

### v1 Module Classification

Modules are classified into three tiers for Build OS v1:

**Tier 1 — Required for v1 assembly (must pass Module Readiness Matrix gate):**

| Module | Folder | Rationale |
|--------|--------|-----------|
| Security patterns | security/ | Every project, every session — non-negotiable |
| Database schema starter | database/ | Schema generation is core to Build OS |
| White-label tenant config | white-label/ | Required — multi-tenant architecture confirmed |
| Auth and access control | auth/ | Required for any product with users |
| UI components | ui-components/ | Core building block for every product build |
| Project management | project-management/ | PLAN.md, DECISIONS.md, LEARNINGS.md generation |
| AI safety and guardrails | ai-safety/ | Required before any AI feature |

**Tier 2 — Referenced but not assembled in v1 (available in v2):**

| Module | Folder | Reason for v1 exclusion |
|--------|--------|--------------------------|
| Stripe subscriptions | subscriptions/ | Deferred — v1 validates pipeline, not billing |
| Admin dashboard shell | admin/ | Deferred — v1 validates assembly, not admin UI |

**Tier 3 — Phase 2 additions (not in scope until v1 is proven):**
Any module not yet in the component library. Build OS does not create new modules —
it assembles from proven ones. New modules are extracted from proven project patterns
per the existing standard, then added to the component library, then become eligible
for Tier 1 or Tier 2 classification.

### Handling Module Conflicts

When two or more modules in scope for a single assembly session have conflicting
assumptions (e.g. different auth patterns, different role models, different Supabase
policy structures), Build OS must:

1. Flag the conflict explicitly in the Known gaps section of the Build Plan
2. Present the conflict to the founder with the two options and their trade-offs
3. Record the resolution in DECISIONS.md before the session opens
4. Never silently choose one pattern over another

---

## Section 4 — Approval Tier Model

Every action in a Build OS session is classified into one of five tiers.
The tier determines the approval event required before the action proceeds.
Approval tiers are declared in the Build Manifest and displayed in the
human-readable Build Plan.

### The Five Tiers

**Tier 1 — Documentation and governance artifacts**
Low risk. One approval covers the batch.
Examples: PLAN.md creation, DECISIONS.md entries, LEARNINGS.md updates,
session handover production, README updates, SCOPING.md production.
Approval event: Founder confirms Build Plan before session opens.

**Tier 2 — File writes and code generation**
Medium risk. One approval covers a diff plan — a listed summary of files
to be created or modified, with their content described before writing.
Cursor or Claude Code may not begin until the diff plan is confirmed.
Examples: New component files, route files, configuration files,
seed files, schema files that do not touch live data.
Approval event: Founder reviews and confirms diff plan section of Build Plan.

**Tier 3 — Git operations**
Medium-high risk. Separate approval required per push event.
Executor (v2) may not push without a distinct approval after file writes are complete.
In v1 (manual relay): founder reviews Cursor output before committing via GitHub Desktop.
Examples: git commit, git push, branch creation, PR creation.
Approval event: Explicit founder confirmation after Cursor session completes.

**Tier 4 — Supabase writes and updates**
High risk. Separate approval required per Supabase operation.
Executor (v2) may not insert or update without a distinct approval.
In v1: founder reviews proposed Supabase changes before opening Studio.
Examples: Schema migrations, RLS policy writes, table creation,
record inserts, record updates, storage bucket changes.
Approval event: Separate explicit confirmation. ChatGPT second-model review
required for all schema changes before approval is given.

**Tier 5 — Critical-path actions**
Highest risk. Separate approval required per action. Second-model verification
mandatory before any Tier 5 action is presented for approval.
The human approval gate fires after second-model verification, not before.

Critical-path actions explicitly include, at minimum:

- Authentication logic (any change to Supabase Auth config, session handling,
  JWT configuration, OAuth providers, or email/password settings)
- Row Level Security policies (any RLS policy creation, modification, or deletion
  on any table in any Supabase project)
- Data migrations (any operation that moves, transforms, or restructures
  existing data in a live or staging database)
- Payment and subscription logic (any Stripe integration, webhook handler,
  subscription status check, billing record, or pricing table change)
- Secrets and API key handling (any file that references, loads, rotates,
  or stores API keys, service role keys, environment variables, or credentials)
- Deletion and archival logic (any operation that deletes, soft-deletes,
  archives, or permanently removes user data, tenant data, or platform records)
- PII and tenant-boundary changes (any operation that moves, exposes, copies,
  or transforms personally identifiable information or crosses a tenant_id boundary)
- Production deployment actions (any Vercel production deployment trigger,
  environment variable change in production, or domain/DNS configuration change)

Approval event: Separate explicit confirmation after second-model review is complete
and the review output is shown to the founder. The founder approves the action
AND acknowledges the second-model review. Both are logged in assembly_logs.

---

## Section 5 — assembly_logs Schema

Table: `assembly_logs`
Supabase instance: to be confirmed at Phase 2 (Build OS has no Supabase instance yet;
schema is defined here so the table is correct on first creation)
RLS: enabled from creation. No assembly log is readable outside the tenant boundary.
tenant_id: mandatory on every row. No row without tenant_id.

```sql
CREATE TABLE assembly_logs (
  id                    UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id             UUID NOT NULL REFERENCES tenants(id),
  session_date          DATE NOT NULL,
  project_name          TEXT NOT NULL,
  repo_url              TEXT,
  branch_name           TEXT,
  commit_sha            TEXT,
  pull_request_url      TEXT,
  input_spec_hash       TEXT,           -- hash of the specification prompt used
  build_plan_id         UUID,           -- references the Build Plan document
  build_manifest_json   JSONB,          -- full Build Manifest from the Build Plan
  modules_used          TEXT[],         -- array of module names assembled
  module_versions       JSONB,          -- { "module_name": "version" } map
  prompt_name           TEXT,           -- governed system prompt used
  prompt_version        TEXT,
  prompt_versions_used  JSONB,          -- if multiple prompts, full map
  risk_class            TEXT NOT NULL,  -- low | medium | high | critical
  verification_status   TEXT,           -- passed | failed | not_required
  approval_status       TEXT NOT NULL,  -- pending | approved | rejected
  approval_event_id     UUID,           -- references approval event record
  approved_by_user_id   UUID,           -- FK to auth.users — not free text
  approved_at           TIMESTAMPTZ,
  executor_triggered    BOOLEAN DEFAULT FALSE,
  executor_actions      JSONB,          -- log of Executor actions if triggered (v2)
  execution_status      TEXT,           -- pending | in_progress | complete | failed
  error_log             TEXT,
  rollback_reference    TEXT,           -- branch, commit, or snapshot reference
  billing_event_id      UUID,           -- for per-assembly pricing (future)
  usage_event_id        UUID,           -- usage tracking (future)
  notes                 TEXT,
  created_at            TIMESTAMPTZ NOT NULL DEFAULT now(),
  updated_at            TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- RLS
ALTER TABLE assembly_logs ENABLE ROW LEVEL SECURITY;

CREATE POLICY "tenant_isolation" ON assembly_logs
  USING (tenant_id = ((auth.jwt() -> 'app_metadata' ->> 'tenant_id')::uuid));

-- No row without tenant_id
ALTER TABLE assembly_logs ALTER COLUMN tenant_id SET NOT NULL;
```

---

## Section 6 — External-Readiness Trigger

Build OS becomes eligible for external product deployment when all of the following
acceptance criteria are met. These criteria are locked at Stage 1 and may not be
lowered without a documented DECISIONS.md entry.

### Acceptance Criteria

**1. Volume threshold**
Minimum three successful internal assembly sessions covering three different build
types: new project start, mid-project feature session, and module extraction/session
handover. At least one session must cover a client-adjacent build (Flourish or
the first Counsel Phase 2 session).

**2. Build Plan correction rate**
The Build Plan required less than 20% founder correction in each qualifying session.
Correction includes: wrong module selected, wrong scope, missing dependency,
incorrect risk classification. Logged in assembly_logs notes field.

**3. Module selection accuracy**
Module selection was correct or defensibly incomplete (a gap was flagged explicitly
rather than silently ignored) in every qualifying session.

**4. Dependency identification**
Missing dependencies were identified by Build OS before the session opened,
not discovered during Cursor execution.

**5. Risk classification accuracy**
Every action in the Build Plan was classified at the correct tier or higher.
No Tier 4 or Tier 5 action was classified below its correct tier.

**6. Execution readiness**
Cursor or Claude Code could open the Build Plan and execute without requiring
major clarification. Minor clarification questions are acceptable. Structural
ambiguity is not.

**7. Governance artifact production**
Session handover, DECISIONS.md entries, and PLAN.md updates were produced
consistently across all qualifying sessions without founder intervention to
remind Build OS of its governance obligations.

**8. No governance contradiction**
No Build Plan introduced an architectural decision that contradicted
UNIVERSAL_DECISIONS.md or the project's DECISIONS.md. If a contradiction
was detected, Build OS flagged it before the session opened.

**9. Repeatability score**
A founder-assessed repeatability score of 4 out of 5 or higher across the
qualifying sessions. Scored on: consistency of Build Plan format, accuracy
of module selection, quality of risk classification, completeness of manifest.

**10. Module Readiness Matrix populated**
The matrix exists and every Tier 1 module has a verified row with last_verified
within 90 days.

### What Does Not Trigger External Deployment

- The Executor being built (Executor is v2 — it does not gate external product)
- A specific number of calendar days
- Founder satisfaction alone without the logged criteria above

### External-Readiness Trigger Decision

When all ten criteria are met, the commercial trigger is assessed in a Developer OS
strategy session. The external product decision is a founder decision, not an
automatic outcome. The criteria confirm readiness. The founder confirms the decision.

---

## Section 7 — Standard Stage 1 Blockers — Confirmed

### Stack

Phase 1 (v1): Claude Project — no code written in v1. Claude Project is the
Build OS interface. No stack decision required for v1 operation.

Phase 2 (when white-label UI is built): Standard primary workflow.
- Next.js 14 App Router
- TypeScript strict
- Tailwind CSS
- shadcn/ui
- Supabase v2 (npm package)
- Vercel Pro (GitHub auto-deploy)

### Multi-Tenant Architecture

Confirmed. External-safe architecture from day one.
Build OS v1 is internal-only in operation. It is multi-tenant-safe in architecture.
tenant_id on every Supabase table. RLS from creation. White-label config loaded
at runtime. No architectural decision in v1 forecloses the external path.

### Tenant Config Shape

Phase 1: not applicable — founder is the only operator.
Phase 2: standard white-label tenant config from component library (white-label/ module).
No custom tenant config shape required. Existing module applies directly.

### Subscription Tier Gating

Phase 1: not applicable.
Phase 2: tier gating confirmed as required. Must be scoped before Phase 2 build begins.
Not a blocker for v1 Stage 1. Flagged for Phase 2 scoping.

### Toggle Implementation

Build OS assembles modules that must themselves be toggle-ready. The toggle standard
applies to assembled modules, not to Build OS itself. Build OS enforces the existing
standard — it does not add or remove toggle requirements.

### Onboarding Flow

Phase 1: not applicable — founder only.
Phase 2: conversational onboarding — the standard. Not a blocker for v1.

### AI Assistant Delivery Mode

Phase 1: Path A — Claude Project, founder's own subscription.
Phase 2: Path B — Anthropic API, white-label UI, Nikari pays per token.
Cost estimate required in Phase 2 SCOPING.md. Not required today.

### Internal Knowledge Layer

Required. Build OS Claude Project knowledge base:
- Component library README (current version)
- cursor-prompts INDEX.md
- UNIVERSAL_DECISIONS.md
- Current Developer OS session handover
- SCOPING.md for any project being assembled in the current session
- Governed system prompt in use for this session

The Internal Knowledge Layer is the existing governance documentation.
It is not a new build requirement. It is what makes enrichment possible.

### Component Library Modules

Confirmed. Seven modules in three tiers. See Section 3.

### Security and White-Label

Security: RLS from creation on all tables. No secrets in AI context.
assembly_logs with tenant isolation and approval event logging.
Executor security constraints (v2): no write without prior read, no push to main,
all actions logged with approving_user_id.

White-label: white-label/ module from component library. Tenant config at runtime.
New tenant onboarded by config change only — no code change.

---

## Section 8 — Governed System Prompt Consumption

Phase 1 approach: human-confirmed selection.

Build OS identifies the relevant governed system prompt or prompt family for the
current build context and presents the recommendation to the founder with rationale.
The founder confirms the selection before the session opens. Build OS does not select
automatically in v1.

Transition to automatic selection: deferred until the formal Governed System Prompt
Library (Component Six of the AI Assistant Suite Module) is built in Supabase and
proven across five or more prompt selections with no founder correction.

Note: prompt portability across inference engines (e.g. Groq/Llama 4 as a Phase 2
production option) is a hypothesis to be tested at Phase 2 scoping. It is not an
architectural assumption and must not be treated as one until tested.

---

## Section 9 — What Build OS Is Not — Explicit Exclusions

These exclusions are locked. Future build sessions must not introduce features or
architecture that cross these lines without a new DECISIONS.md entry and a revision
to this SCOPING.md.

| Excluded | Reason |
|---------|--------|
| Autonomous execution | HITL is permanent — Build OS presents, human approves |
| Push to main or master | Executor (v2) targets feature branches only |
| Bulk data operations | Individual record operations only |
| PII in AI context | Privacy preservation — no PII through the AI layer |
| Cross-tenant data access | tenant_id boundary is enforced at every layer |
| Auto-publish or auto-send | Banned across all Nikari AI architectures |
| Replacement of UNIVERSAL_DECISIONS.md check | Build OS checks UNIVERSAL_DECISIONS.md before every architectural recommendation |
| Replacement of ChatGPT pre-commit review | The two quality gates (prompt precision, pre-commit AI review) are unchanged |

---

## Section 10 — Unresolved Questions — Flagged for Phase 2

These questions were identified during Stage 1 scoping. They are not blockers for
v1 Stage 1. They are flags — they must be answered at Phase 2 scoping and must not
be silently deferred beyond that session.

| Question | Phase 2 action required |
|---------|------------------------|
| First external user archetype | Define before external product architecture begins |
| Minimum external product definition | Is it a build-governance report, assisted setup, configurator, or self-serve app builder? |
| Failure path design | What does Build OS do when it cannot select a module or classify a risk? Halt / flag / escalate rules required |
| IP boundary | How much of the prompt library, module logic, and governance method is exposed to external clients? |
| Pricing model | Per-assembly, per-seat, or per-tenant — must not foreclose any option; multi-tenant architecture already enables all three |
| Expression 2 positioning | When does Build OS become the first instance of Expression 2 (Governed Orchestration Platform as a product)? Trigger and framing required |

---

## Section 11 — Decisions Logged

These decisions are made at Stage 1 and must be reflected in DECISIONS.md
in the Build OS repo when it is created.

| # | Decision | Rationale |
|---|---------|-----------|
| 1 | Build OS v1 is internal proving harness — external-safe architecture posture | Multi-tenant architecture from day one; no architectural decision forecloses external path |
| 2 | Executor is out of v1 execution | Coupling Executor development to Build OS v1 creates two unknowns. Pipeline format must be proven before Executor integration |
| 3 | Build Plan must include machine-readable Build Manifest from v1 | Retrofitting manifest format in v2 is the same category of mistake as retrofitting multi-tenancy |
| 4 | Approval tiers are five-tier model as defined in Section 4 | Single-gate approval insufficient for Tier 4 and Tier 5 actions |
| 5 | Tier 5 critical-path list is explicit — eight categories, not a general label | Future Cursor and Claude Code sessions must not narrow the definition |
| 6 | Module Readiness Matrix gate is mandatory before first assembly | Build OS must not assemble from modules of unknown quality |
| 7 | External-readiness trigger is ten-criteria measurable standard | "Three internal uses" was too weak — criteria must be logged and tested |
| 8 | Prompt portability is a hypothesis — not an architectural assumption | Must be tested at Phase 2 scoping before pricing or engine decisions depend on it |
| 9 | Phase 2 Supabase instance for Build OS is TBD | Build OS v1 runs as Claude Project — no Supabase instance required in v1 |
| 10 | UNIVERSAL_DECISIONS.md check fires before every architectural recommendation | Build OS does not exempt itself from the check hierarchy |

---

## Opening Prompt for First Build OS Build Session

```
Read the following before doing anything else, in this order:

1. BUILD_OS_SCOPING_27042026.md — this document
2. Component library README — current version
3. UNIVERSAL_DECISIONS.md — check before any architectural recommendation
4. Current Developer OS session handover
5. SCOPING.md for the project being assembled (if one exists)

Confirm:
- Module Readiness Matrix has been populated for all Tier 1 modules
- All Tier 1 modules have last_verified within 90 days
- assembly_logs table exists in Supabase with schema from Section 5

Today's goal: [state in one sentence]

Do not produce a Build Plan until the Module Readiness Matrix gate is confirmed.
Do not begin assembly until the governed system prompt for this session is confirmed by the founder.
For sessions with STAGE: ORGAN or STAGE: COMPOSITE — the Joint definition section must be complete and `contracts/` status confirmed before the Build Plan is approved.
Do not classify any action below its correct tier.
```

---

*Version: 1.1 — 30 April 2026 — Patch 02 absorbed*
*Produced: Developer OS — Build OS scoping session; Patch 02 absorbed in Build OS governance cleanup*
*Independent review: ChatGPT — two rounds — same session*
*Approved by: Wiets Marais — 27 April 2026; Patch 02 absorption pending founder confirmation / commit on 30 April 2026*
*Next update trigger: any Section 2, 4, 5, or 6 decision changes; any Build Plan or Build Manifest schema change; any new module tier added; Phase 2 scoping begins; external-readiness trigger criteria met*
*Canonical repo location: wietsmarais/docs/build-os/BUILD_OS_SCOPING.md*
*Live Claude reference copy: claude-knowledge/build-os/BUILD_OS_SCOPING.md*
