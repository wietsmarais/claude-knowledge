# NTK-04 — Nikari Platform Monorepo Architecture
# Version: 1.0
# Date: 28 April 2026
# Status: Working standard — founder confirmed, pending GitHub commit
# Produced in: Build OS — Nikari Tech Architecture Session, 28 April 2026
# Independent review: ChatGPT — same session
# Location when committed: wietsmarais/docs/architecture/NTK-04_Nikari_Platform_Monorepo_Architecture.md
# Read before: any Build OS assembly session targeting nikari-platform,
#              any new product scoping session,
#              any Cursor session that creates or modifies a package
# Read with: NTK-01_Nikari_Tech_Operating_Model.md,
#            NTK-02_Nikari_Tech_Guardrails.md,
#            NTK-03_Nikari_Tech_Decision_Log.md,
#            NTK-05_Component_and_Contracts_Architecture.md
# Alignment patch: NTK-01 / NTK-02 / NTK-03 alignment added 29 April 2026
# Final alignment patch: external review corrections applied 29 April 2026

---

## What this document governs

This document governs the `nikari-platform` Turborepo monorepo — its
structure, the rules that apply to everything inside it, how existing
projects relate to it, and how new projects enter it.

It does not govern the `wietsmarais` governance root.
It does not govern existing v1 legacy repos.
It does not govern the component and contracts architecture — see NTK-05.

---

## Section 1 — What `nikari-platform` is

`nikari-platform` is the single Turborepo monorepo that contains all
Nikari Tech products and all shared packages from which those products
are assembled.

It is not a migration of any existing repo.
It is a new repo, started clean, with the correct foundation from day one.

Every new Nikari Tech product starts inside `nikari-platform`.
Every existing product migrates into `nikari-platform` at its natural
major rebuild point — not before.

---

## Section 2 — What `nikari-platform` is not

- A replacement for the `wietsmarais` governance root
- A migration target for v1 legacy repos before their natural rebuild
- A monolith — each app is independently deployable, and each package is independently testable, versioned, and consumable
- A client-facing product — it is the build chassis, not the product
- A place for governance markdown files — those live in `wietsmarais`

---

## Section 3 — Repo details

| Field | Value |
|-------|-------|
| Repo name | nikari-platform |
| GitHub org | wietsmarais |
| Full URL | github.com/wietsmarais/nikari-platform |
| Default branch | main |
| Tooling | Turborepo |
| Primary framework | Next.js 14 App Router |
| Language | TypeScript strict |
| Styling | Tailwind CSS |
| UI components | shadcn/ui |
| Backend | Supabase v2 (npm package) |
| Deployment | Vercel Pro — auto-deploy from GitHub |

---

## Section 4 — Full folder structure

```
nikari-platform/
  turbo.json                    ← Turborepo configuration
  package.json                  ← root dependencies and workspace config

  apps/
    nre-public/                 ← NRE buyer/renter facing (v2 — when built)
    nre-admin/                  ← NRE operator facing (v2 — when built)
    social-shield/              ← Social Shield (starts here when scoped)
    vix-v2/                     ← VIX v2 (migrates here at rebuild)
    flourish-v2/                ← Flourish v2 (migrates here at rebuild)
    study-os/                   ← StudyOS (starts here when scoped)
    counsel/                    ← Counsel (starts here when scoped)
    local-loop/                 ← LocalLoop (starts here when scoped)

  packages/
    contracts/                  ← BUILT FIRST — arteries of the system
      types/                    ← shared data shapes
      interfaces/               ← shared connection contracts
      constants/                ← system-wide values

    primitives/
      ui/                       ← Level 1A — shadcn + Tailwind tokens
      functional/               ← Level 1B — pure logic, no UI

    core/                       ← Level 2/3 — app shell, routing, onboarding
    data/                       ← Level 2/3 — supabase client, tenant isolation, storage, audit
    auth/                       ← Level 3 — composite auth organ
    security/                   ← Level 2/3 — RLS patterns, tenant enforcement
    white-label/                ← Level 3 — tenant config, theme engine, branding
    commercial/                 ← Level 3 — stripe billing, subscription gating, trials
    ai-assistant/               ← Level 3 — prompt orchestration, HITL, cost controls
    knowledge-layer/            ← Level 3 — SOP library, internal help, handover
    integrations/               ← Level 2/3 — xero, odoo, email, sms, webhooks
    vertical/                   ← product-specific organs pending promotion
      real-estate/              ← NRE-specific organs
      trading-journal/          ← VIX-specific organs
      event-planning/           ← Flourish-specific organs
      legal-drafting/           ← Counsel-specific organs
      study/                    ← StudyOS-specific organs
      community-loyalty/        ← LocalLoop-specific organs
```

---

## Section 5 — The two-repo system

### `wietsmarais` — governance root

Contains all cross-project governance. Read before every session.
Not inside `nikari-platform`. Not absorbed by `nikari-platform`.
NTK documents live here, not in the monorepo.

### `nikari-platform` — product platform

Contains all apps and all shared packages. Built in Cursor.
Deployed via Vercel. Governed by NTK documents in `wietsmarais`.

These two repos are deliberately separate. Governance and code
do not live in the same repo.

---

## Section 6 — Existing repos — v1 legacy status

| Repo | Status | Migration trigger |
|------|--------|------------------|
| nre-01-core-platform | v1 legacy — maintained | NRE v2 scoping session |
| vix-trading-journal | v1 legacy — maintained | VIX v2 scoping session |
| Wedding platform | v1 legacy — maintained | Flourish v2 scoping session |
| component-library | v1 legacy — superseded by nikari-platform/packages | No migration — packages built fresh |
| cursor-prompts | Active — not a legacy repo | Not a migration candidate |
| wietsmarais | Active — governance root | Not a migration candidate |

V1 legacy repos are not touched unless there is a specific maintenance,
security, compliance, operational-continuity, or founder-approved reason.
They do not receive strategic new feature work. Strategic new feature work
goes into `nikari-platform` through the appropriate NTK-01 lane.

---

## Section 7 — How a new product enters `nikari-platform`

A new product enters `nikari-platform` only through the operating model
defined in NTK-01.

1. Product concept note produced and approved by founder.
2. Operating lane and delivery mode confirmed under NTK-01.
3. Required governing NTK documents confirmed current:
   - Lane 3 white-label work requires NTK-06.
   - Lane 4 formal module promotion requires NTK-07.
   - Lane 5 formal AI or knowledge-layer work requires NTK-08 and, where
     applicable, NTK-09.
4. SCOPING.md produced for the product, client build, module, or feature.
5. Module readiness check completed by Build OS.
6. `contracts/` checked and updated for required shared types, interfaces,
   constants, and Joints.
7. New folder created in `apps/` for the product only after the above gates
   are satisfied.
8. Product-specific organs built first in `packages/vertical/[product]/`.
9. Extraction candidates documented after real use or serious pilot.
10. Formal promotion to named package families occurs only under NTK-07.
11. Build Plan produced by Build OS before any Cursor session opens.

---

## Section 8 — How a v1 legacy product migrates

A v1 legacy migration is Lane 2 under NTK-01 and follows the full governed
lifecycle unless a founder-approved exception is recorded.

Migration is not a copy-paste. It is a rebuild.

1. Product reaches natural major rebuild point (new feature set, full redesign,
   or founder decision to rebuild).
2. Lane 2 intake, SCOPING.md, module readiness, and Build OS gates are
   completed.
3. New app folder created in `nikari-platform/apps/`.
4. Product rebuilt from scratch using existing packages.
5. Product-specific logic rebuilt as `packages/vertical/[product]/` organs.
6. V1 legacy repo archived — not deleted — after v2 is confirmed live.
7. Vercel deployment updated to point to `nikari-platform` build.

---

## Section 9 — Deployment model

Each app in `apps/` deploys independently to Vercel Pro.
Vercel auto-detects the Turborepo and builds only what has changed.
Each app has its own Vercel project, its own domain, its own environment
variables, and its own Supabase project reference.

White-label deployment posture is governed by NTK-06 once produced.

Until NTK-06 exists, this section records the baseline monorepo deployment
assumption only: white-label tenants should be configurable without separate
codebases, and deployment should be achievable through Vercel environment
configuration and runtime tenant configuration.

No formal Lane 3 white-label build, onboarding, or client deployment may
proceed from this section alone. NTK-06 must confirm the final tenant
deployment model, including shared vs separate Supabase projects, tenant
identity strategy, domain routing, billing, client admin permissions, data
export, and exit rules.

---

## Section 10 — Non-negotiable rules

- `contracts/` is built before any app or organ assembly begins
- No app imports directly from another app
- Dependency direction is always downward — never sideways
- No package defines its own types for shared concepts
- All Vercel deployments are auto-deploy from GitHub — no manual deploys
- No push to `main` without Build OS approval event confirmed
- RLS enabled on every Supabase table from creation — no exceptions
- Service role key never in any frontend code
- No secrets in any committed file — all secrets in Vercel environment variables
- New product entry into `nikari-platform` must follow NTK-01 lane assignment
  and lifecycle gates
- Formal white-label deployment must not proceed before NTK-06 exists and is
  current
- Formal promotion out of `packages/vertical/` must not proceed before NTK-07
  exists and is current
- Formal AI assistant or knowledge-layer product build must not proceed before
  NTK-08 and, where applicable, NTK-09 exist and are current
- Nikari Tech-specific monorepo decisions and supersessions are recorded in
  NTK-03

---

*Version: 1.0*
*Status: Working standard — founder confirmed, pending GitHub commit*
*Produced: Build OS — Nikari Tech Architecture Session, 28 April 2026*
*Independent review: ChatGPT — same session*
*Approved by: Wiets Marais — 28 April 2026*
*Alignment patch: NTK-01 / NTK-02 / NTK-03 alignment added — 29 April 2026*
*Final alignment patch: external review corrections applied — 29 April 2026*
*Next update trigger: first app added to nikari-platform; package structure changes;
 new product enters portfolio; migration of first v1 legacy product begins*
*Proposed repo location: wietsmarais/docs/architecture/NTK-04_Nikari_Platform_Monorepo_Architecture.md*
