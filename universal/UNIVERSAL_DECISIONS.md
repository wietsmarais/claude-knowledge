# Universal Decisions Log
**Repo:** github.com/wietsmarais (root)
**Applies to:** All projects — cross-project decisions only
**Rules:** Append only. Never edit existing entries. Most recent entry at the bottom.
**Maintained by:** Founder + Claude — Developer OS sessions

Project-specific decisions live in each project's `docs/decisions/DECISIONS.md`.
A decision moves to this file when it changes how ALL projects are built —
or when it creates a named exception to a universal standard.

---

## 2026-04-09 — Three-stage project start protocol adopted

**Decision:** Every new project follows three stages in sequence:
Stage 1 (Developer OS Claude project) → Stage 2 (Project Claude project) →
Stage 3 (Cursor in the repo). Skipping stages is not permitted.

**Reason:** Projects started directly in Cursor without a scoping stage
lacked architectural intent and required rework. Projects without a dedicated
Claude project lost strategic context between sessions.

**Alternatives considered:** Single Claude project for all builds (rejected —
context contamination risk), Cursor only with no Claude architecture stage
(rejected — no strategic memory).

**Constraints this creates:** Every project requires a Developer OS session
before any code is written. This adds time at the start and saves it throughout.

**Approved by:** Founder

---

## 2026-04-09 — One chat per session rule adopted

**Decision:** One chat window equals one session. One session has one stated goal.
When the goal is complete, the chat closes. The next goal opens in a new chat.

**Reason:** Multi-task chats accumulate context that degrades output quality,
inflates token costs, and prevents clean session handovers. Without a formal
session boundary, handovers were inconsistently produced.

**Constraint added:** Claude must state "Session complete. Handover saved. Safe to close."
at the end of every session. This phrase is the session boundary signal.

**Approved by:** Founder

---

## 2026-04-09 — Component library as universal knowledge base

**Decision:** The component library (`github.com/wietsmarais/component-library`)
is the long-term compounding knowledge base for all builds. Every proven pattern
from any project is extracted here with a SPEC.md. The README is the index
Claude reads to know what exists before suggesting anything.

**Reason:** Knowledge trapped in individual project repos does not compound.
A centralised, version-controlled, machine-readable library compounds across
every project and every year.

**Constraint added:** The session close ritual includes an extraction candidate
check. If a pattern built in a session is generic enough for reuse, it is flagged
for extraction before the session closes.

**Approved by:** Founder

---

## 2026-04-09 — Universal vs project-level learnings split

**Decision:** Learnings and decisions that apply to a single project live in
that project's `docs/decisions/DECISIONS.md` and `LEARNINGS.md`.
Learnings and decisions that change how ALL projects are built are extracted
to this file (`UNIVERSAL_DECISIONS.md`) and `UNIVERSAL_LEARNINGS.md` in the
`wietsmarais` root repo.

**Reason:** Project-level files accumulate project-specific noise. Universal
insights were being lost inside individual repos rather than changing the
operating model for all projects.

**Trigger for extraction:** At the end of every project phase, Claude reviews
the project LEARNINGS.md and asks — does anything here change how we build
all projects? If yes, it is extracted to universal level.

**Approved by:** Founder

---

## 2026-04-09 — Supabase organisation Pro plan confirmed as correct setup

**Decision:** All projects run under a single Supabase organisation on the Pro plan
at $25/month. Spend cap remains enabled at all times. Individual project free tiers
are not used — all projects inherit Pro entitlements.

**Reason:** Organisation-level billing covers all projects at a flat rate.
Adding projects does not increase base cost. Spend cap prevents surprise charges.

**Constraint added:** Revenue trigger rule — when any project generates its first
dollar of external revenue, review compute add-on for that project and budget
infrastructure cost into project financials.

**Approved by:** Founder

---

## 2026-04-09 — Governance documents location confirmed

**Decision:** The six canonical governance documents live in NRE-01
`docs/architecture/` as the primary governed repo. The CURSOR_AGENT_PROMPT_LIBRARY
lives in the cursor-prompts repo. Both are read by Cursor from the repo —
not uploaded to Claude except for the three that also live in Developer OS
project knowledge (AI_BUILD_GUARDRAILS, PROJECT_MANAGEMENT_DISCIPLINE, PROJECT_STANDARDS).

**Reason:** Governance documents must be readable by the agent from the repo.
Claude project knowledge holds only what Claude needs to direct — not everything
Cursor needs to execute.

**Approved by:** Founder

---

## 2026-04-13 — ORM confirmed: Supabase client. Prisma not adopted.

**Decision:** Supabase client (`@supabase/supabase-js`) is the ORM for all projects.
Prisma is not adopted at any tier.

**Reason:** Prisma's service role key requirement bypasses RLS — a non-negotiable
security constraint. Running dual migration systems (Prisma + Supabase) creates
schema drift risk. Supabase client with typed queries via `database.types.ts`
covers all query needs without the bypass risk.

**Alternatives considered:** Prisma (rejected — RLS bypass, dual migrations),
Drizzle (not evaluated — Supabase client sufficient at current scale).

**Constraints this creates:** All queries use Supabase client syntax. TypeScript
types generated via `npx supabase gen types typescript`. No raw SQL in application
code except via Supabase RPC functions.

**Approved by:** Founder

---

## 2026-04-13 — LangChain: threshold adoption only

**Decision:** LangChain is not part of the standard stack. It is adopted only
when a specific project requires multi-step retrieval or RAG pipelines that
the raw Anthropic API cannot handle cleanly.

**Reason:** LangChain adds abstraction overhead and debugging complexity for
single-call AI features. Raw API is simpler, cheaper, and easier to debug
for the majority of use cases.

**Trigger for adoption:** Nikari AI-native property matching is the anticipated
first RAG use case. LangChain adoption is deferred until that feature is scoped.

**Approved by:** Founder

---

## 2026-04-13 — Vercel AI SDK adopted as standard for all Next.js projects

**Decision:** Vercel AI SDK (`ai` + `@ai-sdk/anthropic`) is installed at setup
on every Next.js primary workflow project. It handles all streaming AI responses
into React components (`useChat`, `useCompletion`).

**Reason:** Building custom streaming infrastructure is unnecessary and error-prone.
Vercel AI SDK is purpose-built for this stack and integrates cleanly with
Next.js App Router.

**Constraints this creates:** No custom streaming infrastructure is built.
LangChain streaming is also handled via Vercel AI SDK when LangChain is adopted.

**Approved by:** Founder

---

## 2026-04-13 — pgvector via Supabase confirmed as vector store

**Decision:** pgvector inside Supabase is the vector store for all semantic search
and embedding features. External vector databases (Pinecone, Weaviate) are not
adopted at current scale.

**Reason:** Keeping the vector store inside Supabase eliminates a third-party
dependency, keeps data in the same RLS-governed environment, and avoids
additional cost and complexity at current project scale.

**Trigger for revisit:** If a project requires vector search at a scale that
exceeds pgvector performance limits, external vector DB adoption is reconsidered.

**Approved by:** Founder

---

## 2026-04-13 — vix-trading-journal branch exception: master is permanent default

**Decision:** `vix-trading-journal` uses `master` as its permanent default branch.
This is a named exception to the Developer OS universal standard of `main`.

**Reason:** This was an explicit decision locked in VIX Trading Journal Session 1.
`main` was subsequently created and deleted intentionally. The deployment
configuration is bound to `master`. Renaming would break the deployment pipeline.

**Alternatives considered:** Renaming to `main` to align with universal standard
(rejected — breaks deployment, contradicts locked project decision).

**Constraints this creates:**
- Never rename `master` to `main` in `vix-trading-journal`
- Never recreate `main` in `vix-trading-journal`
- Any Developer OS session or agent that references universal branch standards
  must treat `vix-trading-journal` as an explicit exception
- Any session touching `vix-trading-journal` must read VIX project instructions
  before acting on Developer OS branch conventions
- Project-level rules take precedence over Developer OS universal standards
  when a conflict is explicitly documented here

**Scope of exception:** `vix-trading-journal` only. All other repos follow
the `main` standard unless a separate exception is logged.

**Approved by:** Founder

---

*Append new entries below this line.*
*Format: ## [YYYY-MM-DD] — [Decision title]*
*Never edit entries above this line.*

## 2026-04-22 — Added write approval gate guardrails and updated A01
C11 (Write Approval Gate) and C12 (Commit Message Encoding) added to
AI_BUILD_GUARDRAILS.md in nre-01-core-platform.
A01 in CURSOR_AGENT_PROMPT_LIBRARY.md updated to prepend standing instructions
block and universalised file-reading steps.
Reason: em-dash corruption in commit messages and silent writes caused rework.
Approved by: Founder.

## 2026-04-22 — Correction: guardrails landed as C13/C14 not C11/C12
The entry dated 2026-04-22 above references C11 and C12 (Write Approval Gate and
Commit Message Encoding). The actual guardrails were inserted as C13 and C14
because C11 and C12 already existed in docs/AI_BUILD_GUARDRAILS.md with different
content. All future references to these guardrails must use C13 and C14.

---

## 2026-04-25 — Primary commercial model

**Decision:** All Nikari Tech products use subscription SaaS with white-label
self-configuration as the primary commercial model. Separate Supabase instances
are reserved for enterprise tier only and represent a commercial migration event,
not a starting point.

**Approved by:** Founder

---

## 2026-04-25 — Multi-tenant architecture standard

**Decision:** Every product is built multi-tenant from day one. Tenant isolation
via RLS and tenant_id on every table. Consumer and SMB products share one Supabase
instance per product. Enterprise clients migrate to isolated instances when scale
or compliance requires it.

**Approved by:** Founder

---

## 2026-04-25 — Supabase is the pipeline database

**Decision:** Supabase handles all pipeline, lead qualification, call logging, and
agent activity data. Google Sheets is not the pipeline database. Sheets role is
limited to analysis, reporting surface, and Claude intelligence layer only.

**Approved by:** Founder

---

## 2026-04-25 — Odoo deprioritised

**Decision:** Odoo Free CRM is an optional operator view for Gold leads only —
not a database layer. Odoo Custom is not required at current stage. Revisit only
when relational complexity or compliance genuinely requires it. The AI-native stack
(Supabase, Next.js, Claude Projects, Xero) covers what Odoo would have covered.

**Approved by:** Founder

---

## 2026-04-25 — Module library is the business

**Decision:** Every feature built for any Nikari product must be evaluated for
extraction into the white-label module library before the session closes. Modules
must confirm tenant-awareness and toggle-readiness before extraction is considered
complete.

**Approved by:** Founder

---

## 2026-04-25 — AI assistant delivery mode confirmed at Stage 1

**Decision:** Every project with an AI assistant must declare Path A (Claude
Project URL, user's subscription) or Path B (Anthropic API, invisible, Nikari pays)
at scoping. Path B requires API cost estimate in SCOPING.md. This is a Stage 1
blocker.

**Approved by:** Founder

---

## 2026-04-25 — Onboarding is conversational not form-based

**Decision:** Client onboarding for all Nikari Tech products is AI-assisted via
Claude Project. Conversational, guided by questions, not a settings panel. Voice
file captured at onboarding to personalise the AI assistant from day one.
Complexity must not exceed what a non-technical client can complete independently
in under 15 minutes.

**Approved by:** Founder

---

## 2026-04-25 — Client AI assistants are compounding not stateless

**Decision:** Client-specific knowledge accumulates in Supabase and is injected
into prompts at the start of each new chat session via the deep link prompt
injection layer. The Claude Project stays generic and universal. Personalisation
comes from the database layer growing over time. Human-in-the-loop review required
before any pattern is committed to the knowledge base.

**Approved by:** Founder

---

## 2026-04-25 — Claude Code added to workflow

**Decision:** Claude Code handles terminal operations, file writes, repo management,
and git operations autonomously. Cursor remains primary for visual multi-file
editing. ChatGPT remains the pre-commit code reviewer — independent model, external
verification. The two real quality gates are prompt quality going in and AI review
before commit. Claude Code does not change either gate.

**Approved by:** Founder

---

## 2026-04-25 — Stage 1 scoping blockers updated

**Decision:** The following are now non-negotiable Stage 1 blockers alongside RLS:
multi-tenant architecture confirmation, tenant config shape, subscription tier
gating, toggle implementation per module, onboarding flow design confirmed as
conversational, and AI assistant delivery mode declared as Path A or Path B.


---

## 2026-04-27 — AI Assistant Suite Module expanded to six components

**Decision:** The AI Assistant Suite Module is formally defined as a
six-component architecture. The original four-component description
(document library, verification engine, compounding library, privacy
layer) is superseded. Two components added: Component Five (Executor
— agentic execution layer) and Component Six (Governed System Prompt
Library). The master spec document
(docs/architecture/AI_ASSISTANT_SUITE_MODULE_MASTER_SPEC_27042026.md)
is the single source of truth and supersedes all prior references.
**Reason:** Components Five and Six were identified as necessary
gaps during a strategy session reviewing agentic build automation
and visible agent architecture. Without them the module cannot
execute approved outputs or maintain governed, versioned AI behaviour.
**Alternatives considered:** Treating Executor and System Prompt
Library as separate modules. Rejected — they are integral to every
AI assistant deployment and must be part of the core module, not
optional add-ons.
**Constraints this creates:** No AI Assistant Suite Module scoping
session or build session may begin without reading the master spec.
No component is scoped independently — all six are scoped together.
**Approved by:** Founder

---

## 2026-04-27 — Visible Agent Platform added to Nikari Tech portfolio

**Decision:** The Visible Agent Platform is a formal Nikari Tech
portfolio concept with two expressions: Expression A (white-label
client onboarding agent) and Expression B (personal development
workflow agent). Both expressions share the same six-component
AI Assistant Suite Module architecture. Expression B is built
before Expression A without exception.
**Reason:** The concept was identified as the architectural completion
of the governed orchestration platform — making AI output visible,
executable, and compounding in a deployable package. The combination
of governed, visible, compounding, and private in a single system
does not yet exist as a product.
**Alternatives considered:** Treating Expression A and B as separate
products. Rejected — they share identical architecture and building
B first provides the proven foundation for A.
**Constraints this creates:** Expression A cannot be scoped or built
before Expression B is operational in practice. The Build OS scoping
session must treat Expression B (development workflow agent) as a
first-order design goal.
**Approved by:** Founder

---

## 2026-04-27 — In-session verification routing confirmed as Component Two standard

**Decision:** The Dual/Triple Verification Engine (Component Two of
the AI Assistant Suite Module) applies at two levels: pre-proposal
(agent routes uncertain questions to a second model before presenting
to human) and post-output (pre-commit review gate). The routing logic
is governed by the system prompt. Default routing: critical path tasks
route to Claude Sonnet; legal/compliance tasks route to a second model;
conflicting outputs escalate to the human with both responses shown.
Human can invoke verification manually at any time.
**Reason:** In a dynamic non-pre-learnt environment (Expression B),
the primary hallucination risk is the agent acting confidently on a
wrong inference. Pre-proposal verification catches uncertainty before
it reaches the human gate rather than after code is written.
**Alternatives considered:** Post-output review only (current
pre-commit ChatGPT gate). Retained as the second gate — pre-proposal
verification is additive, not a replacement.
**Constraints this creates:** The governed system prompt for every
AI assistant deployment must define the verification routing rules
explicitly. A deployment without routing rules is non-compliant.
**Approved by:** Founder

---

## 2026-04-27 — AnythingLLM Desktop confirmed as Phase 1 interface for Expression B

**Decision:** AnythingLLM Desktop is the application layer for
Expression B (personal development workflow agent) Phase 1.
Install this week. Connect to Claude Sonnet via Anthropic API.
Load governance documents as workspace. Enable Desktop Assistant
overlay (CTRL+/). Run alongside a real NRE-01 build session.
Conversational only in Phase 1 — no Executor connected until
Phase 1 success criteria are met across 3+ consecutive build
sessions with no material context errors.
**Reason:** AnythingLLM Desktop provides the screen-aware overlay,
30+ LLM provider support, MCP compatibility, computer use capability,
and white-label deployment option needed for both expressions.
It is available today with no build work required for Phase 1.
**Alternatives considered:** Building a custom interface from scratch.
Rejected — premature before the architecture is proven in practice.
**Constraints this creates:** Phase 2 (Executor build) cannot begin
until Phase 1 success criteria are documented in a session note.
**Approved by:** Founder

---

## 2026-04-27 — Groq and Cerebras confirmed as Phase 2 inference providers; DeepSeek V3.2 confirmed as primary coding model

**Decision:** For Phase 2 production AI assistant deployments where
coding-heavy reasoning is the primary task, DeepSeek V3.2 via Groq
(latency-critical) or Cerebras (throughput-critical) is the
production inference stack. This replaces Anthropic API at production
scale for applicable task types. Evaluation at commercialisation
point — not at scoping point.
**Reason:** DeepSeek V3.2 delivers approximately 90% of frontier
model quality at $0.28 per million tokens — approximately 1/50th
the cost of GPT-5 level models. Groq and Cerebras provide the
inference speed required for interactive agent use. Data sovereignty:
deployments can be configured so no data leaves the operator's
infrastructure.
**Alternatives considered:** Anthropic API at production scale.
Retained for Phase 1 validation and for tasks requiring maximum
reasoning quality. The two-provider model (Anthropic for build and
validation, Groq/Cerebras for production scale) is the confirmed
architecture.
**Constraints this creates:** Phase 2 inference provider selection
must be confirmed in the AI Assistant Suite Module SCOPING.md.
Path B products must specify inference engine at scoping.
**Approved by:** Founder

---

## Decision: Session handover opening prompts must specify the next session goal explicitly

Date: 27 April 2026
Status: LOCKED

Rule: Every session handover opening prompt must name the next session goal explicitly, drawn from the priority order in that handover. No placeholder text. No "state goal here." The next action is always determined at session close, not at the start of the next session.

Rationale: Open-ended opening prompts have recurred across multiple sessions. The failure mode is the founder opening a new chat without a clear goal stated, leading to scope drift or wasted session time orienting. The handover is the correct place to lock the next goal — it is produced at session close when context is freshest.

Applies to: All projects. All handovers. No exceptions.

---

## 27 April 2026 — File destination and commit instructions are mandatory at point of production

**Decision:** Every file produced in a Claude Web session must be followed immediately by a destination label in this exact format:

File: [filename]
Destination: [exact GitHub path]
Commit message: [exact commit message]
Action: Drag into folder, commit via GitHub Desktop

Appends, patches, and multi-location edits to existing files are never given to the founder as manual instructions. Claude produces a Claude Code prompt for these operations without exception.

When a session produces more than one governance artifact, Claude produces a single Claude Code commit prompt at session close covering all files in one operation.

**Reason:** Manual file routing after session close has been a recurring time cost across all projects. The founder should never need to determine where a file goes or what the commit message should be.

**Applies to:** All projects. All sessions. All file types.

**Approved by:** Wiets Marais — 27 April 2026

---

## 27 April 2026 — Claude Code prompt standard — five mandatory rules

**Decision:** Every Claude Code prompt produced in any Claude Web session must follow these five rules without exception:

Rule 1 — Exact file path. Never "find the file." Always the full path: C:\GitHub\repo\path\to\file.md
Rule 2 — Exact location. Never "find the section called X." Always "append to the bottom" or "replace the exact text below."
Rule 3 — Exact content. Content pasted inline in the prompt. Never a reference to another file.
Rule 4 — One task per prompt. One file, one operation, one commit. Chain nothing.
Rule 5 — Ten second search limit. If the file or text is not found within ten seconds, stop and report the exact path that failed. Do not search alternative files. Do not read related documents. Wait for correction.

**Reason:** Claude Code search loops burn tokens on trivial tasks. A two-minute search for a simple append is a governance failure, not an acceptable outcome.

**Applies to:** All projects. All sessions. All Claude Code prompts.

**Approved by:** Wiets Marais — 27 April 2026

--- 

27 April 2026 — Session handover open actions must become GitHub issues
Decision: Every open action in a session handover that is not confirmed
complete in the same session MUST become a GitHub issue in
wietsmarais/wietsmarais before that handover closes.
The session handover file destination label must list the issue numbers
created. No action is carried forward in prose only.
Scope: All projects. All sessions. All repos. Permanently.
What this replaces: The "Topics Carrying Forward" prose list pattern
in session handovers. That pattern allowed items to drift across multiple
sessions without accountability. It is now retired.
Implementation:

At session close, review all actions not completed this session
Create a GitHub issue in wietsmarais/wietsmarais for each open action
Use --body-file method via gh CLI in Command Prompt (not PowerShell)
Record issue numbers in the session handover file destination label
Handover does not close until issues are created and numbered

Rationale: Eight open actions drifted across six consecutive sessions
(25 April → 27 April 2026) without being actioned. GitHub issues provide
a persistent, visible, searchable record that survives session boundaries.
First application: Issues #10–#18 created 27 April 2026, backfilled
from carry-forward items dating to 25 April 2026 S2.
Approved by: Wiets Marais — 27 April 2026

---

27 April 2026 — claude-knowledge public repo as live Claude reference layer
Decision: A public GitHub repo wietsmarais/claude-knowledge will
serve as the live knowledge layer for all Claude projects across the
entire Nikari Tech portfolio.
Core principle: Claude projects fetch governance and reference files
directly from this repo at session open via raw GitHub URLs. Uploaded
project knowledge files are replaced by live fetches over time. One
source of truth. Always current. No re-upload triggers required.
Raw URL pattern:
https://raw.githubusercontent.com/wietsmarais/claude-knowledge/main/[folder]/[file].md
Proposed folder structure:
wietsmarais/claude-knowledge/
├── universal/
│   ├── UNIVERSAL_DECISIONS.md
│   ├── MODULE_READINESS_MATRIX.md
│   └── BUILD_OS_SCOPING.md
├── developer-os/
│   ├── Component-library_README.md
│   └── PROJECT_STARTER_PACK.md
├── build-os/
│   ├── BUILD_OS_SCOPING.md
│   └── MODULE_READINESS_MATRIX.md
├── nre-01/
├── vix/
└── README.md
What belongs here:
A file goes in claude-knowledge if Claude needs to read it at session open
AND it contains no sensitive IP, no credentials, no client data, and no
internal working documents.
What never goes here:

Session handovers
Cursor prompt library
SPEC.md files (component library IP)
Any file containing credentials or secrets
Client-specific documents
Internal working documents

Maintenance rule:
When a universal governance file is updated in the private wietsmarais
root repo, it is also pushed to claude-knowledge/universal/ in the same
session. Two-commit operation. Never deferred.
Replaces:

Static uploaded copies of universal governance files in Claude project
knowledge for reference documents
Re-upload triggers in session handovers for universal files

Keeps:

Uploaded project knowledge for session handovers
Uploaded project knowledge for anything sensitive or private

Closes: Issue #16 — Build OS Stage 3 repo. Build OS governance files
that are safe to be public live in claude-knowledge/build-os/. A separate
private build-os repo is not required.
Implementation: Tracked in GitHub issue #19 — dedicated session.
Do not build until issue #19 session is opened.
Approved by: Wiets Marais — 27 April 2026

---

Decision: Turborepo adopted as the standard monorepo architecture
Date: 28 April 2026
Status: LOCKED
All new projects and rebuilt projects use Turborepo inside the
nikari-platform monorepo. Existing repos (nre-01-core-platform,
vix-trading-journal, wedding platform) are treated as v1 legacy —
maintained in their current state, not migrated. Each migrates into
nikari-platform only when it reaches a natural major rebuild point.
Rationale: Four active projects already sharing components, auth patterns,
security patterns, and white-label config via manual copy-paste. The manual
sync problem is active, not future. Turborepo eliminates it structurally.

---

Decision: nikari-platform is the confirmed monorepo name and root
Date: 28 April 2026
Status: LOCKED
The Turborepo monorepo is named nikari-platform. It is a new GitHub repo
under the wietsmarais organisation. It is not a rename or migration of any
existing repo.
Repo: github.com/wietsmarais/nikari-platform
Default branch: main

---

Decision: wietsmarais remains the governance root — Option A confirmed
Date: 28 April 2026
Status: LOCKED
UNIVERSAL_DECISIONS.md, UNIVERSAL_LEARNINGS.md, and all architecture
governance documents stay in the wietsmarais root repo. The nikari-platform
monorepo references governance from wietsmarais but does not absorb it.
Governance and code are deliberately separated. The wietsmarais root repo
is the source of truth for all cross-project standards. nikari-platform is
the source of truth for all product code and shared packages.

---

Decision: Nikari Tech is the governing centre — NRE is one product on the platform
Date: 28 April 2026
Status: LOCKED
The architectural and strategic centre of the system is Nikari Tech, not
Nikari Real Estate. NRE is the flagship commercial product built on the
Nikari Tech platform. All other products — Social Shield, VIX, Flourish,
StudyOS, Counsel, LocalLoop — are also products built on the same platform.
All future governing documents, Build OS sessions, and Claude project
instructions must reflect this frame. NRE-centric language in existing
documents is not deleted but is subordinated to the Nikari Tech frame
established in NTK-00.

---

Decision: Three-level component hierarchy locked
Date: 28 April 2026
Status: LOCKED
All packages in nikari-platform are classified at one of three levels:
Level 1A — UI primitives (shadcn/ui + Tailwind tokens). Visual only.
Level 1B — Functional primitives. Pure logic, no UI surface. Single function.
Level 2 — Single-function organs. One job, completely done. Composes from
Level 1A and/or Level 1B. Tested in isolation.
Level 3 — Composite organs. Four to five Level 2 organs assembled into a
named, purposeful system. What apps actually import.
Nothing skips a level. Nothing rebuilds what already exists at a lower level.

---

Decision: contracts/ package is the mandatory foundation layer
Date: 28 April 2026
Status: LOCKED
A packages/contracts/ package is the first thing built in nikari-platform
before any organ or app is assembled. It contains:

types/ — shared data shapes (UserProfile, Tenant, Session, Error, Response)
interfaces/ — shared connection contracts (auth, storage, config interfaces)
constants/ — system-wide values (subscription tiers, user roles, error codes)

Rules:

No package may define its own types for shared concepts
All shared types live in contracts/
Every package imports shared types from contracts/ before implementation begins
Dependency direction is always downward — never sideways at the same level
contracts/ is read by Cursor before any new package is written, the same
way setup.sql is read before any Supabase query

---

Decision: Dependency direction rule — downward only, no sideways imports
Date: 28 April 2026
Status: LOCKED
Apps import from Level 3.
Level 3 imports from Level 2.
Level 2 imports from Level 1A and/or Level 1B.
Everything imports from contracts/.
Nothing imports upward.
Nothing imports sideways at the same level.
If two Level 2 organs need to share something, that something belongs in
contracts/ or in a Level 3 composite that wires them together.

---

Decision: Firebase not adopted universally
Date: 28 April 2026
Status: LOCKED
Firebase is not part of the universal Nikari Tech stack. Supabase Auth is
the authentication layer for all products.
Firebase App Check may be re-evaluated at Social Shield Phase 2 scoping
as a project-level decision only — not a universal standard. This evaluation
is triggered only if coordinated bot attacks on the API become a demonstrated
threat at scale.
Nikari broker/REA verification is a verified-user-tier/ component library
module — not a Firebase problem. To be scoped when NRE v2 build session opens.

---

Decision: Odoo is an integration module — not a universal product foundation
Date: 28 April 2026
Status: CONFIRMED — existing entry dated 2026-04-25 covers this decision.
Do not append a new entry. The existing wording is consistent and sufficient.
Existing entry confirms: Odoo Free CRM is optional, not a database layer.
Odoo Custom not required at current stage. AI-native stack (Supabase, Next.js,
Claude Projects, Xero) covers what Odoo would have covered.
Additional Nikari Tech framing confirmed this session: Supabase is the product
data plane. Odoo is available through packages/integrations/ as an optional
connector. White-label clients must be able to run without Odoo.
This is consistent with the existing entry — not a new decision.

---

Decision: verified-user-tier/ flagged as a component library gap
Date: 28 April 2026
Status: OPEN — to be scoped at NRE v2 build session
Broker and REA verification on Nikari Real Estate requires a new Level 3
composite organ: verified-user-tier/. It sits on top of auth/ and adds
licence verification and tier-based data access gating. Not a Firebase
problem. Scoped at NRE v2 build session inside nikari-platform.

---

Decision: Four governance additions to build discipline documents
Date: 28 April 2026
Status: OPEN — five-patch session required before first nikari-platform build
The following additions are confirmed as required. They are produced in the
next Build OS session as enforcement patches:

Staged build sequencing (7-stage vocabulary) → agent-prompts/ module
and Cursor prompt library
Joint definition as required Build Plan section → Build Plan schema in
BUILD_OS_SCOPING.md
30-line function governor → ai-safety/ module as a hard Cursor rule
Cursor session boundary discipline → PROJECT_MANAGEMENT_DISCIPLINE.md
Project routing and boundary instruction patches → Developer OS, Build OS,
and Nikari Tech project instructions (fifth patch added end of session)

---

Decision: Four-project operating model locked
Date: 28 April 2026
Status: LOCKED
The Nikari Tech system operates across four projects with distinct roles:
ProjectToolRoleNikari TechClaudeStrategic parent — owns architecture, NTK governance, platform decisionsBuild OSClaudeBuild governance — consumes architecture, governs assembly sessionsDeveloper OSClaudeExecution discipline — repo workflow, Cursor rules, developer standardsNikari Tech ReviewChatGPTExternal review — critiques committed outputs, does not originate governance
Locked one-line summary:
GitHub holds the truth. Nikari Tech owns the architecture. Build OS consumes
that architecture to govern build sessions. Developer OS governs execution
discipline. ChatGPT reviews committed outputs from the outside.

---

Decision: ChatGPT is reviewer only — information flow rule locked
Date: 28 April 2026
Status: LOCKED
The ChatGPT Nikari Tech Review project is a continuous external review and
strategic thinking layer. It does not originate governance. It does not
produce documents that become decided without going back through Claude first.
Information flow rule:
Claude produces → GitHub commits → project knowledge updated →
ChatGPT reviews committed documents → gaps identified →
Claude assesses and incorporates → GitHub commits → repeat.
ChatGPT outputs that influence governance must be assessed in Claude,
confirmed by the founder, and committed to GitHub before they are treated
as decided. A ChatGPT output uploaded to project knowledge is not governance.
A committed GitHub document is.

---

Decision: Platform architecture sessions open in Nikari Tech — not Build OS
Date: 28 April 2026
Status: LOCKED
Sessions whose primary question is "how does the platform work", "what are we
building", or "what is the NTK governance structure" open in Nikari Tech.
Sessions whose primary question is "what gets built in this Cursor session
and under what rules" open in Build OS.
Sessions whose primary question is "how do I execute this task correctly"
open in Developer OS.
This session (28 April 2026) opened in Build OS but was primarily a Nikari
Tech session. This is documented as the reference case. Future sessions of
this type open in Nikari Tech from the start.

Decision: Project routing addendum produced — temporary until NTK-01
Date: 28 April 2026
Status: LOCKED
NTK-00_ADDENDUM_Project_Routing_and_Boundaries_28042026.md was produced
as a lean standalone reference for project routing and boundary rules.
It is temporary — it is absorbed into NTK-01_Nikari_Tech_Operating_Model.md
when that document is produced. At that point the addendum is archived,
not deleted.

---

Decision: NTK document set — seven documents produced 28 April 2026
Date: 28 April 2026
Status: LOCKED
Seven documents produced and committed this session:

UNIVERSAL_DECISIONS_APPEND_28042026.md — this file
NTK-00_Nikari_Tech_Master_Intent.md — stub, pending strategic session
NTK-04_Nikari_Platform_Monorepo_Architecture.md — complete
NTK-05_Component_and_Contracts_Architecture.md — complete
NTK_OUTLINE_SET_28042026.md — governed skeleton set, NTK-00 through NTK-10
NTK-00_ADDENDUM_Project_Routing_and_Boundaries_28042026.md — temporary reference
BUILD_OS_SESSION_HANDOVER_28042026_FINAL.md — session handover

NTK-04 and NTK-05 are complete governing documents.
NTK-00 is a stub — requires dedicated strategic session to reach v1.0.
NTK-01 through NTK-03 and NTK-06 through NTK-10 are pending — outlines
in NTK_OUTLINE_SET, production triggers in NTK-00.

End of append block — 28 April 2026 — FINAL VERSION
Replaces earlier version produced same session
Odoo entry: CONFIRMED against existing 2026-04-25 entry — not appended

---

UNIVERSAL_DECISIONS.md — Append Block
Date: 2 May 2026
Session: Nikari Tech — Project Instructions Naming and Source/Output Discipline
Append to: wietsmarais/UNIVERSAL_DECISIONS.md
---
Decision: Canonical Nikari project names remain stable; descriptive subtitles clarify role
Date: 2 May 2026
Status: LOCKED
Canonical project names remain unchanged for continuity:
Nikari Developer OS
Build OS
Nikari Tech
Nikari Tech Review
These names must continue to be used in source references, filenames where they identify a project, Cursor prompts, Claude project instructions, GitHub issue references, handovers, opening prompts, source file paths, project knowledge uploads, and future “read this file first” instructions unless a formal rename migration is later approved.
Descriptive subtitles may be added in README files, project instructions, handovers, and opening prompts to clarify each project’s role:
Canonical project name	Descriptive subtitle
Nikari Developer OS	Development Discipline & Repo Workflow
Build OS	Build Governance & Assembly Planning
Nikari Tech	Architecture & Platform Governance
Nikari Tech Review	Review, Brainstorm & Architecture Check
Tool-specific instruction files may use tool suffixes, such as `_CLAUDE` and `_CHATGPT`, where needed to distinguish live tool behaviour. This does not rename the canonical project. It only clarifies which tool the instruction file governs.
Rationale: The four project names already appear across Cursor prompts, project instructions, GitHub issues, handovers, source paths, opening prompts, and project knowledge uploads. Renaming the projects too aggressively would create reference drift. Subtitles preserve continuity while improving boundary clarity.
Affected files / references:
Nikari Developer OS project instructions
Build OS project instructions
Nikari Tech project instructions
Nikari Tech Review project instructions
`wietsmarais/docs/project-instructions/Nikari-Tech-Project-Instructions/`
Future handovers and opening prompts that refer to these projects

---

---
## Decision: Cursor Agent mode is the preferred execution path, not the governance authoring authority
Date: 6 May 2026
Status: LOCKED
Source / authority: Founder confirmation — Nikari Platform / NRE public rebuild process review

For governed Nikari repo workflows, Cursor Agent mode is the preferred execution path for routine scoped work, validation, file operations, and commit/push workflows.

Cursor Agent mode may:
- execute founder-approved scoped implementation tasks;
- inspect approved files;
- apply approved code or copy changes;
- run validation commands;
- report changed files, validation results, commit hashes, and repo state;
- create or save files where the content has already been founder-approved;
- stage, commit, and push after explicit founder approval.

Cursor Agent mode must not be treated as the default author of governance, canonical documents, formal handovers, scope charters, process decisions, or governance-adjacent summaries.

Formal handover and governance content should be drafted or reviewed in ChatGPT or Claude, using Cursor’s factual execution report as source material.

Reason:
Cursor Agent mode is excellent for execution discipline and repo operations, but formal handovers and governance-adjacent records require higher-level synthesis, sequencing judgment, and process continuity. Keeping handover authorship in ChatGPT or Claude preserves the Nikari tool-role separation.

Boundary:
Cursor may save, format, validate, stage, commit, and push an approved handover, scope, or governance file, but it should not originate or materially rewrite that content by default unless the founder explicitly authorises a narrow factual draft.

---
## Decision: Fast handover-confirmation workflow after clean committed handovers
Date: 6 May 2026
Status: LOCKED
Source / authority: Founder confirmation — Nikari Platform / NRE public rebuild process review

When a phase or slice handover has already been committed and pushed, and the repo is clean and aligned, the next scoping session should use a fast handover-confirmation workflow rather than a full forensic re-review.

Minimum confirmation:

    git status -sb
    git log --oneline -5
    git ls-files [expected handover file]

Stop only if:
- the repo is not clean;
- the branch is not aligned with origin;
- the expected handover file is not tracked;
- the latest commits contradict the stated baseline.

If the checks pass, proceed directly to the next real scoping decision.

Reason:
Full forensic prompts are useful when repo state is uncertain, when risky capability is being opened, or when files may be modified. Once a handover is committed, pushed, tracked, and the repo is clean, repeating the full phase history adds administrative overhead without proportional safety benefit.

Boundary:
This fast workflow does not apply to:
- implementation sessions involving source changes;
- backend, Supabase, forms, CRM, admin, analytics, security, or data-write work;
- uncertain repo state;
- missing or uncommitted handovers;
- cross-repo or legacy/source-mine access;
- situations where the founder requests a full review.

---
## Decision: Approved handover and scope content should be authored outside Cursor and saved by Cursor
Date: 6 May 2026
Status: LOCKED
Source / authority: Founder confirmation — Nikari Platform / NRE public rebuild process review

Formal handover, closeout, scope-charter, and governance-adjacent content should be drafted or reviewed in ChatGPT or Claude, then founder-approved before Cursor saves it into the repo.

Cursor Agent may create, overwrite, validate, stage, commit, and push the approved markdown file, but should not originate or materially rewrite formal handover, scope, or governance content by default.

Standard flow:
1. Cursor completes scoped work and reports factual execution details.
2. ChatGPT or Claude drafts or reviews the handover, scope, or governance-adjacent content.
3. Founder confirms the content.
4. Cursor saves the approved markdown file exactly as provided.
5. Cursor validates formatting and file content.
6. Cursor stages, commits, and pushes after explicit founder approval.

Reason:
This preserves the separation between execution and governance. Cursor executes; ChatGPT or Claude synthesises and reviews; the founder approves; GitHub holds the truth.

Boundary:
Cursor may produce factual reports, validation summaries, changed-file lists, commit hashes, and repo-state summaries. Those factual reports may become source material for handovers, but they are not themselves formal governance unless reviewed, approved, and committed through the proper process.

---
## Decision: New untracked markdown files require content verification before commit
Date: 6 May 2026
Status: LOCKED
Source / authority: Founder confirmation — Nikari Platform / NRE public rebuild process review

When a new markdown handover, scope, governance, or documentation file is created and is still untracked, the review process must not rely on `git diff -- [file]` alone, because Git does not show a normal content diff for untracked files unless they are staged or marked with intent-to-add.

For new untracked markdown files, the required lightweight verification is:
1. Create or save the approved file.
2. Run `git status -sb`.
3. Run `git add -N [file]` to mark intent to add without staging content for commit.
4. Run `git diff -- [file]` so the founder can review the new file content.
5. Run `git diff --check`.
6. If markdown fences are present or formatting is important, display the first 60–100 numbered lines with code fences made visible.
7. Founder confirms.
8. Stage, commit, and push.

Recommended PowerShell check for visible fences:

    $i = 1
    Get-Content -Path "[file path]" -TotalCount 100 |
      ForEach-Object {
        "{0,3}: {1}" -f $i, ($_.Replace('```', '<FENCE>'))
        $i++
      }

Reason:
During the Phase 7 closeout handover, the file was new and untracked, so `git diff -- [file]` showed no content. This created unnecessary confusion around markdown fence rendering. The issue was not caused by the faster workflow; it came from applying a tracked-file diff process to an untracked new file.

Boundary:
This rule applies specifically to new untracked markdown handover, scope, governance, and documentation files before first commit.

---


