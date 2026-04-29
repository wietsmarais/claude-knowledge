# NTK-02 — Nikari Tech Guardrails

**File:** NTK-02_Nikari_Tech_Guardrails.md  
**Status:** Working standard — pending founder confirmation before commit  
**Owner:** Nikari Tech  
**Layer:** Guardrails  
**Purpose:** Defines the non-negotiable rules that protect Nikari Tech architecture, product truth, tenant safety, data boundaries, AI authority, module integrity, and process discipline across every operating lane.  
**Read with:** NTK-00 (Master Intent), NTK-01 (Operating Model), NTK-04 (Monorepo Architecture), NTK-05 (Component and Contracts Architecture)  
**Supersedes / Subordinates:** Subordinate to NTK-00. Operates beside NTK-01. Enforces NTK-04 and NTK-05. Future NTK-06, NTK-07, NTK-08, and NTK-09 expand specific guardrail families but do not weaken this document.  
**Update trigger:** New architecture decision; new operating lane; first external white-label scoping; first module promotion; first AI-assistant feature; first internal knowledge-layer module; any guardrail breach; any change to NTK-01, NTK-04, or NTK-05 that affects operating constraints.

---

## Section 1 — Purpose

This document defines the hard guardrails that apply to Nikari Tech.

NTK-01 defines how work moves through the system.  
NTK-02 defines what the system must never violate while that work moves.

This document exists to prevent drift. It protects Nikari Tech from:

- product truth being weakened by premature reuse;
- platform architecture being distorted by one product;
- white-label tenancy being retrofitted after the fact;
- data boundaries becoming unclear;
- AI features gaining hidden authority;
- loose code being promoted as reusable modules;
- process shortcuts replacing governance; and
- ChatGPT, Claude, Cursor, or any tool being treated as authority outside its role.

These guardrails apply to every operating lane in NTK-01:

1. Internal Nikari Product Builds;
2. Existing Product v2 Migration;
3. White-Label Client Builds;
4. Shared Module Development; and
5. AI Assistant / Internal Knowledge Products.

They also apply to every delivery mode:

- Prototype;
- Product Build;
- White-Label Deployment; and
- Module Extraction.

A guardrail is not advice. A guardrail is a boundary. If a proposed action breaches a guardrail, the action stops until the breach is resolved or escalated to the correct governance layer.

---

## Section 2 — Master Guardrail

### Product correctness before reuse

The master guardrail is:

> **Product correctness comes before reuse. Reuse must never damage product truth.**

Nikari Tech exists to create compounding value through reusable packages, shared contracts, white-label capability, and platform leverage. But reuse is only valuable when it preserves the truth of the product being built.

A product must not be forced into a generic module pattern if doing so weakens:

- user experience;
- commercial logic;
- legal or compliance posture;
- tenant safety;
- data correctness;
- product-specific workflow truth;
- domain-specific language; or
- founder-approved strategic intent.

### What this guardrail prevents

This guardrail prevents two equal and opposite errors:

1. **Over-specificity** — every product becomes isolated, nothing compounds, and Nikari Tech becomes a collection of unrelated builds.
2. **Over-generic abstraction** — everything becomes reusable too early, product truth is flattened, and modules become vague, fragile, or commercially useless.

Both are failures.

### Correct resolution when reuse and product truth conflict

When reuse and product truth conflict:

1. Product truth wins first.
2. Product-specific logic stays in `packages/vertical/[product]/`.
3. The reusable pattern is documented as a future extraction candidate.
4. Promotion occurs only after the pattern is proven and NTK-07 permits promotion.

No one may promote a module simply because it feels reusable. It must prove itself in a real product or serious pilot.

---

## Section 3 — Architecture Guardrails

Architecture guardrails protect the shape of `nikari-platform`, the integrity of shared packages, and the contract-first discipline established in NTK-04 and NTK-05.

---

### Guardrail 3.1 — Contract-first is mandatory

`packages/contracts/` is checked before any package, organ, app, AI feature, white-label deployment, or integration is implemented.

Shared types, interfaces, constants, and Joints are defined in `contracts/` before implementation begins.

**Must happen:**

- Check whether the required type already exists.
- Check whether the required interface or Joint already exists.
- Add missing shared definitions to `contracts/` before building the dependent package.
- Import shared definitions from `contracts/`, not local copies.

**Breach:** A package defines its own shared user, tenant, session, subscription, error, response, document, audit, AI, auth, storage, config, billing, or role type.

**Required response:** Stop implementation. Move the shared definition into `contracts/`. Update imports. Record the correction in the session handover.

---

### Guardrail 3.2 — No shared type outside `contracts/`

No app or package may define a shared type that other packages also need.

Internal types may exist inside a package only if they are truly internal and never exposed across a Joint, API boundary, app boundary, package boundary, or module boundary.

**Breach:** A type begins as internal but is later imported by another package or copied into another package.

**Required response:** Promote the type to `contracts/types/` before further use.

---

### Guardrail 3.3 — Dependency direction is downward only

The dependency direction is always:

```text
apps/
  ↓
Level 3 composites
  ↓
Level 2 organs
  ↓
Level 1A UI primitives / Level 1B functional primitives
  ↓
contracts/
```

Nothing imports upward. Nothing imports sideways at the same level.

**Breach examples:**

- A Level 2 organ imports another Level 2 organ.
- A Level 3 composite imports another Level 3 composite.
- An app imports another app.
- A package reaches into another package’s internal files instead of using its Joint.

**Required response:** Stop. Move the shared concern into `contracts/`, a lower-level primitive, or a higher-level composite that wires the organs together.

---

### Guardrail 3.4 — `vertical/` before promotion

Product-specific logic belongs in `packages/vertical/[product]/` until it proves reusable.

`vertical/` is not a dumping ground. It is the correct holding place for product-specific organs before they earn promotion.

**Breach:** Product-specific logic is placed into a shared package before it has been proven across products or serious pilots.

**Required response:** Move it back into the product’s vertical package. Document the possible extraction candidate. Reassess during Stage 9 Extraction Review.

---

### Guardrail 3.5 — Do not rebuild what already exists

No team, Claude project, Cursor session, or developer may rebuild an existing package, primitive, organ, or interface without first checking whether it already exists and whether it is fit for use.

**Must happen before building from scratch:**

1. Check NTK-05 package family map.
2. Check `contracts/`.
3. Check existing packages.
4. Check relevant SPEC.md and README files.
5. Check module readiness status.
6. Only then build or gap-build.

**Breach:** Cursor creates duplicate auth, tenant, config, logger, error, billing, AI, or security logic because it did not check existing packages.

**Required response:** Stop. Compare duplicate with existing package. Delete or refactor the duplicate only after founder or Build OS approval, depending on risk tier.

---

### Guardrail 3.6 — 30-line function governor applies everywhere

No function exceeds the 30-line function governor.

If a function is trending beyond 30 lines, Cursor must stop and propose a refactor into smaller functions, helpers, primitives, or organs.

**Breach:** A function grows beyond 30 lines for convenience.

**Required response:** Refactor before continuing. Do not justify the breach as temporary unless explicitly recorded as technical debt with founder approval.

---

## Section 4 — White-Label Guardrails

White-label guardrails protect future tenant safety, client independence, and external deployment readiness.

NTK-06 will expand this section into the full White Label Tenant and Deployment Model.

Until NTK-06 exists, these guardrails govern exploratory white-label review only. They do not authorise formal Lane 3 work.

No formal Lane 3 build, onboarding, client implementation commitment, or white-label deployment may proceed unless NTK-06 exists and is current.

---

### Guardrail 4.1 — Tenant isolation is day one where white-label relevance exists

Where a product may become white-label, multi-tenant, client-deployed, or externally operated, tenant posture is addressed at scoping.

Tenant separation must not be retrofitted after production.

**Breach:** A product with clear white-label potential is scoped without tenant model, tenant-owned records, role boundaries, or isolation strategy.

**Required response:** Stop scoping. Define tenant posture before Build OS produces a Build Plan.

---

### Guardrail 4.2 — `tenant_id` is not retrofitted

Tenant-owned records must carry tenant identity from the beginning where tenant separation applies.

**Breach:** Tenant-owned data tables are created without tenant identity and later marked for retrofit.

**Required response:** Do not proceed to implementation. Rework schema before build. If already built, classify as a high-risk correction and route through Build OS.

---

### Guardrail 4.3 — White-label clients must be able to run without Odoo

Odoo is an optional business-operations integration module. It is not a universal product foundation.

White-label clients must be able to run with:

- Supabase as the product data plane;
- Vercel as deployment layer;
- Nikari package architecture; and
- optional integrations added only where scoped.

**Breach:** A white-label product requires Odoo for core product function.

**Required response:** Reclassify the Odoo dependency as an integration, not a foundation. Redesign the core product flow to run without Odoo.

---

### Guardrail 4.4 — Branding never overrides security

Client branding may change logos, colours, copy, domain, labels, and visible configuration. It may not override:

- authentication rules;
- RLS policies;
- tenant boundaries;
- data access rules;
- audit logging;
- admin permissions;
- AI authority levels; or
- deployment safety.

**Breach:** A client branding request weakens access control, bypasses review, hides disclaimers, exposes data, or changes security posture.

**Required response:** Reject or redesign the request. Record the decision in the client scoping notes or DECISIONS.md if architecture-relevant.

---

### Guardrail 4.5 — Client-specific needs do not become universal law

A white-label client request remains tenant-specific configuration or client-specific vertical logic unless it passes the promotion test for general reuse.

**Breach:** A single client requirement changes the universal package layer without proof that it is reusable.

**Required response:** Keep it in tenant configuration or `packages/vertical/[client-or-product]/` until NTK-07 permits promotion.

---

## Section 5 — Data Guardrails

Data guardrails protect product correctness, tenant safety, privacy, auditability, and deployment integrity.

---

### Guardrail 5.1 — Supabase is the product data plane

Supabase is the default product data plane for Nikari Tech products.

Other systems may connect through `packages/integrations/`, but they do not replace the product data plane unless a specific founder-approved architecture decision says so.

**Breach:** A product makes an external operations system the source of product truth without a Nikari Tech architecture decision.

**Required response:** Stop. Escalate to Nikari Tech. Record the architecture decision before implementation.

---

### Guardrail 5.2 — Odoo is optional integration, not foundation

Odoo may be used by Nikari Real Estate or other Nikari units for business operations if scoped, but it is not universal platform infrastructure.

**Breach:** Odoo is required for a non-Odoo product to function, or a package assumes Odoo presence by default.

**Required response:** Move Odoo logic into `packages/integrations/odoo/`. Provide a non-Odoo product path.

---

### Guardrail 5.3 — Service keys never enter frontend code

Service role keys, admin tokens, private API keys, secrets, or privileged credentials must never be exposed in frontend code, public repos, client-visible files, browser runtime, screenshots, prompts, or committed documents.

**Breach:** A secret is added to frontend code, `.env.example` with real values, markdown, prompt text, screenshot, or committed repo file.

**Required response:** Stop immediately. Remove the secret. Rotate the credential if exposure may have occurred. Record the secret audit result in the handover.

---

### Guardrail 5.4 — RLS is mandatory from table creation

Row Level Security must be enabled and designed at table creation for any Supabase table that stores user, tenant, client, private, operational, financial, workflow, or product data.

RLS must not be treated as a later hardening step.

**Breach:** A table is created without RLS because the product is “only internal” or “not live yet”.

**Required response:** Stop. Add RLS before use. If data already exists, classify the correction as Tier 4 or Tier 5 depending on exposure and route through Build OS.

---

### Guardrail 5.5 — Public/private data boundaries must be explicit

Every product scope must define which data is public, private, tenant-owned, admin-only, system-only, AI-accessible, exportable, or never exposed.

**Breach:** A product surface displays, sends, indexes, embeds, retrieves, or exports data without a documented boundary.

**Required response:** Stop the feature. Define the boundary in SCOPING.md, Build Plan, or relevant module spec before implementation continues.

---

### Guardrail 5.6 — Audit-sensitive events must be logged

Events affecting auth, permissions, tenant boundaries, AI outputs, public publishing, data export, billing, module promotion, destructive actions, or deployment must be logged where the product scope requires auditability.

**Breach:** A sensitive action happens silently.

**Required response:** Add logging before the feature is considered complete. If the action already occurred, document the gap and corrective action in the handover.

---

## Section 6 — AI Guardrails

AI guardrails protect authority, truthfulness, privacy, reviewability, and human approval.

NTK-08 will expand this section into the full AI Assistant Product Standard. NTK-09 will expand the knowledge-layer rules where AI work involves internal knowledge, retrieval, SOPs, handovers, governed documents, or workflow support.

Until NTK-08 exists, these guardrails govern AI-related thinking, review, and prototypes only. They do not authorise formal Lane 5 product build.

Formal Lane 5 AI product build requires NTK-08 to exist and be current. Knowledge-layer assembly requires NTK-09 where applicable.

---

### Guardrail 6.1 — AI drafts; it does not become final authority by default

AI may assist, draft, retrieve, summarise, classify, suggest, structure, and explain.

AI does not hold final authority unless the specific product scope explicitly grants a bounded, safe, reviewable authority level.

**Breach:** AI output becomes a final decision, public statement, client commitment, legal/commercial instruction, data mutation, or user-facing result without defined authority and review.

**Required response:** Stop the AI feature. Define authority level, review gate, logging, and escalation behaviour before continuing.

---

### Guardrail 6.2 — No auto-publish without explicit scope

AI output must not be automatically published, sent, submitted, committed, advertised, messaged, or acted on unless the pathway is explicitly scoped, safe, logged, and founder-approved.

**Breach:** AI-generated output bypasses human review and reaches a user, client, regulator, public page, database write, or production action.

**Required response:** Disable auto-publish path. Add HITL review queue or founder-approved scoped automation.

---

### Guardrail 6.3 — No hidden AI decision authority

Users, operators, and reviewers must be able to understand where AI is assisting and where a human or system rule remains authoritative.

**Breach:** AI silently ranks, suppresses, approves, rejects, routes, prices, profiles, or recommends in a way that materially affects users or clients without reviewability.

**Required response:** Surface the AI role, define reviewability, and document decision boundaries.

---

### Guardrail 6.4 — AI outputs must be logged and reviewable where material

Material AI outputs must be stored or logged where required by product scope, risk level, or review needs.

Material outputs include outputs that affect:

- user decisions;
- client commitments;
- commercial terms;
- legal or compliance-sensitive content;
- public copy;
- financial actions;
- tenant access;
- data changes; or
- operational routing.

**Breach:** Material AI output cannot be reviewed after the fact.

**Required response:** Add logging and review history before the feature is complete.

---

### Guardrail 6.5 — Prompt routing is server-side

Prompts, provider keys, model routing logic, retrieval permissions, and sensitive context assembly must run server-side.

**Breach:** Browser-visible code contains prompt routing logic, sensitive prompt templates, model credentials, private context, or unrestricted AI calls.

**Required response:** Move AI orchestration server-side before continuing.

---

### Guardrail 6.6 — Approved sources first; no invented policy

AI retrieval systems must prefer approved documents, governed knowledge, committed policies, and verified source files.

Where no approved source exists, AI must say so or escalate. It must not invent policy.

**Breach:** AI gives procedural, legal, governance, product, pricing, or compliance guidance without a source or approved rule.

**Required response:** Add source restriction, escalation rule, or review gate.

---

### Guardrail 6.7 — Sensitive contexts require tighter AI handling

Legal, financial, compliance, client, tenant, property, health, safety, employment, security, and identity-related AI workflows require explicit review gates and data minimisation.

**Breach:** Sensitive data is placed into an AI prompt without need, boundary, minimisation, or approval.

**Required response:** Remove unnecessary data, narrow context, add review gate, and record the handling rule.

---

### Guardrail 6.8 — Formal Lane 5 work requires the relevant NTK standard

AI-related discussion, review, and prototypes may occur under this NTK-02 minimum guardrail layer. Formal Lane 5 product build does not open until NTK-08 exists and is current.

Where the work involves internal knowledge, retrieval, SOPs, handovers, governed documents, or knowledge-layer assembly, NTK-09 must also exist and be current before formal build or assembly begins.

**Breach:** A Lane 5 AI product, assistant, retrieval system, or knowledge-layer module enters formal Build OS assembly before NTK-08 and, where applicable, NTK-09 exist.

**Required response:** Stop formal build. Reclassify as exploratory review or prototype only, or produce the required NTK standard before proceeding.

---

## Section 7 — Security Guardrails

Security guardrails protect auth, access control, admin safety, deployment integrity, and production reliability.

---

### Guardrail 7.1 — Auth before feature build

Any product or feature that requires user identity, protected data, tenant access, admin privileges, subscriptions, or role-based behaviour must define auth before feature implementation.

**Breach:** Feature implementation starts before auth and access model are defined.

**Required response:** Stop feature work. Define auth, roles, session behaviour, and access model first.

---

### Guardrail 7.2 — No frontend API secrets

No API secret, service role key, private token, webhook signing secret, payment key, AI provider key, or privileged credential may appear in frontend code or public runtime.

**Breach:** Any secret is visible in browser code, client bundle, public repository, logged prompt, screenshot, or committed file.

**Required response:** Treat as a security incident. Remove, rotate if necessary, and document.

---

### Guardrail 7.3 — No unsecured admin routes

Admin routes, operator tools, dashboards, tenant admin surfaces, internal review queues, and management screens must be protected by auth and role checks before use.

**Breach:** An admin route exists without role enforcement or can be accessed by an unauthorised user.

**Required response:** Lock the route before further implementation. Add tests or verification appropriate to risk level.

---

### Guardrail 7.4 — Pre-commit review before merge for risk-bearing changes

Any change involving auth, RLS, payments, migrations, webhooks, public publishing, data export, destructive actions, secrets, tenant boundaries, or AI authority requires the applicable Build OS risk classification and review before merge or deployment.

**Breach:** Risk-bearing change is committed or merged without the required review.

**Required response:** Pause merge/deploy. Run review. Record approval event.

---

### Guardrail 7.5 — No push to `main` without approval event

No push to `main` or production deployment occurs without the required Build OS approval event.

**Breach:** Direct push to `main`, manual production deploy, or unapproved merge.

**Required response:** Stop. Assess impact. Revert if required. Record the breach and correction.

---

### Guardrail 7.6 — Security cannot be downgraded for speed

Security gates must not be downgraded because a product is “just a prototype”, “only internal”, “not public yet”, “small”, or “temporary” if real users, real data, production systems, secrets, tenant boundaries, or external clients are involved.

**Breach:** Risk classification is lowered for convenience.

**Required response:** Reclassify to the highest applicable tier. Continue only after the correct approval path.

---

## Section 8 — Module Guardrails

Module guardrails protect reusable value from becoming undocumented, unstable, or falsely universal.

NTK-07 will expand this section into the full Module Promotion and Versioning Protocol.

Until NTK-07 exists, these guardrails may be used to identify, document, and label extraction candidates. They do not authorise formal promotion out of `packages/vertical/`.

No module may be formally promoted out of `packages/vertical/` unless NTK-07 exists and is current.

---

### Guardrail 8.1 — No loose code as modules

A folder is not a module merely because it contains reusable-looking code.

A module must have:

- clear purpose;
- defined level or package family;
- documented interface or Joint where applicable;
- README or SPEC reference;
- status label;
- version posture; and
- owner or governing document.

**Breach:** Code is moved into `packages/` without documentation, status, version posture, or interface.

**Required response:** Move it back to vertical or working space until module requirements are met.

---

### Guardrail 8.2 — Every reusable module needs docs, version, and status

A reusable module must not be treated as stable unless it has documentation, versioning, and status.

Minimum labels until NTK-07 exists:

- `experimental`;
- `pilot-proven`;
- `reusable`;
- `stable`; or
- `deprecated`.

**Breach:** A module is imported across products with no status or version posture.

**Required response:** Add status and documentation before further reuse.

---

### Guardrail 8.3 — Experimental modules must be labelled

Experimental modules may exist, but they must not masquerade as stable packages.

**Breach:** Experimental code is imported into production without label, review, or founder approval.

**Required response:** Label the module, isolate its use, and route production use through Build OS.

---

### Guardrail 8.4 — Breaking changes require version bump

Any breaking change to a package, Joint, contract, API shape, schema, auth behaviour, tenant behaviour, or exported interface requires a version bump and downstream compatibility check.

**Breach:** A package changes behaviour or interface in a way that can break consumers without versioning.

**Required response:** Stop. Add version bump, changelog entry, compatibility note, and migration path if needed.

---

### Guardrail 8.5 — Module promotion requires proof and NTK-07

A module may be formally promoted out of `packages/vertical/` only after it has worked in a real product or serious pilot and passes the promotion test in NTK-07.

Until NTK-07 exists, no module may be formally promoted out of `packages/vertical/`.

A founder may approve documenting an extraction candidate or promotion candidate before NTK-07 exists, but not formal promotion.

**Breach:** A module is promoted because it feels reusable, because a founder exception was assumed, or before NTK-07 exists.

**Required response:** Reverse the promotion. Move the code back to `packages/vertical/` or mark it as an extraction candidate only. Reassess when NTK-07 is produced.

---

## Section 9 — Product Portfolio Guardrails

Product portfolio guardrails prevent concept sprawl, premature activation, unclear maturity, and architecture distortion.

---

### Guardrail 9.1 — Not every idea becomes active

A product idea may be valuable without becoming an active build.

Every idea must receive a portfolio status before build work begins.

**Breach:** A concept moves into SCOPING.md or Build OS without product status.

**Required response:** Route through product intake and NTK-10 when available. Until NTK-10 exists, record status in the concept note or session handover.

---

### Guardrail 9.2 — Product status must be labelled

Every product or concept must be labelled with a status such as:

- active / flagship;
- active build;
- pilot;
- formal concept;
- scoping;
- legacy v1;
- v2 candidate;
- future candidate;
- parked; or
- retired.

**Breach:** A product is discussed as if active without being labelled.

**Required response:** Assign or confirm status before further strategic or build discussion.

---

### Guardrail 9.3 — Legacy does not auto-migrate

Existing products do not automatically migrate into `nikari-platform`.

A v1 legacy product migrates only at a natural major rebuild point or founder decision.

**Breach:** A v1 product is copied into the monorepo as a shortcut.

**Required response:** Stop. Treat migration as Lane 2 rebuild. Produce SCOPING.md and Build OS plan before any implementation.

---

### Guardrail 9.4 — Intake and scoping are required before build

No active product build begins without:

- concept note;
- lane assignment;
- delivery mode;
- required NTK documents identified;
- SCOPING.md where the delivery mode requires it;
- Build OS readiness check; and
- founder approval.

**Breach:** Cursor is opened against a product idea without intake and scoping.

**Required response:** Close build path. Return to product intake.

---

### Guardrail 9.5 — Portfolio load must be controlled

Too many active products create governance and build risk.

If multiple concepts compete for activation, Nikari Tech must assess sequencing rather than allowing parallel drift.

**Breach:** Multiple products move to active build without capacity, sequence, or founder prioritisation.

**Required response:** Produce or update portfolio routing. NTK-10 should govern once produced.

---

## Section 10 — Process Guardrails

Process guardrails protect the information flow, session discipline, commit discipline, and approval pathway.

---

### Guardrail 10.1 — SCOPING.md before serious build

Any serious product, module, AI feature, white-label deployment, or v2 migration requires SCOPING.md before Build OS produces a Build Plan.

Prototype work may use a lighter concept note, but it must be explicitly labelled as prototype and must not become production by drift.

**Breach:** Build Plan or Cursor session begins without required scope.

**Required response:** Stop. Produce or complete SCOPING.md.

---

### Guardrail 10.2 — PLAN.md before multi-file task

A multi-file implementation task requires PLAN.md or an equivalent approved Build Plan before execution.

**Breach:** Cursor modifies multiple files from conversation memory or vague instructions.

**Required response:** Stop. Produce a plan before continuing.

---

### Guardrail 10.3 — DECISIONS.md is append-only

Decision logs are append-only. Existing decisions are not silently edited.

If a decision changes, add a superseding entry with:

- date;
- decision;
- reason;
- status;
- affected files; and
- superseded decision reference.

**Breach:** A prior decision is rewritten or deleted without supersession.

**Required response:** Restore history where possible and add a supersession entry.

---

### Guardrail 10.4 — Session handover is required

Every governed session closes with a handover where required by the relevant project instructions.

The handover records:

- session goal;
- outputs produced;
- decisions made;
- gates passed;
- files changed;
- open actions;
- next-session prompt;
- secret audit; and
- project ownership of outputs.

**Breach:** Work is left only in conversation memory.

**Required response:** Produce the handover before closing the session.

---

### Guardrail 10.5 — UNIVERSAL_DECISIONS.md checked before architecture change

No architecture recommendation or decision is made without checking UNIVERSAL_DECISIONS.md first.

**Breach:** A new architecture decision is made from memory, convenience, or local project needs.

**Required response:** Check UNIVERSAL_DECISIONS.md. If the proposed decision conflicts, escalate before proceeding.

---

### Guardrail 10.6 — Correct project owns the decision

Project routing is mandatory:

- Nikari Tech owns platform architecture, NTK governance, and product portfolio.
- Build OS owns Build Plans, module readiness, and assembly planning.
- Developer OS owns execution discipline and repo workflow.
- ChatGPT Review reviews from the outside and does not originate governance.

**Breach:** A decision is made in the wrong project.

**Required response:** Stop. Capture the issue in handover and reopen in the correct project.

---

### Guardrail 10.7 — GitHub holds the truth

A decision, document, or standard is not governed truth until committed to the correct GitHub repo.

Project knowledge upload alone is not sufficient. Conversation agreement alone is not sufficient. ChatGPT output alone is not sufficient.

**Breach:** A document is treated as governing because it exists in chat or project knowledge only.

**Required response:** Commit to GitHub or mark as draft/reference only.

---

## Section 11 — Anti-Drift Rules

Anti-drift rules protect the long-term integrity of Nikari Tech as the portfolio grows.

These are not optional principles. They are the highest-risk long-term guardrails because drift often happens gradually and feels reasonable at the time.

---

### Anti-Drift Rule 11.1 — NRE must not dominate Nikari Tech architecture

Nikari Real Estate is the flagship product and first major build. It is not the centre of the architecture.

NRE patterns may become reusable only after they prove general usefulness. NRE-specific requirements remain in `packages/vertical/real-estate/` or NRE app scope until promoted.

**Drift signal:** A platform decision is justified mainly because “NRE needs it” without testing whether it is genuinely platform-level.

**Correct response:** Keep the decision product-specific unless Nikari Tech confirms it as universal.

---

### Anti-Drift Rule 11.2 — Generic architecture must not weaken NRE or any other product

Platform reuse must not flatten product-specific truth.

NRE, Social Shield, VIX, Counsel, StudyOS, LocalLoop, and future products may each need product-specific flows, language, data, compliance posture, or commercial logic.

**Drift signal:** A product loses clarity because it is forced into a generic package pattern too early.

**Correct response:** Move the specific logic to `vertical/` and defer promotion.

---

### Anti-Drift Rule 11.3 — AI convenience must not override governance

AI speed must not bypass human approval, source-of-truth checks, contracts, SCOPING.md, Build Plans, review gates, or commit discipline.

**Drift signal:** “The AI can just do it” becomes the reason for skipping governance.

**Correct response:** Reapply the correct operating lane, quality gate, and project boundary.

---

### Anti-Drift Rule 11.4 — One client’s needs must not become universal law

A white-label client may need a specialised feature. That does not mean the platform should change for everyone.

**Drift signal:** A client request is implemented directly in a shared package without proof of general reuse.

**Correct response:** Keep it as tenant configuration, client-specific vertical logic, or product-specific overlay until it passes module promotion rules.

---

### Anti-Drift Rule 11.5 — Prototype success must not become production permission

A prototype proving an idea does not mean the prototype is production-ready.

**Drift signal:** Prototype code, copy, schema, auth, or deployment is reused directly in production to save time.

**Correct response:** Treat production as a new Product Build with SCOPING.md, Build OS, contracts, security, hardening, and deployment gates.

---

### Anti-Drift Rule 11.6 — Internal tools must not silently become client products

Internal knowledge tools, AI assistants, operator dashboards, or admin workflows may later become productised. They do not become client-ready merely because they work internally.

**Drift signal:** An internal tool is shown or sold externally without tenant, auth, privacy, support, documentation, and commercial model review.

**Correct response:** Re-route through product intake or Lane 3 white-label scoping.

---

### Anti-Drift Rule 11.7 — Review is not governance until confirmed and committed

ChatGPT, external reviewers, brainstorm outputs, Claude drafts, and user comments may produce excellent recommendations. They are not governance until assessed in the correct Claude project, confirmed by the founder, and committed to GitHub.

**Drift signal:** A strong review recommendation is treated as decided because it sounds correct.

**Correct response:** Route through Nikari Tech assessment and commit discipline.

---

## Section 12 — Update Triggers

This document must be reviewed and updated when any of the following occur:

1. NTK-01 is materially revised.
2. NTK-04 or NTK-05 is revised in a way that affects architecture, package, contracts, dependency, or build rules.
3. NTK-06 is produced or revised.
4. NTK-07 is produced or revised.
5. NTK-08 is produced or revised.
6. NTK-09 is produced or revised.
7. NTK-10 is produced or revised.
8. A new operating lane is added.
9. A new delivery mode is added.
10. A guardrail breach occurs in a real session.
11. A white-label client reaches scoping stage.
12. A module is promoted out of `packages/vertical/`.
13. An AI feature is assembled via Build OS.
14. A knowledge-layer module is built.
15. A new security, tenant, AI, data, module, or process risk is identified.
16. A Universal Decision is added that constrains Nikari Tech architecture.
17. The first `nikari-platform` build session opens and reveals a guardrail gap.

---

*Version: 1.0 — final corrected draft for founder confirmation*  
*Produced: Nikari Tech — NTK-01 + NTK-02 Session, 29 April 2026*  
*Corrected after accepted NTK-02 alignment review: NTK-06/Lane 3, NTK-07/module promotion, and NTK-08/09/Lane 5 wording tightened*  
*Approved by: [Founder confirmation required before commit]*  
*Read with: NTK-00, NTK-01, NTK-04, NTK-05*  
*Next update trigger: See Section 12*  
*Proposed repo location: wietsmarais/docs/architecture/NTK-02_Nikari_Tech_Guardrails.md*
