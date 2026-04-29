# NTK-10 — Product Portfolio and Routing Map

**File:** NTK-10_Product_Portfolio_and_Routing_Map.md  
**Status:** Working standard — founder confirmed, pending GitHub commit  
**Owner:** Nikari Tech  
**Layer:** Product Portfolio / Routing Governance  
**Purpose:** Defines the Nikari Tech product portfolio map, product status labels, portfolio categories, product entry template, routing decision test, build readiness criteria, sequencing and prioritisation discipline, activation, parking and retirement rules, migration rules, review cadence, portfolio risks, and update triggers so product ideas, active products, legacy products, white-label opportunities, module pilots, AI products, and knowledge-layer products are routed consistently before Build OS or Cursor work begins.  
**Read with:** UNIVERSAL_DECISIONS.md, NTK-00 (Master Intent), NTK-01 (Operating Model), NTK-02 (Guardrails), NTK-03 (Decision Log), NTK-04 (Monorepo Architecture), NTK-05 (Component and Contracts Architecture), NTK-06 (White Label Tenant and Deployment Model), NTK-07 (Module Promotion and Versioning Protocol), NTK-08 (AI Assistant Product Standard), NTK-09 (Internal Knowledge Layer Module Standard).  
**Supersedes / Subordinates:** Subordinate to UNIVERSAL_DECISIONS.md, NTK-00, NTK-01, and NTK-02. Expands the product portfolio guardrails in NTK-02 and the intake/status rules in NTK-01. Complements NTK-03 by identifying which portfolio-routing decisions may require append-only decision entries. Does not authorise any Build OS assembly session, Cursor session, product build, migration, client deployment, module promotion, AI assistant build, or knowledge-layer build by itself.  
**Update trigger:** New product concept; product status change; product enters or exits active build; v1 legacy product becomes v2 candidate; first white-label client opportunity reaches serious scoping; module pilot becomes reusable candidate; product is parked, retired, rejected, merged, or split; product category changes; portfolio load exceeds active capacity; product requires a new operating lane; or any NTK-01, NTK-02, NTK-03, NTK-04, NTK-05, NTK-06, NTK-07, NTK-08, or NTK-09 change affecting product routing, activation, migration, or portfolio status.

---

## Section 1 — Purpose

This document defines the Product Portfolio and Routing Map for Nikari Tech.

It exists because Nikari Tech is not a single-product company and not a loose idea board. It is a governed platform that can build internal products, migrate v1 legacy products, support white-label clients, develop shared modules, and create AI or knowledge-layer products. Without a portfolio map, too many ideas can become active too early, product maturity can become unclear, legacy products can be forgotten, and build sessions can open before the required governance exists.

NTK-10 answers:

**What products, product concepts, legacy products, white-label opportunities, module pilots, AI products, and knowledge-layer products exist in the Nikari Tech portfolio; what is their current status; where do they belong; and what must happen before they move toward build, migration, deployment, promotion, parking, or retirement?**

This document governs:

- product status labels;
- portfolio categories;
- current portfolio map;
- product entry template;
- routing decision test;
- build readiness criteria;
- sequencing and prioritisation discipline;
- activation, parking, rejection, and retirement rules;
- migration rules;
- portfolio review cadence;
- risks; and
- update triggers.

This document is governance. It is not a Build Plan. It does not open Cursor. It does not create a product folder, repo, app, package, concept note, SCOPING.md, migration plan, client deployment, module, AI assistant, or knowledge layer by itself.

Formal build work still requires the correct lane under NTK-01, guardrails under NTK-02, decision discipline under NTK-03, app/package placement under NTK-04 and NTK-05, and any specialised standard required by NTK-06, NTK-07, NTK-08, or NTK-09.

### What this document does not govern

This document does not govern:

- operating lanes, lifecycle gates, or project roles — see NTK-01;
- hard guardrails and anti-drift rules — see NTK-02;
- decision-log and supersession discipline — see NTK-03;
- monorepo structure and app/package placement — see NTK-04;
- contracts, Joints, dependency direction, and package families — see NTK-05;
- white-label tenant and deployment model — see NTK-06;
- module promotion and versioning — see NTK-07;
- AI assistant authority and HITL standards — see NTK-08;
- internal knowledge-layer standards — see NTK-09; or
- Build OS Build Plans, Developer OS execution, or Cursor implementation.

### Alignment rule

NTK-10 determines **portfolio status and routing**. It does not decide implementation.

A product may be important, commercially attractive, or strategically promising without being build-ready.

A product may be listed in the portfolio without being active.

A product may be active commercially but still remain v1 legacy until a governed v2 migration is approved.

---

## Section 2 — Core Rule

The core rule is:

> **Not every idea is an active product. Every product or concept must have a status before it receives build attention.**

A product idea is not a product merely because it has a name.

A product is not build-ready merely because it is strategically attractive.

A product is not active merely because it appears in a handover, brainstorm, chat, concept note, issue, or review.

Every product, concept, module pilot, white-label opportunity, legacy product, AI assistant, and knowledge-layer idea must have:

- a status label;
- a category;
- an owner or holding project;
- a primary lane candidate;
- a current location;
- a target location if known;
- a next decision; and
- a reason for its current posture.

### What the core rule protects

This rule protects Nikari Tech from:

- concept sprawl;
- active-build overload;
- products being built outside architecture;
- legacy products being forgotten or migrated too early;
- white-label conversations becoming unpaid or unscoped commitments;
- module pilots becoming stable products without proof;
- AI or knowledge-layer ideas bypassing NTK-08 or NTK-09;
- product status being confused with commercial enthusiasm;
- Build OS being asked to plan before scoping exists; and
- Cursor being opened before product routing is complete.

### Default posture for new ideas

The default posture for a new idea is:

```text
new idea → future_candidate or formal_concept → intake review → status confirmed → next decision recorded
```

The default posture is not active build.

### Status before scope

A product must receive a status before SCOPING.md is produced.

SCOPING.md may change the status, but it must not begin from an unlabelled idea.

---

## Section 3 — Product Status Labels

Every product, concept, legacy product, module pilot, AI product, knowledge product, white-label opportunity, or productised internal tool must have one status label.

Status labels are maturity and routing labels. They are not marketing labels.

### Status label summary

| Status | Meaning | Build attention allowed? |
|--------|---------|--------------------------|
| `active_flagship` | Strategic flagship product or product family with current platform significance. | Yes, through approved lane and scope. |
| `active_build` | Currently approved for active build work under Build OS. | Yes, only under approved Build Plans. |
| `pilot` | Controlled pilot, proof-of-use, or serious trial. | Limited, scoped and labelled. |
| `formal_concept` | Concept formally captured and worth future scoping. | No build; concept development only. |
| `scoping` | Approved for SCOPING.md or equivalent governed scoping. | Scoping only; no build. |
| `legacy_v1` | Existing live or maintained v1 product outside `nikari-platform`. | Maintenance only unless founder-approved; v2 requires Lane 2. |
| `v2_candidate` | Existing product identified for future rebuild into `nikari-platform`. | Scoping allowed after founder decision. |
| `future_candidate` | Possible future product, not yet mature enough for formal concept or scoping. | No build; park in portfolio. |
| `parked` | Intentionally paused, not rejected. | No build until reactivated. |
| `retired` | No longer active or intended for future build. | No build except archive or closure work. |

### `active_flagship`

A product or product family with strategic importance to Nikari Tech.

`active_flagship` does not automatically mean active code build. It means the product is strategically central enough to remain visible in portfolio review.

A flagship product still requires:

- lane assignment;
- SCOPING.md where build is proposed;
- Build OS Build Plan before Cursor opens;
- applicable specialised standards; and
- founder approval.

### `active_build`

A product, module, client deployment, AI assistant, or knowledge-layer product that has been approved for current build work.

Requirements:

- approved scope;
- lane confirmed;
- Build OS engaged;
- relevant NTK documents current;
- Build Plan approved before Cursor opens;
- risks classified.

`active_build` is capacity-sensitive. Too many active builds create portfolio risk.

### `pilot`

A controlled proving context.

A pilot may test:

- a product idea;
- a workflow;
- a module;
- a white-label pattern;
- an AI assistant;
- a knowledge-layer behaviour;
- a tenant model;
- a commercial offer.

A pilot must remain labelled as pilot. It must not quietly become production or stable module infrastructure.

### `formal_concept`

A product idea that is strong enough to be formally recorded but not yet approved for scoping.

Requirements:

- name;
- purpose;
- primary users;
- problem;
- likely commercial logic;
- likely lane;
- next decision.

A formal concept may become `scoping`, `future_candidate`, `parked`, or `retired`.

### `scoping`

A concept approved for SCOPING.md or governed equivalent.

Scoping may produce:

- product scope;
- lane confirmation;
- feature map;
- data posture;
- tenant posture;
- AI posture;
- module map;
- commercial framing;
- risk assessment;
- build-readiness decision.

Scoping is not build authority.

### `legacy_v1`

An existing product or repo that remains outside `nikari-platform`.

A `legacy_v1` product may be maintained, secured, or operated. It must not receive strategic new feature expansion unless founder-approved and routed through the correct product decision.

Migration to `nikari-platform` requires Lane 2.

### `v2_candidate`

A `legacy_v1` product that may be rebuilt into `nikari-platform`.

The v2 candidate label does not start migration. It indicates that migration should be assessed.

Migration requires:

- founder decision;
- v1 inventory;
- v2 SCOPING.md;
- Build OS plan;
- data migration assessment where relevant;
- app/package placement under NTK-04 and NTK-05.

### `future_candidate`

A possible future product.

A future candidate may be strategically interesting but lacks enough definition, priority, timing, commercial clarity, governance readiness, or capacity to move into formal concept or scoping.

### `parked`

A paused concept or product.

Parked does not mean rejected. It means the product is intentionally outside active attention until a reactivation trigger occurs.

### `retired`

A product or concept no longer intended for active development, migration, or commercial use.

A retired product may still require archive, data retention, support wind-down, domain closure, client communication, or repo/archive decisions.

### Rejected idea note

`rejected` is not a normal ongoing portfolio status. It is a decision outcome.

A rejected idea should be recorded briefly in the relevant concept or decision log where needed so it does not repeatedly re-enter the system without new facts.

---

## Section 4 — Portfolio Categories

Portfolio category answers: **What kind of thing is this?**

Status answers: **What is its current maturity or action posture?**

The two must not be confused.

### Category 1 — Internal Nikari Products

Products owned and operated by Nikari Tech or a Nikari business unit for Nikari’s own commercial or operational purposes.

Examples:

- Nikari Real Estate;
- Social Shield;
- StudyOS;
- Counsel;
- LocalLoop;
- AI Assistant Suite Module if built as a Nikari-owned platform capability.

Likely lanes:

- Lane 1 for new products;
- Lane 2 for existing v1 migration;
- Lane 5 overlay if AI or knowledge-layer capability is material.

### Category 2 — Nikari BU Products

Products tied to a specific Nikari business unit but built on Nikari Tech architecture.

Examples:

- Nikari Real Estate product surfaces;
- future Nikari Living systems;
- future Nikari Agriculture systems;
- other business-unit systems if formally routed into Nikari Tech.

Likely lanes:

- Lane 1 where net-new;
- Lane 2 where v1 migration;
- Lane 4 where reusable business-unit logic becomes module candidate.

### Category 3 — White-Label Products

Products, deployments, or configurations intended for an external client, partner, tenant, or branded third-party use.

Examples:

- branded client portals;
- white-label real estate platforms;
- client-specific knowledge layers;
- partner-branded assistant products.

Likely lane:

- Lane 3.

NTK-06 applies before serious external white-label scoping or onboarding.

### Category 4 — Module Pilots

Modules, organs, package families, or reusable patterns being tested before formal promotion.

Examples:

- verified-user-tier;
- AI assistant infrastructure;
- knowledge-layer retrieval organs;
- white-label tenant configuration;
- reusable onboarding organs;
- product-specific vertical organs being assessed for extraction.

Likely lane:

- Lane 4;
- Lane 5 overlay where AI or knowledge-layer module is involved.

NTK-07 governs promotion.

### Category 5 — Legacy Products

Existing products outside `nikari-platform`.

Examples:

- NRE v1;
- VIX Trading Journal v1;
- Flourish / Wedding Planning v1.

Likely lane:

- Lane 2 when migrating;
- otherwise maintained as v1 legacy.

### Category 6 — Future / Candidate Concepts

Ideas, strategic possibilities, or product families that are not yet active.

Examples:

- Orchestration Layer / Visible Agent Platform;
- future white-label vertical apps;
- future platform extensions not yet scoped.

Likely posture:

- `future_candidate`;
- `formal_concept`;
- `parked`.

---

## Section 5 — Current Portfolio Map

This section records the current status-banded portfolio map as at 29 April 2026.

Status must be reviewed whenever a product changes category, lane, build readiness, commercial priority, or migration posture.

### Active / Flagship Priority

| Product | Status | Category | Current location | Target location | Primary lane | Next decision |
|---------|--------|----------|------------------|-----------------|--------------|---------------|
| Nikari Real Estate (NRE) | `active_flagship` + `legacy_v1` for current repo | Internal Nikari / Nikari BU Product / Legacy v1 | `nre-01-core-platform` | `nikari-platform/apps/nre-public` and `nikari-platform/apps/nre-admin` at v2 rebuild | Lane 2 for v2 migration | Confirm NRE v2 scoping trigger and SCOPING.md timing. |
| Social Shield | `formal_concept` / flagship candidate | Internal Nikari Product | Concept notes / issue context | `nikari-platform/apps/social-shield` when scoped | Lane 1, with possible Lane 5 overlay later | Produce or confirm SCOPING.md before build. |

### Legacy v1 — Considered for v2 Migration

| Product | Status | Category | Current location | Target location | Primary lane | Next decision |
|---------|--------|----------|------------------|-----------------|--------------|---------------|
| VIX Trading Journal | `legacy_v1` / `v2_candidate` when founder triggers rebuild | Legacy Product | `vix-trading-journal` | `nikari-platform/apps/vix-v2` | Lane 2 | Wait for natural rebuild trigger or founder migration decision. |
| Flourish / Wedding Planning | `legacy_v1` / under review | Legacy Product | Existing wedding platform context | `nikari-platform/apps/flourish-v2` | Lane 2 | Confirm whether product remains live, is parked, or becomes v2 candidate. |

### Formal Concept / Scoping-Stage

| Product | Status | Category | Current location | Target location | Primary lane | Next decision |
|---------|--------|----------|------------------|-----------------|--------------|---------------|
| StudyOS | `formal_concept` | Internal Nikari Product | Concept note / issue context | `nikari-platform/apps/study-os` | Lane 1, possible Lane 5 overlay | Produce SCOPING.md when founder prioritises. |
| Counsel | `formal_concept` | Internal Nikari Product | Concept note / issue context | `nikari-platform/apps/counsel` | Lane 1, possible Lane 5 overlay | Produce SCOPING.md when founder prioritises. |
| LocalLoop | `formal_concept` | Internal Nikari Product | Concept note / issue context | `nikari-platform/apps/local-loop` | Lane 1 / possible white-label later | Produce SCOPING.md when founder prioritises. |

### Future / Candidate

| Product / Product Family | Status | Category | Current location | Target location | Primary lane | Next decision |
|--------------------------|--------|----------|------------------|-----------------|--------------|---------------|
| AI Assistant Suite Module | `future_candidate` / module-pilot candidate | Module Pilot / AI Product | Architecture notes | `packages/ai-assistant/` and/or product-specific vertical packages | Lane 5 / Lane 4 | Confirm whether first implementation is internal, embedded, or standalone. NTK-08 applies. |
| Orchestration Layer / Visible Agent Platform | `future_candidate` | Future Candidate Concept | Concept note / issue context | TBD | Lane 1 or Lane 5 depending scope | Keep parked until product truth and commercial path are clearer. |
| Future white-label vertical apps | `future_candidate` | White-Label Product Family | Pending portfolio routing | `nikari-platform/apps/[future-app]` when scoped | Lane 3 | Wait for specific client/opportunity and NTK-06-aligned scope. |
| Internal Knowledge Layer Products | `future_candidate` / module-pilot candidate | Knowledge Product / Module Pilot | NTK-09 standard now defines governance | `packages/knowledge-layer/` or product vertical | Lane 5 / Lane 4 | First build requires NTK-09-aligned manifest and Build OS plan. |

### Current portfolio note

The portfolio map is a living governance table. It must not be treated as complete product specification.

A product listed here still requires its own concept note, SCOPING.md, Build OS plan, and relevant specialised standards before implementation.

---

## Section 6 — Product Entry Template

Every product, concept, migration candidate, white-label opportunity, module pilot, AI product, or knowledge-layer product should be captured using this template before it receives serious portfolio attention.

```yaml
product_entry_version: "1.0"

product:
  name: ""
  short_name: ""
  status: "active_flagship | active_build | pilot | formal_concept | scoping | legacy_v1 | v2_candidate | future_candidate | parked | retired"
  category: "internal_nikari_product | nikari_bu_product | white_label_product | module_pilot | legacy_product | future_candidate"
  owner: ""
  date_added: ""
  last_reviewed: ""
  next_review_trigger: ""

purpose:
  one_sentence_purpose: ""
  problem_being_solved: ""
  primary_users: []
  excluded_users: []
  user_reliance_risk: "low | medium | high | critical"

commercial:
  commercial_model: ""
  revenue_streams_possible: []
  commercial_priority: "low | medium | high | strategic"
  commercial_terms_required_before_scoping: false

routing:
  primary_lane: "Lane 1 | Lane 2 | Lane 3 | Lane 4 | Lane 5 | undecided"
  overlay_lanes: []
  delivery_mode: "prototype | product_build | white_label_deployment | module_extraction | undecided"
  relevant_ntk_documents: []
  build_os_required: false
  developer_os_required: false
  cursor_allowed: false

architecture:
  current_location: ""
  target_location: ""
  likely_apps: []
  likely_packages: []
  relevant_modules: []
  new_modules_likely_required: []
  integrations_likely_required: []
  product_specific_vertical_logic: []
  repo_posture: "new_app | existing_v1 | v2_migration | package_only | undecided"
  contracts_impact_likely: false

risk:
  data_sensitivity: "none | low | medium | high | critical"
  tenant_relevance: "none | possible | likely | required"
  ai_relevance: "none | possible | likely | required"
  knowledge_layer_relevance: "none | possible | likely | required"
  security_posture_known: false
  compliance_or_legal_sensitivity: "none | low | medium | high | critical"

migration:
  current_repo: ""
  v1_legacy: false
  v2_candidate: false
  migration_trigger: ""
  data_migration_required: false
  continuity_plan_required: false

readiness:
  clear_user: false
  clear_problem: false
  commercial_logic: false
  data_model_understood: false
  tenant_model_understood: false
  module_map_clear: false
  integrations_understood: false
  repo_posture_understood: false
  security_posture_understood: false
  deployment_target_known: false
  scoping_ready: false
  build_ready: false

decision:
  next_decision_required: ""
  decision_owner: ""
  decision_due_or_trigger: ""
  founder_decision_required: true
  ntk_03_append_required: false

notes: ""
```

### Template rule

A product entry with undecided lane, unclear users, unclear commercial logic, unknown data posture, unknown tenant posture, or unknown next decision is not build-ready.

It may still be a good idea. It is simply not ready for Build OS or Cursor.

---

## Section 7 — Routing Decision Test

Use this test before a product concept, client opportunity, module idea, AI feature, or knowledge-layer workflow moves toward scoping or build.

### Step 1 — Is it already inside an existing product?

If yes, ask:

- Is this a feature inside an active product?
- Is it a maintenance/security/compliance issue in a v1 legacy repo?
- Is it a v2 migration trigger?
- Is it a product-specific vertical organ?
- Is it a candidate for shared extraction?

Likely routing:

- existing active product feature → Lane 1 or Lane 2 depending product status;
- v1 migration → Lane 2;
- product-specific organ → product lane first, Lane 4 only after extraction review;
- maintenance/security/compliance in v1 → governed maintenance path, not strategic new build.

### Step 2 — Is it a new Nikari-owned product?

If yes, route as Lane 1.

Required before build:

- product entry;
- concept note;
- status;
- founder approval;
- SCOPING.md;
- Build OS plan.

### Step 3 — Is it an existing v1 product moving to v2?

If yes, route as Lane 2.

Do not copy the v1 repo into `nikari-platform`.

Required before build:

- migration decision;
- v1 inventory;
- v2 SCOPING.md;
- data migration assessment where relevant;
- continuity plan where relevant;
- Build OS plan.

### Step 4 — Is it for an external client, tenant, partner, or white-label deployment?

If yes, route as Lane 3.

Required before serious commitment:

- NTK-06 current;
- commercial terms posture;
- tenant model;
- data ownership;
- export and exit posture;
- client admin model;
- SCOPING.md;
- Build OS plan.

### Step 5 — Is the primary output a reusable package or module?

If yes, route as Lane 4.

Required before formal promotion:

- NTK-07 current;
- proof of real product or serious pilot use unless net-new shared infrastructure is founder-approved;
- module status;
- classification;
- required file set;
- compatibility review;
- Build OS plan.

### Step 6 — Is it an AI assistant, retrieval feature, knowledge-layer product, or AI workflow?

If yes, route as Lane 5 or apply Lane 5 overlay gates.

Required before build:

- NTK-08 for AI assistant behaviour;
- NTK-09 for internal knowledge-layer modules;
- authority level;
- HITL requirement;
- data/source boundary;
- logging and review posture;
- Build OS plan.

### Step 7 — Is it only a concept note or exploratory idea?

If yes, keep it as `formal_concept`, `future_candidate`, or `parked`.

Do not open Build OS unless the founder approves scoping.

### Step 8 — Does it belong outside Nikari Tech?

Some ideas may be valuable but not belong to Nikari Tech.

If an idea is primarily:

- a legal matter;
- a property transaction;
- a marketing campaign;
- a business-unit operating issue;
- a non-software service;
- a private project;
- or a governance item for another project,

then route it to the correct project or business system.

### Routing outcome labels

Use one of:

| Routing outcome | Meaning |
|-----------------|---------|
| `route_lane_1` | Internal Nikari product build. |
| `route_lane_2` | Existing product v2 migration. |
| `route_lane_3` | White-label client build. |
| `route_lane_4` | Shared module development or promotion. |
| `route_lane_5` | AI assistant or knowledge-layer product. |
| `overlay_lane_5` | AI/knowledge gate applies inside another lane. |
| `concept_only` | Record concept; no build path. |
| `park` | Hold outside active portfolio. |
| `retire` | Close or archive. |
| `reject` | Do not proceed unless new facts emerge. |
| `route_elsewhere` | Belongs outside Nikari Tech. |

---

## Section 8 — Build Readiness Criteria

A product is build-ready only when the required criteria are satisfied for its lane and delivery mode.

### Minimum build readiness criteria

| Criterion | Required question |
|----------|-------------------|
| Clear user | Who uses it, and who does not? |
| Clear problem | What specific problem does it solve? |
| Commercial logic | Why should Nikari build or maintain it? |
| Data model | What data exists, who owns it, and how sensitive is it? |
| Tenant model | Is tenant separation irrelevant, possible, likely, or required? |
| Module map | What packages exist, and what gaps are expected? |
| Integrations | What external systems, APIs, or connectors are likely required? |
| Repo posture | Is this a new app, existing v1, v2 migration, package-only item, or undecided? |
| Security posture | What auth, access, RLS, secrets, admin, or audit risks exist? |
| Deployment target | Where will it live, and who will access it? |
| Product truth | What must not be flattened into generic reuse? |
| Relevant standards | Which NTK documents must be current before build? |

### Readiness levels

| Readiness level | Meaning | Build OS allowed? | Cursor allowed? |
|-----------------|---------|-------------------|-----------------|
| `idea_recorded` | Idea captured but not assessed. | No | No |
| `concept_ready` | Enough detail for founder concept review. | No | No |
| `scoping_ready` | Approved to produce SCOPING.md. | Scoping support only | No |
| `build_os_ready` | SCOPING.md approved and ready for Build OS planning. | Yes | No |
| `cursor_ready` | Build Plan approved and session boundaries clear. | Already complete | Yes, under Build Plan only |
| `deployment_ready` | Hardening and release gates complete. | Release planning only | Deployment only with approval |

### Lane-specific readiness additions

#### Lane 1 — Internal product

Additional requirements:

- product concept approved;
- product category confirmed;
- product-specific vertical logic identified;
- likely package reuse mapped;
- commercial logic credible.

#### Lane 2 — v2 migration

Additional requirements:

- v1 inventory;
- retained/discarded feature list;
- data migration posture;
- continuity plan if live;
- archive rule for v1.

#### Lane 3 — white-label

Additional requirements:

- NTK-06 current;
- commercial terms posture;
- tenant model;
- client admin model;
- export/exit posture;
- branding boundary;
- domain/deployment posture.

#### Lane 4 — module

Additional requirements:

- NTK-07 current for promotion;
- status label;
- classification;
- proof or founder-approved shared infrastructure reason;
- compatibility matrix posture;
- versioning posture.

#### Lane 5 — AI / knowledge

Additional requirements:

- NTK-08 current where AI assistant behaviour is involved;
- NTK-09 current where internal knowledge layer is involved;
- authority level;
- HITL review;
- source/data boundary;
- logging and cost controls;
- answer/output status posture.

### Readiness rule

If any required readiness criterion is unknown, the item is not build-ready.

The correct response is to keep the item in concept, scoping, or parked status until the missing criterion is resolved.

---

## Section 9 — Migration Rules

Migration rules govern existing v1 products and legacy repos.

### Rule 9.1 — Existing repos are v1 legacy unless explicitly reclassified

Existing product repos remain v1 legacy until a founder decision and SCOPING.md classify them as active v2 migration.

### Rule 9.2 — Migration is a rebuild, not a copy-paste

A v1 product must not be copied wholesale into `nikari-platform`.

The v2 rebuild must:

- re-check product truth;
- identify reusable packages;
- rebuild product-specific logic in `packages/vertical/[product]/`;
- import from shared packages where ready;
- avoid carrying v1 architecture drift into v2;
- perform data migration review where relevant.

### Rule 9.3 — No forced migration

A v1 product migrates only at:

- natural major rebuild point;
- founder decision;
- major feature set requiring platform architecture;
- technical debt threshold;
- commercial opportunity requiring v2;
- security/compliance reason; or
- operational reason strong enough to justify migration.

### Rule 9.4 — Maintenance is not migration

Maintenance, bug fixes, security patches, compliance fixes, and operational-continuity work may occur in v1 where approved.

Strategic new feature expansion should route to v2 scoping unless founder-approved otherwise.

### Rule 9.5 — SCOPING.md required before migration build

A migration requires:

- v1 inventory;
- v2 SCOPING.md;
- data migration review if data exists;
- continuity/rollback posture;
- module readiness check;
- Build OS Build Plan;
- founder approval.

### Rule 9.6 — Archive, do not delete

A v1 repo should be archived rather than deleted after v2 is confirmed live, unless a separate founder-approved deletion or retention decision exists.

### Rule 9.7 — Migration may create module candidates

During v2 migration, reusable patterns may become extraction candidates.

They do not become shared modules automatically. NTK-07 governs promotion.

---

## Section 10 — Portfolio Review Cadence

The portfolio map must be reviewed at defined moments.

### Review after new product concept

When a new concept appears, review:

- status;
- category;
- likely lane;
- relevant NTK documents;
- whether it duplicates an existing product;
- whether it belongs outside Nikari Tech;
- next decision.

### Review before scoping

Before SCOPING.md, confirm:

- product entry is complete;
- founder approved scoping;
- status is `scoping`;
- lane candidate is clear;
- commercial logic is credible;
- critical unknowns are identified.

### Review before Build OS

Before Build OS produces a Build Plan, confirm:

- SCOPING.md approved;
- relevant NTK documents current;
- product is `build_os_ready`;
- required standards are identified;
- Build OS is the correct project;
- no portfolio overload issue exists.

### Review after pilot success

After a pilot succeeds, decide whether to:

- keep as pilot;
- move to scoping;
- move to active build;
- route module candidate to Lane 4;
- park;
- retire;
- update NTK-03;
- update portfolio map.

### Review after product retirement

When a product is retired, confirm:

- user/client communication where relevant;
- data retention;
- repo/archive status;
- domain status;
- billing/subscription closure;
- support wind-down;
- knowledge/source updates;
- portfolio map update.

### Review after white-label opportunity

When an external opportunity appears, confirm:

- whether it is exploratory or serious;
- commercial terms posture;
- NTK-06 applicability;
- client/tenant status;
- product category;
- white-label risk;
- Build OS boundary.

### Review after NTK document change

If NTK-01 to NTK-09 changes in a way that affects product routing, the portfolio map must be reviewed for affected products.

### Review cadence minimum

Even without a specific trigger, the portfolio map should be reviewed:

- after three Nikari Tech governance sessions; or
- quarterly; or
- whenever founder identifies portfolio drift.

---

## Section 11 — Capacity, Sequencing, and Prioritisation Discipline

Portfolio routing is not only classification. It is also capacity control.

A product may be valid, strategically attractive, and commercially useful while still being sequenced later because Nikari Tech cannot safely activate every product at once.

### Core sequencing rule

The core sequencing rule is:

> **Active build capacity is founder-prioritised. Portfolio status does not create build capacity.**

No product, module, migration, white-label opportunity, AI assistant, or knowledge-layer product may move into `active_build` merely because it is important.

The founder must confirm:

- why this item should be active now;
- what it displaces or delays;
- whether Build OS capacity exists;
- whether the relevant NTK documents are current;
- whether SCOPING.md is complete;
- whether the work is strategically sequenced correctly; and
- whether the item should instead remain `formal_concept`, `scoping`, `pilot`, `future_candidate`, or `parked`.

### Active build capacity rule

A product should not be marked `active_build` unless:

1. founder prioritisation is explicit;
2. SCOPING.md or equivalent governed scope is approved;
3. the correct operating lane is confirmed under NTK-01;
4. applicable specialised standards are current;
5. Build OS can produce a Build Plan without unresolved portfolio conflict;
6. the work does not outrun available review, testing, deployment, or support capacity; and
7. the portfolio map is updated.

### Competing-products rule

When two or more products compete for activation, compare:

- strategic urgency;
- commercial value;
- dependency value;
- whether one product unlocks another;
- risk reduction;
- current user/client need;
- build complexity;
- module leverage;
- AI/knowledge-layer dependency;
- white-label opportunity;
- required founder attention; and
- whether delay creates real downside.

Where the comparison is unclear, do not activate both by default. Park or keep one in scoping until the founder prioritises.

### Sequencing states

Use these sequencing states inside product notes, portfolio review, or product entries where helpful:

| Sequencing state | Meaning |
|------------------|---------|
| `now` | Founder-prioritised for current active work. |
| `next` | Expected next after current active work completes or reaches gate. |
| `after_dependency` | Waiting for another product, module, NTK document, or Build OS output. |
| `parked_until_trigger` | Parked until a named trigger occurs. |
| `watch` | Monitor but do not scope or build yet. |
| `not_prioritised` | Valid idea but not currently prioritised. |

### Activation rule

Activation means a product moves toward current build attention.

Activation requires:

- current product entry;
- status change to `scoping`, `build_os_ready`, or `active_build` as applicable;
- founder confirmation;
- relevant NTK documents current;
- Build OS involvement where build planning is next;
- NTK-03 append where architecture-relevant; and
- portfolio map update.

### Parking rule

Parking is a positive discipline, not rejection.

A parked product must record:

- why it is parked;
- what trigger would reactivate it;
- whether any open issue remains;
- whether any dependency must be watched;
- whether any cost or domain/support obligation remains; and
- next review trigger.

### Retirement rule

Retirement means the product or concept is no longer intended for future build or commercial use.

Retirement should record:

- reason for retirement;
- archive or repo decision;
- data retention implications;
- user/client communication where applicable;
- domain/billing/support closure where applicable;
- knowledge-layer/source update where applicable; and
- whether the product may re-enter only through new founder decision.

### Rejection rule

A rejected idea is not held as a live portfolio item unless traceability is useful.

Where recorded, the rejection note should state:

- what was rejected;
- why;
- what new facts would be required to reconsider; and
- whether it should be archived, ignored, or parked instead.

---

## Section 12 — Risks

### Risk 1 — Too many active products

Too many products move into active build at the same time.

This creates Build OS overload, weak scoping, shallow testing, and execution drift.

**Mitigation:** Active build status requires founder approval, SCOPING.md, Build OS readiness, and portfolio capacity review.

### Risk 2 — Unclear maturity

A product is discussed as if it is active when it is only a concept.

**Mitigation:** Every product must carry a status label. No unlabelled product may proceed to scoping or build.

### Risk 3 — Concepts treated as commitments

A brainstorm, review, issue, or concept note is treated as a delivery commitment.

**Mitigation:** Concept status is not build authority. Serious work requires scoping and founder approval.

### Risk 4 — Legacy forgotten

A v1 product continues to operate without review, security attention, or migration decision.

**Mitigation:** Legacy v1 products remain in the portfolio map with review triggers and migration posture.

### Risk 5 — Forced migration

A v1 product is moved into `nikari-platform` too early.

**Mitigation:** Migration is a Lane 2 rebuild requiring founder decision, v1 inventory, SCOPING.md, Build OS plan, and no copy-paste.

### Risk 6 — Products built outside architecture

A product is started in a separate repo, app, or tool without NTK routing.

**Mitigation:** Every new product starts through NTK-10 routing and NTK-01 lane assignment.

### Risk 7 — White-label promise outruns platform readiness

A client opportunity becomes a build or commercial commitment before tenant, data, exit, billing, admin, and deployment posture are governed.

**Mitigation:** Lane 3 requires NTK-06, commercial posture, SCOPING.md, and Build OS plan.

### Risk 8 — AI or knowledge product bypasses specialised standards

An AI or internal knowledge feature is treated like ordinary product work.

**Mitigation:** Lane 5 and overlay gates apply. NTK-08 and NTK-09 must be current where relevant.

### Risk 9 — Module pilot becomes product by accident

A reusable pattern, package, or organ becomes a product or stable module without proof.

**Mitigation:** Module pilots stay labelled. NTK-07 governs promotion. Productisation requires NTK-10 routing.

### Risk 10 — NRE dominates platform portfolio

Nikari Real Estate remains important but distorts the platform so other products become second-class.

**Mitigation:** NTK-00 and NTK-02 keep Nikari Tech as the centre. NRE is flagship, not the whole architecture.

### Risk 11 — Over-generic portfolio grouping

Products are grouped too generically, causing product truth to be flattened.

**Mitigation:** Category does not erase product-specific truth. Product-specific vertical logic stays product-specific until proven reusable.

### Risk 12 — Parked ideas keep consuming attention

Parked or future candidate ideas repeatedly reopen without new decision triggers.

**Mitigation:** Parked ideas require reactivation trigger before scoping or build attention.

---

## Section 13 — Update Triggers

This document must be reviewed and updated when any of the following occur:

1. a new product concept is created;
2. a product changes status;
3. a product enters `scoping`;
4. a product becomes `active_build`;
5. a product is parked, retired, rejected, merged, or split;
6. a v1 legacy product becomes a v2 candidate;
7. a v2 migration is approved;
8. a white-label client opportunity reaches serious scoping;
9. a module pilot becomes a formal Lane 4 candidate;
10. an AI assistant product or overlay is proposed;
11. a knowledge-layer product or module is proposed;
12. product commercial logic changes materially;
13. tenant relevance changes materially;
14. data sensitivity changes materially;
15. product category changes;
16. current or target repo/app/package location changes;
17. product build readiness changes;
18. product priority or sequencing changes;
19. portfolio load creates active-capacity risk;
20. a new operating lane is proposed;
21. NTK-00 is completed to v1.0;
22. NTK-01 changes operating lanes, delivery modes, lifecycle stages, or intake rules;
23. NTK-02 changes product portfolio guardrails or anti-drift rules;
24. NTK-03 changes decision-log or supersession requirements;
25. NTK-04 changes app placement, migration, or monorepo structure;
26. NTK-05 changes package families, vertical logic, or contracts/Joints affecting products;
27. NTK-06 changes white-label routing;
28. NTK-07 changes module-pilot or promotion implications;
29. NTK-08 changes AI product routing implications;
30. NTK-09 changes knowledge-layer product routing implications; or
31. founder identifies portfolio drift not covered by this document.

### NTK-03 append note

After founder confirmation of NTK-10, NTK-03 should receive append entries for any product-portfolio decisions the founder wants recorded as discrete Nikari Tech decisions.

At minimum, the adoption of NTK-10 as the formal Product Portfolio and Routing Map should be recorded.

Likely NTK-03 entries include:

1. formal product portfolio routing requires NTK-10;
2. every product or concept must have a status label;
3. current portfolio status map adopted;
4. product entry template adopted;
5. routing decision test adopted;
6. build readiness criteria adopted;
7. v1 migration remains rebuild-only and requires Lane 2;
8. portfolio review cadence adopted;
9. active build capacity and sequencing discipline adopted;
10. parked concepts do not consume Build OS capacity without reactivation;
11. NRE is flagship but must not dominate the portfolio architecture.

These entries should remain separate if recorded, because they govern different parts of portfolio status, product routing, migration, and activation discipline.

---

*Version: 1.0 — working standard*  
*Produced: Nikari Tech — NTK-10 Product Portfolio and Routing Map Session, 29 April 2026*  
*Approved by: Wiets Marais — 29 April 2026*  
*Read with: UNIVERSAL_DECISIONS.md, NTK-00, NTK-01, NTK-02, NTK-03, NTK-04, NTK-05, NTK-06, NTK-07, NTK-08, NTK-09*  
*Next update trigger: See Section 13*  
*Proposed repo location: `wietsmarais/docs/architecture/NTK-10_Product_Portfolio_and_Routing_Map.md`*
