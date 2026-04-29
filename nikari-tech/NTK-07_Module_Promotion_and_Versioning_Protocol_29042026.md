# NTK-07 — Module Promotion and Versioning Protocol

**File:** NTK-07_Module_Promotion_and_Versioning_Protocol.md  
**Status:** Working standard — founder confirmed, pending GitHub commit  
**Owner:** Nikari Tech  
**Layer:** Module Governance / Package Promotion / Versioning Governance  
**Purpose:** Defines how Nikari Tech identifies, classifies, promotes, versions, documents, changes, deprecates, and reviews reusable modules and packages inside `nikari-platform`, especially when moving proven product-specific organs out of `packages/vertical/` into shared package families.  
**Read with:** UNIVERSAL_DECISIONS.md, NTK-00 (Master Intent), NTK-01 (Operating Model), NTK-02 (Guardrails), NTK-03 (Decision Log), NTK-04 (Monorepo Architecture), NTK-05 (Component and Contracts Architecture), NTK-06 (White Label Tenant and Deployment Model). Reference NTK_OUTLINE_SET_28042026.md only when checking the governed NTK-07 outline.  
**Supersedes / Subordinates:** Subordinate to UNIVERSAL_DECISIONS.md, NTK-00, NTK-01, and NTK-02. Complements NTK-04 and NTK-05. Expands the module guardrails in NTK-02. Does not weaken NTK-02. Does not authorise any Build OS assembly session, Cursor session, module promotion, package migration, or code change by itself.  
**Update trigger:** First package promoted out of `packages/vertical/`; first module extraction session; new package family proposed; module status model changed; versioning standard changed; compatibility matrix rule changed; deprecation rule changed; breaking package change; module promotion breach; or any NTK-01, NTK-02, NTK-03, NTK-04, NTK-05, NTK-06, NTK-08, NTK-09, or NTK-10 change affecting package promotion, reuse, classification, versioning, or module governance.

---

## Section 1 — Purpose

This document defines the module promotion and versioning protocol for Nikari Tech.

It exists because Nikari Tech is built on compounding reusable packages. Reusable modules are commercially valuable only when they are proven, documented, versioned, compatible, and governed. A folder of useful code is not yet a module. A product-specific organ is not automatically reusable. A pattern that works in one product must not become a platform rule merely because it looks efficient.

NTK-07 answers:

**When may product-specific logic become a shared module, what proof is required, how is that module documented and versioned, and how are future changes controlled without breaking products or weakening product truth?**

This document is governance. It is not a Build Plan. It does not open Cursor. It does not create or move packages. It does not write code, migrations, tests, README files, version files, schemas, examples, or compatibility matrices. It defines the standard that later Build OS and Developer OS sessions must consume when preparing module extraction, module promotion, package change, or versioning work.

### What this document governs

This document governs:

- when a product-specific organ may be considered for promotion;
- the core rule for module promotion;
- module status labels;
- module classification;
- the promotion test;
- the required module file set;
- README requirements;
- implementation guide requirements;
- versioning standards;
- change control;
- compatibility matrices;
- promotion logs;
- deprecation rules;
- extraction review at session close;
- anti-error rules; and
- update triggers.

### What this document does not govern

This document does not govern:

- product lane assignment — see NTK-01;
- product intake, SCOPING.md, lifecycle gates, or delivery modes — see NTK-01;
- hard guardrails and anti-drift rules — see NTK-02;
- the decision register and supersession discipline — see NTK-03;
- monorepo repo structure and app/package placement — see NTK-04;
- contracts, Joints, dependency direction, and component hierarchy — see NTK-05;
- white-label tenant and deployment model — see NTK-06;
- AI assistant authority and HITL standards — see NTK-08 when produced;
- internal knowledge-layer standards — see NTK-09 when produced; or
- product portfolio routing — see NTK-10 when produced.

### Lane 4 boundary

Lane 4 shared module development remains governed by NTK-01.

NTK-07 is a prerequisite for formal module promotion out of `packages/vertical/`, but it does not authorise Lane 4 work by itself.

Formal module promotion still requires:

- extraction review identifying the candidate;
- concept or promotion note, where required;
- correct lane assignment under NTK-01;
- SCOPING.md or approved Build OS scope for the promotion task;
- `contracts/` and Joint review under NTK-05;
- Build OS readiness and risk classification;
- founder approval for Version Promotion;
- no Cursor session opened until Build OS has produced and founder-approved the relevant Build Plan.

### Relationship to `packages/vertical/`

`packages/vertical/` is the correct home for product-specific organs before they are proven reusable.

NTK-07 does not treat `vertical/` as a temporary mistake. It treats `vertical/` as a disciplined proving ground.

A module may move out of `vertical/` only when it has passed the promotion test in this document. Until then, it remains product-specific, even if it appears reusable.

---

## Section 2 — Core Rule

The core rule is:

> **Promote only what has worked in a real product or serious pilot. Do not promote experiments as stable modules.**

A reusable package is not created by naming it well. It is created by proof, documentation, stable interfaces, version discipline, tests, and compatibility awareness.

The purpose of module promotion is not to make the codebase look tidy. The purpose is to preserve and multiply working value across products without weakening the product truth that created the value in the first place.

### What the core rule protects

This rule protects Nikari Tech from two errors.

First, it prevents **premature abstraction**. A product-specific workflow should not become a shared module before it has proven that the underlying pattern is genuinely reusable.

Second, it prevents **module fragmentation**. If every product keeps useful logic locked inside its own vertical folder forever, Nikari Tech loses compounding value and becomes a collection of separate builds.

Both errors are failures.

### Correct default posture

The correct default posture is:

1. Build product-specific truth in `packages/vertical/[product]/`.
2. Document patterns that may later become reusable.
3. Reassess during Stage 9 Extraction Review.
4. Promote only after proof, documentation, contracts, tests, versioning, and founder approval.
5. Keep uncertain modules in `vertical/` or mark them as extraction candidates.

### What counts as proof

Proof may come from:

- successful use in a real product;
- successful use in a serious pilot with realistic data, users, workflow, and risk conditions;
- repeated need across more than one product or tenant;
- clear evidence that the module solves a platform-level problem rather than a one-product problem; or
- founder-confirmed strategic value where the module is intentionally built as net-new shared infrastructure under Lane 4.

A prototype alone is not enough proof for stable promotion.

A single internal demo is not enough proof for stable promotion.

A useful folder of code is not enough proof for stable promotion.

### Promotion never weakens product truth

NTK-02 remains controlling: product correctness comes before reuse.

If promotion would flatten domain language, weaken workflow truth, increase complexity, reduce tenant safety, distort UX, hide compliance needs, or create vague generic behaviour, the module must stay in `vertical/` until the reusable boundary is clearer.

---

## Section 3 — Module Status Labels

Every module, organ, extraction candidate, or shared package must have a status label.

No module may be treated as stable without a status.

For promoted modules and shared packages, the status label must appear in the module README and VERSION file. Where a module is included in a package index, component library index, compatibility matrix, or promotion log, the same status must be recorded there.

For extraction candidates that have not yet been promoted, the status may be recorded in `EXTRACTION_CANDIDATE.md` or the extraction review note. Extraction candidates do not require the full promoted-module file set until promotion is approved.

### Status label summary

| Status | Meaning | May be used across products? | May be relied on as stable? |
|--------|---------|------------------------------|------------------------------|
| `experimental` | Early module or pattern under exploration | No, unless explicitly scoped | No |
| `pilot-proven` | Worked in a serious pilot or controlled product context | Limited, with Build OS approval | No |
| `reusable` | Approved for reuse with documented constraints | Yes, within compatibility rules | Partially |
| `stable` | Approved, versioned, documented, tested, and safe for standard reuse | Yes | Yes |
| `deprecated` | Still present but should no longer be used for new work | Only for existing consumers during transition | No new reliance |

### `experimental`

An experimental module is an early-stage package, organ, or extraction candidate that may be technically useful but is not yet proven.

Experimental modules may exist. They must be labelled clearly.

Experimental modules must not be imported into production products or client deployments unless the Build Plan explicitly scopes the risk, founder approval is recorded, and the module remains isolated.

**Required wording in README:**

```text
Status: experimental — not approved for standard reuse.
```

### `pilot-proven`

A pilot-proven module has worked in a serious pilot or controlled product context.

It has evidence of usefulness, but it has not yet met the full standard for general reuse.

Pilot-proven modules may be reused only where Build OS confirms the compatibility and risk posture in the Build Plan.

**Required wording in README:**

```text
Status: pilot-proven — reuse requires Build OS compatibility confirmation.
```

### `reusable`

A reusable module has passed the promotion test and may be used across products or tenants within stated constraints.

It has documentation, versioning, a defined Joint where applicable, and a compatibility matrix.

Reusable does not necessarily mean stable for every context. It means the module is approved for reuse under documented conditions.

**Required wording in README:**

```text
Status: reusable — approved for reuse within the documented compatibility constraints.
```

### `stable`

A stable module is a reusable module that has matured enough to become standard platform infrastructure.

It has:

- clear purpose;
- complete required file set;
- tested happy, failure, and integration paths appropriate to risk;
- version history;
- compatibility matrix;
- no unresolved critical defects;
- documented migration guidance for prior versions; and
- founder-confirmed status where the module becomes standard platform infrastructure, forms part of formal Version Promotion, or affects active products.

Stable modules are the default import choice where the use case fits.

**Required wording in README:**

```text
Status: stable — approved as standard platform module for compatible use cases.
```

### `deprecated`

A deprecated module remains present because existing consumers still rely on it, but it should not be used for new work.

Deprecation requires a reason, a replacement path where possible, and a migration period unless founder-approved immediate removal is required for safety.

**Required wording in README:**

```text
Status: deprecated — do not use for new work. See deprecation notice and migration path.
```

### Status changes

A status change is a governance event.

- `experimental` to `pilot-proven` requires evidence of serious use.
- `pilot-proven` to `reusable` requires the promotion test.
- `reusable` to `stable` requires maturity evidence and compatibility confirmation.
- Any status to `deprecated` requires a deprecation notice.
- Any downgrade requires a change-control note and compatibility review.

Status changes into `reusable` or `stable` are promotion governance events. Build OS may confirm compatibility, readiness, tests, and documentation, but founder approval is required where the status change forms part of formal Version Promotion, affects active products, or makes the module standard platform infrastructure.

Status changes must be recorded in `CHANGELOG.md` and the Promotion Log where applicable.

---

## Section 4 — Module Classification

Every module must be classified as one of:

- `generic`;
- `hybrid`; or
- `specific`.

Classification answers a different question from status.

Status asks: **How mature is this module?**

Classification asks: **How broadly should this module apply?**

A stable module may still be specific. A generic module may still be experimental. The two labels must not be confused.

### `generic`

A generic module is product-agnostic and can be used across multiple products without carrying the language, assumptions, or workflow of one product.

Examples may include:

- error formatting;
- audit logging;
- tenant ID resolution;
- role checking;
- feature gating;
- subscription-state reading;
- standard UI primitives;
- generic file upload boundaries.

Generic modules usually belong in shared package families such as:

- `packages/contracts/`;
- `packages/primitives/`;
- `packages/core/`;
- `packages/data/`;
- `packages/auth/`;
- `packages/security/`;
- `packages/commercial/`;
- `packages/integrations/`.

### `hybrid`

A hybrid module contains a reusable core with product-specific configuration, adapters, labels, copy, workflow options, or vertical overlays.

Hybrid modules are common in Nikari Tech because different products may share a workflow shape but require product-specific language and configuration.

Examples may include:

- white-label branding engine with tenant-specific configuration;
- generic enquiry intake with real-estate-specific fields as an adapter;
- notification workflow with product-specific templates;
- billing organ with product-specific plans;
- dashboard shell with product-specific cards.

Hybrid modules require special care. The reusable core may belong in a shared package, while the product-specific adapter remains in `packages/vertical/[product]/`.

The promotion decision must state exactly which part is being promoted.

### `specific`

A specific module is tied to a product, client, domain, legal context, workflow, or commercial structure.

Specific modules belong in:

```text
packages/vertical/[product]/
```

or, where a client-specific white-label deployment requires it:

```text
packages/vertical/[client-or-product]/
```

Specific modules should not be promoted to a shared package merely because another product may later need something similar.

They may become extraction candidates only after the reusable boundary is proven.

### Classification rule

When classification is uncertain, classify narrower first.

A module can move from specific to hybrid, or from hybrid to generic, only after proof.

It should not move from generic back to specific unless the original promotion was wrong or the product truth was flattened. If that happens, record the correction through CHANGELOG.md, the Promotion Log, and NTK-03 if the decision is architecture-relevant.

---

## Section 5 — Promotion Test

A module may be promoted only if it passes the six-question promotion test.

If any answer is “no” or “unclear”, the module must not be promoted as reusable or stable. It may remain in `packages/vertical/`, be labelled as an extraction candidate, or be treated as experimental until the gap is resolved.

### The six questions

#### Question 1 — Has the module worked in a real product or serious pilot?

The module must have been used in a real product, serious pilot, or founder-approved shared module build.

Evidence may include:

- product usage;
- pilot usage;
- test record;
- integration record;
- user or operator feedback;
- repeated need across products;
- Build OS extraction review; or
- founder-approved strategic shared-module decision.

If there is no evidence of real use, the module may be experimental only.

#### Question 2 — Is the module responsibility clear and narrow?

The module must have one clear purpose.

The name must describe the responsibility without needing “and” language.

If the module handles unrelated concerns, it must be split before promotion.

Examples of unclear scope:

- auth-and-billing-manager;
- tenant-loader-and-feature-gates;
- admin-dashboard-and-reporting;
- property-search-and-lead-routing.

If a module needs multiple responsibilities, it is probably a Level 3 composite wiring Level 2 organs, not a single module.

#### Question 3 — Does promotion preserve product truth?

Promotion must not weaken the product, client, tenant, legal, commercial, or user reality that created the module.

Check whether promotion would flatten:

- domain language;
- workflow sequence;
- role boundaries;
- compliance requirements;
- tenant separation;
- UX expectations;
- commercial logic;
- product-specific rules.

If promotion would weaken truth, keep the product-specific part in `vertical/` and promote only the genuinely reusable core.

#### Question 4 — Are contracts, Joints, dependencies, and side effects explicit?

The module must declare:

- input types;
- output types;
- Joint, where applicable;
- dependencies;
- side effects;
- tenant assumptions;
- role assumptions;
- data access assumptions;
- audit/logging assumptions; and
- failure modes.

Shared types and Joints must live in `packages/contracts/`.

No promoted module may rely on hidden product assumptions.

#### Question 5 — Is the required file set complete?

The module must include the required module file set defined in Section 6.

Where a file is not applicable, the module must state why it is not applicable rather than silently omitting the concern.

A module without documentation, version, status, changelog, implementation guidance, and compatibility information cannot be promoted as reusable or stable.

#### Question 6 — Are compatibility, versioning, and change impact understood?

The module must identify:

- current version;
- expected consumers;
- compatible product/app contexts;
- incompatible contexts;
- breaking-change risks;
- migration needs;
- required environment variables;
- schema dependencies;
- related packages; and
- known limitations.

If the impact of reuse is unknown, the module is not ready for promotion.

### Promotion test result labels

Use one of the following results:

| Result | Meaning | Required action |
|--------|---------|-----------------|
| PASS — promote | All six questions pass | Proceed to Build OS promotion planning |
| PASS WITH CONSTRAINTS | Passes but with stated compatibility limits | Promote only within constraints |
| HOLD — needs proof | Useful but not proven | Keep in `vertical/` or label extraction candidate |
| HOLD — needs split | Scope too broad | Split before promotion |
| HOLD — needs docs/version/tests | Governance file set incomplete | Complete before promotion |
| REJECT | Not reusable or damages product truth | Keep specific or archive candidate |

### Promotion test template

```md
## Promotion Test — [module name]

**Current location:** packages/vertical/[product]/[module]/  
**Proposed location:** packages/[family]/[module]/  
**Current status:** [experimental / pilot-proven / reusable / stable / deprecated]  
**Proposed status:** [status]  
**Classification:** [generic / hybrid / specific]  
**Review date:** [date]  
**Reviewed by:** [Build OS / Founder / Nikari Tech]

1. Real product or serious pilot proof: PASS / HOLD / REJECT — [notes]
2. Clear and narrow responsibility: PASS / HOLD / REJECT — [notes]
3. Product truth preserved: PASS / HOLD / REJECT — [notes]
4. Contracts, Joints, dependencies, side effects explicit: PASS / HOLD / REJECT — [notes]
5. Required file set complete: PASS / HOLD / REJECT — [notes]
6. Compatibility, versioning, and change impact understood: PASS / HOLD / REJECT — [notes]

**Result:** PASS / PASS WITH CONSTRAINTS / HOLD / REJECT  
**Founder decision required:** Yes / No  
**Next action:** [promote / keep in vertical / split / document / retest / reject]
```

---

## Section 6 — Required Module File Set

A promoted module must have a complete file set.

The required file set exists to prevent loose code from becoming platform infrastructure.

### Standard file set

A promoted module must include:

```text
[module-root]/
  README.md
  SPEC.md
  IMPLEMENTATION_GUIDE.md
  CHANGELOG.md
  VERSION.md
  CONFIG.example.md
  schema/
  examples/
  src/
```

### Required files

| File / Folder | Required? | Purpose |
|---------------|-----------|---------|
| `README.md` | Always | Human-readable purpose, status, classification, usage, boundaries |
| `SPEC.md` | Always for Level 2/3 organs and promoted packages | Formal module specification, Joint, responsibilities, risk notes |
| `IMPLEMENTATION_GUIDE.md` | Always | How to use, configure, import, test, and safely adopt the module |
| `CHANGELOG.md` | Always | Append-only version and change history |
| `VERSION.md` | Always | Current version, status, compatibility posture, owner |
| `CONFIG.example.md` | Required unless no configuration exists | Safe example configuration without secrets |
| `schema/` | Required where schema, migrations, policies, tables, types, or storage rules apply | Data and database-related artefacts |
| `examples/` | Required where usage examples materially reduce misuse risk | Safe usage examples and anti-examples |
| `src/` | Always for implementation modules | Source code location |

### Where a file is not applicable

Some modules will not need a schema, config, or examples folder.

Where a file or folder is not applicable, the README or IMPLEMENTATION_GUIDE must state this clearly.

Examples:

```text
No schema/ folder is required. This module does not create tables, policies, storage buckets, or migrations.
```

```text
No CONFIG.example.md is required. This module accepts no runtime configuration beyond typed inputs from contracts/.
```

Silent omission is not allowed.

### Minimum for extraction candidates

An extraction candidate that has not yet been promoted does not need the full file set immediately.

Minimum extraction candidate record:

```text
EXTRACTION_CANDIDATE.md
```

or an extraction review note containing:

- current location;
- reason for candidate status;
- evidence of reuse potential;
- product contexts where observed;
- likely target package family;
- risks;
- missing proof or documentation;
- recommended next action.

An extraction candidate is not a promoted module.

### Secrets and configuration safety

No required file may contain real secrets, API keys, credentials, service role keys, tokens, webhook secrets, private endpoints, or production client values.

`CONFIG.example.md` must show safe placeholder values only.

---

## Section 7 — README Requirements

Every promoted module requires a README.md.

The README is the first human-readable explanation of the module. It must allow a future Build OS, Developer OS, Cursor, reviewer, or developer to understand what the module is, what it is not, when to use it, and when not to use it.

### Required README structure

```md
# [Module Name]

## Status

## Classification

## Purpose

## What this module does

## What this module does not do

## When to use this module

## When not to use this module

## Package family and level

## Public interface / Joint

## Dependencies

## Configuration

## Tenant / auth / role assumptions

## Data and side effects

## Compatibility

## Examples

## Known limitations

## Version

## Owner / governing document
```

### Status section

The Status section must state:

- current status label;
- version;
- date of status assignment;
- who approved or recorded the status;
- whether reuse is unrestricted, constrained, or not approved.

Example:

```md
## Status

Status: reusable  
Version: v1.0  
Approved: [date / founder confirmation / Build OS promotion record]  
Reuse posture: approved for compatible products listed in the compatibility matrix.
```

### Classification section

The Classification section must state whether the module is:

- generic;
- hybrid; or
- specific.

For hybrid modules, the README must distinguish the reusable core from product-specific adapters.

### Purpose section

The Purpose section must be short and precise.

It should answer:

**What one job does this module do?**

If the purpose requires multiple unrelated sentences, the module may be too broad.

### What this module does

This section lists the module’s actual responsibilities.

Responsibilities must match the SPEC.md and implementation guide.

### What this module does not do

This section prevents scope creep.

It should list adjacent responsibilities that belong elsewhere.

Example:

```md
This module resolves tenant identity. It does not enforce billing entitlements, perform authentication, or render tenant UI.
```

### When to use / when not to use

Every README must include both positive and negative usage guidance.

A reusable module is safe only when future users know its boundaries.

### Package family and level

The README must state:

- package family;
- component level under NTK-05;
- whether it is a Level 1A primitive, Level 1B primitive, Level 2 organ, or Level 3 composite;
- import posture;
- whether apps should import it directly or through a composite.

### Public interface / Joint

The README must identify the module’s public interface or Joint.

If no Joint is required, the README must explain why.

For Level 2 and Level 3 modules, the Joint must be defined in `contracts/interfaces/` before implementation.

### Dependencies

The README must distinguish:

- internal dependencies;
- lower-level package dependencies;
- contracts dependencies;
- external service dependencies;
- optional integrations.

No sideways dependency may be hidden.

### Tenant / auth / role assumptions

If the module touches tenant-owned data, auth, roles, permissions, billing, admin functions, data export, AI outputs, or external clients, the README must state the assumptions clearly.

If tenant or auth does not apply, state that explicitly.

### Data and side effects

The README must state whether the module:

- reads data;
- writes data;
- mutates state;
- calls external APIs;
- sends messages;
- creates logs;
- triggers webhooks;
- affects permissions;
- changes billing state;
- affects AI output authority.

Side effects must not be hidden.

### Known limitations

A module without known limitations is either unusually mature or poorly documented.

Known limitations should be explicit, especially for pilot-proven and reusable modules.

---

## Section 8 — Implementation Guide Requirements

Every promoted module requires an IMPLEMENTATION_GUIDE.md.

The implementation guide is not a marketing description. It is the operational guide for safely using the module in a product, client deployment, or package assembly.

### Required implementation guide structure

```md
# [Module Name] — Implementation Guide

## Pre-use checklist

## Required reads

## Import path

## Required contracts and Joints

## Configuration steps

## Environment variables

## Schema / migration requirements

## RLS / security requirements

## Tenant requirements

## Billing / entitlement requirements

## AI / knowledge-layer requirements

## Testing requirements

## Common implementation mistakes

## Rollback / removal notes

## Upgrade notes
```

### Pre-use checklist

The pre-use checklist must confirm:

- module status and version checked;
- compatibility matrix checked;
- relevant NTK documents read;
- required contracts/Joints present;
- required dependencies present;
- risk class identified;
- Build OS has included the module in the Build Plan where required.

### Required reads

The guide must list required documents before use.

Examples:

- NTK-01 for lane and lifecycle;
- NTK-02 for guardrails;
- NTK-05 for contracts and dependency direction;
- NTK-06 if tenant or white-label behaviour applies;
- NTK-08 if AI authority applies;
- NTK-09 if knowledge-layer behaviour applies;
- module README, SPEC, VERSION, CHANGELOG, and compatibility matrix.

### Import path

The guide must state the allowed import path.

It must also state any prohibited import path, such as reaching into internal files.

Example:

```md
Allowed: import { resolveTenant } from "@nikari/data/tenant-resolver";
Prohibited: import from internal helper files not exported by the module Joint.
```

### Required contracts and Joints

The guide must list required types, interfaces, constants, and Joints in `packages/contracts/`.

If the implementation requires a new shared type or interface, that must be routed through contract-first design before use.

### Configuration steps

The guide must provide safe configuration instructions without real secrets.

Configuration must be explicit enough that a future session does not guess.

### Schema / migration requirements

If schema changes are required, the guide must identify them.

It must not include unapproved production migrations as instructions to execute. Actual migration planning belongs to Build OS and Developer OS sessions.

### RLS / security requirements

Any auth, RLS, role, permission, admin, data export, tenant boundary, webhook, or secret-handling concern must be explicitly documented.

Security requirements must not be left to later hardening if the module depends on them.

### Tenant requirements

If a module is tenant-aware, the guide must state:

- tenant identity source;
- tenant-owned records;
- tenant isolation assumptions;
- server-side validation needs;
- admin override rules;
- cross-tenant leakage risks.

### Billing / entitlement requirements

If the module is gated by subscription, feature entitlement, module licensing, trial state, or billing status, the guide must state the relevant gating requirement.

### AI / knowledge-layer requirements

If the module uses AI output, retrieval, prompts, embeddings, knowledge documents, workflow guidance, or internal support answers, the guide must state that NTK-08 and/or NTK-09 applies when produced.

### Testing requirements

Testing requirements must match module risk.

At minimum, the guide should identify:

- unit tests;
- integration tests;
- failure-path tests;
- tenant-isolation tests where relevant;
- RLS tests where relevant;
- role-access tests where relevant;
- AI-output review tests where relevant;
- compatibility tests for consuming products.

### Common implementation mistakes

This section is mandatory.

It should capture known failure patterns so future Cursor or developer sessions do not repeat them.

### Rollback / removal notes

The guide must explain how to safely remove or disable the module if an implementation fails.

For high-risk modules, rollback requirements must be included in the Build Plan.

### Upgrade notes

The guide must explain how future versions should be adopted and what to check before upgrading.

---

## Section 9 — Versioning Standard

Nikari Tech uses explicit module versioning for every reusable package, promoted organ, and formal module.

A module without versioning is not stable.

### Version format

Use the format:

```text
vMAJOR.MINOR.PATCH
```

Examples:

```text
v0.1.0
v1.0.0
v1.1.0
v1.1.1
v2.0.0
```

For shorthand in governance documents, `v0.x`, `v1.0`, `v1.1`, and `v2.0` may be used, but VERSION.md must use the full version format.

### Version meaning

| Version | Meaning |
|---------|---------|
| `v0.x.x` | Experimental, candidate, or pilot-stage module. Not stable. |
| `v1.0.0` | First approved reusable version. Promotion approved. |
| `v1.1.0` | Non-breaking feature addition or compatible expansion. |
| `v1.1.1` | Patch fix that does not change interface or expected behaviour. |
| `v2.0.0` | Breaking structural change, interface change, Joint change, schema change, or behaviour change requiring migration. |

### `v0.x.x` — experimental and pilot versions

Use `v0.x.x` for:

- experimental modules;
- extraction candidates;
- pilot-proven modules not yet approved for standard reuse;
- serious pilot modules;
- modules still missing full documentation or compatibility proof.

`v0.x.x` modules must not masquerade as stable.

### `v1.0.0` — first approved reusable version

Use `v1.0.0` when a module first passes the promotion test and is approved for reuse.

The module must have:

- required file set;
- README;
- SPEC;
- implementation guide;
- CHANGELOG;
- VERSION;
- compatibility matrix;
- promotion log entry;
- status label;
- founder approval where required.

### `v1.1.0` — non-breaking compatible expansion

Use `v1.1.0`, `v1.2.0`, and similar for compatible additions that do not break existing consumers.

Examples:

- optional field added with safe default;
- new helper exported without changing existing interface;
- new supported configuration option;
- new example;
- additive compatibility expansion.

### `v1.1.1` — patch fix

Use patch versions for fixes that do not change the public interface, Joint, schema, expected behaviour, tenant assumptions, auth assumptions, or consumer contract.

Examples:

- bug fix preserving behaviour;
- documentation correction that does not alter governance meaning;
- test correction;
- minor internal refactor with no external effect.

### `v2.0.0` — breaking structural change

Use `v2.0.0` where a change breaks or materially affects consumers.

Breaking changes include:

- Joint change;
- public interface change;
- required input change;
- output shape change;
- schema change requiring migration;
- RLS behaviour change;
- auth or role assumption change;
- tenant isolation behaviour change;
- billing or entitlement behaviour change;
- AI authority or HITL behaviour change;
- removal of an export;
- change in side effects;
- change in failure behaviour that consumers rely on.

Breaking changes require:

- change-control note;
- compatibility matrix update;
- migration path;
- Build OS risk classification;
- founder approval where the change affects active products or stable modules.

### VERSION.md requirements

VERSION.md must include:

```md
# VERSION — [Module Name]

**Current version:** v[MAJOR.MINOR.PATCH]  
**Status:** [experimental / pilot-proven / reusable / stable / deprecated]  
**Classification:** [generic / hybrid / specific]  
**Approved by:** [Founder / Build OS / pending]  
**Date approved:** [date]  
**Compatible with:** [products / package versions / app contexts]  
**Breaking change from previous version:** Yes / No  
**Migration required:** Yes / No  
**Next review trigger:** [trigger]
```

### CHANGELOG.md requirements

CHANGELOG.md is append-only.

Each entry must include:

- version;
- date;
- status change, if any;
- change type;
- summary;
- breaking-change assessment;
- affected consumers;
- migration note;
- approval source.

Example:

```md
## v1.1.0 — 29 April 2026

**Change type:** Minor — non-breaking  
**Summary:** Added optional tenant label override.  
**Breaking change:** No  
**Affected consumers:** nre-admin, social-shield pilot  
**Migration required:** No  
**Approved by:** Build OS review / founder approval if required
```

---

## Section 10 — Change Control

Change control governs all changes to reusable modules after creation or promotion.

No change to a reusable or stable module is treated as “just a small edit” until it has been classified.

### Change categories

| Category | Meaning | Version impact | Approval posture |
|----------|---------|----------------|------------------|
| Documentation-only | Clarifies docs without changing behaviour | Patch if meaningful | Build OS or document review |
| Internal refactor | No public interface or behaviour change | Patch | Build OS risk classification |
| Patch fix | Fixes bug without changing interface | Patch | Build OS risk classification |
| Additive feature | Adds compatible optional capability | Minor | Build OS review; founder if high-risk |
| Behaviour change | Changes how consumers experience the module | Major unless proven non-breaking | Founder review likely |
| Interface / Joint change | Changes public contract | Major | Founder approval required |
| Schema / RLS / auth change | Affects data/security boundary | Major or high-risk patch | Build OS Tier 4/5 review and founder approval |
| Deprecation | Marks module or version for retirement | Status change | Founder or Build OS approval depending risk |
| Removal | Deletes module or export | Major / destructive | Founder approval required |

### Change-control checklist

Before changing a reusable or stable module, confirm:

- current version checked;
- status checked;
- classification checked;
- consumers identified;
- public Joint reviewed;
- contracts impact reviewed;
- compatibility matrix reviewed;
- tests identified;
- migration need assessed;
- risk class assigned;
- Build OS approval path identified;
- CHANGELOG entry planned;
- VERSION update planned where required.

### Consumer impact review

A reusable or stable module may have multiple consumers.

Before any change, the session must identify:

- apps importing the module;
- packages importing the module;
- vertical organs depending on it;
- tenant or client deployments relying on it;
- external integrations relying on it;
- tests covering consumer behaviour.

If consumers cannot be identified, the change must be treated as higher risk.

### Contract-first change rule

If a change affects shared types, interfaces, constants, or Joints, `packages/contracts/` must be updated first under NTK-05.

No package may silently change its public contract without a corresponding contracts review.

### Security-sensitive changes

Changes involving auth, RLS, tenant boundaries, billing, payments, webhooks, secrets, data export, admin permissions, AI authority, or public publishing require the applicable Build OS risk classification and review.

Security cannot be downgraded because the change appears small.

### Change approval

Build OS determines the risk classification in the Build Plan. Founder approval is required where NTK-01 or Build OS risk rules require it, especially for Stage 10 Version Promotion, breaking changes, production-impacting changes, and high-risk module changes.

---

## Section 11 — Compatibility Matrix

Every reusable or stable module must have a compatibility matrix.

The compatibility matrix records where the module is approved for use, where it is not approved, and what constraints apply.

The matrix may live in README.md, VERSION.md, COMPATIBILITY.md, or a central package index, provided it is clearly referenced from the README and VERSION file.

### Required compatibility fields

A compatibility matrix must include:

- module name;
- module version;
- status;
- classification;
- package family;
- component level;
- approved app consumers;
- approved package consumers;
- tenant-aware status;
- white-label safe status;
- AI-related status;
- knowledge-layer status;
- schema dependency;
- auth/RLS dependency;
- environment/config dependency;
- incompatible contexts;
- required tests;
- last verified date;
- next review trigger.

### Compatibility matrix template

```md
# Compatibility Matrix — [Module Name]

| Field | Value |
|-------|-------|
| Module | [name] |
| Version | v[MAJOR.MINOR.PATCH] |
| Status | experimental / pilot-proven / reusable / stable / deprecated |
| Classification | generic / hybrid / specific |
| Package family | packages/[family]/ |
| Component level | Level 1A / Level 1B / Level 2 / Level 3 |
| Approved app consumers | [apps] |
| Approved package consumers | [packages] |
| Tenant-aware | yes / no / not applicable |
| White-label safe | yes / no / conditional / not applicable |
| AI-related | yes / no / conditional |
| Knowledge-layer related | yes / no / conditional |
| Schema dependency | none / listed |
| Auth/RLS dependency | none / listed |
| Environment/config dependency | none / listed |
| Incompatible contexts | [list] |
| Required tests | [list] |
| Last verified | [date] |
| Next review trigger | [trigger] |
```

### White-label compatibility

A module marked white-label safe must not assume a single tenant, single brand, single domain, or single operator unless the assumption is explicitly configurable.

Where white-label compatibility is conditional, the condition must be stated.

Example:

```text
White-label safe: conditional — requires tenant_id validation and per-tenant config loaded server-side.
```

### AI and knowledge-layer compatibility

A module that touches AI prompts, retrieval, AI outputs, knowledge documents, SOPs, internal guidance, or generated content must identify whether NTK-08 or NTK-09 applies when produced.

A module is not AI-safe merely because it compiles.

### Last verified rule

A compatibility matrix must include `last_verified`.

If the module has not been verified within the relevant Build OS window, Build OS may require re-verification before use.

---

## Section 12 — Promotion Log

Every formal module promotion must be recorded in a Promotion Log.

The Promotion Log may exist as a central file for `nikari-platform`, as a package-family log, or as a module-level log, provided the location is consistent and referenced in the module README.

### Promotion Log purpose

The Promotion Log records:

- what moved;
- where it moved from;
- where it moved to;
- why it moved;
- what proof supported the move;
- who approved the move;
- what version was assigned;
- what compatibility constraints apply;
- what follow-up actions remain.

### Promotion Log is append-only

Promotion entries are append-only.

If a promotion was wrong, do not delete the entry. Add a later correction, reversal, deprecation, or supersession entry.

### Promotion Log entry template

```md
## [Date] — [Module Name] promoted to [target package family]

**Promotion ID:** PROMO-[YYYYMMDD]-[NN]  
**Module:** [module name]  
**Previous location:** packages/vertical/[product]/[module]/  
**New location:** packages/[family]/[module]/  
**Previous status:** [status]  
**New status:** [status]  
**Classification:** generic / hybrid / specific  
**Assigned version:** v[MAJOR.MINOR.PATCH]  
**Promotion result:** PASS / PASS WITH CONSTRAINTS  
**Proof source:** [product / pilot / extraction review / founder-approved shared module]  
**Approving authority:** Founder / Build OS / Nikari Tech decision  
**Affected products:** [list]  
**Affected packages:** [list]  
**Compatibility matrix updated:** Yes / No  
**Contracts / Joints updated:** Yes / No / Not applicable  
**Migration required:** Yes / No  
**NTK-03 entry required:** Yes / No  
**Notes:** [context]
```

### When NTK-03 is required

NTK-03 append entry is required where a promotion:

- creates a new package family;
- changes the package family map;
- changes module status standards;
- changes versioning standards;
- changes compatibility requirements;
- creates a strategic platform module;
- affects white-label, AI, knowledge-layer, or product portfolio posture;
- supersedes a previous Nikari Tech decision.

Routine promotion within an existing family may be recorded in the Promotion Log without NTK-03 if no architecture decision changes.

### Reversal entries

If a promotion is reversed, record a reversal entry.

```md
## [Date] — Promotion reversal: [Module Name]

**Original promotion ID:** PROMO-[YYYYMMDD]-[NN]  
**Reason for reversal:** [reason]  
**New location:** [vertical / deprecated / archived]  
**Consumer impact:** [impact]  
**Migration required:** Yes / No  
**Founder approval required:** Yes / No  
**Notes:** [context]
```

---

## Section 13 — Deprecation Rule

Deprecation is the governed process for marking a module, version, interface, export, schema pattern, or package as no longer preferred for new work.

Deprecation is not deletion.

A deprecated module may remain available for existing consumers during a transition period, but it must not be used for new work unless explicitly approved.

### When to deprecate

Deprecate a module or version when:

- a better replacement exists;
- the module has known limitations that make new use unsafe;
- the module has been superseded by a new version;
- the module no longer fits the package architecture;
- the module carries product-specific assumptions incorrectly promoted as generic;
- the module creates compatibility risk;
- the module creates security, tenant, billing, AI, or data-boundary risk;
- the module is no longer maintained.

### Deprecation notice requirements

A deprecation notice must include:

- module name;
- deprecated version or scope;
- date deprecated;
- reason;
- replacement module or version, if any;
- affected consumers;
- migration path;
- support period;
- removal conditions;
- approving authority;
- changelog entry reference.

### Deprecation notice template

```md
# Deprecation Notice — [Module Name]

**Deprecated version / scope:** [version or module]  
**Date deprecated:** [date]  
**Reason:** [reason]  
**Replacement:** [replacement or “none”]  
**Affected consumers:** [apps/packages]  
**Migration path:** [summary]  
**Support period:** [period or trigger]  
**Removal condition:** [condition]  
**Approved by:** [Founder / Build OS / Nikari Tech]  
**CHANGELOG reference:** [entry]
```

### Immediate deprecation

Immediate deprecation may be required where a module creates serious security, tenant isolation, data integrity, legal, billing, or AI-authority risk.

Immediate deprecation still requires documentation. Emergency action does not remove the need for a record.

### Removal after deprecation

Removal is a higher-risk action than deprecation.

Before removal:

- identify all consumers;
- confirm replacement path;
- confirm migration complete or unnecessary;
- update compatibility matrix;
- update CHANGELOG;
- update VERSION;
- record Build OS risk classification;
- obtain founder approval where active consumers, production use, destructive change, or breaking change exists.

### Deprecated modules and new work

A deprecated module must not be selected for new Build OS assembly unless:

- no replacement exists;
- risk is documented;
- founder approval is recorded; and
- the Build Plan states why temporary use is justified.

---

## Section 14 — Extraction Review at Session Close

Every Lane 1, Lane 2, Lane 3, or Lane 5 product delivery that produces product-specific logic must include an extraction review at session close where reusable logic may have emerged.

Extraction review is Stage 9 under NTK-01.

The purpose is not to promote immediately. The purpose is to identify whether any product-specific organs should become:

- no candidate;
- extraction candidate;
- future module candidate;
- immediate Lane 4 promotion candidate; or
- rejected as product-specific.

### Extraction review timing

Extraction review happens:

- after product assembly;
- after hardening where relevant;
- before the session handover is finalised;
- before any claim is made that a product-specific organ is reusable.

Extraction review does not replace NTK-07 promotion. It feeds into NTK-07.

### Extraction review questions

At session close, review:

1. Did any product-specific organ solve a problem likely to recur in another product?
2. Did the organ rely on product-specific language, workflow, schema, tenant posture, or commercial logic?
3. Could a reusable core be separated from a vertical-specific adapter?
4. Is there real use evidence or only theoretical reuse potential?
5. Which package family would be the likely target if promoted?
6. What contracts or Joints would be required?
7. What documentation, tests, compatibility checks, or versioning are missing?
8. Would promotion preserve product truth?
9. Does the organ touch tenant, auth, RLS, billing, AI, knowledge-layer, or external integration risk?
10. Should the item be rejected, watched, documented as candidate, or routed into a Lane 4 promotion session?

### Extraction review output

The session handover must include an Extraction Review section with one of the following outcomes:

| Outcome | Meaning |
|---------|---------|
| No extraction candidates | Nothing reusable identified |
| Candidate identified — hold | Potential exists but not enough proof |
| Candidate identified — document | Create EXTRACTION_CANDIDATE.md or candidate note |
| Candidate identified — route to Lane 4 | Promotion may be appropriate; open future Build OS planning |
| Rejected | Not reusable; keep vertical-specific |

### Extraction candidate record template

```md
## Extraction Candidate — [Name]

**Current location:** packages/vertical/[product]/[candidate]/  
**Observed in:** [product / pilot / session]  
**Candidate type:** generic / hybrid / specific / unclear  
**Likely target family:** packages/[family]/  
**Reason for candidate status:** [reason]  
**Evidence:** [real product / serious pilot / repeated need / founder strategic decision]  
**Product-specific assumptions:** [list]  
**Reusable core:** [if known]  
**Missing proof:** [list]  
**Risks:** [list]  
**Recommended next action:** hold / document / split / Lane 4 promotion review / reject
```

### No automatic promotion at session close

A product delivery session must not silently promote modules at close.

Promotion is a separate governed action unless it was already included in the approved Build Plan as a Lane 4 task with founder approval.

### Handover requirement

A handover that closes a relevant product or module session without extraction review is incomplete.

If no candidates exist, the handover must state:

```text
Extraction Review: completed — no candidates identified.
```

---

## Section 15 — Anti-Error Rules

These rules prevent the most common module governance failures.

### Anti-Error Rule 15.1 — No dumping ground

A package family must not become a dumping ground for code that does not clearly belong elsewhere.

**Error signal:** A module is moved into `packages/core/`, `packages/data/`, `packages/security/`, or another shared family because the team is unsure where to put it.

**Correct response:** Keep it in `packages/vertical/[product]/`, create an extraction candidate note, or route the classification question to Nikari Tech.

### Anti-Error Rule 15.2 — No premature abstraction

Do not abstract a product-specific workflow before it proves reusable.

**Error signal:** A module is made generic while still carrying product-specific rules, labels, assumptions, or workflow sequence.

**Correct response:** Keep the product-specific module in `vertical/`. Extract only the reusable core if clear.

### Anti-Error Rule 15.3 — No undocumented reuse

No module may be reused across products without documentation, status, version posture, and compatibility review.

**Error signal:** Cursor imports a useful folder from another product because it compiles.

**Correct response:** Stop. Check NTK-07 status, required file set, compatibility matrix, and Build OS approval path.

### Anti-Error Rule 15.4 — No module without owner, status, and version

Every module must have an owner or governing document, a status label, and a version posture.

**Error signal:** A package exists but no one can tell whether it is experimental, reusable, stable, or deprecated.

**Correct response:** Assign status and version before further use.

### Anti-Error Rule 15.5 — No promotion by folder move only

Moving files from `packages/vertical/` to another package family is not promotion.

Promotion requires the test, file set, versioning, compatibility matrix, promotion log, change control, and required approvals.

**Error signal:** A folder was moved and imports updated, but no README, VERSION, CHANGELOG, or Promotion Log entry exists.

**Correct response:** Reverse the move or complete the promotion process through Build OS.

### Anti-Error Rule 15.6 — No shared module that hides tenant assumptions

A tenant-aware or white-label-relevant module must not hide tenant assumptions.

**Error signal:** A module works in one tenant context but does not state whether it is safe for shared deployment, separate deployment, or hybrid use.

**Correct response:** Add tenant assumptions, NTK-06 compatibility, and isolation notes before reuse.

### Anti-Error Rule 15.7 — No breaking change without version bump

Breaking changes require version bump, changelog, compatibility review, and migration path.

**Error signal:** A public interface or Joint changes but the version remains unchanged.

**Correct response:** Stop. Reclassify the change and update versioning.

### Anti-Error Rule 15.8 — No package-family change without Nikari Tech decision

A new package family or major change to the family map is an architecture decision.

**Error signal:** Build OS or Cursor creates a new top-level package family for convenience.

**Correct response:** Escalate to Nikari Tech. Record the decision in NTK-03 if approved.

### Anti-Error Rule 15.9 — No client-specific request becoming universal law

A client-specific request must not change a shared module unless it passes the promotion and classification standards.

**Error signal:** A white-label client requirement changes a generic package for all products.

**Correct response:** Keep it in tenant configuration, client-specific vertical logic, or a hybrid adapter until proof exists.

### Anti-Error Rule 15.10 — No AI or knowledge-layer module promoted without specialised standards

AI assistant and knowledge-layer modules remain subject to NTK-08 and NTK-09 when produced.

**Error signal:** An AI or retrieval-related module is promoted as ordinary shared logic without HITL, authority, source, privacy, or retrieval rules.

**Correct response:** Hold promotion or classify it as experimental until the relevant AI or knowledge-layer standard applies.

---

## Section 16 — Update Triggers

This document must be reviewed and updated when any of the following occur.

### 16.1 First formal promotion out of `packages/vertical/`

Review NTK-07 before the first module is formally promoted out of `packages/vertical/`.

Confirm that:

- promotion test is sufficient;
- required file set is realistic;
- versioning standard is adequate;
- promotion log location is clear;
- compatibility matrix is sufficient;
- Build OS can consume the protocol.

### 16.2 New package family proposed

Any proposal to add a new package family requires NTK-07 review and likely NTK-03 entry.

The review must confirm whether the new family is genuinely needed or whether the concern belongs in an existing family, `contracts/`, primitives, a Level 3 composite, or `vertical/`.

### 16.3 Module status model changed

If the status labels change, NTK-07 must be updated.

Status changes may affect NTK-02, NTK-03, NTK-05, Build OS prompts, module readiness matrix, and package documentation.

### 16.4 Versioning standard changed

If the versioning standard changes, NTK-07 and affected module docs must be updated.

Where the change affects existing modules, a migration or compatibility note is required.

### 16.5 Compatibility matrix rule changed

If compatibility requirements expand or contract, NTK-07 must be updated.

This includes changes involving tenant safety, white-label compatibility, AI/knowledge-layer compatibility, package consumers, or Build OS readiness windows.

### 16.6 Deprecation or removal rule changed

If deprecation or removal rules change, NTK-07 must be updated before deprecated modules are removed or new deprecation posture is applied.

### 16.7 Breaking package change occurs

Any breaking change to a stable or reusable package must trigger NTK-07 review to confirm whether the change-control and versioning standards were sufficient.

### 16.8 Module promotion breach occurs

If a module is promoted prematurely, reused without documentation, imported without compatibility review, changed without version bump, or moved without promotion log, NTK-07 must be reviewed and patched if the breach reveals a governance gap.

### 16.9 NTK-01 to NTK-06 changes affect module promotion

Review NTK-07 when:

- NTK-01 changes Lane 4, Module Extraction, Stage 9, or Stage 10;
- NTK-02 changes module guardrails;
- NTK-03 changes decision-log requirements;
- NTK-04 changes package placement or monorepo structure;
- NTK-05 changes component levels, contracts, Joints, dependency direction, or package family map;
- NTK-06 changes white-label package implications.

### 16.10 NTK-08 or NTK-09 changes module implications

When NTK-08 or NTK-09 is produced, review NTK-07 for AI assistant and knowledge-layer module promotion implications.

AI-related or knowledge-layer modules may require additional promotion criteria beyond ordinary package rules.

### 16.11 NTK-10 changes product portfolio routing

When NTK-10 is produced, review whether product portfolio status affects extraction candidates, module pilots, and reusable package sequencing.

### 16.12 NTK-03 append entries after founder confirmation

After founder confirmation of NTK-07, NTK-03 should receive append entries for any module-promotion decisions the founder wants recorded as discrete Nikari Tech decisions. At minimum, the adoption of NTK-07 as the formal module promotion authority should be recorded.

Likely NTK-03 entries include:

1. Formal module promotion requires NTK-07.
2. Promotion requires real product or serious pilot proof.
3. Module status labels adopted.
4. Module classification model adopted.
5. Required module file set adopted.
6. Versioning standard adopted.
7. Compatibility matrix and promotion log required.
8. Deprecation rule adopted.

These entries should remain separate if recorded, because they govern different parts of the module lifecycle.

---

*Version: 1.0 — working standard*  
*Produced: Nikari Tech — NTK-07 Module Promotion and Versioning Protocol Session, 29 April 2026*  
*Approved by: Wiets Marais — 29 April 2026*  
*Read with: UNIVERSAL_DECISIONS.md, NTK-00, NTK-01, NTK-02, NTK-03, NTK-04, NTK-05, NTK-06*  
*Next update trigger: See Section 16*  
*Proposed repo location: `wietsmarais/docs/architecture/NTK-07_Module_Promotion_and_Versioning_Protocol.md`*
