# NTK-06 — White Label Tenant and Deployment Model

**File:** NTK-06_White_Label_Tenant_and_Deployment_Model.md  
**Status:** Working standard — founder confirmed, pending GitHub commit  
**Owner:** Nikari Tech  
**Layer:** Build Architecture / White-Label Governance / Deployment Governance  
**Purpose:** Defines the white-label tenant model, deployment posture, tenant isolation rules, branding boundaries, domain routing, feature gating, billing posture, client admin model, data export rules, and external-system posture for Nikari Tech products and client deployments.  
**Read with:** UNIVERSAL_DECISIONS.md, NTK-00 (Master Intent), NTK-01 (Operating Model), NTK-02 (Guardrails), NTK-03 (Decision Log), NTK-04 (Monorepo Architecture), NTK-05 (Component and Contracts Architecture). Reference NTK_OUTLINE_SET_28042026.md only when checking the governed NTK-06 outline.  
**Supersedes / Subordinates:** Subordinate to UNIVERSAL_DECISIONS.md, NTK-00, NTK-01, and NTK-02. Complements NTK-04 and NTK-05. Expands the white-label guardrails in NTK-02. Does not weaken NTK-02. Does not authorise any Lane 3 client build by itself.  
**Update trigger:** First external white-label scoping; first Lane 3 client build; tenant isolation strategy change; domain routing strategy change; billing or licensing model change; Supabase project isolation change; client admin model change; data export or exit rule change; white-label security incident; or any NTK-01, NTK-02, NTK-03, NTK-04, or NTK-05 change affecting tenancy, deployment, billing, branding, isolation, or client operation.

---

## Section 1 — Purpose

This document defines the white-label tenant and deployment model for Nikari Tech.

It exists because Nikari Tech is not only a single-product build environment. It is a governed, modular, white-label capable platform that must be able to support:

- internal Nikari products;
- existing product v2 migrations;
- external white-label client builds;
- future tenant-based product deployments;
- shared packages reused across products; and
- client-branded product experiences that remain technically and legally safe.

NTK-06 answers:

**How does Nikari Tech safely support white-label clients, tenant separation, client branding, product deployment, billing, client administration, and exit rights without weakening the platform architecture or exposing one tenant to another?**

This document is governance. It is not a Build Plan. It does not open Cursor. It does not create `nikari-platform`. It does not produce deployment code, database migrations, RLS policies, Stripe configuration, DNS configuration, Vercel configuration, or Supabase implementation steps.

It defines the model that later Build OS sessions must consume when producing SCOPING.md documents and Build Plans for white-label or tenant-aware products.

### What this document governs

This document governs:

- the meaning of tenant, organisation, workspace, user, role, entitlement, subscription, and brand configuration;
- tenant isolation rules;
- branding boundaries;
- deployment model options;
- domain routing posture;
- feature gating posture;
- billing and licensing posture;
- client admin role boundaries;
- data export and exit rules;
- Odoo and external-system posture;
- security and compliance posture;
- deployment readiness checklist; and
- risks and update triggers.

### What this document does not govern

This document does not govern:

- product lane assignment — see NTK-01;
- product intake, SCOPING.md, lifecycle gates, or delivery modes — see NTK-01;
- hard guardrails and anti-drift rules — see NTK-02;
- the decision register and supersession discipline — see NTK-03;
- monorepo repo structure and app/package placement — see NTK-04;
- package hierarchy, contracts, Joints, and dependency direction — see NTK-05;
- module promotion out of `packages/vertical/` — see NTK-07 when produced;
- AI assistant authority and HITL standards — see NTK-08 when produced;
- internal knowledge-layer standards — see NTK-09 when produced; or
- product portfolio routing — see NTK-10 when produced.

### Lane 3 boundary

Lane 3 white-label client work remains governed by NTK-01.

NTK-06 is a prerequisite for formal Lane 3 work, but it does not authorise Lane 3 work by itself.

A formal Lane 3 white-label build still requires:

- client brief received and assessed;
- commercial terms agreed before any build session opens;
- SCOPING.md produced specifically for the client product;
- NTK-06 confirmed current;
- Build OS gates satisfied;
- Module Readiness Matrix confirmed;
- founder approval; and
- no Cursor or `nikari-platform` build session opened until Build OS has produced and founder-approved a Build Plan.

---

## Section 2 — Core Rule

The core rule is:

> **White-label readiness is day-one where relevant. Tenant separation must not be retrofitted.**

White-label readiness does not mean every product must be sold externally on day one. It means that when a product has credible white-label, multi-tenant, client-operated, or future external deployment potential, its tenant posture must be addressed from the beginning.

Tenant separation must not be treated as a later hardening step.

If a product, feature, table, workflow, admin surface, billing model, AI surface, or deployment may become tenant-aware, the tenant implications must be captured at scoping and reflected in contracts, data boundaries, role boundaries, and deployment posture before implementation begins.

### What day-one white-label readiness means

Day-one white-label readiness means:

- tenant identity is part of the conceptual model where tenant relevance exists;
- tenant-owned records are designed to carry tenant identity from creation;
- RLS is considered at table creation, not after launch;
- server-side tenant validation is expected, not optional;
- branding is configuration, not a forked codebase;
- domain routing is mapped to tenant identity, not hard-coded to one client;
- features can be enabled, disabled, trialled, or licensed per tenant;
- client admin roles are bounded and auditable;
- billing is connected to tenant or subscription posture;
- data export and exit rights are defined before client handover; and
- external systems such as Odoo are optional integrations, not product foundations.

### What day-one white-label readiness does not mean

Day-one white-label readiness does not mean:

- every product must immediately become multi-tenant;
- every prototype requires full external-client hardening;
- every client receives a separate deployment;
- every client receives a separate Supabase project;
- every internal product is automatically client-ready;
- every tenant can override core platform behaviour;
- branding can override security;
- client-specific needs become universal package law; or
- NTK-06 bypasses the NTK-01 lifecycle.

### Retrofitting prohibition

Tenant separation must not be retrofitted after production for any product or client deployment where tenant separation was reasonably foreseeable.

The following are breach signals:

- tenant-owned records exist without tenant identity;
- access control relies only on front-end filtering;
- domain routing resolves tenant context only in the browser;
- admin users can access multiple tenants without logged reason;
- client branding is hard-coded into product logic;
- feature access is manually hidden rather than entitlement-based;
- billing is handled outside the tenant/subscription model without a recorded decision; or
- Odoo or another external system becomes required for core product function.

### NTK-03 flag

The following decisions in this document should now be recorded in NTK-03 after founder confirmation:

- default deployment model for Nikari Tech white-label posture;
- Supabase project isolation strategy;
- tenant ID strategy;
- billing anchor per tenant/subscription;
- domain routing authority and host-to-tenant resolution rule;
- client admin permissions model; and
- data export and exit standard.

---

## Section 3 — Tenant Model

This section defines the core white-label vocabulary for Nikari Tech.

These definitions must be reflected in `packages/contracts/` before implementation begins. NTK-06 defines the governance meaning. NTK-05 governs how the types, interfaces, constants, and Joints are later represented in `contracts/`.

### Tenant

A tenant is the operational customer or deployment boundary under which users, workspaces, records, branding, features, billing, and permissions are grouped.

A tenant may represent:

- an external white-label client;
- a Nikari-owned product operating unit;
- a client-branded deployment;
- an enterprise customer;
- a pilot customer;
- a future SaaS customer; or
- an internal Nikari tenant used for testing, demonstration, or operations.

A tenant is not merely a brand. A tenant is an access, data, billing, configuration, and governance boundary.

### Organisation

An organisation is the legal or commercial entity associated with one or more tenants.

An organisation may own or contract for:

- one tenant;
- multiple tenants;
- multiple workspaces within a tenant;
- multiple subscriptions; or
- multiple branded product deployments.

The organisation is the commercial and legal relationship layer. The tenant is the product and access boundary layer.

Example:

- Organisation: ABC Advisory Pty Ltd
- Tenant: ABC Advisory client portal
- Workspace: ABC Advisory — Sydney Team

### Workspace

A workspace is a sub-environment inside a tenant.

Workspaces allow a tenant to separate teams, departments, regions, client groups, projects, branches, or operating units without creating a separate tenant.

Workspaces must remain subordinate to tenant isolation. A workspace does not weaken tenant boundaries.

Workspace use cases may include:

- departments inside an enterprise tenant;
- branches inside a franchise tenant;
- project rooms inside a client portal;
- teams inside an internal product;
- offices or regions inside a white-label client deployment.

### User

A user is an authenticated person with access to one or more tenants, workspaces, or roles.

A user may belong to:

- one tenant;
- multiple tenants where explicitly invited;
- one workspace;
- multiple workspaces;
- a tenant staff role;
- an external partner role; or
- a Nikari super admin role.

A user identity is not itself a tenant. Access must be resolved through membership, role, entitlement, and tenant context.

### Role

A role defines what a user may do inside a tenant or workspace.

The minimum white-label role set is:

| Role | Meaning |
|------|---------|
| `tenant_admin` | Client-side administrator with bounded control over users, workspace settings, approved brand settings, and tenant-level operational settings. |
| `staff` | Standard tenant user with operational access based on assigned workspace and feature entitlements. |
| `read_only` | User who may view permitted information but may not create, edit, delete, publish, export, or administer unless separately authorised. |
| `external_partner` | External collaborator such as broker, adviser, contractor, consultant, or partner with limited scoped access. |
| `super_admin` | Nikari-controlled privileged role for platform administration, support, audit, and emergency intervention. |

Roles must not be defined only in UI logic. They must be enforceable server-side and compatible with RLS.

### Feature entitlement

A feature entitlement is a tenant, subscription, module, role, or trial-based right to access a feature.

Entitlements answer:

- Is this feature enabled for this tenant?
- Is this feature enabled for this subscription tier?
- Is this feature enabled for this workspace?
- Is this feature enabled for this role?
- Is this feature in trial mode?
- Is this feature disabled, hidden, read-only, or locked?

Entitlements are not the same as UI visibility. UI visibility may reflect entitlement state, but entitlement enforcement must occur server-side where the feature affects data, access, billing, security, AI authority, or tenant boundaries.

### Subscription

A subscription is the commercial access arrangement for a tenant or organisation.

The default billing anchor is the tenant subscription.

A subscription may include:

- base platform access;
- module access;
- seat limits;
- workspace limits;
- usage limits;
- trial period;
- managed service package;
- support level;
- integration add-ons; and
- client-specific commercial terms.

A subscription may be billed through Stripe, invoice, manual billing, partner billing, or a future commercial system, but the product access model must still be expressible through tenant subscription and entitlement records.

### Brand configuration

Brand configuration is the tenant-specific presentation and communication layer.

Brand configuration may include:

- logo;
- colour tokens;
- typography tokens;
- domain;
- email sender identity;
- UI labels;
- module visibility labels;
- support contact details;
- public-facing copy variants; and
- permitted client-specific terminology.

Brand configuration must never override security, RLS, audit logging, admin permissions, data boundaries, legal disclaimers, or tenant isolation.

### Tenant-owned record

A tenant-owned record is any product record that belongs to, was created for, is controlled by, or must be isolated to a tenant.

Tenant-owned records must carry tenant identity unless a founder-approved architecture decision says the record is global, public, system-owned, or cross-tenant by design.

Examples of tenant-owned records may include:

- users' tenant memberships;
- workspace records;
- client records;
- uploaded files;
- product records;
- workflows;
- tasks;
- invoices or billing objects;
- AI output logs;
- audit-sensitive events;
- client settings;
- brand configuration;
- domain mappings; and
- feature entitlements.

---

## Section 4 — Tenant Isolation Rules

Tenant isolation is a hard guardrail.

The default posture is that one tenant must not be able to access, infer, export, route, display, search, embed, retrieve, bill, configure, or administer another tenant's data or configuration.

### Rule 4.1 — Tenant identity on tenant-owned records

Every tenant-owned record must carry tenant identity from creation unless the record is expressly classified as:

- system-global;
- public;
- cross-tenant by design;
- platform-owned;
- universal reference data; or
- non-tenant-specific metadata.

Tenant identity must not be added later as a retrofit where tenant relevance was foreseeable.

### Rule 4.2 — Tenant ID strategy and format

The tenant ID strategy is:

- internal tenant identity uses a UUID primary key;
- tenant-owned records reference the tenant through `tenant_id`;
- `tenant_id` must not be a brand name, domain name, client name, email, or human-readable commercial label;
- a separate tenant slug or tenant code may exist for routing, display, support, or admin convenience;
- tenant slugs must not be treated as the authority for access control; and
- domain routing resolves to the internal tenant ID server-side.

Recommended conceptual fields:

| Field | Purpose |
|-------|---------|
| `tenant_id` | Internal UUID identity used for record ownership and access control. |
| `tenant_slug` | Human-readable stable slug for display, support, non-sensitive routing references, or admin search. |
| `organisation_id` | Commercial/legal parent relationship where applicable. |
| `workspace_id` | Optional sub-tenant workspace boundary. |
| `domain_id` | Domain mapping identity where custom or subdomain routing applies. |

The tenant ID must be stable. A brand rename, domain change, billing change, or organisation restructure must not change the underlying tenant ID unless a formal migration decision is made.

### Rule 4.3 — RLS is mandatory

Row Level Security is mandatory for any Supabase table that stores tenant-owned, user-owned, client-owned, private, operational, financial, workflow, AI, audit, or product data.

RLS must be designed at table creation.

A table must not be created first and secured later merely because the product is early, internal, prototype-stage, or small.

### Rule 4.4 — Server-side validation is mandatory

Tenant access must be validated server-side.

Front-end filtering may improve user experience, but it is not a security boundary.

Server-side tenant validation must confirm:

- authenticated user identity;
- tenant membership;
- workspace membership where applicable;
- role;
- feature entitlement;
- subscription state where relevant;
- requested record tenant ownership; and
- whether an admin override is active.

### Rule 4.5 — No cross-tenant leakage

Cross-tenant leakage includes more than direct data exposure.

The system must prevent leakage through:

- search results;
- dropdown options;
- dashboard counts;
- analytics summaries;
- AI retrieval context;
- document exports;
- file storage paths;
- public pages;
- cache keys;
- logs surfaced to client admins;
- billing records;
- notification templates;
- emails;
- webhooks;
- support screens; and
- browser-visible metadata.

Where aggregated analytics are intentionally cross-tenant, the aggregation must be anonymised, authorised, and documented.

### Rule 4.6 — Admin override must be logged

A Nikari super admin may need access for support, migration, audit, security, billing, or emergency intervention.

Super admin access must be:

- role-restricted;
- reason-recorded where material;
- logged;
- time-bounded where practical;
- visible in internal audit logs;
- excluded from client-facing role inflation; and
- never used as a substitute for proper tenant-level permissions.

Client tenant admins must not receive unrestricted cross-tenant access.

### Rule 4.7 — Storage isolation must follow tenant isolation

Tenant-owned files, images, documents, exports, and generated assets must follow tenant isolation.

Storage isolation may be implemented by bucket, prefix, policy, signed URL boundary, or project isolation depending on the deployment model, but the governance requirement remains the same:

**one tenant must not be able to access another tenant's files or infer private file existence.**

### Rule 4.8 — AI and retrieval isolation

If a product includes AI features, retrieval, embeddings, internal knowledge, or tenant-specific document processing, tenant isolation applies to AI context.

AI systems must not retrieve, summarise, embed, classify, cite, reason from, or expose another tenant's data unless an explicit cross-tenant aggregate use case is approved and anonymised.

Formal AI assistant or knowledge-layer builds remain governed by NTK-08 and NTK-09 when produced.

### Rule 4.9 — Tenant isolation applies even in separate deployments

A separate deployment does not remove the requirement for tenant discipline.

Even where a client has a dedicated deployment or dedicated Supabase project, the tenant model should remain present where relevant so the system can support:

- future sub-tenants;
- internal workspaces;
- migration between models;
- acquisition or restructuring;
- consistent package reuse;
- audit clarity; and
- client exit/export obligations.

---

## Section 5 — Branding Model

White-label branding is a configuration layer, not a separate codebase.

A client may receive a branded experience, but client branding must not fork the platform, bypass shared packages, weaken tenant isolation, or create product-specific architecture unless a recorded Lane 3 or product-specific decision permits it.

### Brand configuration scope

Brand configuration may include:

- logo;
- favicon;
- colour tokens;
- typography tokens;
- spacing or surface tokens where approved;
- domain;
- subdomain;
- email sender identity;
- support contact information;
- UI labels;
- navigation labels;
- dashboard labels;
- module visibility labels;
- permitted copy variants;
- client-facing legal footer text where approved; and
- tenant-specific help or onboarding content.

### Brand configuration boundaries

Brand configuration must not change:

- authentication rules;
- role permissions;
- RLS policies;
- tenant boundaries;
- data ownership;
- admin override rules;
- AI authority levels;
- audit logging;
- billing enforcement;
- export rights;
- security disclaimers;
- platform ownership notices where required; or
- Build OS / Developer OS governance.

### Branding and product truth

Branding must preserve product truth.

If a client requests terminology, workflows, or labels that materially change the meaning of a product, the request must be classified as one of:

1. permitted brand configuration;
2. tenant-specific configuration;
3. client-specific vertical logic;
4. product-specific fork risk;
5. new module candidate; or
6. rejected request because it weakens security, compliance, or product truth.

Client terminology may be supported, but it must not silently alter the underlying model.

### Module visibility

A tenant may see only the modules that are enabled for that tenant, subscription, role, workspace, or trial.

Module visibility must reflect feature entitlements.

A hidden module is not necessarily disabled. A disabled module is not merely hidden.

The difference must be clear in scoping and implementation:

| State | Meaning |
|-------|---------|
| Visible and enabled | Tenant can see and use the module. |
| Visible and locked | Tenant can see the module but cannot use it without upgrade, approval, or onboarding. |
| Hidden and disabled | Tenant cannot see or use the module. |
| Admin-visible only | Client admin or Nikari super admin can see state for support or configuration. |
| Trial-enabled | Tenant can use the module subject to trial terms and expiry. |

### Email branding

Client-branded emails may use approved sender identity, template configuration, and support details.

Email branding must not obscure:

- system notices;
- legal notices;
- billing notices;
- data export communications;
- security alerts;
- audit-relevant notifications; or
- required Nikari platform relationship notices where contractually or legally required.

---

## Section 6 — Deployment Models

NTK-06 recognises three deployment models.

All three models use the same governed codebase and package architecture. The difference is deployment isolation, environment separation, Supabase project strategy, domain routing, operational complexity, and client risk posture.

### Model A — Single shared deployment, multi-tenant

Model A uses one shared app deployment for a product, with multiple tenants resolved at runtime.

A typical Model A posture is:

- one Vercel project for the app;
- one Supabase project for the product/app;
- multiple tenants inside the same product data plane;
- tenant identity on tenant-owned records;
- RLS mandatory;
- tenant config resolved at runtime;
- domain or subdomain maps to tenant identity;
- feature entitlements enforced per tenant; and
- billing linked to tenant subscription.

Model A is strongest where:

- tenants are standardised;
- the product is SaaS-like;
- operational simplicity matters;
- cost efficiency matters;
- tenant isolation can be safely enforced through RLS and server-side validation;
- client customisation is mostly brand/configuration; and
- clients do not require dedicated infrastructure.

Model A risks:

- a tenant-isolation breach affects confidence in the whole platform;
- data model changes must consider all tenants;
- noisy-tenant issues may require controls;
- client-specific needs can pressure the universal layer; and
- support tooling must be disciplined.

Model A must not be used where the client requires physical infrastructure isolation, dedicated contractual data boundary, separate compliance posture, or bespoke operational control that cannot be safely supported in a shared deployment.

### Model B — Separate deployment per client

Model B uses a separate deployment for a client or tenant.

A typical Model B posture is:

- separate Vercel project or deployment instance;
- separate environment variables;
- separate Supabase project or dedicated database boundary;
- custom domain for the client;
- tenant model still present inside the app where relevant;
- same codebase and packages;
- client-specific configuration isolated at deployment level; and
- stronger operational separation.

Model B is strongest where:

- the client requires dedicated infrastructure;
- the client has stronger contractual or compliance requirements;
- the client wants stronger operational isolation;
- performance or volume justifies separation;
- custom integration risk is high;
- client-specific release cadence is required; or
- the engagement is high-value enough to justify additional operations.

Model B risks:

- more deployments to maintain;
- more environment variables and secrets to manage;
- more complex upgrade coordination;
- higher support burden;
- more expensive infrastructure;
- greater risk of client-specific divergence; and
- slower module compounding if not governed.

Model B must not become a justification for code forks. Separate deployment does not mean separate architecture.

### Model C — Hybrid

Model C allows Nikari Tech to operate both shared multi-tenant deployments and separate client deployments from the same governed codebase.

A typical Model C posture is:

- standard tenants default to Model A;
- high-risk, high-value, or special-condition clients may use Model B;
- shared packages remain common;
- tenant identity remains part of the model even in separated deployments;
- product logic remains in packages or vertical organs, not client forks;
- deployment choice is recorded in SCOPING.md and NTK-03 where architecture-relevant; and
- client-specific needs do not become universal law without NTK-07 promotion logic.

Model C is strongest where Nikari Tech must preserve:

- early speed;
- multi-tenant readiness;
- future client optionality;
- commercial flexibility;
- stronger isolation for selected clients;
- platform compounding; and
- the ability to operate internal products, standard white-label clients, and enterprise-like clients under one architecture.

Model C risks:

- decision ambiguity if defaults are not clear;
- inconsistent isolation if scoping is weak;
- operational complexity if too many clients are separated too early;
- support complexity across deployment types; and
- documentation drift if each deployment posture is not recorded.

### Recommended default for Nikari Tech

The recommended default is:

> **Model C — Hybrid, with Model A as the standard starting posture for ordinary tenants and Model B reserved for founder-approved high-risk, high-value, or contractually isolated clients.**

This is the best default for Nikari Tech at this stage because it preserves speed and compounding value while protecting future flexibility.

The standard starting assumption is:

- one shared codebase;
- no separate repos per client;
- tenant-aware runtime configuration;
- shared app deployment where commercially and technically appropriate;
- shared Supabase project per product/app for standard tenants;
- tenant-owned records carrying `tenant_id`;
- RLS and server-side validation from day one; and
- separate deployment / separate Supabase project only where the approved client scope requires it.

This recommendation should now be recorded in NTK-03 after founder confirmation.

### Supabase project strategy

The Supabase project strategy is:

| Situation | Default posture |
|-----------|-----------------|
| Internal product or standard SaaS-like tenant use | Shared Supabase project per product/app, with tenant isolation enforced by `tenant_id`, RLS, and server-side validation. |
| Standard Lane 3 white-label client with normal data-boundary needs | Shared Supabase project may be used if SCOPING.md confirms tenant isolation and client terms allow it. |
| High-risk, high-value, regulated, enterprise, unusually customised, or contractually isolated client | Separate Supabase project or dedicated database boundary may be used with founder approval. |
| Product requiring extreme isolation or materially different compliance posture | Model B or a specifically approved variant must be scoped. |

A separate Supabase project is an isolation tool, not a substitute for good tenant architecture.

A shared Supabase project is permitted only where tenant isolation is designed properly from the start.

### Deployment decision rule

Deployment model selection must be recorded in the product or client SCOPING.md.

If the deployment decision materially affects platform architecture, client commitments, data boundaries, billing, operational support, or package structure, it must also be flagged for NTK-03 entry.

---

## Section 7 — Domain Routing

Domain routing is the process by which a request domain or subdomain resolves to the correct tenant and brand configuration.

Domain routing is not merely visual branding. It is part of tenant context resolution.

### Domain routing rule

The rule is:

> **Host-to-tenant resolution must happen server-side before tenant-owned data, features, branding, or admin surfaces are loaded.**

The browser must not be trusted as the source of tenant identity.

### Supported domain patterns

Nikari Tech may support the following patterns:

| Pattern | Example | Use case |
|---------|---------|----------|
| Nikari-owned product domain | `product.nikari.com.au` | Internal product, shared product, or Nikari-operated platform. |
| Tenant subdomain | `client.product.nikari.com.au` | Standard tenant identity under a Nikari-controlled product domain. |
| Client custom domain | `portal.client.com.au` | White-label client-branded deployment. |
| Dedicated deployment domain | `app.client.com.au` | Model B separate client deployment. |
| Internal/admin domain | `admin.product.nikari.com.au` | Nikari or product-level administration. |

Actual domain implementation belongs to Build OS and deployment sessions. NTK-06 defines the governance posture only.

### Domain mapping model

A domain mapping must resolve to:

- tenant ID;
- product/app identity;
- brand configuration;
- deployment model;
- canonical domain;
- allowed hostnames;
- SSL/TLS status where applicable;
- email sender posture where applicable;
- environment posture; and
- active/inactive status.

A domain must not resolve directly to a tenant merely because the domain string contains a client name.

The host must be matched against a governed domain mapping.

### Canonical domain

Each tenant should have one canonical domain for primary user access.

Additional domains may redirect, alias, or support special flows if scoped.

A canonical domain helps prevent:

- duplicate login contexts;
- cookie/session confusion;
- inconsistent branding;
- SEO ambiguity where relevant;
- email link mismatch;
- support confusion; and
- user trust issues.

### Failed domain resolution

If a request domain cannot be resolved to a valid active tenant, the system must fail safely.

Safe failure means:

- no tenant data is loaded;
- no fallback tenant is assumed;
- no default client data is displayed;
- no cross-tenant search or inference occurs;
- the user sees a neutral error or holding page; and
- the event is logged where appropriate.

### Domain routing and admin surfaces

Admin domains and client domains must be deliberately scoped.

A client custom domain does not automatically grant access to Nikari super-admin surfaces.

Nikari super-admin surfaces must remain protected by role, environment, and access controls regardless of branding.

### Domain routing and Model B

In Model B, a client may have a separate deployment and separate environment variables. Even then, domain routing must remain explicit.

The deployment may know its client context through environment configuration, but tenant identity must still be clear, auditable, and compatible with export, billing, and support obligations.

### NTK-03 flag

The host-to-tenant server-side resolution rule and the domain mapping posture should now be recorded in NTK-03 after founder confirmation.

---

## Section 8 — Feature Gating

Feature gating controls which modules, capabilities, workflows, surfaces, and actions are available to a tenant, workspace, role, subscription, or trial.

Feature gating is a governance and security concern. It is not merely UI hiding.

### Feature gate dimensions

Feature gates may apply by:

- tenant;
- organisation;
- workspace;
- subscription tier;
- module;
- role;
- trial state;
- onboarding state;
- payment status;
- client contract;
- jurisdiction or region where relevant;
- risk tier;
- admin approval; or
- founder-approved exception.

### Per-tenant gating

Per-tenant gating controls whether a tenant may access a feature at all.

Examples:

- Tenant A has the reporting module enabled.
- Tenant B does not have the reporting module.
- Tenant C has the reporting module in trial mode.

Per-tenant gating must be stored in tenant or entitlement configuration, not hard-coded into app logic.

### Per-subscription-tier gating

Subscription tiers may enable or limit feature sets.

The subscription tier must not be the only access-control mechanism where the feature affects sensitive data, tenant boundaries, admin actions, billing, exports, AI authority, or public publishing.

Role and server-side validation still apply.

### Per-module gating

Modules may be enabled, disabled, locked, trialled, or hidden per tenant.

Module gates should support:

- enabled;
- disabled;
- locked;
- trial;
- expired;
- read-only;
- admin-only; and
- pending setup.

### Trial mode

Trial mode must be explicit.

A trial may include:

- start date;
- end date;
- trial feature set;
- usage limits;
- seat limits;
- export restrictions;
- conversion behaviour;
- expiry behaviour; and
- client notification posture.

Trial expiry must not create insecure bypasses or silent data loss.

### Disabled state

A disabled feature must not merely disappear visually.

Where a feature is disabled, the system must define:

- whether existing data remains viewable;
- whether export remains available;
- whether admins can see the disabled state;
- whether users are redirected;
- whether billing changes apply;
- whether data retention rules apply; and
- whether reactivation is possible.

### Feature gates and Build OS

When a Build Plan includes a feature that is tenant-gated, Build OS must require the relevant entitlement posture to be specified before implementation.

NTK-06 defines the requirement. Build OS enforces it later.

---

## Section 9 — Billing and Licensing

Billing and licensing must align with tenant posture.

The default commercial access unit is the tenant subscription.

This does not prevent per-seat, per-module, per-usage, per-build, managed-service, or future SaaS pricing. It means the product entitlement model must be able to express billing and licensing through tenant, subscription, module, role, and entitlement relationships.

### Billing anchor

The default billing anchor is:

> **One tenant has one primary subscription posture, with optional seats, modules, workspaces, usage, integrations, managed services, and contract-specific add-ons.**

Where an organisation owns multiple tenants, billing may occur at organisation level, but product access must still be expressible per tenant.

### Billing posture by lane

| Lane | Billing posture |
|------|-----------------|
| Lane 1 — Internal Nikari Product Builds | Product-specific revenue model. Tenant/subscription structure used where product is multi-tenant or future white-label capable. |
| Lane 2 — Existing Product v2 Migration | Existing product commercial model may continue, but v2 must not block future tenant/subscription posture where relevant. |
| Lane 3 — White-Label Client Builds | White-label build fee + platform licence + optional managed service + optional module licence. Commercial terms confirmed before SCOPING.md. |
| Lane 4 — Shared Module Development | Usually internal leverage, but future module licensing preserved. |
| Lane 5 — AI Assistant / Internal Knowledge Products | Embedded features inherit parent product billing; standalone AI products require separate SCOPING.md and commercial decision. |

### Subscription fields to preserve conceptually

The product model should preserve the ability to represent:

- subscription tier;
- subscription status;
- billing account;
- billing owner;
- payment method posture;
- contract start date;
- renewal date;
- cancellation date;
- trial dates;
- seat limits;
- workspace limits;
- module entitlements;
- usage limits;
- support level;
- managed service level;
- integration add-ons;
- invoice billing posture; and
- founder-approved exceptions.

### Billing must not depend on Odoo

Odoo may be used for Nikari's own business operations or a client-specific operations workflow if scoped.

Odoo must not be required for core product billing, subscription gating, feature entitlement enforcement, or white-label client operation unless a specific product-level decision is made and a non-Odoo path remains available where white-label architecture requires it.

### Licensing posture

Licensing may apply at multiple levels:

- platform licence;
- tenant licence;
- module licence;
- seat licence;
- managed service licence;
- integration licence;
- AI feature licence;
- support licence; or
- future SaaS licence.

Licensing must be documented in commercial terms and reflected in entitlement logic.

### Billing and exit

Commercial terms must define what happens on cancellation, non-payment, expiry, termination, or exit.

At minimum, SCOPING.md or commercial terms must specify:

- access downgrade behaviour;
- data export availability;
- retention period;
- deletion/anonymisation posture;
- outstanding billing treatment;
- transition support;
- domain release or redirect behaviour; and
- continued access to historical records where applicable.

### NTK-03 flag

The tenant subscription billing anchor should now be recorded in NTK-03 after founder confirmation.

---

## Section 10 — Client Admin Model

The client admin model defines what a white-label client can control inside its tenant.

Client administration must empower the client without giving the client platform authority.

### Role hierarchy

The minimum role hierarchy is:

1. `super_admin` — Nikari-controlled platform role.
2. `tenant_admin` — client-side administrator for a tenant.
3. `staff` — ordinary tenant user.
4. `external_partner` — scoped collaborator.
5. `read_only` — limited view user.

A product may add product-specific roles if scoped, but product-specific roles must not weaken the minimum hierarchy or bypass tenant isolation.

### Super admin

The `super_admin` role belongs to Nikari.

A super admin may support:

- tenant setup;
- domain setup;
- billing support;
- security review;
- support escalation;
- audit investigation;
- migration;
- emergency access; and
- platform administration.

Super admin actions affecting tenant data, permissions, billing, exports, public publishing, AI authority, or security must be logged where material.

### Tenant admin

The `tenant_admin` role belongs to the client-side administrative layer.

A tenant admin may be allowed to manage:

- tenant users;
- workspace users;
- staff invitations;
- external partner invitations;
- role assignments within permitted bounds;
- workspace configuration;
- approved brand configuration;
- notification preferences;
- tenant-level operational settings;
- module requests;
- export requests where permitted;
- billing contact details where scoped; and
- support tickets where scoped.

A tenant admin must not be allowed to:

- access another tenant;
- assign themselves super admin;
- disable RLS;
- change auth rules;
- bypass subscription or feature gating;
- override audit logging;
- access service keys;
- alter domain routing without approved process;
- export another tenant's data;
- alter package behaviour;
- change platform-wide settings;
- disable mandatory security notices; or
- turn client-specific requirements into universal package behaviour.

### Staff

The `staff` role is the ordinary tenant operating role.

Staff permissions are product-specific but must be bounded by:

- tenant membership;
- workspace membership;
- role;
- feature entitlements;
- product-specific access rules; and
- tenant admin configuration where allowed.

### Read-only

The `read_only` role may view permitted records but must not mutate data unless a specific product scope grants a narrowly defined exception.

Read-only users must not:

- publish;
- export sensitive data unless expressly permitted;
- invite users;
- change settings;
- trigger billing changes;
- alter AI outputs;
- perform destructive actions; or
- administer other users.

### External partner

The `external_partner` role is for scoped external collaborators.

Examples may include:

- brokers;
- advisers;
- builders;
- lawyers;
- consultants;
- suppliers;
- referral partners;
- auditors; or
- client contractors.

External partner access must be:

- purpose-limited;
- time-limited where appropriate;
- workspace-limited where appropriate;
- data-limited;
- revocable;
- logged where material; and
- unable to expand itself.

### Client admin permissions model

The default permissions model is:

| Capability | Super admin | Tenant admin | Staff | External partner | Read-only |
|------------|-------------|--------------|-------|------------------|-----------|
| Access own tenant data | Yes | Yes | Yes, scoped | Yes, scoped | Yes, scoped |
| Access other tenant data | Only with logged platform reason | No | No | No | No |
| Manage tenant users | Yes | Yes, bounded | No | No | No |
| Manage roles | Yes | Yes, bounded | No | No | No |
| Manage brand settings | Yes | Approved settings only | No | No | No |
| Manage domain routing | Yes | Request/approval only | No | No | No |
| Manage billing settings | Yes | Scoped billing contact/admin only | No | No | No |
| Enable modules | Yes | Request/approval only unless scoped | No | No | No |
| Export tenant data | Yes, logged | Yes if scoped and logged | No unless scoped | No unless scoped | No unless scoped |
| Override tenant isolation | Emergency/support only, logged | No | No | No | No |
| Change platform settings | Yes | No | No | No | No |

### NTK-03 flag

The minimum white-label role hierarchy and permissions model should now be recorded in NTK-03 after founder confirmation.

---

## Section 11 — Data Export and Exit Rules

Data export and exit rights must be defined before any formal Lane 3 client handover.

White-label clients must not be trapped because the system failed to define exit obligations. At the same time, client exit must not transfer Nikari platform IP, shared packages, internal tools, other tenant data, proprietary prompts, system logic, or governance documents unless expressly contracted.

### Core exit rule

The core rule is:

> **A tenant may export its tenant-owned data, but not the Nikari Tech platform.**

Client data portability and Nikari platform ownership must be held together.

### Exportable by default, subject to contract and security

Subject to commercial terms, product scope, privacy obligations, and security review, the following are generally exportable for the relevant tenant:

- tenant-owned records;
- tenant user list and membership records;
- workspace records;
- tenant-created content;
- client-uploaded files;
- client-owned documents;
- tenant-specific operational records;
- tenant-specific audit extracts where appropriate;
- billing history relevant to the tenant where appropriate;
- feature usage records where appropriate;
- AI outputs generated for that tenant where product scope permits; and
- brand configuration values.

### Not exportable by default

The following are not exportable by default:

- Nikari platform source code;
- shared packages;
- package architecture;
- `contracts/` definitions as a standalone asset;
- Build OS documents;
- Developer OS documents;
- NTK governance documents;
- internal Nikari prompts;
- system prompts;
- proprietary AI orchestration logic;
- model routing logic;
- internal support notes not intended for client release;
- other tenant data;
- cross-tenant analytics that cannot be safely anonymised;
- security rules;
- RLS policies as reusable implementation assets;
- private audit logs affecting other tenants or platform security;
- Nikari-owned templates not licensed to the tenant; and
- platform-level configuration not owned by the tenant.

A contract may grant additional deliverables, but that must be explicit.

### Export format

Export format should be commercially practical and technically reasonable.

Possible formats include:

- CSV;
- JSON;
- ZIP archive;
- document export;
- media folder export;
- structured relational export;
- API-based export; or
- agreed migration package.

The exact export format belongs in the client SCOPING.md and commercial terms.

### Exit process

A client exit should follow a documented process:

1. Exit trigger confirmed.
2. Authority to request export confirmed.
3. Billing and contract status checked.
4. Export scope confirmed.
5. Tenant data boundary verified.
6. Export generated.
7. Export integrity checked.
8. Secure handover completed.
9. Retention period begins.
10. Domain transition, redirect, or deactivation handled.
11. Access downgrade or closure performed.
12. Deletion, anonymisation, or archive action completed according to agreed retention posture.
13. Exit recorded in audit and handover records.

### Retention and deletion

Retention and deletion rules must be defined before handover.

At minimum, the client scope or commercial terms must define:

- retention period after termination;
- whether data is archived, deleted, anonymised, or retained for legal reasons;
- how backups are handled;
- whether audit logs are retained;
- whether AI logs are retained;
- whether billing records are retained;
- whether support records are retained;
- how deletion confirmation is handled; and
- what legal or compliance exceptions apply.

### Export security

Export is a high-risk action where tenant data, private user information, financial information, legal information, AI outputs, or client records are involved.

Export must be:

- authorised;
- tenant-scoped;
- logged;
- reviewed where risk requires;
- delivered securely;
- time-limited where a download link is used; and
- protected from cross-tenant inclusion.

### Exit does not equal code handover

A white-label client may operate under its brand, but unless contractually agreed, it does not own the Nikari Tech platform, source code, shared packages, internal governance, or reusable module library.

White-label operation is not automatic software ownership.

### NTK-03 flag

The core exit rule — tenant may export tenant-owned data but not the Nikari Tech platform — should now be recorded in NTK-03 after founder confirmation.

---

## Section 12 — Odoo and External System Rule

The rule is:

> **Supabase is the Nikari Tech product data plane. Odoo is optional integration only. White-label clients must be able to run without Odoo.**

This rule is already locked in the universal and Nikari Tech governance posture. NTK-06 applies it specifically to white-label tenants and deployment models.

### Supabase product data plane

Supabase is the product data plane for Nikari Tech products unless a founder-approved architecture decision says otherwise.

For white-label posture, this means product data, tenant-owned records, tenant memberships, feature entitlements, brand configuration, domain mapping, audit-sensitive records, and product workflows should be capable of operating through the Supabase product data plane.

### Odoo as optional integration

Odoo may be used as:

- Nikari's own business operations system;
- a client-specific operations integration;
- CRM integration;
- invoicing or accounting integration;
- support or back-office integration;
- workflow integration; or
- future integration module under `packages/integrations/`.

Odoo must not be treated as:

- the universal product foundation;
- the required tenant store;
- the required billing authority;
- the required white-label client operations layer;
- the source of tenant isolation;
- the source of RLS;
- the required admin model; or
- the reason a client cannot run independently of Odoo.

### External system posture

External systems may include:

- Odoo;
- Xero;
- Stripe;
- email providers;
- SMS providers;
- CRM systems;
- analytics tools;
- identity providers;
- webhooks;
- third-party data providers;
- AI providers; and
- client-specific systems.

External systems must connect through scoped integrations.

An integration must not silently become the product foundation.

### Integration failure posture

A product should define what happens if an external integration fails.

The default posture is:

- core product data remains in the product data plane;
- failed integration events are logged;
- retry or reconciliation posture is defined where required;
- user-facing failure states are safe;
- tenant data is not leaked through failed sync;
- integration credentials remain server-side; and
- client operation is not wholly dependent on optional external systems unless the dependency is explicitly scoped and accepted.

### White-label client independence

A white-label client must be able to operate without Odoo unless Odoo is expressly included in that client scope as an optional integration.

A client-specific Odoo integration must not alter the universal white-label model.

---

## Section 13 — Security and Compliance

White-label readiness increases security and compliance obligations because multiple clients, brands, users, domains, subscriptions, exports, and admin layers may share the same platform architecture.

Security must be designed into the tenant model, not added as a later review.

### Security baseline

The security baseline for white-label or tenant-aware products includes:

- authentication before protected feature build;
- tenant identity on tenant-owned records;
- RLS at table creation;
- server-side tenant validation;
- role-based access control;
- no frontend service role keys;
- no frontend secrets;
- no browser-only tenant enforcement;
- audit logging for sensitive events;
- export logging;
- admin override logging;
- domain mapping validation;
- environment-variable discipline;
- integration credential isolation;
- secure file access; and
- safe failure where tenant context cannot be resolved.

### Compliance posture

NTK-06 does not create a legal compliance program. It defines the architectural posture required to support compliance.

Each product or client SCOPING.md must consider whether the product involves:

- personal information;
- financial information;
- legal information;
- health or safety information;
- employment information;
- children or vulnerable users;
- regulated industries;
- public publishing;
- AI-assisted decisions;
- cross-border data issues;
- data retention obligations;
- export obligations;
- audit obligations; or
- client-specific contractual obligations.

Where these are present, the Build OS risk classification must reflect the highest applicable risk.

### Audit-sensitive events

The following events are audit-sensitive where present:

- tenant creation;
- domain mapping change;
- brand configuration change;
- user invitation;
- role change;
- tenant admin creation;
- super admin override;
- module enable/disable;
- subscription status change;
- billing-related access change;
- data export;
- client exit;
- integration connection or disconnection;
- public publishing;
- AI output affecting users or clients;
- RLS policy change;
- auth configuration change;
- secrets rotation;
- production deployment; and
- destructive action.

### Environment separation

Environment posture must be defined for each product and white-label client.

At minimum, scoping must distinguish:

- local development;
- preview/staging;
- production;
- demo tenant;
- test tenant;
- internal Nikari tenant;
- client production tenant; and
- client sandbox tenant where applicable.

A demo or test tenant must not contain real client data unless approved and secured.

### Privacy and data minimisation

Tenant-aware products should collect and expose only the data required for the product purpose.

Data minimisation applies to:

- user profiles;
- tenant records;
- workspace records;
- AI prompts;
- support workflows;
- exports;
- analytics;
- logs;
- integration sync; and
- admin screens.

### Secrets and credentials

Secrets must never be committed to GitHub, exposed in frontend code, placed in prompts, inserted into screenshots, included in public documents, or shared with AI unnecessarily.

Client-specific credentials must be isolated and access-controlled.

### Security does not downgrade for white-label speed

White-label speed must not override security.

A client-branded demo, pilot, or early deployment that uses real users, real data, client domains, payment flows, admin roles, tenant boundaries, or external integrations must receive the correct security posture and risk classification.

---

## Section 14 — Deployment Checklist

This checklist is a governance checklist. It is not an implementation plan.

A product or client may not proceed to formal Lane 3 Build OS build planning, Cursor execution, deployment, or client handover unless the relevant items have been addressed in the concept note, SCOPING.md, Build Plan, commercial terms, or handover documents as applicable.

### A. Session and document boundary

- [ ] Session is confirmed as Nikari Tech, Build OS, or Developer OS according to decision type.
- [ ] NTK-06 is current.
- [ ] NTK-01 confirms lane assignment.
- [ ] NTK-02 guardrails reviewed.
- [ ] NTK-03 reviewed for relevant prior decisions.
- [ ] NTK-04 deployment posture reviewed.
- [ ] NTK-05 contracts and package implications reviewed.
- [ ] No Cursor session opened before Build OS produces an approved Build Plan.

### B. Tenant model

- [ ] Tenant definition confirmed.
- [ ] Organisation relationship confirmed.
- [ ] Workspace model confirmed or marked not applicable.
- [ ] User membership model confirmed.
- [ ] Role set confirmed.
- [ ] Tenant-owned records identified.
- [ ] Tenant ID strategy confirmed.
- [ ] Tenant slug/display identity separated from tenant ID.

### C. Isolation and data

- [ ] Tenant-owned records carry `tenant_id` where applicable.
- [ ] RLS required from table creation.
- [ ] Server-side tenant validation required.
- [ ] Cross-tenant leakage risks reviewed.
- [ ] Storage isolation posture confirmed.
- [ ] AI/retrieval tenant isolation reviewed where applicable.
- [ ] Admin override logging required.
- [ ] Public/private data boundaries documented.

### D. Deployment model

- [ ] Model A, B, or C selected.
- [ ] If Model C, default path selected: shared standard tenant or separated client deployment.
- [ ] Supabase project strategy confirmed.
- [ ] Vercel/project deployment posture confirmed conceptually.
- [ ] Environment posture defined.
- [ ] Deployment model recorded in SCOPING.md.
- [ ] Architecture-relevant deployment decision flagged for NTK-03 if required.

### E. Branding and domains

- [ ] Brand configuration scope confirmed.
- [ ] Branding boundaries confirmed.
- [ ] Domain pattern selected.
- [ ] Host-to-tenant resolution required server-side.
- [ ] Canonical domain defined.
- [ ] Failed domain resolution safe state defined.
- [ ] Email branding posture reviewed where applicable.

### F. Feature gating and billing

- [ ] Feature entitlement model confirmed.
- [ ] Subscription posture confirmed.
- [ ] Trial mode rules defined where applicable.
- [ ] Disabled state behaviour defined where applicable.
- [ ] Billing anchor confirmed.
- [ ] Commercial terms agreed before Lane 3 SCOPING.md.
- [ ] Odoo not required for core billing or product function unless specifically scoped.

### G. Client admin

- [ ] Super admin role confirmed.
- [ ] Tenant admin role confirmed.
- [ ] Staff role confirmed.
- [ ] Read-only role confirmed.
- [ ] External partner role confirmed where applicable.
- [ ] Role boundaries documented.
- [ ] Client admin cannot bypass tenant isolation, RLS, billing, or security.
- [ ] Admin override audit posture defined.

### H. Export and exit

- [ ] Exportable data defined.
- [ ] Non-exportable platform assets defined.
- [ ] Export format defined.
- [ ] Export authority defined.
- [ ] Exit process defined.
- [ ] Retention period defined.
- [ ] Deletion/anonymisation/archive posture defined.
- [ ] Domain transition or deactivation posture defined.
- [ ] Exit support obligations defined.

### I. External systems

- [ ] Supabase confirmed as product data plane.
- [ ] Odoo classified as optional integration only.
- [ ] White-label client can run without Odoo.
- [ ] External integrations identified.
- [ ] Integration failure posture defined.
- [ ] Credentials and secrets posture reviewed.

### J. Security and compliance

- [ ] Auth posture defined.
- [ ] Role-based access posture defined.
- [ ] RLS posture defined.
- [ ] Secrets posture reviewed.
- [ ] Audit-sensitive events identified.
- [ ] Privacy/data minimisation considered.
- [ ] Highest applicable Build OS risk classification identified.
- [ ] Security cannot be downgraded for demo, pilot, or speed.

---

## Section 15 — Risks

NTK-06 exists because white-label architecture creates material risks if not governed early.

### Risk 15.1 — Tenant separation retrofitted too late

If tenant separation is added after product logic, data tables, admin screens, storage, and AI workflows already exist, the risk of leakage and rework becomes high.

**Control:** Tenant relevance must be addressed at scoping. Tenant-owned records carry tenant identity from creation where applicable.

### Risk 15.2 — Front-end filtering mistaken for security

A UI may show only one tenant's records while the underlying API, query, storage path, or retrieval context can still access more.

**Control:** Server-side validation and RLS are mandatory. UI filtering is not a security boundary.

### Risk 15.3 — Branding weakens security

A client may request brand, copy, domain, email, or workflow changes that hide warnings, alter access, bypass review, or weaken platform controls.

**Control:** Branding is configuration only. Branding never overrides security, tenant isolation, audit logging, or admin permissions.

### Risk 15.4 — Odoo or another external system becomes accidental foundation

A client or internal product may start depending on Odoo, CRM, accounting, email, or another external system for core product function.

**Control:** Supabase remains the product data plane. External systems connect through integrations and must not become universal foundation without a recorded architecture decision.

### Risk 15.5 — Client-specific needs become universal law

One client request may distort shared packages, contracts, UI, workflows, or product logic for all products.

**Control:** Client-specific logic remains tenant configuration or vertical logic unless NTK-07 later permits promotion.

### Risk 15.6 — Over-isolation too early

Giving every client a separate deployment and separate Supabase project too early may increase support burden, slow upgrades, create inconsistent environments, and reduce platform compounding.

**Control:** Model C is the recommended default, with Model A standard for ordinary tenants and Model B reserved for founder-approved cases.

### Risk 15.7 — Under-isolation for high-risk clients

A high-risk, high-value, regulated, or contractually sensitive client may need stronger isolation than the standard shared model provides.

**Control:** Model B remains available where approved and scoped. Deployment model selection must be recorded.

### Risk 15.8 — Domain routing leaks tenant context

Incorrect host-to-tenant resolution may show the wrong brand, wrong login context, wrong records, or wrong admin surface.

**Control:** Domain resolution is server-side, based on governed domain mappings, and fails safely.

### Risk 15.9 — Billing ambiguity creates entitlement drift

If billing is not connected to tenant/subscription/entitlement posture, tenants may receive unlicensed access, lose paid access, or require manual support intervention.

**Control:** Tenant subscription is the default billing anchor. Entitlements control access and must be documented.

### Risk 15.10 — Client admin overreach

Tenant admins may accidentally or deliberately gain more authority than intended.

**Control:** Tenant admin is bounded. Super admin remains Nikari-controlled. Sensitive admin actions are logged.

### Risk 15.11 — Data export disputes

A client may assume they own more than tenant-owned data, or Nikari may fail to provide a reasonable export path.

**Control:** Exportable and non-exportable assets are defined before handover. Client data portability and Nikari platform ownership are both preserved.

### Risk 15.12 — AI cross-tenant leakage

AI retrieval, embeddings, logs, prompt context, or generated outputs may accidentally include another tenant's data.

**Control:** AI and retrieval contexts are tenant-scoped. Formal AI standards remain governed by NTK-08 and NTK-09 when produced.

### Risk 15.13 — NTK-06 mistaken as build authority

Because NTK-06 defines white-label architecture, it may be misread as permission to begin Lane 3 work.

**Control:** NTK-06 is prerequisite governance only. Lane 3 still requires NTK-01 intake, commercial terms, SCOPING.md, Build OS gates, and founder approval.

---

## Section 16 — Update Triggers

NTK-06 must be reviewed and updated when any of the following occur:

1. First external white-label client reaches scoping stage.
2. First Lane 3 white-label Build OS session is proposed.
3. First client-branded deployment is scoped.
4. First custom domain is scoped for a tenant.
5. First Model B separate client deployment is scoped.
6. First shared multi-tenant production deployment is scoped.
7. Supabase project strategy changes.
8. Tenant ID strategy changes.
9. Domain routing strategy changes.
10. Feature entitlement or subscription model changes.
11. Client admin permissions model changes.
12. Data export or exit obligations change.
13. A client requires dedicated infrastructure.
14. A client requires stronger compliance or contractual data isolation.
15. An external integration becomes materially important to product function.
16. Odoo is proposed as more than optional integration.
17. A security, privacy, tenant-isolation, or cross-tenant leakage incident occurs.
18. NTK-01 is revised in a way that affects Lane 3 or delivery modes.
19. NTK-02 is revised in a way that affects tenant, data, security, or white-label guardrails.
20. NTK-03 records a superseding white-label or deployment decision.
21. NTK-04 is revised in a way that affects deployment posture, app structure, or Supabase/Vercel assumptions.
22. NTK-05 is revised in a way that affects `packages/white-label/`, `packages/data/`, `packages/security/`, `packages/commercial/`, `packages/integrations/`, or `contracts/` tenant definitions.
23. NTK-07 introduces module promotion rules that affect client-specific white-label logic.
24. NTK-08 or NTK-09 introduces AI or knowledge-layer rules that affect tenant isolation or retrieval.
25. NTK-10 introduces portfolio routing decisions affecting white-label products.

### NTK-03 entries required after founder confirmation

Following founder confirmation of NTK-06, the following should now be appended to NTK-03 as Nikari Tech-specific decisions:

1. **Default white-label deployment posture:** Model C hybrid adopted, with Model A as standard starting posture and Model B reserved for founder-approved high-risk, high-value, or contractually isolated clients.
2. **Supabase project strategy:** shared Supabase project per product/app permitted for standard tenants with tenant ID, RLS, and server-side validation; separate Supabase project reserved for approved isolation cases.
3. **Tenant ID strategy:** internal tenant identity uses UUID `tenant_id`; slugs/domains are not access-control authority.
4. **Domain routing rule:** host-to-tenant resolution must occur server-side before tenant data, branding, features, or admin surfaces load.
5. **Billing anchor:** tenant subscription is the default commercial access anchor, preserving per-seat, per-module, per-usage, per-build, managed-service, and future SaaS flexibility.
6. **Client admin permissions model:** minimum roles are `super_admin`, `tenant_admin`, `staff`, `external_partner`, and `read_only`, with tenant admin bounded and super admin Nikari-controlled.
7. **Data export and exit standard:** a tenant may export tenant-owned data, but not the Nikari Tech platform, packages, source code, governance, internal prompts, or other tenant data unless expressly contracted.

### Commit posture

Founder confirmation has been given. This document remains pending GitHub commit.

It may guide review and correction, but it does not become committed governance until committed to:

```text
wietsmarais/docs/architecture/NTK-06_White_Label_Tenant_and_Deployment_Model.md
```

---

*Version: 1.0 — working standard, founder confirmed*  
*Produced: Nikari Tech — NTK-06 White Label Tenant and Deployment Model Session, 29 April 2026*  
*Approved by: Wiets Marais — 29 April 2026*  
*Read with: UNIVERSAL_DECISIONS.md, NTK-00, NTK-01, NTK-02, NTK-03, NTK-04, NTK-05*  
*Next update trigger: See Section 16*  
*Proposed repo location: `wietsmarais/docs/architecture/NTK-06_White_Label_Tenant_and_Deployment_Model.md`*
