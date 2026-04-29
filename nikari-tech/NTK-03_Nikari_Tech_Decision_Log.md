# NTK-03 — Nikari Tech Decision Log

**File:** NTK-03_Nikari_Tech_Decision_Log.md  
**Status:** Working standard — founder confirmed, pending GitHub commit  
**Owner:** Nikari Tech  
**Layer:** Operating / Decision Governance  
**Purpose:** Provides the append-only Nikari Tech decision register. It records Nikari Tech-specific architecture, operating, product-routing, package, and governance decisions so they can be traced without duplicating UNIVERSAL_DECISIONS.md.  
**Read with:** UNIVERSAL_DECISIONS.md, NTK-00 (Master Intent), NTK-01 (Operating Model), NTK-02 (Guardrails), NTK-04 (Monorepo Architecture), NTK-05 (Component and Contracts Architecture). Reference NTK_OUTLINE_SET_28042026.md only when checking original document sequencing.  
**Supersedes / Subordinates:** Subordinate to UNIVERSAL_DECISIONS.md and NTK-00. Complements UNIVERSAL_DECISIONS.md by recording Nikari Tech-specific decisions. Does not supersede UNIVERSAL_DECISIONS.md.  
**Update trigger:** Major Nikari Tech architecture session; new product creation; monorepo restructuring; package family change; operating lane change; module promotion; white-label model decision; AI/knowledge-layer authority decision; any supersession of an existing Nikari Tech decision.

---

## Section 1 — Purpose

This document is the Nikari Tech decision log.

It exists to record decisions that belong specifically to the Nikari Tech architecture, operating model, product portfolio, package system, white-label posture, AI/knowledge-layer posture, and governance workflow.

It is not the universal decision register.

UNIVERSAL_DECISIONS.md remains the higher-level register for decisions that apply across all Nikari projects, repos, Claude projects, Cursor workflows, or organisation-wide governance. NTK-03 records Nikari Tech-specific decisions that operate within that universal frame.

This document answers:

**What has Nikari Tech decided, why was it decided, what is its current status, and which files does it affect?**

NTK-03 is intended to prevent:

- decisions being scattered across handovers, prompts, reviews, or chat memory;
- Nikari Tech-specific choices being confused with universal decisions;
- old decisions being silently edited or overwritten;
- architecture drift caused by forgotten context;
- product portfolio decisions being treated as informal assumptions; and
- future NTK documents contradicting earlier accepted decisions.

A decision is not governed merely because it appears in this file. It becomes governed only when the relevant document is founder-confirmed and committed to GitHub in the correct location.

---

## Section 2 — Decision Log Rules

### Rule 2.1 — Append-only

This decision log is append-only from creation.

Existing entries must not be deleted, rewritten, reordered, compressed, or silently corrected.

Minor typographical fixes are permitted only where they do not alter meaning. Any correction that changes meaning must be recorded through a superseding decision entry under Section 5.

### Rule 2.2 — No silent edits

If a decision changes, the old decision remains visible.

The new decision must:

- reference the earlier decision ID;
- state what has changed;
- explain why the change is required;
- identify affected files;
- assign a new status; and
- record whether any document must be updated.

### Rule 2.3 — Every decision entry requires the minimum fields

Every decision entry must include:

- Decision ID;
- date;
- decision;
- reason;
- status;
- affected files;
- source / authority;
- relationship to UNIVERSAL_DECISIONS.md; and
- next review trigger.

Entries missing these fields are incomplete and must not be treated as final.

### Rule 2.4 — Universal decisions also belong in UNIVERSAL_DECISIONS.md

If a decision applies beyond Nikari Tech, it must be recorded in UNIVERSAL_DECISIONS.md.

NTK-03 may reference the universal decision, but it must not replace the universal register.

Examples of decisions that belong in UNIVERSAL_DECISIONS.md:

- repo-wide governance rules;
- cross-project GitHub process rules;
- Claude / ChatGPT / Cursor source-of-truth rules;
- organisation-wide architecture constraints;
- universal security constraints;
- universal prompt or project-boundary standards.

Examples of decisions that belong in NTK-03:

- Nikari Tech product portfolio routing;
- `nikari-platform` package family choices;
- Nikari Tech lane decisions;
- NTK document sequencing;
- Nikari Tech-specific module promotion posture;
- Nikari Tech white-label sequencing;
- Nikari Tech AI/knowledge-layer sequencing;
- decisions that affect only the NTK architecture set.

### Rule 2.5 — Decision status labels

Use the following status labels:

| Status | Meaning |
|--------|---------|
| LOCKED | Decision is accepted and must not be reopened without a superseding entry. |
| WORKING STANDARD | Decision governs current work but may be refined through the relevant NTK update trigger. |
| OPEN | Decision is identified but not yet fully resolved. |
| DEFERRED | Decision is deliberately postponed until a named trigger. |
| SUPERSEDED | Decision has been replaced by a later decision entry. |
| ARCHIVED | Decision is no longer active but remains historically relevant. |

### Rule 2.6 — Affected files must be explicit

Affected files must be listed by filename, and where possible by intended repo path.

Where the decision affects a document that does not yet exist, mark it as pending.

Example:

```text
Affected files:
- wietsmarais/docs/architecture/NTK-06_White_Label_Tenant_and_Deployment_Model.md — pending
- wietsmarais/docs/architecture/NTK-01_Nikari_Tech_Operating_Model.md — current
```

### Rule 2.7 — NTK-03 does not authorise build execution

This document records decisions.

It does not produce Build Plans, authorise Cursor sessions, confirm Module Readiness Matrix gates, or open `nikari-platform` build work.

Build execution remains governed by Build OS and Developer OS.

---

## Section 3 — Decision Entry Template

Use this template for every new decision.

```md
### NTK03-[YYYYMMDD]-[NN] — [Short decision title]

**Date:** [DD Month YYYY]  
**Status:** LOCKED / WORKING STANDARD / OPEN / DEFERRED / SUPERSEDED / ARCHIVED  
**Decision:** [One clear sentence stating what has been decided.]  
**Reason:** [Why this decision was made.]  
**Scope:** [Nikari Tech-specific / Universal / Product-specific / Package-specific / Portfolio-specific.]  
**Source / authority:** [Founder confirmation / NTK session / UNIVERSAL_DECISIONS.md / accepted NTK document / other source.]  
**Affected files:**  
- [file path] — [effect]
- [file path] — [effect]

**Relationship to UNIVERSAL_DECISIONS.md:** [Already recorded there / Must be added there / Referenced only / Not universal.]  
**Supersedes:** [Decision ID or “None”.]  
**Superseded by:** [Decision ID or “None”.]  
**Next review trigger:** [When this must be reviewed.]  
**Notes:** [Optional implementation or context notes.]
```

No entry is complete unless it can be read independently without relying on chat memory.

---

## Section 4 — Initial Decisions to Record

The following entries initialise NTK-03. They record the founder-confirmed Nikari Tech-specific decision set as at 29 April 2026.

The initial entries below are founder-confirmed. They become active committed governance once this NTK-03 file is committed to GitHub in the correct repo location.

---

### NTK03-20260429-01 — Nikari Tech is the parent architecture

**Date:** 29 April 2026  
**Status:** LOCKED  
**Decision:** Nikari Tech is the parent architecture; Nikari Real Estate is one product built on the platform, not the centre of the architecture.  
**Reason:** The platform must support multiple commercial products through shared packages, contracts, tenant-aware architecture, and product-specific overlays without becoming NRE-only.  
**Scope:** Nikari Tech-specific, with universal architecture implications already reflected in the universal register.  
**Source / authority:** Founder confirmation — 29 April 2026; accepted NTK-00, NTK-01, and NTK-02; governance effect begins on GitHub commit.  
**Affected files:**  
- `wietsmarais/docs/architecture/NTK-00_Nikari_Tech_Master_Intent.md` — strategic parent frame  
- `wietsmarais/docs/architecture/NTK-01_Nikari_Tech_Operating_Model.md` — lane and project routing model  
- `wietsmarais/docs/architecture/NTK-02_Nikari_Tech_Guardrails.md` — anti-drift guardrails  
- `wietsmarais/docs/architecture/NTK-10_Product_Portfolio_and_Routing_Map.md` — pending portfolio expansion  

**Relationship to UNIVERSAL_DECISIONS.md:** Universal framing already reflected; NTK-03 records the Nikari Tech-specific effect.  
**Supersedes:** None.  
**Superseded by:** None.  
**Next review trigger:** NTK-00 completion to v1.0 or NTK-10 production.  
**Notes:** Replaces informal earlier NRE-centric architectural assumptions that were not recorded as NTK-03 decisions. NRE remains the flagship product and first major build, but it must not dominate platform architecture.

---

### NTK03-20260429-02 — `nikari-platform` is the product monorepo

**Date:** 29 April 2026  
**Status:** LOCKED  
**Decision:** `nikari-platform` is the Turborepo monorepo that will contain Nikari Tech apps and shared packages.  
**Reason:** Multiple products already require shared auth, security, tenant, UI, and package patterns. A monorepo prevents copy-paste drift and allows shared packages to compound.  
**Scope:** Nikari Tech-specific implementation of the universal monorepo decision.  
**Source / authority:** UNIVERSAL_DECISIONS.md and founder confirmation — 29 April 2026; governance effect begins on GitHub commit.  
**Affected files:**  
- `wietsmarais/docs/architecture/NTK-04_Nikari_Platform_Monorepo_Architecture.md` — governing architecture  
- `wietsmarais/docs/architecture/NTK-05_Component_and_Contracts_Architecture.md` — package hierarchy and contracts layer  
- `github.com/wietsmarais/nikari-platform` — target product platform repo  

**Relationship to UNIVERSAL_DECISIONS.md:** Universal decision already recorded; NTK-03 records Nikari Tech-specific consequences.  
**Supersedes:** None.  
**Superseded by:** None.  
**Next review trigger:** First app added to `nikari-platform` or monorepo restructuring.  
**Notes:** Replaces informal earlier separate-repo-first assumptions for new Nikari Tech products that were not recorded as NTK-03 decisions. Existing v1 repos are maintained until a natural rebuild point.

---

### NTK03-20260429-03 — `wietsmarais` remains the governance root

**Date:** 29 April 2026  
**Status:** LOCKED  
**Decision:** The `wietsmarais` repo remains the governance root; `nikari-platform` is the product platform and does not absorb governance markdown.  
**Reason:** Governance and code must remain deliberately separated so the product platform consumes architecture without becoming the source of architectural truth.  
**Scope:** Universal decision with Nikari Tech-specific application.  
**Source / authority:** UNIVERSAL_DECISIONS.md and founder confirmation — 29 April 2026; governance effect begins on GitHub commit.  
**Affected files:**  
- `wietsmarais/UNIVERSAL_DECISIONS.md` — universal decision source  
- `wietsmarais/docs/architecture/` — NTK document location  
- `github.com/wietsmarais/nikari-platform` — product code location  

**Relationship to UNIVERSAL_DECISIONS.md:** Already recorded universally; NTK-03 records Nikari Tech-specific routing.  
**Supersedes:** None.  
**Superseded by:** None.  
**Next review trigger:** Any proposal to relocate governance files.  
**Notes:** Replaces informal earlier assumptions that NTK documents could live inside `nikari-platform`; those assumptions were not recorded as NTK-03 decisions. NTK documents govern the monorepo from the governance root.

---

### NTK03-20260429-04 — Supabase is the product data plane; Odoo is optional integration

**Date:** 29 April 2026  
**Status:** LOCKED  
**Decision:** Supabase is the Nikari Tech product data plane; Odoo is an optional business-operations integration module, not a universal product foundation.  
**Reason:** White-label clients and Nikari Tech products must be able to run without Odoo. Product architecture must not depend on a business operations system unless deliberately scoped at product level.  
**Scope:** Universal decision with Nikari Tech-specific implementation.  
**Source / authority:** UNIVERSAL_DECISIONS.md and founder confirmation — 29 April 2026; governance effect begins on GitHub commit.  
**Affected files:**  
- `wietsmarais/docs/architecture/NTK-02_Nikari_Tech_Guardrails.md` — data and white-label guardrails  
- `wietsmarais/docs/architecture/NTK-04_Nikari_Platform_Monorepo_Architecture.md` — product platform structure  
- `wietsmarais/docs/architecture/NTK-06_White_Label_Tenant_and_Deployment_Model.md` — pending white-label expansion  
- `packages/integrations/odoo/` — future implementation location  

**Relationship to UNIVERSAL_DECISIONS.md:** Already recorded or confirmed there; NTK-03 records the Nikari Tech-specific effect.  
**Supersedes:** None.  
**Superseded by:** None.  
**Next review trigger:** NTK-06 production or any product requiring Odoo at core.  
**Notes:** Replaces informal earlier Odoo-as-product-foundation assumptions in older business architecture notes that were not recorded as NTK-03 decisions. Nikari Real Estate may still use Odoo for its own operations if scoped.

---

### NTK03-20260429-05 — `contracts/` is the foundational package

**Date:** 29 April 2026  
**Status:** LOCKED  
**Decision:** `packages/contracts/` is the first package built in `nikari-platform`; shared types, interfaces, constants, and Joints are defined once there before implementation begins.  
**Reason:** Shared products and packages require a single language for user, tenant, session, auth, storage, AI, billing, error, document, and audit concepts.  
**Scope:** Nikari Tech package architecture.  
**Source / authority:** Founder confirmation — 29 April 2026; accepted NTK-05; governance effect begins on GitHub commit.  
**Affected files:**  
- `wietsmarais/docs/architecture/NTK-05_Component_and_Contracts_Architecture.md` — governing package architecture  
- `wietsmarais/docs/architecture/NTK-02_Nikari_Tech_Guardrails.md` — contract-first guardrail  
- `nikari-platform/packages/contracts/` — first package to build  

**Relationship to UNIVERSAL_DECISIONS.md:** Universal architecture decision already reflected; NTK-03 records package-level implications.  
**Supersedes:** None.  
**Superseded by:** None.  
**Next review trigger:** First `contracts/` build session or new shared type family.  
**Notes:** Replaces informal earlier package-local shared type assumptions for cross-system concepts that were not recorded as NTK-03 decisions. `contracts/` contains definitions only; it is not a utility library.

---

### NTK03-20260429-06 — Package family map adopted

**Date:** 29 April 2026  
**Status:** LOCKED  
**Decision:** The Nikari Tech package family map is adopted as the organising structure for shared packages inside `nikari-platform`.  
**Reason:** Package families prevent loose code, clarify ownership, and provide predictable locations for reusable logic, UI, data, integrations, AI, knowledge, commercial, and vertical-specific concerns.  
**Scope:** Nikari Tech package architecture.  
**Source / authority:** Founder confirmation — 29 April 2026; accepted NTK-05; governance effect begins on GitHub commit.  
**Affected files:**  
- `wietsmarais/docs/architecture/NTK-05_Component_and_Contracts_Architecture.md` — package family map  
- `nikari-platform/packages/` — target implementation location  
- `wietsmarais/docs/architecture/NTK-07_Module_Promotion_and_Versioning_Protocol.md` — pending promotion governance  

**Relationship to UNIVERSAL_DECISIONS.md:** Referenced only where the decision is universal; the family map itself is Nikari Tech-specific.  
**Supersedes:** None.  
**Superseded by:** None.  
**Next review trigger:** New package family proposed or first module promotion.  
**Notes:** Replaces informal earlier unstructured component-library assumptions for future builds that were not recorded as NTK-03 decisions. Product-specific logic begins in `packages/vertical/` until proven reusable.

---

### NTK03-20260429-07 — Existing repos are v1 legacy and migrate only at natural rebuild

**Date:** 29 April 2026  
**Status:** LOCKED  
**Decision:** Existing product repos are treated as v1 legacy and migrate into `nikari-platform` only at a natural major rebuild point or founder decision.  
**Reason:** Forced migration risks unnecessary churn, broken live products, and copy-paste transfer of old architecture into the new platform.  
**Scope:** Nikari Tech product migration.  
**Source / authority:** UNIVERSAL_DECISIONS.md, NTK-04, and founder confirmation — 29 April 2026; governance effect begins on GitHub commit.  
**Affected files:**  
- `wietsmarais/docs/architecture/NTK-04_Nikari_Platform_Monorepo_Architecture.md` — v1 legacy and migration rules  
- `wietsmarais/docs/architecture/NTK-01_Nikari_Tech_Operating_Model.md` — Lane 2 migration model  
- `wietsmarais/docs/architecture/NTK-10_Product_Portfolio_and_Routing_Map.md` — pending portfolio map  

**Relationship to UNIVERSAL_DECISIONS.md:** Universal decision reflected; NTK-03 records Nikari Tech migration consequences.  
**Supersedes:** None.  
**Superseded by:** None.  
**Next review trigger:** First v2 migration scoping session.  
**Notes:** Replaces informal earlier assumptions that existing repos should be moved immediately into the monorepo; those assumptions were not recorded as NTK-03 decisions. Migration is a rebuild, not a copy-paste.

---

### NTK03-20260429-08 — Module library is the commercial engine

**Date:** 29 April 2026  
**Status:** WORKING STANDARD  
**Decision:** The reusable module and package library is a commercial engine for Nikari Tech, not merely internal development support.  
**Reason:** Shared packages make internal products, v2 migrations, white-label deployments, managed services, and future SaaS products faster, safer, and more profitable over time.  
**Scope:** Nikari Tech commercial and package architecture.  
**Source / authority:** Founder confirmation — 29 April 2026; accepted NTK-01 and NTK-05 architecture; governance effect begins on GitHub commit.  
**Affected files:**  
- `wietsmarais/docs/architecture/NTK-01_Nikari_Tech_Operating_Model.md` — commercial model and Lane 4  
- `wietsmarais/docs/architecture/NTK-05_Component_and_Contracts_Architecture.md` — reusable package architecture  
- `wietsmarais/docs/architecture/NTK-07_Module_Promotion_and_Versioning_Protocol.md` — pending module commercialisation and promotion rules  

**Relationship to UNIVERSAL_DECISIONS.md:** Not universal unless later adopted across non-NTK systems.  
**Supersedes:** None.  
**Superseded by:** None.  
**Next review trigger:** NTK-07 production or first module licensing decision.  
**Notes:** Replaces informal earlier assumptions that the component library was only an internal convenience layer; those assumptions were not recorded as NTK-03 decisions. Module value may be realised indirectly through speed, safety, reuse, licensing, or managed service.

---

### NTK03-20260429-09 — Seven-stage module build protocol adopted for packages

**Date:** 29 April 2026  
**Status:** WORKING STANDARD  
**Decision:** The seven-stage module build protocol applies to package and organ construction inside `nikari-platform`, with treatment adjusted by component level.  
**Reason:** A named sequence prevents Cursor from skipping design, contracts, Joints, error handling, UI surface, tests, or integration proof.  
**Scope:** Nikari Tech build architecture consumed by Build OS and Developer OS.  
**Source / authority:** Founder confirmation — 29 April 2026; accepted NTK-05 architecture and Build OS enforcement patch sequence; governance effect begins on GitHub commit.  
**Affected files:**  
- `wietsmarais/docs/architecture/NTK-05_Component_and_Contracts_Architecture.md` — seven-stage treatment by level  
- Build OS staged vocabulary patch documents — produced separately  
- Developer OS Cursor prompt and safety documents — enforcement layer  

**Relationship to UNIVERSAL_DECISIONS.md:** Referenced where universal build discipline applies; NTK-03 records the Nikari Tech package effect.  
**Supersedes:** None.  
**Superseded by:** None.  
**Next review trigger:** First package built in `nikari-platform` or staged protocol revision.  
**Notes:** Replaces informal earlier ad hoc component build sequencing for `nikari-platform` that was not recorded as an NTK-03 decision. Build OS and Developer OS enforce this; NTK-03 only records the decision.

---

### NTK03-20260429-10 — Firebase is not adopted universally

**Date:** 29 April 2026  
**Status:** LOCKED  
**Decision:** Firebase is not adopted as a universal Nikari Tech platform dependency; Supabase Auth remains the authentication layer unless a product-specific exception is later scoped.  
**Reason:** The platform should not add Firebase as a universal dependency where Supabase Auth already provides the required authentication foundation. Firebase App Check may be re-evaluated only as a specific future product-level security decision.  
**Scope:** Universal architecture decision with Nikari Tech-specific product implications.  
**Source / authority:** UNIVERSAL_DECISIONS.md and founder confirmation — 29 April 2026; governance effect begins on GitHub commit.  
**Affected files:**  
- `wietsmarais/UNIVERSAL_DECISIONS.md` — universal decision location  
- `wietsmarais/docs/architecture/NTK-02_Nikari_Tech_Guardrails.md` — security and auth guardrails  
- Future Social Shield Phase 2 scoping — possible product-specific review only  

**Relationship to UNIVERSAL_DECISIONS.md:** Already recorded universally; NTK-03 records Nikari Tech-specific consequences.  
**Supersedes:** None.  
**Superseded by:** None.  
**Next review trigger:** Social Shield Phase 2 scoping demonstrates coordinated bot attacks or product-specific need.  
**Notes:** Replaces informal earlier universal Firebase adoption proposals that were not recorded as NTK-03 decisions. Firebase App Check is not ruled out forever; it is ruled out as a universal default.

---

### NTK03-20260429-11 — NTK-01 absorbs the routing addendum

**Date:** 29 April 2026  
**Status:** WORKING STANDARD  
**Decision:** NTK-01 absorbs and supersedes `NTK-00_ADDENDUM_Project_Routing_and_Boundaries_28042026.md`; the addendum is archived, not deleted, once NTK-01 is committed.  
**Reason:** Project routing belongs in the operating model, not in a temporary addendum. Archiving preserves history while avoiding duplicate authority.  
**Scope:** Nikari Tech governance document structure.  
**Source / authority:** Founder confirmation — 29 April 2026; accepted NTK-01 operating model and Nikari Tech session handover; governance effect begins on GitHub commit.  
**Affected files:**  
- `wietsmarais/docs/architecture/NTK-01_Nikari_Tech_Operating_Model.md` — authoritative routing source  
- `wietsmarais/docs/architecture/NTK-00_ADDENDUM_Project_Routing_and_Boundaries_28042026.md` — archived reference after NTK-01 commit  
- Nikari Tech / Build OS / Developer OS / ChatGPT Review project instructions — routing reference updates  

**Relationship to UNIVERSAL_DECISIONS.md:** Not universal unless project-routing summary is updated universally.  
**Supersedes:** None.  
**Superseded by:** None.  
**Next review trigger:** Project routing model revised or project instructions updated.  
**Notes:** NTK-01 supersedes the temporary routing addendum as active authority, but this is not a prior NTK-03 decision ID. The addendum must remain available for historical audit.

---

### NTK03-20260429-12 — ChatGPT Review remains external review only

**Date:** 29 April 2026  
**Status:** LOCKED  
**Decision:** ChatGPT Nikari Tech Review is an external review, critique, gap-spotting, and brainstorming layer only; it does not originate governance.  
**Reason:** Governance must remain produced and confirmed in the correct Claude project and committed to GitHub before being treated as decided.  
**Scope:** Cross-project governance, recorded here for Nikari Tech routing clarity.  
**Source / authority:** UNIVERSAL_DECISIONS.md information-flow rule and founder-confirmed NTK-01/NTK-02 role boundaries; governance effect begins on GitHub commit.  
**Affected files:**  
- `wietsmarais/docs/architecture/NTK-01_Nikari_Tech_Operating_Model.md` — role boundary  
- `wietsmarais/docs/architecture/NTK-02_Nikari_Tech_Guardrails.md` — process and anti-drift guardrails  
- ChatGPT Nikari Tech Review project instructions — external review layer  

**Relationship to UNIVERSAL_DECISIONS.md:** Universal information-flow principle already reflected.  
**Supersedes:** None.  
**Superseded by:** None.  
**Next review trigger:** Project review workflow changes or source-of-truth model changes.  
**Notes:** Replaces informal earlier assumptions that ChatGPT review output becomes governance by upload or agreement alone; those assumptions were not recorded as NTK-03 decisions. Strong review findings must be assessed in Nikari Tech before incorporation.

---

### NTK03-20260429-13 — Formal Lane 3, Lane 4, and Lane 5 work cannot outrun their governing NTK standards

**Date:** 29 April 2026  
**Status:** WORKING STANDARD  
**Decision:** Formal Lane 3 white-label work cannot proceed before NTK-06; formal module promotion cannot proceed before NTK-07; formal Lane 5 AI or knowledge-layer build cannot proceed before NTK-08 and, where relevant, NTK-09.  
**Reason:** NTK-02 establishes minimum guardrails now while preventing specialised areas from being treated as fully authorised before their governing documents exist.  
**Scope:** Nikari Tech operating and guardrail sequencing.  
**Source / authority:** Founder confirmation — 29 April 2026; accepted NTK-01 operating model and NTK-02 guardrails; governance effect begins on GitHub commit.  
**Affected files:**  
- `wietsmarais/docs/architecture/NTK-02_Nikari_Tech_Guardrails.md` — guardrail hierarchy  
- `wietsmarais/docs/architecture/NTK-06_White_Label_Tenant_and_Deployment_Model.md` — pending  
- `wietsmarais/docs/architecture/NTK-07_Module_Promotion_and_Versioning_Protocol.md` — pending  
- `wietsmarais/docs/architecture/NTK-08_AI_Assistant_Product_Standard.md` — pending  
- `wietsmarais/docs/architecture/NTK-09_Internal_Knowledge_Layer_Module_Standard.md` — pending  

**Relationship to UNIVERSAL_DECISIONS.md:** Not universal unless later elevated to cross-project governance.  
**Supersedes:** None.  
**Superseded by:** None.  
**Next review trigger:** Production of NTK-06, NTK-07, NTK-08, or NTK-09.  
**Notes:** Replaces informal earlier assumptions that NTK-02 alone authorises formal white-label, module-promotion, AI-assistant, or knowledge-layer builds; those assumptions were not recorded as NTK-03 decisions. Exploratory review and prototypes may still occur where allowed by NTK-02, but formal build authority waits for the specialised standards.

---

### NTK03-20260429-14 — NTK-00 v1.0 adopted as Nikari Tech Master Intent

**Date:** 29 April 2026  
**Status:** LOCKED  
**Decision:** NTK-00 v1.0 is adopted as the Nikari Tech Master Intent and supersedes the NTK-00 stub dated 28 April 2026 once committed to the correct GitHub location.  
**Reason:** NTK-01 through NTK-10 have now been drafted, founder-confirmed, and committed, allowing NTK-00 to be completed from stub to full master strategic intent. NTK-00 now defines the parent strategic frame above the complete NTK architecture set without reopening the lower-level operating, guardrail, monorepo, package, white-label, module, AI, knowledge-layer, or portfolio standards.  
**Scope:** Nikari Tech-specific master architecture / strategic intent.  
**Source / authority:** Founder confirmation — 29 April 2026; confirmed final NTK-00 v1.0; NTK-01 through NTK-10 committed; governance effect begins on GitHub commit.  
**Affected files:**  
- `wietsmarais/docs/architecture/NTK-00_Nikari_Tech_Master_Intent.md` — replaced with NTK-00 v1.0 master intent  
- `wietsmarais/docs/architecture/NTK-00_Nikari_Tech_Master_Intent.md` previous stub — superseded by NTK-00 v1.0  
- `wietsmarais/docs/architecture/NTK-01_Nikari_Tech_Operating_Model.md` — remains subordinate operating model  
- `wietsmarais/docs/architecture/NTK-02_Nikari_Tech_Guardrails.md` — remains subordinate guardrail layer  
- `wietsmarais/docs/architecture/NTK-03_Nikari_Tech_Decision_Log.md` — receives this append entry  
- `wietsmarais/docs/architecture/NTK-04_Nikari_Platform_Monorepo_Architecture.md` through `NTK-10_Product_Portfolio_and_Routing_Map.md` — remain subordinate specialised standards  
- `claude-knowledge/nikari-tech/NTK-00_Nikari_Tech_Master_Intent.md` — updated reference copy after GitHub commit  

**Relationship to UNIVERSAL_DECISIONS.md:** Subordinate to UNIVERSAL_DECISIONS.md. Universal source-of-truth and project-routing principles are already reflected there; this entry records the Nikari Tech-specific adoption of NTK-00 v1.0.  
**Supersedes:** NTK-00 stub dated 28 April 2026.  
**Superseded by:** None.  
**Next review trigger:** Strategic purpose change; operating lane change in NTK-01; master guardrail change in NTK-02; monorepo/package/white-label/module/AI/knowledge-layer/portfolio change affecting Nikari Tech’s strategic identity; or founder decision that Nikari Tech’s strategic identity has changed.  
**Notes:** NTK-00 v1.0 confirms that Nikari Tech is the parent architecture; Nikari Real Estate is the flagship product but not the centre of the architecture; all NTK documents remain subordinate to UNIVERSAL_DECISIONS.md; and NTK-00 governs strategic intent above NTK-01 through NTK-10. NTK-00 does not authorise Build OS assembly, Cursor execution, product builds, migrations, white-label deployments, module promotion, AI assistant builds, or knowledge-layer builds by itself.

---

## Section 5 — Supersession Rule

Supersession is the only permitted way to change a prior decision.

A superseding entry must not erase the earlier entry. It must create a new decision entry that clearly records:

1. the decision ID being superseded;
2. the new decision;
3. the reason for the change;
4. whether the prior decision is fully superseded or partially superseded;
5. the affected files;
6. whether UNIVERSAL_DECISIONS.md also requires an update;
7. who confirmed the supersession; and
8. the next review trigger.

### Supersession template

```md
### NTK03-[YYYYMMDD]-[NN] — Supersession: [Old decision title]

**Date:** [DD Month YYYY]  
**Status:** LOCKED / WORKING STANDARD  
**Decision:** [New decision.]  
**Reason:** [Why the previous decision no longer holds.]  
**Source / authority:** [Founder confirmation / NTK session / UNIVERSAL_DECISIONS.md / accepted NTK document / other source.]  
**Supersedes:** NTK03-[YYYYMMDD]-[NN]  
**Supersession type:** Full / Partial  
**Prior decision status after this entry:** SUPERSEDED / PARTIALLY SUPERSEDED  
**Affected files:**  
- [file path] — [required update]

**Relationship to UNIVERSAL_DECISIONS.md:** [No update required / update required / already updated.]  
**Confirmed by:** [Founder / governance session reference]  
**Next review trigger:** [Trigger]
```

### Supersession discipline

If a decision was wrong, it is superseded, not deleted.

If a decision was correct but incomplete, it is expanded through a new entry and the old entry remains valid unless expressly superseded.

If a universal decision changes, UNIVERSAL_DECISIONS.md must be updated first or at the same time. NTK-03 then records the Nikari Tech effect.

If a Nikari Tech-specific decision becomes universal, it must be promoted to UNIVERSAL_DECISIONS.md and cross-referenced here.

---

## Section 6 — Review Cadence

NTK-03 must be reviewed at the following points.

### 6.1 Before major architecture sessions

Review NTK-03 before any session that may change:

- `nikari-platform` structure;
- package hierarchy;
- contracts structure;
- operating lanes;
- white-label deployment model;
- module promotion rules;
- AI assistant authority;
- internal knowledge-layer architecture;
- product portfolio routing; or
- source-of-truth workflow.

### 6.2 Before new product creation

Review NTK-03 before a new product concept moves from idea to formal concept note, scoping, Build OS readiness, or active build.

The review must check:

- whether the product fits an existing operating lane;
- whether the product affects existing package families;
- whether tenant or white-label posture is relevant;
- whether AI or knowledge-layer standards apply;
- whether the concept duplicates or conflicts with an existing product;
- whether a prior decision constrains the build.

### 6.3 Before monorepo restructuring

Review NTK-03 before any change to:

- `apps/`;
- `packages/`;
- package family names;
- dependency direction;
- `contracts/`;
- vertical package promotion;
- shared module boundaries; or
- deployment architecture.

### 6.4 Before specialised NTK documents are produced

Review NTK-03 before producing or revising:

- NTK-06 — White Label Tenant and Deployment Model;
- NTK-07 — Module Promotion and Versioning Protocol;
- NTK-08 — AI Assistant Product Standard;
- NTK-09 — Internal Knowledge Layer Module Standard;
- NTK-10 — Product Portfolio and Routing Map; and
- NTK-00 completion to v1.0.

### 6.5 At session close when a decision was made

If any Nikari Tech-specific decision was made during a session, the session handover must state whether NTK-03 requires an append entry.

If a decision belongs in UNIVERSAL_DECISIONS.md instead, the handover must say so.

### 6.6 Quarterly or after three NTK sessions, whichever comes first

If no major trigger occurs, NTK-03 should still be reviewed quarterly or after three Nikari Tech governance sessions, whichever comes first, to identify:

- stale open decisions;
- missing supersession entries;
- product portfolio drift;
- universal decisions that should be cross-referenced; and
- NTK documents requiring update.

---

*Version: 1.0 — working standard, founder confirmed*  
*Produced: Nikari Tech — NTK-03 Decision Log Session, 29 April 2026*  
*Approved by: Wiets Marais — 29 April 2026*  
*Read with: UNIVERSAL_DECISIONS.md, NTK-00, NTK-01, NTK-02, NTK-04, NTK-05*  
*Next update trigger: See Section 6*  
*Proposed repo location: `wietsmarais/docs/architecture/NTK-03_Nikari_Tech_Decision_Log.md`*
