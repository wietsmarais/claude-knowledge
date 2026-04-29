# NTK-05 — Component and Contracts Architecture

**File:** NTK-05_Component_and_Contracts_Architecture.md  
**Version:** 1.1 — alignment draft  
**Date:** 29 April 2026  
**Status:** Working standard alignment draft — pending founder confirmation before commit  
**Owner:** Nikari Tech  
**Layer:** Build Architecture / Component Governance  
**Purpose:** Defines how components, contracts, package families, Joints, dependency direction, and package-level build sequencing work inside `nikari-platform`, while remaining subordinate to the Nikari Tech operating model and guardrails.  
**Read with:** UNIVERSAL_DECISIONS.md, NTK-00 (Master Intent), NTK-01 (Operating Model), NTK-02 (Guardrails), NTK-03 (Decision Log), NTK-04 (Monorepo Architecture). Reference NTK_OUTLINE_SET_28042026.md only when checking original document sequencing.  
**Supersedes / Subordinates:** Subordinate to UNIVERSAL_DECISIONS.md, NTK-00, NTK-01, and NTK-02. Complements NTK-04. Recorded and superseded through NTK-03 where Nikari Tech-specific decisions change. Future NTK-06, NTK-07, NTK-08, and NTK-09 expand specialised areas but do not weaken this document.  
**Update trigger:** First package built in `nikari-platform`; `contracts/` populated; new package family added; dependency-direction rule revised; Joint standard revised; seven-stage package protocol revised; NTK-06, NTK-07, NTK-08, or NTK-09 changes the package implications of white-label, module promotion, AI assistant, or knowledge-layer work.

---

## Section 1 — What this document governs

This document governs how components are designed, classified, built, connected, and prepared for reuse inside `nikari-platform`.

It defines:

- the four-element component system;
- the `contracts/` package;
- Level 1A UI primitives;
- Level 1B functional primitives;
- Level 2 single-function organs;
- Level 3 composite organs;
- dependency direction;
- the Joint definition standard;
- the package family map;
- how complete products are assembled from packages; and
- non-negotiable component and contract rules.

This document does **not** govern:

- product lane assignment — see NTK-01;
- product intake, SCOPING.md, lifecycle gates, or delivery modes — see NTK-01;
- hard guardrails and anti-drift rules — see NTK-02;
- the decision register and supersession discipline — see NTK-03;
- monorepo repo structure and deployment posture — see NTK-04;
- final white-label tenant and deployment model — see NTK-06 when produced;
- formal module promotion out of `packages/vertical/` — see NTK-07 when produced;
- AI assistant authority, HITL, and product standards — see NTK-08 when produced; or
- internal knowledge-layer product standards — see NTK-09 when produced.

### Alignment rule

NTK-05 defines the **package architecture**. It does not authorise a product build, a white-label deployment, a formal module promotion, an AI assistant product, or a knowledge-layer build by itself.

All product work must first be routed through NTK-01. All guardrails in NTK-02 apply. All Nikari Tech-specific decisions and supersessions are recorded through NTK-03. All app and monorepo placement is governed by NTK-04.

---

## Section 2 — The four-element system

The `nikari-platform` component system has four elements that must be understood as a whole before any build session opens.

### Element 1 — Contracts

The arteries. The shared language every component speaks.

`contracts/` is built first. It is never skipped. Every package imports shared types, interfaces, constants, and Joints from here.

### Element 2 — Level 1A: UI Primitives

Visual building blocks.

These are shadcn/ui components configured with Nikari Tech Tailwind tokens. They are small, single-purpose, and presentational only.

### Element 3 — Level 1B: Functional Primitives

Logic building blocks.

These are pure functions with no UI surface. They are small, single-purpose, and have no side effects beyond their stated function.

### Element 4 — Level 2 and Level 3 Organs

The reusable commercial engine of Nikari Tech.

Level 2 organs do one job completely. Level 3 composites assemble Level 2 organs into purposeful systems that apps actually import.

---

## Section 3 — The `contracts/` package

### Purpose

`contracts/` is the single source of truth for all shared data shapes, connection contracts, and system-wide constants across `nikari-platform`.

It is not a utility library. It does not execute logic. It contains only definitions:

- types;
- interfaces;
- constants; and
- Joints.

### Built first — non-negotiable

`contracts/` is the first package built in `nikari-platform`.

No organ, package, AI feature, app assembly, white-label configuration, or product-specific vertical organ is implemented before the required contracts exist.

This rule has no exceptions.

### Structure

```text
packages/contracts/
  types/
    user.types.ts         ← UserProfile, CreateUserInput, UserRole
    tenant.types.ts       ← Tenant, TenantConfig, TenantTheme
    session.types.ts      ← Session, SessionState, AuthToken
    subscription.types.ts ← SubscriptionTier, SubscriptionStatus, Plan
    error.types.ts        ← AppError, ErrorCode, ErrorResponse
    response.types.ts     ← ApiResponse, PaginatedResponse, Result
    document.types.ts     ← Document, DocumentStatus, DocumentMeta
    audit.types.ts        ← AuditEvent, AuditActor, AuditAction
    ai.types.ts           ← AIOutput, AIPrompt, AIContext, HITLEvent

  interfaces/
    auth.interface.ts     ← what any auth organ accepts and returns
    storage.interface.ts  ← what any data organ accepts and returns
    config.interface.ts   ← what any config organ accepts and returns
    billing.interface.ts  ← what any billing organ accepts and returns
    ai.interface.ts       ← what any AI organ accepts and returns

  constants/
    tiers.ts              ← subscription tier values
    roles.ts              ← user role values
    errors.ts             ← error codes and standard messages
    features.ts           ← feature flag keys
```

### The contracts rule

No package anywhere in `nikari-platform` may define its own types for shared concepts.

If a type for user, tenant, session, subscription, error, response, document, audit, AI, auth, storage, config, billing, role, or any other cross-system concept is needed, it is added to `contracts/types/` first, then imported.

A package may define internal types only where they are genuinely internal and never exposed across:

- a package boundary;
- a Joint;
- an API boundary;
- an app boundary;
- a module boundary; or
- a future promotion boundary.

### Cursor rule — contracts first

Before writing any new package, Cursor reads `contracts/` to check whether the types, constants, interfaces, and Joints needed already exist.

If a required shared type or interface does not exist in `contracts/`, it is added there before implementation begins.

This is the same discipline as reading `setup.sql` before writing any Supabase query.

---

## Section 4 — Level 1A: UI Primitives

### What Level 1A means

Level 1A contains the smallest visual building blocks.

These are shadcn/ui components configured with Nikari Tech Tailwind tokens.

### Examples

- Button
- Card
- Input
- Dialog
- Table
- Form
- Badge
- Toast
- Drawer
- Avatar
- Skeleton
- Dropdown

### Location

```text
packages/primitives/ui/
```

### Rules

- Check shadcn/ui before building any UI component from scratch.
- Apply Nikari Tech Tailwind tokens for colour, typography, spacing, and component posture.
- No business logic inside a UI primitive.
- No Supabase calls inside a UI primitive.
- No auth logic inside a UI primitive.
- Props only, except for internal behaviour already provided by the shadcn/ui component.
- A UI primitive must not know which product is using it.

### Seven-stage treatment

Level 1A usually receives abbreviated seven-stage treatment:

1. Confirm component exists in shadcn/ui or identify the custom primitive need.
2. Configure or scaffold the component.
3. Apply Nikari Tech tokens.
4. Verify render.
5. Confirm no business logic.
6. Confirm no direct data access.
7. Add minimal usage documentation where required.

Standard shadcn installs do not require full Spine / Muscles / Immune System treatment. Custom primitives follow the full package discipline appropriate to their complexity.

---

## Section 5 — Level 1B: Functional Primitives

### What Level 1B means

Level 1B contains the smallest logical building blocks.

A functional primitive is a pure function or very small class with one responsibility and no UI surface.

### Examples

- `supabase-client/` — creates the typed Supabase client. Nothing else.
- `jwt-validator/` — validates a JWT token. Nothing else.
- `tenant-id-resolver/` — extracts `tenant_id` from context. Nothing else.
- `env-loader/` — loads and validates environment variables. Nothing else.
- `error-formatter/` — standardises error shape. Nothing else.
- `logger/` — structured logging. Nothing else.

### Location

```text
packages/primitives/functional/
```

### Rules

- One exported function or class per primitive.
- One responsibility only.
- Hard 30-line limit per function.
- No UI imports.
- No direct Supabase calls except inside `supabase-client/` itself.
- Import shared types from `contracts/`.
- Never define own shared types.
- Every primitive has at least one happy-path and one failure-path unit test.

### Seven-stage treatment

Level 1B receives compressed seven-stage treatment:

1. **Spine** — define function signature, input type, output type, and error shape.
2. **Index** — one file, one export.
3. **Muscles** — implement the function within the 30-line governor.
4. **Nervous System** — one structured error pathway.
5. **Flesh** — not applicable unless exposed through a hook or wrapper.
6. **Skin** — not applicable.
7. **Immune System** — unit tests for happy path and failure path.

---

## Section 6 — Level 2: Single-Function Organs

### What Level 2 means

A Level 2 organ is a complete, self-contained system that does one job entirely.

It may compose Level 1A and/or Level 1B primitives. It may be used alone or as part of a Level 3 composite.

### Examples

- `session-manager/` — everything needed to manage a Supabase session.
- `tenant-loader/` — loads and validates tenant config at runtime.
- `rls-enforcer/` — the full RLS pattern set and enforcement logic.
- `profile-sync/` — creates and syncs user profile on signup.
- `stripe-checkout/` — the complete Stripe checkout flow.
- `feature-flags/` — reads and enforces feature flag states.

### Location

```text
packages/[family]/[organ-name-or-module]/
```

Level 2 organs normally live inside the relevant package family. They are not automatically created as new top-level package folders unless NTK-05 or a later NTK-03 decision explicitly defines that package as a top-level family.

Examples:

```text
packages/auth/session-manager/
packages/auth/profile-sync/
packages/security/rls-enforcer/
packages/commercial/stripe-checkout/
packages/vertical/real-estate/property-search/
```

### Rules

- One clearly named responsibility.
- If the name needs “and”, it probably does too much.
- Imports types, interfaces, and Joints from `contracts/`.
- Imports logic from `packages/primitives/functional/` where lower-level logic already exists.
- Does not reimplement lower-level primitives.
- Defines its Joint in `contracts/interfaces/` before implementation begins.
- Hard 30-line limit per function.
- Has its own SPEC.md.
- Has a README entry or component-library index entry where relevant.
- Has tests appropriate to risk level.

### Seven-stage treatment

Level 2 receives full seven-stage treatment:

1. **Spine** — check `contracts/`, add types if needed, define Joint in `contracts/interfaces/`.
2. **Index** — scaffold files and define empty exports.
3. **Muscles** — implement core logic, enforcing 30-line function limit.
4. **Nervous System** — error formatting, structured logging, and known failure behaviour.
5. **Flesh** — hooks and state management if the organ has a UI surface.
6. **Skin** — styling if the organ has a UI surface.
7. **Immune System** — integration tests, RLS verification if applicable, and Joint compatibility confirmation.

---

## Section 7 — Level 3: Composite Organs

### What Level 3 means

A Level 3 composite organ is a named, purposeful system assembled from Level 2 organs.

This is what apps normally import and use.

A Level 3 composite does not rewrite Level 2 logic. It wires Level 2 organs together through their defined Joints.

### Examples

- `auth/` = `session-manager/` + `profile-sync/` + `protected-routes/`
- `white-label/` = `tenant-loader/` + tenant config + theme engine + domain routing, subject to NTK-06
- `verified-user/` = `auth/` + `licence-verifier/` + `tier-gating/`
- `commercial/` = `stripe-checkout/` + `subscription-gating/` + `trial-manager/`

### Location

```text
packages/[family-or-composite-name]/
```

A Level 3 composite may occupy a named package family where that family is itself the composite system, such as `packages/auth/`, `packages/commercial/`, or `packages/white-label/`. It must still expose its Joint through `contracts/interfaces/` and must not import sideways from another Level 3 composite.

Where a Level 3 composite does not map cleanly to an existing family, it may receive a named top-level package location only if NTK-05 is updated or a later NTK-03 decision records that package as a recognised top-level family or composite.

### Rules

- Composes Level 2 organs.
- Does not reimplement Level 2 logic.
- Defines its own Joint in `contracts/interfaces/`.
- Has its own SPEC.md.
- Clearly states which Level 2 organs it assembles.
- Clearly states when to use the composite versus one underlying Level 2 organ.
- Must not become a dumping ground for unrelated organs.

### Seven-stage treatment

Level 3 receives abbreviated seven-stage treatment because the hard work should already be done at Level 2:

1. **Spine** — confirm all Level 2 Joints are compatible via `contracts/interfaces/`.
2. **Index** — scaffold the composite and import Level 2 organs.
3. **Muscles** — write the wiring logic only.
4. **Nervous System** — unified error handling across the composite.
5. **Flesh** — hooks and state management if the composite has a UI surface.
6. **Skin** — styling if the composite has a UI surface.
7. **Immune System** — integration test the full composite as a system.

---

## Section 8 — The dependency direction rule

The dependency direction is always downward. Never sideways.

```text
apps/
  ↓ imports from
packages/[Level 3 family-or-composite packages]/
  ↓ imports from
packages/[family]/[Level 2 organs or modules]/
  ↓ imports from
packages/primitives/functional/ and packages/primitives/ui/
  ↓ imports from
packages/contracts/
```

Everything imports from `contracts/` where shared types, interfaces, constants, or Joints are required.

Nothing imports upward.

Nothing imports sideways at the same level.

### Specific prohibitions

- A Level 2 organ never imports from another Level 2 organ.
- A Level 3 composite never imports from another Level 3 composite.
- An app never imports from another app.
- A package never reaches into another package’s internal files instead of using its public Joint.

### Correct response when two organs need to share something

If two Level 2 organs need to share something, that shared concern belongs in one of three places:

1. `contracts/`, if it is a shared type, interface, constant, or Joint;
2. a lower-level primitive, if it is reusable logic or UI; or
3. a Level 3 composite, if the concern is wiring between organs.

Violations of this rule create sideways dependencies that destroy organ independence and make future changes unpredictable.

---

## Section 9 — The Joint definition standard

A Joint is the explicit definition of how a component connects to the rest of the system.

It is defined in `contracts/interfaces/` before implementation begins.

### What a Joint defines

A Joint defines:

- input: what the organ accepts;
- output: what the organ returns;
- required and optional fields;
- success shape;
- error shape;
- dependencies;
- side effects;
- permission assumptions;
- tenant assumptions where applicable; and
- audit/logging assumptions where applicable.

### Joint definition is the Spine stage

For every Level 2 organ and every Level 3 composite, the Spine stage is:

1. Check `contracts/interfaces/` — does this Joint already exist?
2. If yes, import it. Do not redefine.
3. If no, add the Joint to `contracts/interfaces/` before implementation.
4. Check `contracts/types/` — do the input and output types already exist?
5. If no, add them to `contracts/types/` before implementation.
6. Check `contracts/constants/` — do the relevant system-wide values already exist?
7. If no, add them before implementation.
8. Only then begin the organ or composite implementation.

### Why Joints prevent incompatibility

When `session-manager/` and `profile-sync/` both define their inputs and outputs in `contracts/interfaces/`, they speak the same language before either is built.

When they are composed into `auth/`, the wiring is mechanical.

TypeScript enforces compatibility at build time. The compiler rejects incompatible Joints before any code runs.

### Build OS implication

Every Build Plan that assembles a Level 2 organ or Level 3 composite must include Joint definition or Joint confirmation as a required pre-implementation item.

NTK-05 records the rule. Build OS enforces it before Cursor opens.

---

## Section 10 — The package family map

Packages are organised into named families by function.

The package family map is a structure and location standard. It is not automatic authority to build formal white-label, module-promotion, AI-assistant, or knowledge-layer products before their governing NTK documents exist.

| Family | Path | Contents |
|--------|------|----------|
| Contracts | `packages/contracts/` | Types, interfaces, constants, Joints |
| UI Primitives | `packages/primitives/ui/` | shadcn/ui components + Tailwind tokens |
| Functional Primitives | `packages/primitives/functional/` | Pure logic functions |
| Core | `packages/core/` | App shell, admin shell, routing, onboarding, role access |
| Data | `packages/data/` | Supabase client, tenant isolation, storage, audit log |
| Auth | `packages/auth/` | Session, profile sync, protected routes |
| Security | `packages/security/` | RLS patterns, tenant enforcement, access checks |
| White Label | `packages/white-label/` | Tenant config, theme engine, branding, domain routing — formal Lane 3 use requires NTK-06 |
| Commercial | `packages/commercial/` | Stripe billing, subscription gating, trials, affiliate |
| AI Assistant | `packages/ai-assistant/` | Prompt orchestration, retrieval, verification, HITL, cost controls — formal Lane 5 use requires NTK-08 |
| Knowledge Layer | `packages/knowledge-layer/` | SOP library, internal help, function reference, handover, retrieval — formal knowledge-layer build requires NTK-09 |
| Integrations | `packages/integrations/` | Xero, Odoo, email, SMS, social APIs, webhooks |
| Vertical | `packages/vertical/` | Product-specific organs pending promotion — formal promotion requires NTK-07 |

### The `vertical/` family

`packages/vertical/` is where product-specific organs live before they are general enough to promote to a named package family.

NRE-specific property search starts in:

```text
packages/vertical/real-estate/
```

VIX-specific market or trade-log logic starts in:

```text
packages/vertical/trading-journal/
```

Flourish-specific event-planning logic starts in:

```text
packages/vertical/event-planning/
```

Until NTK-07 exists and is current, product-specific organs may be documented as extraction candidates but may not be formally promoted out of `packages/vertical/`.

### Package family caveat

The existence of a package family does not authorise formal build work in that domain.

- `packages/white-label/` may hold white-label-ready primitives and organs, but formal Lane 3 work requires NTK-06.
- `packages/ai-assistant/` may hold scoped AI primitives and organs, but formal Lane 5 AI product build requires NTK-08.
- `packages/knowledge-layer/` may hold knowledge-layer primitives and organs, but formal knowledge-layer build requires NTK-09.
- `packages/vertical/` may hold product-specific organs, but formal promotion requires NTK-07.

---

## Section 11 — How this produces complete products

An app in `apps/` is a complete, functioning product assembled from packages.

It contains:

- product-specific pages;
- product-specific routes;
- product-specific copy;
- product-specific Vercel configuration;
- product-specific Supabase project reference;
- product-specific environment variables; and
- imports from `packages/` for shared logic, UI, auth, data, security, commercial, AI, knowledge, integrations, and vertical-specific organs.

An app does not reimplement auth, security, billing, tenant config, error formatting, logging, storage, or other concerns that already exist as packages.

### App creation must follow NTK-01 and NTK-04

NTK-05 does not authorise app creation by itself.

Before an app folder is created in `nikari-platform/apps/`:

1. the product must be routed through the correct NTK-01 lane;
2. delivery mode must be confirmed;
3. required NTK documents must exist where applicable;
4. SCOPING.md must be produced where required;
5. Module Readiness Matrix must be confirmed by Build OS;
6. `contracts/` must be checked and updated; and
7. Build OS must produce the required Build Plan before Cursor opens.

### Example — Nikari Real Estate v2

```text
apps/nre-public/ imports:
  packages/contracts/                ← shared types, interfaces, constants, Joints
  packages/primitives/ui/            ← property cards, search forms, UI atoms
  packages/primitives/functional/    ← supabase client, logger, error formatter
  packages/auth/                     ← buyer / agent login
  packages/security/                 ← protected routes, access checks, RLS helpers
  packages/white-label/              ← tenant config if applicable under NTK-06 posture
  packages/vertical/real-estate/     ← property search, listing display, suppression rules

apps/nre-admin/ imports:
  packages/contracts/
  packages/primitives/ui/            ← tables, dashboards, forms
  packages/primitives/functional/    ← supabase client, logger, error formatter
  packages/auth/                     ← same auth package, zero rebuild
  packages/security/                 ← admin access and permission checks
  packages/vertical/real-estate/     ← suppression queue, listing manager, stock workflows
```

### Example — VIX Trading Journal v2

```text
apps/vix-v2/ imports:
  packages/contracts/
  packages/primitives/ui/              ← trade log tables, charts, forms
  packages/primitives/functional/      ← supabase client, logger, error formatter
  packages/auth/                       ← same auth package as NRE, zero rebuild
  packages/security/                   ← protected user data and access checks
  packages/vertical/trading-journal/   ← market data, trade log, VIX-specific workflows
```

VIX gets production-grade auth proven across NRE. NRE gets improvements made for VIX. Neither app imports from the other. The shared packages are the compounding asset.

---

## Section 12 — Non-negotiable rules

- `contracts/` is built before any organ, package, app assembly, AI feature, white-label configuration, or vertical organ implementation begins.
- No shared type is defined outside `contracts/`.
- No shared interface or Joint is defined outside `contracts/interfaces/`.
- No organ imports from a sibling organ at the same level.
- No app imports from another app.
- Dependency direction is always downward.
- 30-line limit per function is enforced at every level.
- Every Level 2 organ has a SPEC.md and a defined Joint before build begins.
- Level 2 organs normally live under the relevant package family, not automatically as top-level folders under `packages/`.
- Every Level 3 composite has a SPEC.md and a defined Joint before build begins.
- A Level 3 composite may occupy a package family only where that family is the composite system or where an NTK-03 decision records the top-level package posture.
- shadcn/ui is checked before building any UI primitive from scratch.
- `contracts/` is read by Cursor before any new package is written.
- Product-specific logic starts in `packages/vertical/[product]/` unless it is already governed as a stable shared package.
- Formal promotion out of `packages/vertical/` must not proceed before NTK-07 exists and is current.
- Formal Lane 3 white-label work must not proceed before NTK-06 exists and is current.
- Formal Lane 5 AI assistant product build must not proceed before NTK-08 exists and is current.
- Formal knowledge-layer product or module build must not proceed before NTK-09 exists and is current.
- NTK-05 does not produce Build Plans; Build OS does.
- NTK-05 does not authorise Cursor execution; an approved Build Plan does.
- Nikari Tech-specific package and architecture decisions are recorded and superseded through NTK-03.

---

*Version: 1.1 — alignment draft*  
*Produced: Build OS — Nikari Tech Architecture Session, 28 April 2026*  
*Aligned in: Nikari Tech — NTK-03 / NTK-04 / NTK-05 alignment session, 29 April 2026*  
*Alignment basis: NTK-01 Operating Model, NTK-02 Guardrails, NTK-03 Decision Log, NTK-04 Monorepo Architecture*  
*Status: Working standard alignment draft — pending founder confirmation before commit*  
*Approved by: [Founder confirmation required before commit]*  
*Read with: UNIVERSAL_DECISIONS.md, NTK-00, NTK-01, NTK-02, NTK-03, NTK-04*  
*Next update trigger: first package built in `nikari-platform`; `contracts/` populated; package family added or revised; Joint standard revised; NTK-06/07/08/09 creates package implications*  
*Proposed repo location: wietsmarais/docs/architecture/NTK-05_Component_and_Contracts_Architecture.md*
