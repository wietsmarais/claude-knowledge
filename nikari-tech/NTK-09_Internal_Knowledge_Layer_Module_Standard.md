# NTK-09 — Internal Knowledge Layer Module Standard

**File:** NTK-09_Internal_Knowledge_Layer_Module_Standard.md  
**Status:** Working standard — founder confirmed, pending GitHub commit  
**Owner:** Nikari Tech  
**Layer:** Knowledge Governance / Lane 5 Standard / Internal Knowledge Architecture  
**Purpose:** Defines the governance standard for internal knowledge-layer modules, approved source registries, SOP libraries, handover libraries, governed document retrieval, source hierarchy, source status labels, ingestion rules, retrieval boundaries, knowledge gap handling, access control, staleness management, testing, and package implications inside `packages/knowledge-layer/`.  
**Read with:** UNIVERSAL_DECISIONS.md, NTK-00 (Master Intent), NTK-01 (Operating Model), NTK-02 (Guardrails), NTK-03 (Decision Log), NTK-04 (Monorepo Architecture), NTK-05 (Component and Contracts Architecture), NTK-06 (White Label Tenant and Deployment Model), NTK-07 (Module Promotion and Versioning Protocol), NTK-08 (AI Assistant Product Standard).  
**Supersedes / Subordinates:** Subordinate to UNIVERSAL_DECISIONS.md, NTK-00, NTK-01, and NTK-02. Expands the knowledge-layer rules implied by NTK-02 and NTK-05. Complements NTK-08 where AI assistants retrieve, summarise, reason from, or act on internal knowledge. Does not weaken NTK-02 or NTK-08. Does not authorise any Build OS assembly session, Cursor session, database schema, embedding index, retrieval system, or knowledge product by itself.  
**Update trigger:** First internal knowledge-layer module build; first governed document retrieval feature; first SOP library build; first handover index; first source registry; first embedding or vector index for internal documents; first knowledge-layer use in a white-label product; source hierarchy change; source-status model change; retrieval boundary incident; stale or superseded-source incident; tenant/data leakage incident; or any NTK-01, NTK-02, NTK-03, NTK-04, NTK-05, NTK-07, NTK-08, or NTK-10 change affecting internal knowledge, retrieval, source authority, or knowledge-layer modules.

---

## Section 1 — Purpose

This document defines the Internal Knowledge Layer Module Standard for Nikari Tech.

It exists because internal knowledge is not ordinary content. Nikari Tech relies on governing documents, decisions, handovers, SOPs, project instructions, package documentation, Build OS records, Developer OS discipline, and product-specific knowledge. If that knowledge is ingested, indexed, retrieved, summarised, or surfaced without governance, the system can drift quickly.

NTK-09 answers:

**How does Nikari Tech safely store, classify, retrieve, index, expose, maintain, and reason from internal knowledge without turning drafts, handovers, outdated files, or AI summaries into false authority?**

This document governs:

- internal knowledge-layer scope;
- source authority hierarchy;
- source status labels;
- knowledge answer status labels;
- knowledge artefact types;
- source ingestion rules;
- metadata requirements;
- retrieval and indexing rules;
- access and tenant boundaries;
- source conflict and supersession handling;
- knowledge gap handling;
- knowledge module architecture;
- Knowledge Module Manifest requirements;
- maintenance and review cadence;
- testing and evaluation;
- risks; and
- update triggers.

This document is governance. It is not a Build Plan. It does not open Cursor. It does not create a database, table, vector index, chunking process, retrieval endpoint, SOP library, handover index, or AI assistant by itself.

Formal knowledge-layer build may proceed only after NTK-09 exists and is current, the relevant SCOPING.md is approved, Build OS produces the required Build Plan, and the applicable gates in NTK-01 and NTK-02 are satisfied.

### What this document does not govern

This document does not govern:

- product lane assignment — see NTK-01;
- hard cross-system guardrails — see NTK-02;
- decision-log and supersession discipline — see NTK-03;
- monorepo placement — see NTK-04;
- package architecture, contracts, Joints, and dependency direction — see NTK-05;
- formal white-label tenant deployment — see NTK-06;
- module promotion and versioning — see NTK-07;
- AI assistant authority, output status, prompt routing, HITL, and provider abstraction — see NTK-08;
- product portfolio routing — see NTK-10 when produced; or
- Build Plans, Cursor sessions, code execution, migrations, RLS policies, or deployment.

### Relationship to NTK-08

NTK-08 governs AI assistant product behaviour.

NTK-09 governs the internal knowledge layer that an AI assistant, operator tool, retrieval system, SOP browser, handover index, or workflow assistant may use.

Where an AI assistant retrieves from, summarises, answers from, or reasons over internal knowledge, both standards apply:

- NTK-08 controls assistant authority, prompt routing, output handling, HITL, model/provider abstraction, and AI output review.
- NTK-09 controls source authority, ingestion, metadata, retrieval permissions, staleness, supersession, source status, and knowledge-layer maintenance.

NTK-09 must not become a way to bypass NTK-08. NTK-08 must not become a way to bypass NTK-09.

---

## Section 2 — Core Rule

The core rule is:

> **Source truth before retrieval. The knowledge layer may surface, organise, retrieve, and explain approved knowledge, but it must not create authority, silently resolve contradictions, or turn unapproved material into governance.**

A knowledge system is only valuable if it preserves source truth.

A retrieved answer, AI summary, search result, embedding match, SOP excerpt, handover summary, or internal help response is not governance by itself.

Governance remains governed by:

- committed source files;
- approved decision registers;
- founder-confirmed NTK documents;
- UNIVERSAL_DECISIONS.md where applicable;
- product SCOPING.md and DECISIONS.md files where applicable;
- approved module documentation;
- approved SOPs; and
- GitHub commit discipline.

### What the core rule protects

This rule protects Nikari Tech from:

- treating chat memory as source of truth;
- treating AI summaries as governing documents;
- treating old handovers as current instructions;
- retrieving from superseded files without warning;
- mixing tenant knowledge across tenants;
- exposing internal governance to external users;
- letting drafts outrank approved documents;
- allowing stale SOPs to guide current workflows;
- turning project knowledge upload into governance;
- letting retrieval answers silently decide conflicts; and
- using internal knowledge tools externally before product, tenant, privacy, and commercial review.

### Default authority posture

The default knowledge-layer authority posture is:

```text
Committed approved source → source registry → permission-aware retrieval → answer with source basis → human review where material
```

Where no approved source exists, the correct output is:

```text
No approved source found → escalate / create knowledge gap / request clarification
```

The knowledge layer must not fill gaps with plausible policy.

---

## Section 3 — Knowledge Layer Scope

The knowledge layer includes internal information that may be organised, indexed, retrieved, presented, or used to support workflows.

### In-scope knowledge categories

The following are in scope where approved for ingestion:

1. **Governing documents**
   - UNIVERSAL_DECISIONS.md
   - UNIVERSAL_LEARNINGS.md
   - NTK documents
   - Build OS governance
   - Developer OS governance
   - product governance files

2. **Decision records**
   - NTK-03
   - product DECISIONS.md files
   - architecture decision records
   - issue-linked decision notes
   - founder-confirmed decision appendices

3. **Session handovers**
   - Nikari Tech handovers
   - Build OS handovers
   - Developer OS handovers
   - product handovers
   - release handovers
   - incident handovers

4. **SOPs and playbooks**
   - build-start SOPs
   - commit SOPs
   - review SOPs
   - module promotion SOPs
   - white-label scoping SOPs
   - support SOPs
   - operational playbooks

5. **Module and package documentation**
   - README.md
   - SPEC.md
   - IMPLEMENTATION_GUIDE.md
   - VERSION.md
   - CHANGELOG.md
   - CONFIG.example.md
   - compatibility matrices
   - promotion logs

6. **Product and tenant documentation**
   - product SCOPING.md
   - product README files
   - product operating notes
   - client-specific configuration notes
   - tenant-specific help material where approved

7. **Internal help and function references**
   - role guides
   - system maps
   - feature explanations
   - workflow diagrams
   - internal FAQ
   - function reference material

8. **Knowledge gap records**
   - missing-source notes
   - contradiction notes
   - stale-source alerts
   - unresolved source questions
   - reviewer feedback requiring source update

### Out-of-scope unless explicitly approved

The following must not enter the formal knowledge layer unless specifically scoped and approved:

- private chat transcripts;
- unreviewed brainstorming;
- raw user-uploaded documents;
- private emails;
- personal information;
- credentials or secrets;
- private legal/client documents;
- commercial terms not approved for the relevant audience;
- confidential partner documents;
- production data;
- raw database exports;
- tenant data;
- third-party content without permission;
- AI-generated summaries not tied to approved sources; and
- outdated or superseded documents without status metadata.

### Internal knowledge is not automatically external knowledge

An internal knowledge module may later become client-facing or white-label-ready, but it does not become external-ready merely because it works internally.

External use requires product intake, tenant/privacy review, user-facing scope, support model, commercial posture, and where relevant NTK-06 and NTK-08.

---

## Section 4 — Source Authority Hierarchy

The knowledge layer must know which source wins when sources conflict.

A source hierarchy must be recorded before formal retrieval or answering is enabled.

### Default hierarchy

The default Nikari Tech source authority hierarchy is:

| Rank | Source class | Authority posture |
|------|--------------|------------------|
| 1 | UNIVERSAL_DECISIONS.md | Highest cross-project authority where the decision is universal. |
| 2 | Founder-confirmed NTK documents | Highest Nikari Tech architecture authority within their scope. |
| 3 | NTK-03 Decision Log | Append-only record of Nikari Tech-specific decisions and supersessions. |
| 4 | Product SCOPING.md / DECISIONS.md | Governs the specific product or build scope where current. |
| 5 | Build OS approved Build Plans | Governs the specific build session once approved. |
| 6 | Module docs: SPEC, VERSION, CHANGELOG, README, compatibility matrix | Governs module use within the module’s scope and status. |
| 7 | Session handovers | Reliable session record, but subordinate to governing documents and decisions. |
| 8 | Approved SOPs and playbooks | Operational guidance, subordinate to decisions and current project scope. |
| 9 | Approved internal help / function reference | Helpful explanation, not authority over governing documents. |
| 10 | Drafts, brainstorms, reviews, notes, AI summaries | Not governing authority unless later assessed, confirmed, and committed. |

### Universal vs Nikari Tech-specific authority

Where a universal decision and an NTK document overlap, UNIVERSAL_DECISIONS.md controls the universal point.

Where an NTK document applies the universal decision to Nikari Tech, the NTK document controls the Nikari Tech implementation detail unless it conflicts with the universal rule.

Where a product file applies NTK governance to a specific product, the product file controls the product detail unless it conflicts with NTK or universal governance.

### Handovers are records, not governing documents

Handovers are important because they capture what happened.

They do not outrank committed governance documents.

If a handover conflicts with an approved governing document, the governing document controls unless the handover records a later founder-confirmed decision that has also been committed to the correct governance file.

### AI summaries are never source authority

An AI summary may be useful, but it is not source authority.

A knowledge layer may store AI-generated summaries only if the source basis is retained and the summary is clearly labelled.

The source document remains the authority.

### Conflict rule

If two approved sources conflict and the hierarchy does not clearly resolve the conflict, the knowledge layer must not choose silently.

It must:

1. show or record the conflict;
2. identify the sources involved;
3. state that the conflict requires review;
4. route to Nikari Tech, Build OS, Developer OS, or product owner as appropriate;
5. create a knowledge gap or contradiction record; and
6. avoid presenting either answer as settled until resolved.

---

## Section 5 — Knowledge Artefact Types

Every ingested or retrievable artefact must have a type.

### Minimum artefact types

| Type | Meaning |
|------|---------|
| `governance_document` | Formal governing document such as NTK, universal decision, Build OS, or Developer OS governance. |
| `decision_log` | Append-only decision register or decision record. |
| `session_handover` | Record of a completed session, outputs, open actions, and next prompt. |
| `sop` | Approved standard operating procedure. |
| `playbook` | Operational guidance for repeated workflows. |
| `module_doc` | README, SPEC, VERSION, CHANGELOG, implementation guide, compatibility matrix, or package documentation. |
| `product_scope` | Product SCOPING.md, product decisions, product-specific architecture notes. |
| `tenant_doc` | Tenant-specific configuration or approved tenant knowledge. |
| `internal_help` | Approved explainer, FAQ, role guide, or function reference. |
| `knowledge_gap` | Record of missing, conflicting, stale, or insufficient source material. |
| `review_output` | External review, ChatGPT review, Claude critique, or assessment not yet governance. |
| `draft` | Draft document not yet approved or committed as governance. |
| `archive` | Historical artefact retained for traceability but not current authority. |

### Artefact type does not determine authority by itself

A `governance_document` may be a draft. A `session_handover` may contain a decision that was later superseded. A `module_doc` may be deprecated. A `review_output` may be valuable but not governing.

Every artefact needs type, status, source path, authority level, and date metadata.

---

## Section 6 — Source Status Labels

Every source in the knowledge layer must have a status label.

No source may be used as current authority without a status.

### Minimum source status labels

| Status | Meaning |
|--------|---------|
| `draft` | Work in progress. Not approved. Not source authority. |
| `reviewed_draft` | Reviewed but not founder-confirmed or committed as final. Use with caution. |
| `working_standard` | Current governing or operating standard within its scope. |
| `founder_confirmed` | Founder confirmed. Governance effect begins or is confirmed on GitHub commit. |
| `committed_current` | Committed current source in the correct repo/path. |
| `approved_reference` | Approved for explanation or support, but not governing authority. |
| `session_record` | Reliable record of a session, subordinate to governing documents. |
| `superseded` | Replaced by a later source. Retain but warn and route to replacement. |
| `archived` | Historical reference only. Not current instruction. |
| `deprecated` | Still present for existing consumers but not for new work. |
| `external_reference` | External source, not Nikari governance unless adopted. |
| `tenant_specific` | Valid only for the named tenant or client context. |
| `restricted_internal` | Internal-only. Must not be exposed externally. |
| `unapproved` | Not approved for retrieval or reliance. |
| `conflict_flagged` | Source is involved in unresolved conflict. Do not treat as settled authority. |
| `stale_review_required` | Source may be outdated and requires review before reliance. |

### Status transition rule

A source may move between statuses only through the appropriate governance process.

Examples:

- `draft` to `working_standard` requires review and founder confirmation where applicable.
- `working_standard` to `committed_current` requires GitHub commit in the correct location.
- `committed_current` to `superseded` requires a later source or decision.
- `approved_reference` to `working_standard` requires governance confirmation.
- `session_record` to `governing decision` requires the relevant decision to be captured in NTK-03, UNIVERSAL_DECISIONS.md, product DECISIONS.md, or another governing file.

Status changes must be logged where the source is used by retrieval, AI, or workflow systems.

---

## Section 7 — Source Ingestion Rules

Source ingestion is the process of making an artefact available to the knowledge layer.

Ingestion is a governance event when the source will be used for retrieval, AI assistance, workflow guidance, or decision support.

### Rule 7.1 — Approved source registry required

Every formal knowledge layer must include a source registry.

The source registry records:

- source ID;
- title;
- file path or canonical location;
- repo;
- artefact type;
- source status;
- authority rank;
- owner;
- approval status;
- founder confirmation where applicable;
- commit hash or version reference where available;
- created date;
- last updated date;
- last reviewed date;
- next review trigger;
- product scope;
- tenant scope;
- access classification;
- retrieval allowed yes/no;
- AI use allowed yes/no;
- external exposure allowed yes/no;
- superseded-by source ID where applicable;
- conflict flags; and
- notes.

### Rule 7.2 — GitHub path or governed storage reference required

Where a source is governance, module documentation, product scope, or build discipline, it must point to its committed GitHub path or governed storage reference.

Project knowledge upload alone is not enough.

A file uploaded to a project may be convenient for retrieval, but the source registry must still record the committed source of truth where the document is governance.

### Rule 7.3 — No source without provenance

A knowledge source must have provenance.

Minimum provenance:

- where it came from;
- who produced it or confirmed it;
- when it was produced;
- whether it was committed;
- whether it was superseded;
- which project or repo owns it; and
- whether it is safe for retrieval.

Sources without provenance must remain `unapproved`.

### Rule 7.4 — Drafts must remain labelled

Draft documents may be ingested only if the product scope requires draft retrieval.

If ingested, they must be labelled as draft, and retrieval output must not treat them as authority.

### Rule 7.5 — Sensitive source ingestion requires approval

Do not ingest sensitive internal, client, tenant, legal, financial, employment, property, identity, security, or personal material without explicit scope and access controls.

Sensitive source ingestion must define:

- access class;
- permitted users;
- permitted retrieval contexts;
- whether AI may see it;
- whether summaries may be stored;
- retention rules;
- deletion rules;
- audit needs; and
- export limits.

### Rule 7.6 — Source ingestion is not source promotion

Ingesting a source into the knowledge layer does not make it governing.

A draft remains a draft. A handover remains a handover. A review remains a review. An external document remains external. A deprecated module doc remains deprecated.

Promotion to governance occurs only through the appropriate governance process.

---

## Section 8 — Metadata and Classification Rules

Metadata is not optional. Retrieval safety depends on it.

### Required metadata fields

Every retrievable source must record:

```yaml
source_id: ""
title: ""
source_type: ""
source_status: ""
authority_rank: ""
owner: ""
repo_or_storage_location: ""
file_path: ""
version: ""
commit_ref: ""
created_date: ""
last_updated_date: ""
last_reviewed_date: ""
next_review_trigger: ""
product_scope: ""
tenant_scope: ""
workspace_scope: ""
access_class: ""
retrieval_allowed: true
ai_use_allowed: true
external_exposure_allowed: false
contains_personal_data: false
contains_sensitive_data: false
supersedes: []
superseded_by: []
related_sources: []
conflict_flags: []
source_summary: ""
```

### Access class labels

Minimum access class labels:

| Access class | Meaning |
|--------------|---------|
| `public` | May be shown publicly if product scope allows. |
| `client_visible` | May be shown to a defined client or tenant audience. |
| `tenant_internal` | Visible only within the tenant boundary. |
| `nikari_internal` | Internal Nikari use only. |
| `restricted_internal` | Restricted internal use; requires specific role or approval. |
| `founder_only` | Founder-only or explicit founder-approved access. |
| `system_only` | System may use for routing/validation; not user-visible. |
| `no_retrieval` | Stored for record, but retrieval is not allowed. |

### Source summaries must not replace sources

A source summary may help retrieval, but it must not replace the source.

Where a summary is stored, it must link back to the source ID and source status.

### Metadata must be updateable

The system must allow source metadata to be updated when:

- a source is superseded;
- a source becomes stale;
- a source is approved;
- a source becomes restricted;
- a source is reclassified;
- a source is involved in a conflict;
- a source changes tenant or product scope; or
- a source is removed from retrieval.

---

## Section 9 — Retrieval and Indexing Rules

Retrieval and indexing must preserve source authority, access boundaries, and source status.

### Rule 9.1 — Retrieval must be permission-aware

A retrieval system must filter by:

- user identity;
- role;
- tenant ID;
- workspace ID where applicable;
- product scope;
- source status;
- access class;
- retrieval permission;
- AI-use permission;
- external exposure permission; and
- supersession state.

No user may retrieve a source they are not allowed to access.

### Rule 9.2 — Retrieval must respect source status

Retrieval may include draft, archived, superseded, or external-reference material only if the product scope allows it and the output clearly reflects the status.

A current answer should not rely on a superseded source without warning.

### Rule 9.3 — Approved sources first

Retrieval must prioritise approved and current sources over drafts, handovers, notes, external references, and reviews.

The retrieval ranking should consider:

- authority rank;
- source status;
- recency;
- product scope;
- tenant scope;
- source type;
- exact match;
- source owner;
- review status; and
- supersession.

### Rule 9.4 — Chunking must preserve context

If sources are chunked for search or embedding, chunks must retain enough metadata to preserve:

- source ID;
- title;
- heading path;
- section number;
- source status;
- authority rank;
- access class;
- product scope;
- tenant scope;
- version;
- commit reference where available;
- supersession status; and
- source path.

A chunk without metadata must not be used as authoritative retrieval.

### Rule 9.5 — Embeddings do not determine authority

Semantic similarity is not authority.

A highly similar but low-authority source must not outrank a lower-similarity but governing source where the query is about policy, architecture, decisions, compliance, Build OS rules, module standards, or product scope.

### Rule 9.6 — Retrieval answers need source basis

Where retrieval informs a material output, the source basis must be retained.

Depending on context, source basis may be:

- visible citation;
- internal source ID;
- file path;
- document title;
- section reference;
- retrieval event ID;
- source registry record;
- answer-source log; or
- audit event.

### Rule 9.7 — No-source behaviour must be explicit

If no approved source exists, the system must not invent an answer.

It must:

- say no approved source was found;
- escalate;
- create a knowledge gap;
- ask for clarification;
- return a draft-only response; or
- route to human review.

### Rule 9.8 — Retrieval logs must be privacy-safe

Retrieval logs may be needed for audit, debugging, and quality improvement.

They must not become a privacy leak.

Logs should avoid unnecessary raw sensitive content and should record only what is needed for source basis, permission verification, system debugging, and review.

---

## Section 10 — Knowledge Gap and Conflict Handling

A knowledge layer becomes useful when it identifies what it does not know.

### Knowledge gap types

Minimum gap types:

| Gap type | Meaning |
|----------|---------|
| `missing_source` | No approved source exists for the question or workflow. |
| `stale_source` | Source may be outdated or past review date. |
| `conflicting_sources` | Two or more sources appear to contradict. |
| `insufficient_authority` | Source exists but does not have enough authority for the requested answer. |
| `permission_blocked` | Source exists but user cannot access it. |
| `unclear_scope` | Source exists but product, tenant, or workflow scope is unclear. |
| `supersession_unclear` | Source may be superseded but replacement path is unclear. |
| `draft_only_source` | Only draft material exists. |
| `external_only_source` | Only external reference material exists. |
| `owner_review_required` | Source owner must review before use. |

### Knowledge gap record

A knowledge gap record should include:

```yaml
gap_id: ""
gap_type: ""
question_or_workflow: ""
detected_by: ""
detected_date: ""
affected_product: ""
affected_tenant: ""
candidate_sources: []
reason: ""
risk_level: ""
recommended_owner: ""
recommended_action: ""
status: "open | under_review | resolved | archived"
resolution_source_id: ""
resolution_date: ""
```

### Conflict handling

If sources conflict, the system must not hide the conflict.

It must record:

- sources involved;
- authority rank of each source;
- status of each source;
- conflicting claims;
- affected product/workflow;
- proposed owner for resolution;
- whether any retrieval answer must be blocked; and
- next action.

### Knowledge gap closure

A knowledge gap may be closed only when:

- a source is added or updated;
- a decision is recorded;
- the question is explicitly rejected as out of scope;
- the source owner confirms no source will be created; or
- the gap is archived with reason.

AI-generated answers do not close knowledge gaps unless the underlying source is created, approved, and registered.

---

## Section 11 — Knowledge Answer Status Labels

Every material knowledge-layer answer or retrieval response must have a status label where the product stores, reviews, displays, relies on, or audits the answer.

A source has a status. A knowledge gap has a status. A knowledge answer must also have a status where the answer may influence a user, operator, workflow, decision, source update, or audit trail.

### Minimum knowledge answer status labels

| Status | Meaning |
|--------|---------|
| `source_supported` | Answer is supported by current approved source material. |
| `source_limited` | Answer has some source support, but the source is incomplete, narrow, or context-limited. |
| `no_approved_source` | No approved source was found. |
| `conflict_detected` | Relevant sources conflict and the answer must not be treated as settled. |
| `stale_source_warning` | Answer depends on a source that may be outdated or review-required. |
| `superseded_source_warning` | Answer depends on a source that has been superseded and needs replacement review. |
| `permission_blocked` | Source exists but the user is not permitted to access it. |
| `human_review_required` | Answer requires source owner, founder, or project-owner review before reliance. |
| `approved_for_use` | Human reviewer approved the answer for the scoped use. |
| `rejected` | Human reviewer rejected the answer. |
| `archived` | Answer retained for traceability but not current reliance. |

### Settled-answer rule

A knowledge answer must not be presented as settled where its status is:

- `no_approved_source`;
- `conflict_detected`;
- `stale_source_warning`;
- `superseded_source_warning`; or
- `human_review_required`.

In those cases, the system must warn, escalate, create a knowledge gap, route to review, or refuse to provide a settled answer depending on product scope.

### Answer status change logging

Where a knowledge answer is material, status changes must be logged.

Examples:

- `source_limited` to `approved_for_use`;
- `human_review_required` to `approved_for_use`;
- `conflict_detected` to `archived`;
- `stale_source_warning` to `source_supported` after source review;
- `source_supported` to `superseded_source_warning` after source supersession.

Answer status is not a substitute for source status. It records the state of the answer generated from the available sources.

---

## Section 12 — Access, Privacy, and Tenant Boundaries

Knowledge-layer access must respect the same boundary discipline as product data.

### Rule 12.1 — Knowledge access is role-bound

Users may retrieve only sources that their role permits.

Roles may include:

- founder;
- Nikari Tech operator;
- Build OS operator;
- Developer OS operator;
- product operator;
- tenant admin;
- tenant staff;
- external partner;
- read-only user;
- client user;
- public user;
- system service.

### Rule 12.2 — Tenant knowledge remains tenant-bound

Tenant-specific sources must not be retrieved, indexed, embedded, summarised, or surfaced to another tenant.

Tenant-specific source metadata must include tenant ID or equivalent governed tenant reference.

Domain, slug, brand name, or human-readable tenant label must not be treated as access authority.

### Rule 12.3 — Internal governance is not automatically client-visible

NTK documents, Build OS documents, Developer OS documents, internal handovers, internal prompt standards, and architecture rules may be internal-only even where they govern client-facing products.

Client-facing help must be separately approved and written for the intended audience.

### Rule 12.4 — Sensitive knowledge requires minimisation

Where retrieval or AI uses sensitive knowledge, context must be minimised.

The system should retrieve the narrowest useful section, not the broadest available document.

### Rule 12.5 — Source exports must respect permissions

A user who can receive a retrieval answer does not automatically have export rights to the underlying source.

Export rules must be defined separately.

### Rule 12.6 — Prompt and instruction protection

Internal prompts, hidden governance instructions, system routing rules, provider configuration, API keys, secrets, and internal architecture not approved for exposure must not be surfaced through retrieval.

Where a user asks for hidden instructions or restricted internals, the system must refuse or route to an authorised internal process.

---

## Section 13 — Knowledge Module Architecture

Knowledge-layer code, indexing, retrieval, source registry, metadata, SOP libraries, handover libraries, and knowledge gap workflows must be placed according to NTK-05 package architecture.

### Default package posture

- generic knowledge-layer infrastructure belongs in `packages/knowledge-layer/`;
- product-specific knowledge logic belongs in `packages/vertical/[product]/`;
- tenant-specific knowledge configuration must comply with NTK-06;
- AI assistant behaviour that uses the knowledge layer must comply with NTK-08;
- reusable knowledge-layer modules may be promoted only under NTK-07;
- shared types, source records, retrieval interfaces, and Joints belong in `packages/contracts/`;
- low-level pure utilities may belong in `packages/primitives/functional/` if they are genuinely generic.

### Possible knowledge-layer organs

Possible Level 2 organs include:

- `source-registry/` — records approved source metadata and status.
- `source-ingestion/` — validates and registers sources for retrieval.
- `source-status-manager/` — manages current, stale, superseded, archived, and restricted statuses.
- `document-chunker/` — chunks documents while preserving metadata.
- `retrieval-permission-gate/` — filters retrieval by role, tenant, product, status, and access class.
- `source-ranker/` — ranks sources by authority, status, scope, and relevance.
- `knowledge-gap-manager/` — records missing, conflicting, stale, or insufficient sources.
- `handover-index/` — indexes session handovers as records, not governing authority.
- `sop-library/` — stores approved SOPs and playbooks.
- `function-reference/` — stores internal help and function reference material.
- `source-conflict-detector/` — identifies likely contradictions.
- `citation-builder/` — creates internal source references or visible citations where product scope allows.

Possible Level 3 composites include:

- `internal-knowledge/` — source registry + ingestion + retrieval permission + gap manager.
- `governance-retrieval/` — source ranking + decision hierarchy + approved-source retrieval.
- `sop-support/` — SOP library + function reference + retrieval permission.
- `handover-support/` — handover index + source status + knowledge gap manager.
- `knowledge-review/` — gap manager + conflict detector + source status manager.

### Package family caveat

The existence of `packages/knowledge-layer/` does not authorise formal knowledge-layer build.

Formal knowledge-layer build still requires:

- NTK-09 current;
- lane assignment under NTK-01;
- guardrails under NTK-02;
- decisions and supersessions under NTK-03;
- contracts and Joints under NTK-05;
- module promotion rules under NTK-07;
- AI assistant rules under NTK-08 where AI is involved;
- SCOPING.md where required;
- Build OS Build Plan; and
- founder approval.

### A folder is not a knowledge module

A folder of documents, chunks, prompts, indexes, embeddings, or notes is not a knowledge module by itself.

A knowledge module must have:

- clear purpose;
- source types;
- source status rules;
- metadata schema;
- access controls;
- retrieval boundaries;
- owner;
- testing;
- documentation;
- status;
- version posture;
- Build OS compatibility; and
- package location consistent with NTK-05.

---

## Section 14 — Knowledge Module Manifest

Every formal knowledge-layer module requires a Knowledge Module Manifest.

The manifest is the minimum structured artefact Build OS must consume before preparing a Build Plan for a knowledge-layer module.

### Required manifest fields

```yaml
knowledge_manifest_version: "1.0"

module:
  name: ""
  slug: ""
  package_family: "knowledge-layer | vertical/[product] | ai-assistant | other"
  operating_lane: "Lane 1 | Lane 2 | Lane 3 | Lane 4 | Lane 5"
  lane_5_posture: "primary | overlay | not_applicable"
  purpose: ""
  primary_users: []
  excluded_users: []
  product_context: ""
  tenant_context: ""

source_scope:
  allowed_source_types: []
  prohibited_source_types: []
  source_statuses_allowed: []
  source_statuses_blocked: []
  authority_hierarchy: []
  source_registry_required: true
  source_owner: ""

access:
  access_classes_allowed: []
  roles_allowed: []
  tenant_data_involved: false
  workspace_data_involved: false
  cross_tenant_retrieval_allowed: false
  external_exposure_allowed: false
  export_allowed: false

ingestion:
  ingestion_method: ""
  approval_required_before_ingestion: true
  provenance_required: true
  commit_reference_required: true
  metadata_required: true
  sensitive_source_handling: ""

retrieval:
  retrieval_enabled: true
  ai_use_allowed: false
  ntk_08_applies: false
  citation_or_source_reference_required: true
  no_source_behaviour: ""
  conflict_behaviour: ""
  stale_source_behaviour: ""
  superseded_source_behaviour: ""
  permission_filtering_required: true
  answer_status_labels_required: true
  answer_status_behaviour: ""

indexing:
  chunking_required: false
  embedding_required: false
  chunk_metadata_required: true
  index_refresh_rule: ""
  index_deletion_rule: ""
  reindex_trigger: ""

logging:
  retrieval_logging_required: true
  source_status_change_logging_required: true
  knowledge_gap_logging_required: true
  answer_status_change_logging_required: true
  privacy_safe_logging_rule: ""
  retention_rule: ""

review:
  source_review_required: true
  review_owner: ""
  review_cadence: ""
  knowledge_gap_review_required: true
  conflict_review_required: true

testing:
  permission_tests_required: true
  tenant_isolation_tests_required: true
  source_status_tests_required: true
  no_source_tests_required: true
  conflict_tests_required: true
  stale_source_tests_required: true
  retrieval_quality_tests_required: true

risk:
  build_os_risk_tier: ""
  critical_risks: []
  mitigation_summary: ""

status:
  manifest_status: "draft | founder_approved | build_os_ready | superseded"
  founder_approved_by: ""
  approval_date: ""
  next_review_trigger: ""
```

### Manifest rule

A missing manifest means the knowledge-layer module is not ready for Build OS assembly.

A manifest that leaves source hierarchy, source status labels, answer status behaviour, access class, tenant boundary, retrieval permissions, no-source behaviour, conflict behaviour, or review cadence undecided is incomplete.

---

## Section 15 — Maintenance, Review, and Staleness

A knowledge layer must be maintained.

A stale knowledge layer is worse than no knowledge layer because it can produce confident outdated answers.

### Required maintenance controls

Every formal knowledge-layer module must define:

- source owner;
- review owner;
- review cadence;
- staleness threshold;
- stale-source label;
- supersession handling;
- source removal rule;
- source refresh process;
- index refresh process;
- conflict review process;
- knowledge gap review process;
- broken-link or missing-file process;
- deprecated-source handling;
- archive handling;
- tenant-specific review requirements; and
- emergency correction path.

### Staleness review

Sources should be reviewed when:

- the document reaches its review date;
- the owning NTK document changes;
- a product scope changes;
- a module version changes;
- a decision is superseded;
- a source conflict is detected;
- a retrieval incident occurs;
- a user flags an answer as wrong;
- a source path changes;
- a repo is restructured;
- a white-label or tenant implication changes;
- an AI assistant begins using the source; or
- a founder requests review.

### Superseded source handling

When a source is superseded:

1. mark the old source as `superseded`;
2. record the replacement source ID;
3. update retrieval ranking;
4. reindex where needed;
5. update summaries where needed;
6. log the status change;
7. flag affected knowledge gaps or answers where necessary; and
8. prevent current answers from relying on the superseded source without warning.

### Archive handling

Archived material may remain searchable for history if scope permits.

Archived material must not be used as current instruction.

---

## Section 16 — Knowledge Testing and Evaluation

Every formal knowledge-layer module must define testing appropriate to its risk level before production use.

Testing may include:

- source registry validation tests;
- required metadata tests;
- source status transition tests;
- authority hierarchy tests;
- permission filtering tests;
- tenant isolation tests;
- workspace isolation tests;
- source visibility tests;
- no-source escalation tests;
- superseded-source warning tests;
- stale-source warning tests;
- conflicting-source tests;
- retrieval quality samples;
- citation or source-reference tests;
- prompt-injection resistance tests where AI is involved;
- sensitive-data minimisation checks;
- export boundary tests;
- logging tests;
- index refresh tests;
- deletion or archive handling tests; and
- regression checks after source, index, metadata, or hierarchy changes.

### Evaluation rule

Knowledge testing does not prove that every answer is correct.

It proves that the knowledge layer:

- retrieves from approved sources first;
- respects authority hierarchy;
- respects permissions;
- refuses or escalates when source support is insufficient;
- handles stale and superseded sources safely;
- preserves source basis;
- logs material retrieval appropriately;
- does not leak tenant or restricted information; and
- fails safely when the knowledge base is incomplete.

### Human review samples

For material knowledge-layer workflows, periodic human review samples should check:

- answer-source alignment;
- missing source issues;
- outdated source use;
- hallucinated or unsupported claims where AI is involved;
- user reliance risk;
- access-boundary correctness;
- tenant-boundary correctness;
- knowledge gap routing; and
- whether source documents need update.

---

## Section 17 — Risks

### Risk 1 — False authority

The knowledge layer may present a draft, handover, review, or AI summary as if it were governing authority.

Mitigation:

- source status labels;
- source authority hierarchy;
- source registry;
- approved-source-first retrieval;
- visible or internal source basis;
- no-source and conflict escalation.

### Risk 2 — Stale source reliance

The system may answer from old files, outdated handovers, superseded decisions, or deprecated module docs.

Mitigation:

- review cadence;
- stale-source labels;
- supersession metadata;
- index refresh triggers;
- source owner accountability.

### Risk 3 — Tenant or access leakage

The system may retrieve or expose knowledge outside the permitted user, tenant, product, workspace, or role boundary.

Mitigation:

- permission-aware retrieval;
- tenant metadata;
- access classes;
- RLS and server-side validation where implemented;
- tenant isolation tests;
- privacy-safe logging.

### Risk 4 — Governance drift

The knowledge layer may cause informal notes, reviews, summaries, or chat outputs to influence decisions without being committed governance.

Mitigation:

- NTK-03 discipline;
- GitHub path requirement;
- source status labels;
- review-not-governance rule;
- knowledge gap records for uncommitted decisions.

### Risk 5 — Retrieval without provenance

The system may provide answers without reliable source basis.

Mitigation:

- source registry;
- required metadata;
- source reference logging;
- citation builder where applicable;
- no-source escalation.

### Risk 6 — Conflict hiding

The system may silently choose one source when sources conflict.

Mitigation:

- conflict detection;
- conflict flags;
- escalation workflow;
- authority hierarchy;
- blocked answer state where necessary.

### Risk 7 — Overexposure of internal material

Internal governance, strategy, prompts, handovers, or architecture may become visible to external users.

Mitigation:

- access class labels;
- external exposure flags;
- client-facing knowledge separation;
- prompt/instruction protection;
- review before external use.

### Risk 8 — Knowledge-layer modules promoted too early

A knowledge-layer pattern may be treated as reusable before it has proven stable, documented, versioned, and compatible.

Mitigation:

- NTK-07 promotion rules;
- Knowledge Module Manifest;
- compatibility review;
- status and version posture;
- extraction review after real use.

### Risk 9 — AI misuse of knowledge

An AI assistant may retrieve correct sources but exceed authority, overstate confidence, or act without HITL.

Mitigation:

- NTK-08 applies;
- assistant authority levels;
- HITL;
- output status labels;
- source-bound answers;
- AI testing and evaluation.

### Risk 10 — Index drift

Indexes, chunks, summaries, or embeddings may become disconnected from current source files.

Mitigation:

- commit or version references;
- reindex triggers;
- chunk metadata;
- source-status updates;
- stale-index detection;
- source owner review.

---

## Section 18 — Update Triggers

This document must be reviewed and updated when any of the following occur:

1. first internal knowledge-layer module is built;
2. first source registry is built;
3. first SOP library is built;
4. first handover index is built;
5. first governed document retrieval feature is scoped;
6. first embedding or vector index is created for internal documents;
7. first retrieval answer is shown to a user, operator, tenant, or client;
8. first knowledge-layer module is used by an AI assistant;
9. first white-label or tenant-specific knowledge layer is scoped;
10. first source authority conflict occurs;
11. first stale-source or superseded-source incident occurs;
12. first knowledge gap workflow is used in production;
13. first tenant or access-boundary issue occurs;
14. first internal knowledge is proposed for external or client-facing use;
15. source status labels change;
16. knowledge answer status labels change;
17. source hierarchy changes;
18. source registry metadata requirements change;
19. retrieval testing reveals a governance gap;
20. NTK-01 changes Lane 5, lifecycle stages, or delivery modes;
21. NTK-02 changes AI, data, security, process, or anti-drift guardrails;
22. NTK-03 changes decision-log or supersession requirements;
23. NTK-04 changes `packages/knowledge-layer/` placement or monorepo structure;
24. NTK-05 changes contracts, Joints, package family map, or dependency direction;
25. NTK-06 changes tenant, white-label, data export, or domain-routing implications for knowledge;
26. NTK-07 changes module promotion implications for knowledge-layer modules;
27. NTK-08 changes AI assistant retrieval, output, HITL, source, or provider rules;
28. NTK-10 changes product portfolio routing for knowledge-layer products; or
29. founder identifies a knowledge-layer risk not covered by this document.

### NTK-03 append note

After founder confirmation of NTK-09, NTK-03 should receive append entries for any knowledge-layer decisions the founder wants recorded as discrete Nikari Tech decisions.

At minimum, the adoption of NTK-09 as the formal Internal Knowledge Layer Module Standard should be recorded.

Likely NTK-03 entries include:

1. formal knowledge-layer build requires NTK-09;
2. source truth before retrieval;
3. source authority hierarchy adopted;
4. source status labels adopted;
5. knowledge answer status labels adopted;
6. approved source registry required;
7. Knowledge Module Manifest adopted;
8. retrieval must be permission-aware and source-status-aware;
9. drafts, handovers, reviews, and AI summaries do not become governance by ingestion;
10. stale, superseded, and conflicting sources require escalation or warning;
11. NTK-08 applies wherever AI assistants use the knowledge layer.

These entries should remain separate if recorded, because they govern different parts of knowledge-layer architecture and authority.

---

*Version: 1.0 — working standard*  
*Produced: Nikari Tech — NTK-09 Internal Knowledge Layer Module Standard Session, 29 April 2026*  
*Approved by: Wiets Marais — 29 April 2026*  
*Read with: UNIVERSAL_DECISIONS.md, NTK-00, NTK-01, NTK-02, NTK-03, NTK-04, NTK-05, NTK-06, NTK-07, NTK-08*  
*Next update trigger: See Section 18*  
*Proposed repo location: `wietsmarais/docs/architecture/NTK-09_Internal_Knowledge_Layer_Module_Standard.md`*
