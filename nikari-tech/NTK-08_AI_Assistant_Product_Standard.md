# NTK-08 — AI Assistant Product Standard

**File:** NTK-08_AI_Assistant_Product_Standard.md  
**Status:** Working standard — founder confirmed, pending GitHub commit  
**Approved by:** Wiets Marais — 29 April 2026  
**Owner:** Nikari Tech  
**Layer:** AI Product Governance / Lane 5 Standard  
**Purpose:** Defines the governance standard for AI assistant products, embedded AI features, retrieval assistants, workflow assistants, build assistants, human-in-the-loop review, prompt routing, output logging, authority boundaries, privacy, cost controls, and assistant module manifests across Nikari Tech.  
**Read with:** UNIVERSAL_DECISIONS.md, NTK-00 (Master Intent), NTK-01 (Operating Model), NTK-02 (Guardrails), NTK-03 (Decision Log), NTK-04 (Monorepo Architecture), NTK-05 (Component and Contracts Architecture), NTK-06 (White Label Tenant and Deployment Model), NTK-07 (Module Promotion and Versioning Protocol).  
**Supersedes / Subordinates:** Subordinate to UNIVERSAL_DECISIONS.md, NTK-00, NTK-01, and NTK-02. Expands the AI guardrails in NTK-02. Complements NTK-05 by governing what may be built into `packages/ai-assistant/`. Does not weaken NTK-02. Does not supersede NTK-09 where the work involves internal knowledge-layer modules, SOPs, governed documents, handovers, retrieval libraries, or knowledge-management workflows.  
**Update trigger:** First AI assistant feature assembled via Build OS; first client-facing AI assistant; first embedded workflow assistant; first retrieval assistant; first AI output published to a user-facing surface; first material AI authority request; AI breach or hallucination incident; provider abstraction change; prompt-routing change; cost-control breach; NTK-01, NTK-02, NTK-05, NTK-07, or NTK-09 change affecting AI assistant work.

---

## Section 1 — Purpose

This document defines the AI Assistant Product Standard for Nikari Tech.

It exists because AI features are not ordinary product features. AI can draft, retrieve, summarise, classify, suggest, structure, explain, and assist, but it can also create hidden authority, hallucinated confidence, privacy leakage, public misstatement, tenant-boundary risk, and over-automation if it is treated as normal UI or workflow logic.

NTK-08 answers:

**When may Nikari Tech build AI assistant features, what authority may those assistants hold, how are prompts and context controlled, how are outputs reviewed and logged, and what must be true before an AI assistant can be used inside a product or client deployment?**

This document governs:

- AI assistant categories;
- AI architecture principles;
- provider abstraction;
- server-side prompt routing;
- prompt and context rules;
- human-in-the-loop review;
- AI output types;
- retrieval rules;
- privacy and data rules;
- cost and usage controls;
- AI Assistant Start Protocol;
- Assistant Module Manifest requirements;
- AI-specific risks; and
- update triggers.

This document is governance. It is not a Build Plan. It does not open Cursor. It does not create an app, package, schema, migration, prompt library, model router, retrieval index, review queue, or AI surface by itself.

Formal Lane 5 AI product build may proceed only after NTK-08 exists and is current, the relevant SCOPING.md is approved, Build OS produces the required Build Plan, and the applicable gates in NTK-01 and NTK-02 are satisfied.

### What this document does not govern

This document does not govern:

- product lane assignment — see NTK-01;
- hard cross-system guardrails — see NTK-02;
- monorepo placement — see NTK-04;
- package architecture, contracts, Joints, and dependency direction — see NTK-05;
- formal white-label tenant deployment — see NTK-06;
- module promotion and versioning — see NTK-07;
- internal knowledge-layer module standards — see NTK-09 when produced;
- product portfolio routing — see NTK-10 when produced; or
- Build Plans, Cursor sessions, or code execution — see Build OS and Developer OS.

### Alignment rule

NTK-08 governs **AI assistant product standards**. It does not authorise every AI idea to become a product. It does not authorise autonomous AI decisions by default. It does not authorise AI features to bypass human approval, product truth, tenant boundaries, data rules, or module governance.

AI capability is useful only when it remains governed.

---

## Section 2 — Core Rule

The core rule is:

> **AI assists, drafts, retrieves, suggests, structures, and explains. AI does not hold final authority unless that authority is explicitly scoped, bounded, safe, logged, reviewable, and founder-approved.**

Human approval is required for sensitive outputs.

Sensitive outputs include any output that affects:

- public content;
- client commitments;
- user decisions;
- commercial terms;
- financial action;
- legal or compliance-sensitive content;
- property or transaction advice;
- tenant access;
- permission changes;
- data changes;
- operational routing;
- recruitment, employment, or safety-related decisions;
- deletion, archiving, suppression, or publication; or
- any action that a reasonable user could treat as authoritative.

### Default authority posture

The default authority posture for all AI assistants is:

```text
Draft only → human review → approve / reject / edit → logged output
```

Any departure from this default requires:

1. explicit authority level in the Assistant Module Manifest;
2. product-specific SCOPING.md approval;
3. review gate;
4. audit trail;
5. rollback or correction path;
6. founder approval; and
7. Build OS risk classification.

### What is prohibited by default

The following are prohibited by default unless separately scoped and approved under the highest applicable risk path:

- AI auto-publishing public content;
- AI sending messages directly to clients, users, regulators, partners, or the public;
- AI committing code or governance documents without human review;
- AI changing prices, commercial terms, permissions, access, tenant settings, or billing;
- AI deleting, archiving, suppressing, or mutating user data;
- AI making final legal, financial, property, employment, safety, or compliance decisions;
- AI silently ranking, approving, rejecting, profiling, or routing users where the result materially affects them; and
- AI using private or tenant data outside the documented boundary.

---

## Section 3 — AI Product Categories

Every AI feature or assistant must be classified before scoping proceeds.

The category determines authority limits, review gates, data rules, and Build OS risk posture.

### Category 1 — Internal Assistant

An assistant used by Nikari operators, founders, staff, or approved internal users.

Examples:

- drafting internal notes;
- summarising non-sensitive inputs;
- preparing first-draft checklists;
- structuring project handovers;
- drafting support responses for review;
- preparing document outlines.

Default posture:

- draft-only;
- internal review required before external use;
- source boundaries documented;
- material outputs logged where they affect decisions.

### Category 2 — Client-Facing Assistant

An assistant visible to external users, customers, tenants, white-label clients, buyers, sellers, investors, students, community users, or other non-internal users.

Examples:

- website support assistant;
- onboarding assistant;
- product guidance assistant;
- property enquiry assistant;
- client help assistant;
- white-label tenant assistant.

Default posture:

- constrained scope;
- visible limitations;
- no legal, financial, compliance, or transaction finality;
- escalation path to human support;
- output logging where material;
- stricter prompt and data controls.

### Category 3 — Embedded Workflow Assistant

An assistant embedded inside a business workflow or product process.

Examples:

- matching explanation assistant;
- content drafting assistant;
- document preparation assistant;
- compliance checklist assistant;
- onboarding workflow assistant;
- admin review assistant;
- triage support assistant.

Default posture:

- assists the workflow;
- does not own the workflow;
- human or system rule remains final authority;
- material recommendations are reviewable;
- output must not mutate data unless the mutation is separately approved.

### Category 4 — Build Assistant

An assistant used to support Nikari Tech, Build OS, Developer OS, or Cursor-related work.

Examples:

- code-review helper;
- prompt construction helper;
- Build Plan support assistant;
- module readiness summary assistant;
- test-plan drafting assistant.

Default posture:

- draft and review support only;
- does not replace Build OS gates;
- does not replace Developer OS discipline;
- does not commit code, governance, migrations, prompts, or architecture decisions;
- never becomes source of truth.

### Category 5 — Retrieval Assistant

An assistant that answers questions using approved documents, governed sources, project files, committed policies, product documentation, or selected data sources.

Examples:

- internal governance Q&A;
- product help retrieval;
- SOP retrieval;
- tenant-specific document assistant;
- support knowledge assistant;
- project file lookup assistant.

Default posture:

- approved sources first;
- cite or record internal source reference where applicable;
- say when no approved source exists;
- escalate unknowns;
- no invented policy.

If the retrieval assistant is part of the internal knowledge layer, SOP layer, handover system, governed document system, function reference, or knowledge-module architecture, NTK-09 also applies.

---

## Section 4 — AI Architecture Principles

### Principle 4.1 — AI is an abstraction layer, not the product authority

AI functions as a replaceable backend engine behind the Nikari Tech product layer.

The product owns:

- business rules;
- workflow state;
- permission rules;
- tenant boundaries;
- review gates;
- audit trail;
- data model;
- publishing rules;
- commercial logic; and
- final authority.

The AI provider does not own these things.

### Principle 4.2 — Provider abstraction is mandatory

AI provider selection must be abstracted behind a server-side service boundary.

Products must not hard-code a specific provider, model, prompt, API key, or model-routing assumption into UI code or product logic.

The architecture should allow future substitution of provider or model without changing the user interface or rewriting product workflows.

### Principle 4.3 — Prompt routing is server-side

Prompt templates, system instructions, provider routing, model selection, retrieval context assembly, sensitive context filtering, and provider credentials must run server-side.

Browser-visible code must not contain:

- private prompts;
- unrestricted prompt templates;
- model provider keys;
- sensitive context assembly;
- hidden governance logic;
- retrieval permission logic;
- tenant-sensitive filtering logic; or
- direct unrestricted AI calls.

### Principle 4.4 — Structured inputs before freeform prompts

AI assistants should receive structured inputs wherever possible.

Structured inputs may include:

- user role;
- tenant ID;
- product context;
- assistant purpose;
- allowed task type;
- selected source IDs;
- output type;
- risk level;
- review requirement;
- data boundary;
- authority level;
- language / tone settings;
- timeout and token limits.

Freeform user prompts may be accepted only inside the assistant’s documented scope and after input validation, safety checks, and data-boundary filtering.

### Principle 4.5 — Outputs are logged where material

Material AI outputs must be logged or stored in a reviewable way according to product scope.

The log should capture:

- assistant ID;
- user ID or system actor;
- tenant ID where applicable;
- input summary or reference;
- source references where applicable;
- model/provider reference where appropriate;
- output;
- authority level;
- review status;
- reviewer;
- approval / rejection / edit action;
- timestamp; and
- error or escalation state.

Sensitive data should not be over-logged. Logging must respect privacy, tenant boundaries, and data minimisation.

### Principle 4.6 — Product functions should work without AI where practical

Where a product function is mission-critical, the product should not fail completely merely because an AI provider is unavailable.

Where practical, products should provide:

- non-AI fallback;
- saved draft recovery;
- manual workflow path;
- retry or queue behaviour;
- clear user message when AI is unavailable; and
- no false claim that the task has completed.

### Principle 4.7 — No hidden business authority

AI must not silently control business outcomes.

Where AI assists with ranking, scoring, routing, matching, suppression, recommendation, drafting, classification, or escalation, the product must define:

- whether the AI output is advisory or determinative;
- whether a human can override it;
- whether the user sees it;
- whether the operator sees its reasoning or source basis;
- how errors are corrected; and
- how the output is logged.

---

## Section 5 — Prompt and Context Rules

### Rule 5.1 — Prompt families must be named

Every formal assistant must use a named prompt family or prompt configuration.

A prompt family must define:

- assistant purpose;
- allowed task types;
- prohibited task types;
- authority level;
- tone and style boundaries;
- source-use rules;
- escalation behaviour;
- output format;
- logging requirement;
- privacy boundary; and
- review requirement.

### Rule 5.2 — Product prompts are server-side assets

Product prompts must be stored and routed server-side.

They must not be embedded in:

- frontend components;
- browser-visible JavaScript;
- public markdown;
- screenshots;
- client-visible debug panels;
- prompt examples containing secrets or sensitive business rules; or
- any place where a user can extract hidden instructions.

### Rule 5.3 — Context is minimised

AI assistants receive only the context needed for the approved task.

Do not include:

- full user profiles where a narrow field is sufficient;
- tenant records unrelated to the task;
- private notes unrelated to the request;
- documents not approved for that user or tenant;
- personal data not required for the output;
- service keys, internal credentials, tokens, or secrets;
- hidden governance files not required for the assistant’s role; or
- sensitive material merely because it is available.

### Rule 5.4 — Prompt injection must be treated as a product risk

Any assistant that uses user-provided text, files, retrieved documents, emails, web content, or imported data must treat that content as untrusted.

The assistant must not obey instructions contained inside retrieved or uploaded content unless those instructions are part of the approved system or product scope.

Where prompt injection risk exists, the assistant scope must define:

- instruction hierarchy;
- untrusted content handling;
- source filtering;
- allowed tool behaviour;
- escalation behaviour;
- output verification path; and
- review requirement.

### Rule 5.5 — Sensitive prompt contexts require explicit classification

Legal, financial, property, compliance, employment, health, safety, identity, tenant, security, and payment-related contexts require explicit risk classification before implementation.

Sensitive contexts must use:

- narrower inputs;
- stricter review gates;
- clearer disclaimers where user-facing;
- stronger logging;
- escalation to human review; and
- no autonomous final decision.

### Rule 5.6 — Prompt changes are product changes

A material prompt change may change product behaviour.

Prompt changes must be handled like product changes where they affect:

- output quality;
- user guidance;
- legal or compliance posture;
- public copy;
- commercial content;
- routing;
- data mutation;
- permissions;
- tenant boundaries; or
- review gates.

Material prompt changes require versioning, review, and changelog treatment appropriate to risk.

---

## Section 6 — HITL Rules

Human-in-the-loop review is permanent for sensitive or material AI outputs.

### Default HITL flow

The default flow is:

```text
AI draft → review queue → human approve / reject / edit → audit trail → release or archive
```

This applies unless the assistant is explicitly scoped as low-risk, non-material, non-public, non-sensitive, and non-mutating.

### Review outcomes

A reviewer must be able to:

- approve the output;
- reject the output;
- edit the output;
- request regeneration;
- escalate to a more qualified reviewer;
- mark source insufficient;
- mark hallucination or unsafe output;
- return to user for more information;
- archive the draft; and
- record a correction note.

### No direct publish for public or sensitive content

AI output must not go directly to:

- public websites;
- client messages;
- email sends;
- SMS sends;
- social media posts;
- advertisements;
- contracts;
- legal documents;
- commercial terms;
- payment actions;
- data mutations;
- tenant permission changes;
- governance documents; or
- production code commits

unless the auto-action pathway is separately scoped, safe, logged, reviewable, and founder-approved.

### Review role must match risk

The reviewer must be appropriate to the output risk.

Examples:

- public copy: approved internal reviewer;
- legal/compliance-sensitive text: qualified human review;
- property or finance-sensitive output: qualified operator review;
- tenant or admin access output: authorised admin review;
- governance output: founder / Nikari Tech review;
- code or migration output: Build OS / Developer OS / founder gate as applicable.

### HITL cannot be bypassed by UI convenience

A faster user experience is not a reason to remove review where review is required.

If review makes a workflow slower, the correct response is to improve queue design, template clarity, source quality, or reviewer tooling — not to remove the human gate.

---

## Section 7 — AI Output Types

Every assistant must define its allowed output types before build.

### Type 1 — Draft Text

Text intended for review before use.

Examples:

- email draft;
- property description draft;
- support response draft;
- internal note;
- report section;
- checklist.

Default authority: no final authority.

### Type 2 — Structured Summary

A summary of provided or retrieved material.

Examples:

- meeting summary;
- file summary;
- lead summary;
- support case summary;
- product context summary.

Default authority: assistive only. Must not add unsupported facts.

### Type 3 — Recommendation

A suggested next action, option, match, route, or decision support output.

Examples:

- likely best next step;
- possible product routing;
- support escalation suggestion;
- draft classification;
- match explanation.

Default authority: advisory only. Human or system rule remains final authority.

### Type 4 — Classification

A label applied to an input.

Examples:

- issue type;
- urgency level;
- lead category;
- risk category;
- document type;
- support topic.

Default authority: advisory unless the product scope explicitly allows bounded automation with review or correction path.

### Type 5 — Retrieval Answer

An answer based on approved sources.

Examples:

- policy answer;
- SOP answer;
- product help answer;
- governance reference answer.

Default authority: source-bound only. If no approved source exists, assistant must say so or escalate.

### Type 6 — Workflow Action Proposal

A proposed action inside a workflow.

Examples:

- “create task” suggestion;
- “send to review” suggestion;
- “request missing document” suggestion;
- “route to qualified operator” suggestion.

Default authority: proposal only. User or authorised operator confirms before action.

### Type 7 — Bounded Automation

An AI-supported path that performs a narrow action without individual human approval each time.

Examples may include:

- auto-tagging low-risk support tickets;
- generating internal non-public labels;
- drafting but not sending;
- low-risk classification with review sampling.

Default authority: prohibited unless explicitly scoped, logged, tested, bounded, reversible, and founder-approved.

### Type 8 — Prohibited Final Authority by Default

The assistant must not be given final authority over:

- legal advice;
- financial advice;
- property transaction decisions;
- commercial commitments;
- employment decisions;
- safety decisions;
- tenant access;
- payments;
- deletions;
- public publication;
- governance decisions;
- production deployments; or
- destructive or irreversible actions

without a separate founder-approved architecture decision and highest applicable Build OS risk pathway.

---

## Section 8 — AI Output Status Labels

Every material AI output must have a status label where the product stores, reviews, releases, relies on, or audits the output.

Minimum AI output status labels:

| Status | Meaning |
|--------|---------|
| `draft` | AI-generated output not yet reviewed. |
| `pending_review` | Output is waiting for human review. |
| `approved` | Output approved for the scoped use. |
| `approved_with_edits` | Output approved after human modification. |
| `rejected` | Output reviewed and rejected. |
| `escalated` | Output requires higher-level or specialist review. |
| `released` | Output has been sent, published, displayed, or applied according to approved scope. |
| `archived` | Output retained for record but not used. |
| `superseded` | Output replaced by a later approved version. |
| `unsafe` | Output marked unsafe, hallucinated, source-insufficient, privacy-risk, or otherwise unsuitable. |

A material AI output must not move from `draft` or `pending_review` to `released` unless the product scope permits release and the required review gate has been satisfied.

Status changes must be logged where the output is material.

---

## Section 9 — Retrieval Rules

Retrieval assistants are governed by this section.

If the assistant is part of the internal knowledge layer, NTK-09 also applies.

### Rule 9.1 — Approved documents first

Retrieval systems must prefer approved documents, governed knowledge, committed policies, verified product files, approved SOPs, and source-controlled references.

The assistant must not invent policy where no approved source exists.

### Rule 9.2 — Source basis must be retained

Where retrieval informs a material output, the system must retain the source basis internally.

Depending on product scope, this may be:

- citation shown to the user;
- internal source reference;
- document ID;
- file path;
- retrieval result ID;
- answer-source log;
- approved policy reference.

### Rule 9.3 — Unknowns must escalate

If no approved source exists, the assistant must not fill the gap with plausible content.

It must:

- say the source is not available;
- ask for clarification;
- route to human review;
- flag a missing source; or
- create a knowledge gap item, if the product supports that workflow.

### Rule 9.4 — Retrieval permissions must match user permissions

A user must not receive information from documents, tenants, products, or sources they are not allowed to access.

Retrieval filtering must respect:

- tenant ID;
- user role;
- workspace;
- product;
- document status;
- public/private classification;
- source approval status;
- data retention rules;
- export rules; and
- internal-only restrictions.

### Rule 9.5 — Retrieved content is not automatically true

Retrieval reduces hallucination risk but does not remove it.

Retrieved content may be:

- outdated;
- superseded;
- contradictory;
- incomplete;
- draft only;
- user-provided;
- tenant-specific;
- product-specific;
- not approved.

The assistant must respect source status and escalate contradictions.

### Rule 9.6 — Retrieval must not become silent governance

A retrieval assistant may explain existing governance. It may not create new governance, silently resolve contradictions, or treat an answer as a committed decision.

Governance decisions remain governed by NTK-03, founder confirmation, and GitHub commit.

---

## Section 10 — Privacy and Data Rules

### Rule 10.1 — Data boundaries must be defined before build

Every AI assistant must define:

- allowed input data;
- prohibited input data;
- allowed retrieved data;
- prohibited retrieved data;
- whether tenant data is involved;
- whether personal data is involved;
- whether sensitive data is involved;
- whether outputs are stored;
- who can view outputs;
- retention rules;
- export rules;
- deletion rules; and
- review permissions.

### Rule 10.2 — Tenant data must remain tenant-bound

AI context assembly must not mix tenant data across tenants.

Tenant ID must be enforced server-side where tenant data is involved.

Domain, slug, user-provided tenant name, or visible branding must not be treated as the authority for data access.

### Rule 10.3 — Personal and sensitive data are minimised

The assistant must receive the minimum data required for the task.

Sensitive data should be redacted, summarised, referenced, or excluded unless it is necessary for the approved output.

### Rule 10.4 — AI provider exposure must be understood

Before an assistant sends data to an AI provider, the scope must define:

- what data leaves Nikari-controlled infrastructure;
- whether the provider may retain or train on the data;
- what contractual or product terms apply;
- whether the user must be notified;
- whether tenant or client approval is required;
- whether a safer provider or local method is required; and
- what redaction or minimisation applies.

### Rule 10.5 — User-facing AI must be transparent enough

Where a user interacts with AI, the product should not misrepresent the assistant as a human.

The user experience must make clear enough that the user is receiving AI-assisted output where that matters to trust, risk, or reliance.

### Rule 10.6 — Logs must not become privacy leaks

Logging is required for material outputs, but logs must not capture unnecessary secrets, personal data, private notes, tenant data, provider responses, or raw prompts beyond what the product needs for review, audit, debugging, and improvement.

---

## Section 11 — Cost and Usage Controls

AI usage must be financially governable before production use.

### Required controls

Every formal assistant must define:

- model/provider selection rule;
- token budget;
- request rate limit;
- user-level quota where relevant;
- tenant-level quota where relevant;
- client-level quota where relevant;
- daily or monthly budget threshold;
- abuse handling;
- timeout behaviour;
- retry behaviour;
- fallback behaviour;
- usage logging;
- cost visibility; and
- escalation when cost thresholds are reached.

### Provider and model routing

Model routing must be server-side and governed.

Routing may consider:

- task type;
- risk level;
- required quality;
- latency;
- cost;
- context size;
- privacy posture;
- user or tenant plan;
- availability;
- fallback state.

The user interface should not depend on a specific provider.

### Client-level quotas

For white-label or client-facing use, quotas may be attached to:

- tenant;
- subscription tier;
- feature entitlement;
- product plan;
- user role;
- monthly allowance;
- fair-use limit; or
- paid usage threshold.

Quotas must be product-scoped and visible to operators where needed.

### Abuse handling

Assistant scope must define abuse handling for:

- repeated high-cost requests;
- prompt injection attempts;
- prohibited content attempts;
- sensitive data insertion;
- scraping-like behaviour;
- automated misuse;
- cross-tenant probing;
- excessive retries;
- user attempts to bypass review; and
- attempts to extract hidden prompts or system instructions.

---

## Section 12 — AI Assistant Start Protocol

No formal AI assistant build begins until the five-stage start protocol is complete.

### Stage 1 — Assistant Intake

Define:

- assistant name;
- product or package context;
- operating lane;
- category;
- users;
- purpose;
- commercial logic;
- user-facing or internal posture;
- whether it is standalone or embedded;
- whether it is a primary Lane 5 product or Lane 5 overlay; and
- whether NTK-09 also applies.

**Output:** AI assistant concept note.  
**Gate:** Founder approval.

### Stage 2 — Authority and Risk Classification

Define:

- allowed output types;
- authority level;
- prohibited outputs;
- human review gate;
- risk class;
- sensitive domains involved;
- data mutation possibility;
- publication possibility;
- user reliance risk;
- tenant risk;
- security risk; and
- required reviewer role.

**Output:** Authority and risk classification note.  
**Gate:** Founder approval and Build OS confirmation where relevant.

### Stage 3 — Data, Source, and Context Boundary

Define:

- allowed inputs;
- allowed retrieval sources;
- source approval status;
- tenant boundary;
- role boundary;
- prompt context assembly;
- privacy minimisation;
- logging requirement;
- retention posture;
- escalation path; and
- unknown-source behaviour.

**Output:** Data and source boundary note.  
**Gate:** Build OS confirmation.

### Stage 4 — Assistant Module Manifest

Produce the Assistant Module Manifest defined in Section 13.

The manifest must be complete before Build OS produces a Build Plan.

**Output:** Assistant Module Manifest.  
**Gate:** Founder approval.

### Stage 5 — Build OS Readiness

Build OS confirms:

- NTK-08 is current;
- NTK-09 applies or does not apply;
- SCOPING.md exists where required;
- contracts/Joints are identified;
- package family is correct;
- review queue is scoped;
- logging is scoped;
- provider routing is server-side;
- cost controls are defined;
- risk tier is correct;
- rollback and fallback behaviour are defined; and
- no formal build proceeds without an approved Build Plan.

**Output:** Build OS readiness confirmation.  
**Gate:** Build OS gate before Cursor opens.

---

## Section 13 — Assistant Module Manifest

Every formal AI assistant feature requires an Assistant Module Manifest.

The manifest is the minimum structured artefact Build OS must consume before preparing a Build Plan.

### Required manifest fields

```yaml
assistant_manifest_version: "1.0"

assistant:
  name: ""
  slug: ""
  category: "internal | client_facing | embedded_workflow | build_assistant | retrieval"
  product_context: ""
  package_family: "ai-assistant | vertical/[product] | knowledge-layer | other"
  operating_lane: "Lane 1 | Lane 2 | Lane 3 | Lane 4 | Lane 5"
  lane_5_posture: "primary | overlay | not_applicable"
  purpose: ""
  primary_users: []
  excluded_users: []

authority:
  authority_level: "draft_only | advisory | source_bound_answer | bounded_automation | prohibited_final_authority"
  allowed_output_types: []
  prohibited_output_types: []
  human_review_required: true
  reviewer_role: ""
  auto_publish_allowed: false
  data_mutation_allowed: false
  external_send_allowed: false
  escalation_required_when: []

inputs:
  allowed_inputs: []
  prohibited_inputs: []
  sensitive_contexts: []
  input_validation_required: true
  prompt_injection_risk: "low | medium | high | critical"

context:
  allowed_sources: []
  source_approval_required: true
  retrieval_required: false
  ntk_09_applies: false
  tenant_data_involved: false
  personal_data_involved: false
  sensitive_data_involved: false
  context_minimisation_rule: ""

architecture:
  server_side_prompt_routing: true
  provider_abstraction_required: true
  model_routing_rule: ""
  fallback_behaviour: ""
  non_ai_fallback: ""
  frontend_prompt_visibility_allowed: false

logging:
  output_logging_required: true
  output_status_labels_required: true
  review_history_required: true
  source_reference_required: true
  retention_rule: ""
  audit_events: []

cost_controls:
  token_limit: ""
  rate_limit: ""
  user_quota: ""
  tenant_quota: ""
  monthly_budget_limit: ""
  abuse_handling: ""

review:
  review_queue_required: true
  approval_actions:
    - approve
    - reject
    - edit
    - escalate
  pre_release_check_required: true
  post_release_review_required: false

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

A missing manifest means the assistant is not ready for Build OS assembly.

A manifest that says “to be decided later” for authority level, data boundary, review gate, logging, or server-side routing is incomplete.

---

## Section 14 — AI Assistant Package and Module Implications

AI assistant code, prompt orchestration, model routing, review queues, cost controls, and assistant manifests must be placed according to NTK-05 package architecture.

Default package posture:

- generic AI assistant infrastructure belongs in `packages/ai-assistant/`;
- product-specific AI assistant logic belongs in `packages/vertical/[product]/`;
- white-label-specific AI configuration must comply with NTK-06;
- reusable AI assistant modules may be promoted only under NTK-07;
- internal knowledge-layer modules belong under NTK-09 once produced.

A folder in `packages/ai-assistant/` is not automatically reusable or stable. AI assistant modules must follow NTK-07 status, versioning, compatibility, and promotion rules before being treated as reusable platform infrastructure.

Where an AI assistant depends on retrieval against internal governed documents, SOPs, handovers, or knowledge libraries, NTK-09 must apply before formal knowledge-layer build.

---

## Section 15 — AI Testing and Evaluation

Every formal AI assistant must define testing appropriate to its risk level before production use.

Testing may include:

- prompt behaviour tests;
- approved-source retrieval tests;
- no-source escalation tests;
- prompt-injection resistance tests;
- tenant-isolation tests;
- role-permission tests;
- hallucination review samples;
- sensitive-data minimisation checks;
- output-format validation;
- HITL queue tests;
- cost and rate-limit tests;
- fallback / provider failure tests; and
- regression checks after material prompt or model changes.

AI testing does not prove the assistant is always correct. It proves the assistant behaves within its approved scope and fails safely when confidence, source, permission, or context is insufficient.

---

## Section 16 — Risks

### Risk 1 — Hallucination

AI may produce plausible but incorrect content.

Mitigation:

- approved sources first;
- retrieval source logging;
- human review;
- uncertainty escalation;
- no invented policy;
- post-release correction path.

### Risk 2 — Privacy leakage

AI may expose personal, tenant, client, confidential, or sensitive data.

Mitigation:

- context minimisation;
- tenant-bound retrieval;
- server-side filtering;
- role-aware access;
- redaction;
- privacy-safe logging;
- provider exposure review.

### Risk 3 — Over-automation

AI may be allowed to perform actions that should remain human-controlled.

Mitigation:

- default draft-only posture;
- authority levels;
- HITL review;
- no auto-publish without explicit scope;
- Build OS risk classification;
- founder approval for bounded automation.

### Risk 4 — Client reliance

Users or clients may treat AI output as final advice or binding guidance.

Mitigation:

- clear scope;
- visible limitations where needed;
- escalation path;
- human review for sensitive domains;
- no legal, financial, property, compliance, or commercial finality by default.

### Risk 5 — Public misstatement

AI may publish or draft content that misleads, misstates, overpromises, breaches policy, or creates commercial risk.

Mitigation:

- no direct public publishing by default;
- review queue;
- source checks;
- approval role matched to risk;
- output logging;
- correction path.

### Risk 6 — Silent AI decision-making

AI may silently affect ranking, routing, suppression, scoring, access, or recommendations.

Mitigation:

- authority declaration;
- reviewability;
- audit trail;
- operator visibility;
- human override;
- source and reasoning basis where appropriate.

### Risk 7 — Prompt injection

User-provided, retrieved, uploaded, or imported content may attempt to override system instructions.

Mitigation:

- untrusted-content treatment;
- instruction hierarchy;
- server-side prompt routing;
- tool restrictions;
- source filtering;
- review gate for risky outputs.

### Risk 8 — Provider lock-in

Product workflows may become dependent on one AI provider or model.

Mitigation:

- provider abstraction;
- server-side routing;
- structured inputs;
- fallback behaviour;
- model-independent product logic.

### Risk 9 — Cost runaway

AI features may become commercially unsustainable due to uncontrolled usage.

Mitigation:

- quotas;
- token budgets;
- rate limits;
- model routing;
- usage logs;
- tenant/client budget thresholds;
- abuse handling.

### Risk 10 — AI module promoted too early

An assistant pattern may be treated as reusable before it has been proven, documented, versioned, and tested.

Mitigation:

- start product-specific or vertical where appropriate;
- apply NTK-07 for promotion;
- require assistant manifest;
- require compatibility review;
- require versioning and changelog for reusable assistant modules.

---

## Section 17 — Update Triggers

This document must be reviewed and updated when any of the following occur:

1. first AI assistant feature is assembled via Build OS;
2. first client-facing AI assistant is scoped;
3. first embedded workflow assistant is scoped;
4. first retrieval assistant is scoped;
5. first AI assistant appears in a white-label product;
6. first AI output is shown on a public or user-facing surface;
7. AI output status labels are changed or prove insufficient;
8. first bounded automation request is proposed;
9. first AI output affects a material user, client, commercial, tenant, legal, property, financial, compliance, or operational decision;
10. first prompt family is versioned or materially changed;
11. first provider abstraction or model-routing change is proposed;
12. first cost-control breach occurs;
13. first hallucination, privacy, prompt-injection, source-boundary, or over-automation incident occurs;
14. first AI assistant package or module is proposed for reuse or promotion;
15. first AI testing and evaluation pattern is adopted or proves insufficient;
16. NTK-01 changes Lane 5, delivery modes, lifecycle gates, or operating roles;
17. NTK-02 changes AI, data, security, process, or anti-drift guardrails;
18. NTK-03 changes decision-log or supersession requirements;
19. NTK-04 changes monorepo placement or AI package structure;
20. NTK-05 changes `packages/ai-assistant/`, `contracts/`, Joints, package families, or dependency direction;
21. NTK-06 changes white-label AI implications;
22. NTK-07 changes module promotion implications for AI assistant packages;
23. NTK-09 is produced or changes retrieval / knowledge-layer implications;
24. NTK-10 changes portfolio routing for AI products; or
25. founder identifies a new AI authority risk not covered by this document.

### NTK-03 append note

After founder confirmation of NTK-08, NTK-03 should receive append entries for any AI assistant decisions the founder wants recorded as discrete Nikari Tech decisions. At minimum, the adoption of NTK-08 as the formal Lane 5 AI Assistant Product Standard should be recorded.

Likely NTK-03 entries include:

1. formal Lane 5 AI product build requires NTK-08;
2. AI assists by default and does not hold final authority unless explicitly scoped;
3. server-side prompt routing is mandatory;
4. AI output logging and reviewability are required where material;
5. AI output status labels adopted;
6. Assistant Module Manifest adopted;
7. AI assistant package and module implications adopted;
8. AI testing and evaluation standard adopted;
9. HITL review is permanent for sensitive outputs;
10. provider abstraction adopted for AI assistant products;
11. NTK-09 remains required for internal knowledge-layer module builds.

These entries should remain separate if recorded because they govern different parts of AI assistant architecture and authority.

---

*Version: 1.0 — working standard*  
*Produced: Nikari Tech — NTK-08 AI Assistant Product Standard Session, 29 April 2026*  
*Approved by: Wiets Marais — 29 April 2026*  
*Read with: UNIVERSAL_DECISIONS.md, NTK-00, NTK-01, NTK-02, NTK-03, NTK-04, NTK-05, NTK-06, NTK-07, NTK-09 when produced*  
*Next update trigger: See Section 17*  
*Proposed repo location: `wietsmarais/docs/architecture/NTK-08_AI_Assistant_Product_Standard.md`*
