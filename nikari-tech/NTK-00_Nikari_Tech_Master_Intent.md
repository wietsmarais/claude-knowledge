# NTK-00 — Nikari Tech Master Intent
# Version: 0.1 — Stub
# Date: 28 April 2026
# Status: STUB — full content requires dedicated strategic session
# Produced in: Build OS — Nikari Tech Architecture Session, 28 April 2026
# Location when committed: wietsmarais/docs/architecture/NTK-00_Nikari_Tech_Master_Intent.md
# Read before: any Build OS session, any new product scoping session,
#              any session that touches cross-product architecture

---

## What this document is

NTK-00 is the governing strategic frame for the entire Nikari Tech system.
It establishes what Nikari Tech is, what it is building, how its products
relate to each other, and what the platform exists to do.

All other NTK documents are subordinate to this one. All Build OS sessions,
Developer OS sessions, and Claude project instructions operate within the
frame this document establishes.

Status: This is a stub. The strategic intent section below captures the
confirmed frame. The full operating model, commercial intent, and founder
vision require a dedicated strategic session to complete.

---

## The confirmed frame — locked

Nikari Tech is a governed, white-label, modular app-building platform.

It uses reusable contracts, shared packages, AI-assistant standards,
tenant-aware architecture, and product-specific overlays to build multiple
commercial products faster, safer, and with compounding value over time.

Nikari Real Estate is one product built on this platform.
It is the flagship commercial product and the first major build.
It is not the centre of the architecture.

The centre is Nikari Tech.

Every product Nikari Tech builds — including NRE — is an assembly of
governed, proven, reusable packages from the `nikari-platform` monorepo,
combined with product-specific logic that belongs only to that product.

---

## What Nikari Tech is not

- A single real estate company with a website
- A collection of unrelated projects maintained separately
- A services business that builds custom apps for clients from scratch
- A platform that depends on any single backend, auth system, or third-party
  tool as an unreplaceable foundation

---

## The platform architecture — confirmed

Two repos govern everything:

**`wietsmarais`** — governance root
Contains: UNIVERSAL_DECISIONS.md, UNIVERSAL_LEARNINGS.md, all NTK
architecture documents, cross-project standards. Source of truth for
how the system operates. Read before every session.

**`nikari-platform`** — product platform
Contains: all apps in `apps/`, all shared packages in `packages/`.
Every new product starts here. Every rebuilt product migrates here.
The commercial engine of Nikari Tech.

See NTK-04 for the full monorepo architecture.
See NTK-05 for the full component and contracts architecture.

---

## Nikari Tech Product Portfolio

### Active / Flagship
| Product | Repo | Status |
|---------|------|--------|
| Nikari Real Estate (NRE) | nre-01-core-platform (v1 legacy) | Active build — v2 planned in nikari-platform |
| Social Shield | TBD | Concept note produced — scoping required |

### Legacy v1 — considered for v2 migration
| Product | Repo | Status |
|---------|------|--------|
| VIX Trading Journal | vix-trading-journal | Live — v1 legacy — migrate at natural rebuild |
| Flourish / Wedding Planning | TBD | Live — under review — migrate at natural rebuild |

### Formal concept / scoping-stage
| Product | Status |
|---------|--------|
| StudyOS | Concept note produced — scoping session required |
| Counsel | Concept note produced — scoping session required |
| LocalLoop | Concept note produced — scoping session required |

### Future / candidate
| Product | Status |
|---------|--------|
| AI Assistant Suite Module | Architecture notes produced — build sequencing TBD |
| Orchestration Layer / Visible Agent Platform | Concept note produced — Expression B first |
| Future white-label vertical apps | Pending portfolio routing decisions |

---

## The NTK document set — full index

| File | Title | Status |
|------|-------|--------|
| NTK-00 | Nikari Tech Master Intent | Stub — this file |
| NTK-01 | Nikari Tech Operating Model | Pending — dedicated session required |
| NTK-02 | Nikari Tech Guardrails | Pending — dedicated session required |
| NTK-03 | Nikari Tech Decision Log | Pending — superseded by UNIVERSAL_DECISIONS.md for now |
| NTK-04 | Nikari Platform Monorepo Architecture | Produced — 28 April 2026 |
| NTK-05 | Component and Contracts Architecture | Produced — 28 April 2026 |
| NTK-06 | White Label Tenant and Deployment Model | Pending — dedicated session required |
| NTK-07 | Module Promotion and Versioning Protocol | Pending — dedicated session required |
| NTK-08 | AI Assistant Product Standard | Pending — dedicated session required |
| NTK-09 | Internal Knowledge Layer Module Standard | Pending — dedicated session required |
| NTK-10 | Product Portfolio and Routing Map | Pending — dedicated session required |

### Document production triggers

| Document | Trigger |
|----------|---------|
| NTK-01 | Before first external product is scoped |
| NTK-02 | Before first external product is scoped |
| NTK-03 | When UNIVERSAL_DECISIONS.md is split into Nikari Tech vs universal decisions |
| NTK-06 | Before second white-label tenant is onboarded |
| NTK-07 | Before fifth package is promoted into nikari-platform |
| NTK-08 | Before first AI-assistant feature is assembled via Build OS |
| NTK-09 | Before first internal knowledge layer module is built |
| NTK-10 | After NTK-01 is produced — portfolio routing requires operating model first |

---

## Relationship to existing documents

| Existing document | Relationship to NTK |
|------------------|---------------------|
| UNIVERSAL_DECISIONS.md | Remains the highest-level constraint document. NTK documents operate within it. |
| PROJECT_STARTER_PACK_v4.1a.md | Remains the universal session-start governance layer. Not superseded. |
| BUILD_OS_SCOPING_27042026.md | Remains the governing document for Build OS sessions. Subordinate to NTK-00. |
| Component-library_README.md | Superseded in scope by NTK-05. README remains as the quick-reference index. |
| NRE-01 governance docs | Remain valid for NRE v1. Subordinated to NTK frame for v2. |

---

## What must happen before NTK-00 is completed

1. Dedicated strategic session — founder vision, commercial intent, operating
   model, first external product definition
2. NTK-01 and NTK-02 produced in that session
3. NTK-00 updated with full strategic intent section
4. NTK-00 version bumped from 0.1 to 1.0

Until that session, this stub is the governing frame. The confirmed
decisions above are locked. The stub sections are not.

---

*Version: 0.1 — Stub*
*Produced: Build OS — Nikari Tech Architecture Session, 28 April 2026*
*Next update trigger: Dedicated Nikari Tech strategic session*
*Proposed repo location: wietsmarais/docs/architecture/NTK-00_Nikari_Tech_Master_Intent.md*
