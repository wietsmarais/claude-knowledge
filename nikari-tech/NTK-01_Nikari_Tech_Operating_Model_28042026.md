# NTK-01 — Nikari Tech Operating Model

**File:** NTK-01_Nikari_Tech_Operating_Model.md  
**Status:** Working standard — pending founder confirmation before commit  
**Owner:** Nikari Tech  
**Layer:** Operating  
**Purpose:** Defines how Nikari Tech operates as a platform business — the lanes of work, the build lifecycle, the roles of every participant (human and AI), the commercial model, and the quality gates that govern every delivery.  
**Read with:** NTK-00 (Master Intent), NTK-02 (Guardrails), NTK-04 (Monorepo Architecture), NTK-05 (Component and Contracts Architecture)  
**Supersedes / Subordinates:** Subordinate to NTK-00. Supersedes ad hoc session-level operating assumptions. Supersedes and absorbs `NTK-00_ADDENDUM_Project_Routing_and_Boundaries_28042026.md` once this file is approved and committed.  
**Update trigger:** New lane added; commercial model decision made; build lifecycle stage revised; new role defined; first external product scoped.

---

## Section 1 — Purpose

This document defines how Nikari Tech works.

It does not define what Nikari Tech exists to be — that is NTK-00.  
It does not define how the monorepo is structured — that is NTK-04.  
It does not define the component and contracts architecture — that is NTK-05.  
It does not define the hard guardrails — that is NTK-02.

This document answers:

**How does work enter the Nikari Tech system, move through it, and exit as a governed, deployable product, module, or platform capability?**

Every build session, product decision, commercial conversation, platform discussion, and module extraction must be routable to:

- an operating lane;
- a lifecycle stage;
- a delivery mode;
- a project owner;
- a role boundary; and
- a quality gate.

If a proposed piece of work cannot be routed through this operating model, the intake process is incomplete and the work must not proceed to Build OS or Cursor execution.

---

## Section 2 — Operating Model Summary

Nikari Tech operates as a governed platform business.

It has:

- one governance root: `wietsmarais`;
- one product platform: `nikari-platform`;
- one operating hierarchy: Nikari Tech → Build OS → Developer OS → Cursor;
- one review layer: ChatGPT Nikari Tech Review;
- one contract-first architecture; and
- five operating lanes through which all work is routed.

Work enters the system through one of five lanes. Lane assignment determines:

- which Build OS template applies;
- which quality gates apply;
- which project owns the next decision;
- which commercial model applies;
- which NTK documents must be read; and
- whether additional guardrails are triggered.

The build lifecycle has ten stages for full product builds, white-label deployments, and net-new shared modules. Prototypes and proven module extractions may use abbreviated lifecycle rules defined in Section 8, but they still require founder approval, documented scope, and recorded gates.

Three categories of participants operate the system:

1. **Founder** — final authority and approval layer.
2. **Claude projects** — strategic, governance, planning, and discipline layers.
3. **Cursor** — build execution layer.

Each participant has a defined role. Claude may reason, draft, assess, and plan inside its project boundary. Cursor may execute only against approved Build Plans. ChatGPT may review committed outputs but does not originate governance.

The commercial model has five revenue streams. No architecture decision may foreclose future pricing flexibility. The multi-tenant, modular structure must preserve the ability to support per-build, per-tenant, per-seat, per-module, managed-service, and future SaaS models.

---

## Section 3 — Core Operating Lanes

Every piece of work belongs to a lane before any Build OS or Cursor session opens.

The lanes are intended to be mutually exclusive at the primary routing level. Where a piece of work appears to fit more than one lane, it must be decomposed into a parent lane and any overlay gates or sub-tasks.

Example: an internal product build with a material AI assistant feature remains commercially routed through Lane 1, but Lane 5 AI-specific quality gates apply to the AI feature.

---

### Lane 1 — Internal Nikari Product Builds

**What:** Building a new product that Nikari Tech owns and operates for its own commercial purposes.

**Examples:** Social Shield, StudyOS, Counsel, LocalLoop, future Nikari-owned products that do not already exist as v1 legacy repos.

**Trigger:** Product concept approved by founder. SCOPING.md completed. Module readiness matrix confirmed by Build OS.

**Quality gate level:** Full — all ten lifecycle stages apply.

**Commercial model:** Internal product leverage. Revenue comes from the product itself, not from the build process.

**Distinguishing rule:** If Nikari Tech is the operator, the end users are external customers, and the product is not a v1 legacy migration, this is Lane 1.

**Boundary note:** If the product already exists as a v1 legacy repo and is being rebuilt into `nikari-platform`, it belongs in Lane 2, even if Nikari Tech will continue to own and operate it.

---

### Lane 2 — Existing Product v2 Migration

**What:** Rebuilding an existing v1 legacy product into `nikari-platform` at a natural major rebuild point.

**Examples:** Nikari Real Estate v2, VIX Trading Journal v2, Flourish v2.

**Trigger:** Founder decision that a natural rebuild point has been reached. New SCOPING.md produced for the v2. V1 repo archived — not deleted — after v2 is confirmed live.

**Quality gate level:** Full — all ten lifecycle stages apply. Additional gate: v1 feature parity and intentional v2 differences confirmed before deployment.

**Commercial model:** Same as Lane 1 unless a specific product decision says otherwise. The product itself remains the commercial vehicle.

**Distinguishing rule:** If a `v1 legacy` repo in the product portfolio is being rebuilt into `nikari-platform`, this is Lane 2. It is not Lane 1 merely because Nikari Tech owns the product.

---

### Lane 3 — White-Label Client Builds

**What:** Building a product for an external client using the Nikari Tech platform. The client operates the product under their own brand. Nikari Tech provides the platform, the packages, and the build capability.

**Trigger:** Client brief received and assessed. Commercial terms agreed before any build session opens. SCOPING.md produced specifically for the client product. NTK-06 (White Label Tenant and Deployment Model) confirmed present and current before this lane opens.

**Quality gate level:** Full — all ten lifecycle stages apply. Additional gates: tenant isolation verified independently before client handover; client admin permissions confirmed; data export obligations documented; branding confirmed not to override security or tenant separation.

**Commercial model:** White-label build fee + platform licensing + optional managed service + optional module licensing. Commercial terms confirmed before SCOPING.md is produced.

**Distinguishing rule:** If the end operator is an external client who is not Nikari Tech, this is Lane 3. It does not matter how similar the product is to an existing Nikari Tech product.

---

### Lane 4 — Shared Module Development

**What:** Building, extracting, or promoting a package intended to be reused across multiple products — either as a new shared package or as a promoted organ from `packages/vertical/`.

**Trigger:** Extraction review identifies a vertical organ ready for promotion, or a gap-build session identifies a shared concern not covered by existing packages. NTK-07 (Module Promotion and Versioning Protocol) must exist before any module promotion out of `packages/vertical/` occurs.

**Quality gate level:**

- Full lifecycle for net-new shared modules.
- Abbreviated extraction lifecycle for organs already proven in a real product or serious pilot.

**Commercial model:** Shared module development is not usually directly billed as a standalone product. Its commercial value is compounding leverage: it makes Lane 1, Lane 2, and Lane 3 faster, safer, and more profitable over time. Future module licensing remains available where commercially appropriate.

**Distinguishing rule:** If the primary output is a reusable package rather than a deployable product, this is Lane 4. If a product build produces a promotable organ, promotion becomes a Lane 4 sub-task triggered by the product’s extraction review.

---

### Lane 5 — AI Assistant / Internal Knowledge Products

**What:** Building AI-powered assistant features, retrieval systems, internal knowledge layer modules, or governed AI workflow tools — either embedded in an existing product or operating as standalone internal/product capabilities.

**Trigger:** NTK-08 (AI Assistant Product Standard) exists and is current. NTK-09 (Internal Knowledge Layer Standard) exists if the work involves the knowledge layer. SCOPING.md produced for the specific AI feature, assistant, retrieval system, or knowledge module.

**Quality gate level:** Full lifecycle where Lane 5 is the primary lane. Overlay gates apply where AI is embedded inside Lane 1, 2, or 3.

Additional gates include:

- HITL (human-in-the-loop) review mechanism confirmed before any sensitive AI output surface goes live;
- output logging confirmed;
- no auto-publish path without explicit founder-approved scope;
- server-side prompt routing confirmed;
- data source boundaries documented; and
- reviewable audit trail confirmed.

**Commercial model:** AI features inherit the commercial model of the parent product when embedded. Standalone AI products follow Lane 1 commercial logic unless separately defined. Internal knowledge tools are platform capability investments unless later commercialised.

**Distinguishing rule:** Lane 5 may operate in two ways:

1. **Primary lane** — where the main output is an AI assistant, internal knowledge module, or AI workflow product.
2. **Overlay gate** — where a Lane 1, 2, or 3 product includes material AI capability. In that case, the parent lane remains the commercial lane and Lane 5 adds AI-specific quality gates.

---

## Section 4 — Build Lifecycle (10 Stages)

Full Product Builds, White-Label Deployments, and net-new shared modules pass through the ten-stage lifecycle below.

Prototypes and proven Module Extractions may use abbreviated lifecycle rules defined in Section 8. They do not skip governance; they use a smaller, explicitly approved lifecycle appropriate to their delivery mode.

A stage is not complete until its assigned gate is confirmed and recorded. Founder gates require founder confirmation. Build OS gates require Build OS confirmation and must be recorded in the session handover.

---

### Stage 1 — Product Intake

The product or module concept is formally assessed.

A concept note is produced capturing:

- purpose;
- primary users;
- commercial logic;
- operating lane;
- relationship to existing products and packages;
- likely delivery mode; and
- whether any overlay gates apply.

**Output:** Approved concept note committed to `wietsmarais/docs/concepts/` or the relevant governed concept folder.

**Gate:** Founder approves concept note. **[FOUNDER GATE]**

---

### Stage 2 — Scoping

A full SCOPING.md is produced for the product, client build, module, or AI feature.

SCOPING.md defines:

- feature set;
- data model;
- tenant model, where applicable;
- module map;
- security posture;
- deployment target;
- quality gates;
- risks;
- known exclusions; and
- Build OS readiness requirements.

**Output:** SCOPING.md committed to the product, module, or build folder.

**Gate:** Founder approves SCOPING.md. Build OS confirms it is complete enough to proceed. **[FOUNDER GATE]**

---

### Stage 3 — Module Readiness Matrix

Build OS confirms which required packages already exist and pass readiness checks, and which are gaps requiring a gap-build session before assembly can begin.

**Output:** Module Readiness Matrix confirmed or updated by Build OS.

**Gate:** All required modules either pass readiness or are scheduled as gap-builds. **[FOUNDER GATE]**

---

### Stage 4 — Contract-First Design

`packages/contracts/` is checked and updated for any new shared types, interfaces, constants, or Joints required by the product, module, or feature.

No organ, app, AI surface, or white-label build implementation begins until the required contracts are defined.

**Output:** `contracts/` updated and committed. New types confirmed in `contracts/types/`. New Joints confirmed in `contracts/interfaces/`. Relevant constants confirmed in `contracts/constants/`.

**Gate:** Build OS confirms contracts are complete for the approved scope. **[BUILD OS GATE]**

---

### Stage 5 — Gap-Build

Any packages identified as missing in Stage 3 are built as dedicated gap-build sessions before the main assembly session opens.

Each gap-build follows the relevant organ build sequence defined in NTK-05 and the enforcement rules in Build OS / Developer OS.

**Output:** Missing packages built, tested, documented, and committed to `nikari-platform`.

**Gate:** Build OS confirms each gap-build is complete. Module Readiness Matrix updated. **[BUILD OS GATE]**

---

### Stage 6 — Assembly

The product is assembled inside `apps/` by importing from completed packages. Product-specific logic is built in `packages/vertical/[product]/` unless and until it is promoted under NTK-07.

No shared logic is rebuilt inside the app. If it exists in packages, it is imported. If it does not exist, it is either scoped as a vertical organ or routed into a gap-build.

Build Plans are produced by Build OS before Cursor sessions open.

**Output:** Working product, client deployment, module, or feature assembled in the correct `nikari-platform` location.

**Gate:** Build OS confirms assembly session complete. Founder approves before deployment or production use. **[FOUNDER GATE]**

---

### Stage 7 — Hardening

Security review, RLS verification, tenant isolation checks, performance checks, AI safety checks where applicable, and pre-launch checklist completion.

No product moves to deployment without this stage.

**Output:** Hardening checklist completed and committed. Critical and high findings resolved or formally deferred with founder approval.

**Gate:** Founder confirms hardening checklist complete. **[FOUNDER GATE]**

---

### Stage 8 — Deployment

Deployment is confirmed through the approved deployment model.

For `nikari-platform` apps, this usually means Vercel Pro deployment with auto-deploy from GitHub active, environment variables held in Vercel, no secrets committed, and the correct domain configured.

**Output:** Product, client deployment, or internal tool live on confirmed domain or approved internal environment.

**Gate:** Founder confirms live deployment or approved internal release. **[FOUNDER GATE]**

---

### Stage 9 — Extraction Review

After deployment or completion, the session reviews whether any product-specific organs in `packages/vertical/[product]/` are candidates for promotion to a named package family.

This is a Lane 4 sub-task triggered at the close of every Lane 1, 2, 3, or 5 delivery where reusable logic may have emerged.

**Output:** Extraction review note committed. Promotion candidates flagged or rejected with reasons.

**Gate:** Build OS confirms extraction review completed. **[BUILD OS GATE]**

---

### Stage 10 — Version Promotion

Organs confirmed ready for promotion are moved from `packages/vertical/` to their target package family following NTK-07.

Version numbers are assigned. CHANGELOG.md updated. Compatibility and breaking-change rules applied.

**Output:** Promoted packages committed at their new location. Version tags applied.

**Gate:** Founder confirms promotion. **[FOUNDER GATE]**

---

## Section 5 — Human, AI, and Project Roles

Every participant in the Nikari Tech operating model has a defined scope.

The boundary between what requires founder approval and what Claude, Build OS, Developer OS, Cursor, or ChatGPT may do without additional confirmation is explicit.

---

### The Founder

**Authority:** Final decision authority on all governance, commercial, architecture, and release questions.

No document becomes committed governance without founder confirmation. No commercial Lane 3 work begins without founder-approved commercial terms. No deployment is treated as live without founder confirmation.

**What requires founder approval — always:**

- concept note approval;
- SCOPING.md approval;
- lane assignment for any new piece of work;
- commercial terms for any Lane 3 engagement;
- Module Readiness Matrix gate before full assembly;
- assembly completion before deployment;
- hardening checklist completion;
- live deployment or internal release;
- version promotion;
- any decision that adds to UNIVERSAL_DECISIONS.md;
- any decision that revises a locked NTK document;
- any material architecture change; and
- any production deployment, breaking change, or high-risk data/security action.

**What the founder does not need to approve separately within an already approved session:**

- routine Cursor execution steps inside an approved Build Plan;
- minor document formatting corrections that do not change meaning;
- Build OS technical confirmation at Stage 4;
- Build OS gap-build completion confirmation at Stage 5;
- Build OS extraction review documentation at Stage 9.

---

### Claude — Nikari Tech Project

**Role:** Strategic intelligence and NTK governance. The architecture and operating-model layer.

**What Claude (Nikari Tech) produces:**

- NTK documents;
- product concept note assessments;
- strategic brainstorm assessments;
- ChatGPT review incorporation;
- architecture decisions assessed against UNIVERSAL_DECISIONS.md;
- product portfolio decisions; and
- Nikari Tech session handovers.

**What Claude (Nikari Tech) does not do:**

- produce Build Plans — that is Build OS;
- execute Cursor sessions — that is Cursor;
- approve its own outputs as decided — founder confirmation is required before commit;
- bypass UNIVERSAL_DECISIONS.md; or
- treat ChatGPT review outputs as governance without founder-confirmed incorporation.

---

### Claude — Build OS Project

**Role:** Build governance. The planning and assembly-control layer.

**What Claude (Build OS) produces:**

- Build Plans for Cursor sessions;
- Module Readiness Matrix confirmations;
- stage gate confirmations for Build OS gates;
- governed system prompt selection;
- risk classification for build actions;
- Build Manifests; and
- Build OS session handovers.

**What Claude (Build OS) does not do:**

- produce NTK governance documents — that is Nikari Tech;
- execute code — that is Cursor;
- make platform architecture decisions — that is Nikari Tech;
- open a Cursor session without founder-approved Build Plan; or
- downgrade risk classifications for convenience.

---

### Claude — Developer OS Project

**Role:** Execution discipline. The developer standards and workflow layer.

**What Claude (Developer OS) produces:**

- Cursor session execution rules;
- repo and branch workflow guidance;
- GitHub process discipline;
- agent prompt construction;
- Developer OS guardrails; and
- Developer OS session handovers.

**What Claude (Developer OS) does not do:**

- make platform architecture decisions — that is Nikari Tech;
- produce Build Plans — that is Build OS;
- produce NTK governance — that is Nikari Tech; or
- redefine approved Build OS scope mid-execution.

---

### Cursor

**Role:** Build execution. The production layer.

**What Cursor does:**

- executes approved Build Plans produced by Build OS;
- reads `contracts/` before writing any new package;
- reads relevant SPEC.md files before implementing any organ;
- applies the 30-line function governor;
- follows stage boundary discipline;
- flags missing decisions rather than inventing them;
- commits completed work to GitHub through the approved workflow.

**What Cursor does not do:**

- make architecture decisions mid-session;
- proceed past a stage boundary without the required Build OS approval event;
- implement anything outside the approved Build Plan without flagging;
- push to `main` without approval event confirmed;
- expose secrets or service role keys; or
- treat generated code as approved merely because it compiles.

---

### ChatGPT — Nikari Tech Review Project

**Role:** External review. The critique and second-opinion layer.

**What ChatGPT does:**

- reviews Claude-produced and GitHub-committed documents from the outside;
- identifies gaps, contradictions, missing considerations, and premature decisions;
- produces brainstorm and strategic thinking inputs;
- recommends next actions; and
- helps convert review findings into prompts for Claude.

**What ChatGPT does not do:**

- originate governance;
- produce documents treated as decided without Claude assessment and GitHub commit;
- replace Claude as the governance production layer;
- produce Build Plans; or
- treat exploratory brainstorms as resolved architecture.

---

### Project Routing and Boundary Rule

The locked operating summary is:

> **GitHub holds the truth. Nikari Tech owns the architecture. Build OS consumes that architecture to govern build sessions. Developer OS governs execution discipline. ChatGPT reviews committed outputs from the outside.**

This is the routing rule for the full operating model.

| If the decision is about... | Owning project |
|-----------------------------|----------------|
| Platform architecture, NTK governance, product portfolio, monorepo, component hierarchy, white-label strategy, AI assistant product standards | Nikari Tech |
| Specific Build Plans, module assembly, readiness gates, governed prompt selection, Cursor session preparation | Build OS |
| Developer execution, repo workflow, branch discipline, Cursor rules, agent prompts, GitHub process | Developer OS |
| External review, critique, gap identification, contradiction checking, brainstorm, sequence recommendations | ChatGPT Nikari Tech Review |

A session may cross project boundaries only when the outputs are clearly separable. If they are separable, each output is committed and uploaded to the project that owns it. If they are not separable, the session should be split and the handover must flag the routing problem.

Once this NTK-01 file is approved and committed, `NTK-00_ADDENDUM_Project_Routing_and_Boundaries_28042026.md` is superseded. The addendum must be archived, not deleted.

---

## Section 6 — Commercial Operating Model

The Nikari Tech commercial model has five revenue streams.

These streams are not mutually exclusive. Multiple streams may apply to the same product, client engagement, or future commercial structure.

No architecture decision may foreclose any stream. The multi-tenant, modular structure enables all five simultaneously.

---

### Stream 1 — Internal Product Revenue

Products built and operated by Nikari Tech for external customers.

Revenue may be:

- subscription-based;
- transaction-based;
- usage-based;
- commission-based;
- licence-based; or
- bundled with a broader Nikari business unit model.

Examples may include NRE subscription tiers, Social Shield subscriptions, VIX Journal subscriptions, or future product-specific revenue models.

---

### Stream 2 — White-Label Build Fees

Fixed, milestone-based, or scoped delivery fees for building a white-label product for an external client using the Nikari Tech platform.

Applicable primarily to Lane 3 engagements.

No Lane 3 scoping begins without agreed commercial terms.

---

### Stream 3 — Platform Licensing

Ongoing licensing fees for clients using the `nikari-platform` packages, tenant model, deployment architecture, or governed modules as their production foundation.

Licensing may be:

- per tenant;
- per seat;
- per module;
- per deployment;
- usage-based; or
- bundled with managed service.

The architecture must preserve flexibility across these pricing models.

---

### Stream 4 — Module Maintenance and Managed Service

Ongoing retainer or managed-service fees for maintaining a client’s white-label deployment, applying security patches, managing Supabase and Vercel configuration, updating packages, and maintaining module compatibility.

Applicable to Lane 3 clients who do not have internal developer capacity or who prefer Nikari Tech to remain the platform maintainer.

---

### Stream 5 — Future SaaS

Selected internal products may later be repositioned as multi-tenant SaaS products available to external operators, not only used by Nikari Tech.

This stream is not automatically activated by building a product. It is a future option made possible by the platform architecture.

A product becomes SaaS only after a deliberate portfolio and commercial decision.

---

### Commercial Rule

Commercial terms for any Lane 3 engagement must be confirmed before SCOPING.md is produced.

No scoping work begins on a client product without agreed commercial terms.

No exception is permitted unless founder approval explicitly records why unpaid or speculative scoping is strategically justified.

---

## Section 7 — Product Intake Rules

A product concept may not enter the build lifecycle until all of the following are confirmed:

1. **Named purpose** — one sentence stating what the product does and for whom.
2. **Named user** — a specific type of person, business, client, operator, or internal user.
3. **Commercial logic** — how it generates revenue, or why it is strategically worth building without direct revenue.
4. **Lane assignment** — which of the five lanes it belongs to.
5. **Delivery mode** — Prototype, Product Build, White-Label Deployment, or Module Extraction.
6. **Relationship to existing products and packages** — what it reuses, overlaps with, replaces, extends, or proves.
7. **Required NTK documents** — which governing documents must exist before work proceeds.
8. **Founder approval** — the concept note is approved before SCOPING.md begins.

A concept note that cannot answer these questions is not ready for intake. It remains a concept or candidate in the product portfolio until clarified.

---

## Section 8 — Delivery Modes

Every Lane 1–5 engagement produces output in one of four delivery modes.

Delivery mode is confirmed during product intake.

---

### Prototype

A working proof-of-concept used to validate a concept before committing to a full product build.

A prototype may be built in a secondary workflow, such as plain HTML, Supabase CDN, or a temporary proof environment. It is not automatically a `nikari-platform` build.

A prototype does not require the full ten-stage lifecycle, but it does require:

- concept note;
- founder approval;
- scope boundary;
- explicit statement that it is not production architecture;
- clear decision point after testing; and
- handover or review note.

Prototype code is not promoted into production by copy-paste. If the concept proceeds, it is scoped properly and rebuilt or adapted under the appropriate lane.

---

### Product Build

A full production product built in `nikari-platform`.

All ten lifecycle stages apply.

This is the default delivery mode for Lane 1, Lane 2, and standalone Lane 5 products.

---

### White-Label Deployment

A Product Build delivered to an external client under their brand.

All ten lifecycle stages apply. Additional Lane 3 and NTK-06 quality gates apply.

Commercial terms must be confirmed before SCOPING.md begins.

---

### Module Extraction

A focused session that promotes one or more organs from `packages/vertical/` to a named package family.

This is Lane 4.

It follows an abbreviated lifecycle only where the organ has already been proven in a real product or serious pilot. Net-new shared modules use the full lifecycle.

NTK-07 must exist before Module Extraction is used as a formal delivery mode.

---

## Section 9 — Quality Gates

Quality gates are confirmation events that must occur before a lifecycle stage is considered complete.

Gates marked **[FOUNDER]** require founder confirmation. Gates marked **[BUILD OS]** require Build OS confirmation. Gates are not optional.

Skipping a gate is a process violation. The session is incomplete until the gate is confirmed and recorded.

| Stage | Gate Type | Gate Content |
|-------|-----------|--------------|
| 1 — Product Intake | FOUNDER | Concept note approved |
| 2 — Scoping | FOUNDER | SCOPING.md approved; Build OS confirms completeness |
| 3 — Module Readiness | FOUNDER | Required modules pass or gap-builds scheduled |
| 4 — Contract-First | BUILD OS | Contracts complete for approved scope |
| 5 — Gap-Build | BUILD OS | Gap-builds complete; matrix updated |
| 6 — Assembly | FOUNDER | Assembly complete and reviewed before deployment |
| 7 — Hardening | FOUNDER | Hardening checklist complete; critical findings resolved or approved for deferral |
| 8 — Deployment | FOUNDER | Live deployment or internal release confirmed |
| 9 — Extraction Review | BUILD OS | Extraction review documented; candidates flagged or rejected |
| 10 — Version Promotion | FOUNDER | Promotion approved; version tags applied |

**Gate rule:** A stage is not complete until its assigned gate is confirmed and documented in the session handover. A handover that does not record gate confirmations is incomplete.

---

## Section 10 — Operating Risks

These risks are documented so every session participant understands what the operating model is protecting against. NTK-02 converts the necessary protections into guardrails.

---

### Risk 1 — Lane Drift

Work that belongs in one lane is executed in another, bypassing the quality gates and commercial logic that apply to the correct lane.

Most common example: a client engagement treated as an internal product build, causing Lane 3 commercial and tenant-isolation gates to be missed.

**Mitigation:** Lane assignment confirmed during intake. Build OS confirms lane before any Build Plan is produced.

---

### Risk 2 — Stage Skipping

A lifecycle stage is skipped under time pressure.

Most common examples:

- assembly begins without a completed Module Readiness Matrix;
- contracts are not updated before implementation;
- deployment happens without hardening; or
- extraction review is skipped after launch.

**Mitigation:** Stage gates are mandatory. Build OS rejects a Build Plan that skips a required stage without documented founder-approved reason.

---

### Risk 3 — Governance Drift

Architecture decisions are made in Cursor sessions or Build OS sessions without going through Nikari Tech.

The codebase then diverges from the NTK documents.

**Mitigation:** Material architecture decisions are escalated to Nikari Tech. Cursor and Build OS flag rather than decide.

---

### Risk 4 — Role Confusion

One project starts doing another project’s job.

Examples:

- Build OS starts producing NTK documents;
- Nikari Tech starts drafting Build Plans;
- Developer OS makes product architecture decisions;
- ChatGPT review outputs are treated as governance; or
- Cursor makes scoping decisions mid-session.

**Mitigation:** Project routing rule in Section 5. Cross-boundary conversations are flagged and routed.

---

### Risk 5 — Unpriced Lane 3 Work

A client engagement begins without confirmed commercial terms.

This creates unpaid scoping, unclear ownership, and pressure to convert exploratory thinking into committed delivery.

**Mitigation:** Commercial terms gate in Section 6 and Lane 3 definition in Section 3.

---

### Risk 6 — Premature Module Promotion

An organ is promoted from `packages/vertical/` before it has been proven, documented, versioned, or tested across a real use case.

This creates a supposedly stable module that is not actually stable.

**Mitigation:** NTK-07 governs all promotions. Promotion is a Stage 10 founder gate.

---

### Risk 7 — AI Overlay Treated as Ordinary Feature Work

AI-powered outputs are treated as normal UI or workflow features, causing HITL, audit trail, prompt routing, and reviewability requirements to be missed.

**Mitigation:** Lane 5 may operate as an overlay gate inside Lane 1, 2, or 3. AI-specific gates apply whenever material AI capability is present.

---

## Section 11 — Update Triggers

This document must be reviewed and updated when any of the following occur:

- a new operating lane is identified that does not fit any of the five existing lanes;
- the build lifecycle gains, loses, or resequences a stage;
- a new participant role is added to the system;
- a commercial model decision adds a sixth revenue stream;
- a new delivery mode is needed;
- a quality gate is added, removed, or resequenced;
- NTK-02 adds a guardrail that creates a new gate requirement;
- NTK-06 changes the white-label operating model;
- NTK-07 changes the module extraction or promotion pathway;
- NTK-08 changes the AI assistant authority model;
- NTK-09 changes the internal knowledge layer model;
- the first Lane 3 engagement is scoped;
- the first Lane 4 promotion occurs;
- the first Lane 5 AI product or AI overlay is built; or
- the project routing model is revised.

---

*Version: 1.0 — final corrected draft*  
*Produced: Nikari Tech — NTK-01 + NTK-02 Session, 28 April 2026*  
*Corrected after ChatGPT review: lane overlap, lifecycle/gate consistency, routing absorption, and Lane 5 overlay clarification*  
*Approved by: [Founder confirmation required before commit]*  
*Read with: NTK-00, NTK-02, NTK-04, NTK-05*  
*Next update trigger: See Section 11*  
*Proposed repo location: wietsmarais/docs/architecture/NTK-01_Nikari_Tech_Operating_Model.md*
