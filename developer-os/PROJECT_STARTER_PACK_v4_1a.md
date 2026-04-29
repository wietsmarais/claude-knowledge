# PROJECT STARTER PACK
## Upload this file to every Claude project — new and existing
## Read before every session. No exceptions.
## Version: April 2026 — v4.1a

---

## What this document is — read first

This file is the **session-start and build-start governance layer**.
It is not a complete engineering governance manual.

Its job is to control what the agent does at the start of every session
and before writing any code. Deeper policy lives in linked companion specs.
If a rule in this file conflicts with a more specific project spec or
companion document, the more specific document governs.

**Governance tiers used in this document:**

| Tier | Meaning |
|------|---------|
| **Mandatory** | Always obey — no exceptions, no overrides of any kind |
| **Default** | Obey unless a project-specific DECISIONS.md entry explicitly overrides |
| **Exception** | Permitted only with a logged approval entry in DECISIONS.md |

Every rule in this document is marked with its tier where it is not obvious.

**Known governance gaps — logged, not forgotten:**
The following areas are real governance needs not covered in this file.
Each will become a separate companion spec:
- Testing and quality gates
- Release and rollback governance
- Migration and data-change governance
- Accessibility and performance standards
- AI prompt versioning, eval, and fallback governance
- Dependency and vendor governance
- Data retention, deletion, and audit governance

---

## Stack — primary workflow (confirmed for all governed builds)

- Next.js 14+ (App Router)
- TypeScript (strict mode — `strict: true` in tsconfig.json — **Mandatory**)
- Tailwind CSS (utility-first)
- shadcn/ui — always check ui.shadcn.com before building
  any component from scratch
- Supabase (`@supabase/supabase-js` npm package) — the locked typed
  database client and data-access layer for all projects
- Vercel AI SDK (`ai` + `@ai-sdk/anthropic`) — standard for all Next.js projects
- Lucide React (icons)
- Vercel Pro — auto-deploy from GitHub
- GitHub + GitHub Desktop

**Data-access decision (locked):** Supabase client is the typed data-access
layer for all projects. Prisma is not adopted.
See DECISIONS.md entry dated 2026-04-13 for full rationale.

**Tenancy model (locked):** Each customer gets their own Vercel deployment
connected to the same codebase. Zero code changes between customers.
All branding differences are handled by a runtime tenant config object.
Each customer deployment uses its own environment variables.
Supabase projects are shared unless a project DECISIONS.md entry explicitly
specifies per-tenant database isolation.

---

## Cursor rules — apply to every session

### Component architecture
- Use `'use client'` only when hooks or browser APIs required — **Default**
- Prefer Server Components for all data fetching via Supabase — **Default**
- `components/ui/` — shadcn components only
- `components/features/` — business logic components
- **No single file exceeds 300 lines** — refactor before continuing — **Default**
  *(Exception: generated files, migration files, schema files, and type definition
  files are exempt from this limit)*
- Descriptive variable names: `isUserLoading` not `loading`
- No `any` types. Ever. — **Mandatory**

### Supabase and data — CRITICAL
- Always use createClient helper for Server/Client/Middleware
- Reference `database.types.ts` for all queries — type safety required — **Mandatory**
- RLS enabled on every table — never bypass it — **Mandatory**
- Generate types after any schema change: `npx supabase gen types typescript`
- RLS policy templates and patterns: see `security/SPEC.md` — **Mandatory**

#### ⚠️ Schema discipline — mandatory before writing any query (added v4)

**Before writing any application code that queries Supabase — Mandatory:**

1. Read the schema file (`setup.sql` or equivalent) in full
2. Every column name in every query must come directly from the schema file
3. Never invent or assume column names
4. After writing queries, verify each column name against the schema before committing
5. If no schema file exists yet — create it first before writing any application code

**Why this rule exists:**
VIX Trading Journal Session 4 — Cursor built application code without reading
setup.sql. It invented plausible-sounding column names that did not exist in the
real schema. Every Supabase query failed with `42703 column does not exist` errors
across positions, trades, and app_config. Three files required full rework.
One session lost. Schema file must always be read before application code is written.

### AI features
- Default to raw Anthropic API for single AI calls — summarise, classify, generate
- Vercel AI SDK handles all streaming AI responses into React components
  (`useChat`, `useCompletion` — never build custom streaming infrastructure)
- LangChain is not in the standard stack — **Exception** — adopted per project only
  when multi-step retrieval or RAG pipelines are required (log in DECISIONS.md)
- pgvector via Supabase is the vector store when semantic search is needed —
  no external vector DB (Pinecone, Weaviate) unless scale demands it — **Default**
- Helicone monitors all AI calls in production — **Mandatory**
- No PII in any prompt sent to an external AI API — **Mandatory**
- All AI-generated content requires human approval before going live — **Mandatory**

### Styling
- Tailwind standard scale throughout — **Mandatory**
- No custom CSS files — `@apply` in globals.css only — **Default**
- Mobile-first responsive design by default — **Default**
- Dark theme default: background `#0d1117` — **Default**

### Code quality
- No `any` types. Ever. — **Mandatory**
- Every Supabase call wrapped in try/catch — **Mandatory**
- Failed fetches show inline error — never crash — **Mandatory**
- shadcn Toast for all save confirmations and errors — **Default**

### Agent error escalation — what happens after 3 failed attempts

If the agent attempts the same action 3 times and fails each time,
it must stop immediately and report in this exact format:

```
⚠️ LOOP DETECTED — halting

Task: [one sentence — what was being attempted]
Attempts: [n]
Error received each time: [exact error message]
Files affected: [list]
Suspected cause: [agent's best diagnosis]

Options:
A. [Specific alternative approach]
B. [Second alternative if one exists]
C. Escalate to founder — provide more context

Awaiting instruction. No further attempts until directed.
```

The agent does not proceed, does not try a variation without approval,
and does not silently move on to another task.
See also: A13 in AI_BUILD_GUARDRAILS.md

---

## Environment variables — Mandatory

**API keys are NEVER hardcoded in any committed file.**

| Context | Where keys live |
|---------|----------------|
| Local development | `.env.local` — never committed |
| Vercel deployment | Vercel Dashboard → Project → Settings → Env Variables |
| Cursor prompts | Placeholder text only — `your-anon-key-here` |
| Code files | `process.env.VARIABLE_NAME` only — never the actual key |

**Required env vars for every Next.js project:**

| Variable | Required when |
|----------|---------------|
| `NEXT_PUBLIC_SUPABASE_URL` | Always |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Always |
| `SUPABASE_SERVICE_ROLE_KEY` | Server-side only — never NEXT_PUBLIC_ |
| `ANTHROPIC_API_KEY` | Any project with AI features |
| `HELICONE_API_KEY` | All production deployments — Mandatory |

`.env.local` must always be in `.gitignore` — confirm before every first push.

---

## Security — Mandatory from session one

- RLS enabled on every Supabase table at creation
- Policies written for every table before data is inserted
- Policy patterns and templates: see `security/SPEC.md`
- Service role key never in any frontend file
- Input sanitisation and validation on all form fields before DB writes
- No user data rendered as raw HTML — no unaudited `dangerouslySetInnerHTML`
- Admin routes protected before any content renders
- Pre-launch security checklist completed before go-live

See: `security/SPEC.md` and `ai-safety/SPEC.md` for full checklists

---

## AI-native build discipline — Mandatory every session

### Before writing any code

1. Agent reads SCOPING.md, PLAN.md, and DECISIONS.md
2. Agent states what it understands the current task to be
3. Founder confirms the task and approves the plan
4. Agent executes atomically and reports after each task

### ⚠️ Pre-flight prompt check — Mandatory for complex builds (added v4)

Before starting any Cursor session involving database queries,
multi-file changes, or new architectural patterns — paste the intended
Cursor prompt into Claude first and ask:

> "What gaps or assumptions does this prompt leave open that could cause problems?"

**Why this rule exists:**
VIX Trading Journal — a pre-flight check on the Session 1 Cursor prompt
would have caught the schema mismatch before any code was written.
It was identified only after deployment failure in Session 4.
This check costs 2 minutes. The rework cost 1 full session.

### Required documents in every project repo

| Document | Purpose | Who updates it |
|----------|---------|----------------|
| SCOPING.md | Outcomes, constraints, definition of done | Founder + agent |
| PLAN.md | Step-by-step plan, current and next tasks | Agent — before every multi-file task |
| ROADMAP.md | Phased milestones and timeline | Founder + agent |
| DECISIONS.md | Append-only architectural decision log | Agent — every decision |
| LEARNINGS.md | Sprint retrospective notes | Agent — end of sprint |
| PROMPTS.md | Project-adapted prompt library | Agent — from agent-prompts/SPEC.md |

**DECISIONS.md entry format — use this every time:**
```markdown
## [YYYY-MM-DD] — [Decision title]
**Decision:** [What was decided — one clear statement]
**Reason:** [Why this was chosen]
**Alternatives considered:** [What else was evaluated and why rejected]
**Constraints this creates:** [What this decision locks in or rules out]
**Approved by:** Founder
```

**Session handover format:** see F04 in CURSOR_AGENT_PROMPT_LIBRARY.md.
Every session produces a handover. No exceptions. — **Mandatory**

**Branch naming convention:** see PROJECT_MANAGEMENT_DISCIPLINE.md Section C.
`feature/issue-[n]-[short-description]` — **Default**

See: `project-management/SPEC.md` for full document templates and rules

### Token and cost discipline

- Agent uses `tree` or `ls` before reading any files — **Mandatory**
- Diffs only — no full file rewrites for small changes — **Default**
- No `any` types, no empty catch blocks, no deprecated patterns — **Mandatory**
- Agent halts and reports in escalation format after 3 failed attempts — **Mandatory**
- Session chat cleared when task is complete — start fresh — **Default**

See: `ai-cost-constraints/SPEC.md` for full rules and .cursorrules block

### Agent mode prompts

Canonical prompts live in `agent-prompts/SPEC.md`.
Adapt for each project and save to `docs/PROMPTS.md` in the project repo.

Key prompts to always have at hand:
- A01 Universal Session Opener — every session
- B02 Blueprint — before any multi-file task
- D03 Secret Audit — after any session
- G02 Code Reviewer — before merging auth/payments/RLS
- G03 Context Refresh — start of every session after a gap

---

## Architecture boundaries — Mandatory

| Layer | Tool | What goes here |
|-------|------|----------------|
| Frontend | Vercel + Supabase | UI, listings, portals, enquiries |
| Operations | Odoo | CRM, contracts, pipelines, vendors |
| Accounting | Xero | Invoicing, billing, financial reporting |

- Never build complex backend processing into the frontend
- Never design for any accounting system other than Xero
- Flag anything that sounds like it belongs in Odoo before designing it

---

## Subscription-first — every project (Default)

- Supabase profiles table always includes plan/tier field
- Feature access gated by plan from day one
- Stripe integration designed in at architecture stage
- Free → paid upgrade path always exists in UI

---

## White-label — built in from day one (Default)

- Tenant config object controls all branding at runtime
- No brand assets hardcoded in components
- New tenant onboarded by config change only — no new code
- Logo, colours, name, domain all from tenant config
- Tenant config canonical shape: see `white-label/SPEC.md`

---

## Component library — check before building

**Repo:** github.com/wietsmarais/component-library (private)
**Local:** C:\GitHub\wietsmarais\component-library

If a module in the library is stale or incompatible, flag it to the founder
before building from scratch. Do not silently ignore the library.

| Module | Use when |
|--------|----------|
| security/SPEC.md | Every project — session one |
| database/SPEC.md | Schema design |
| white-label/SPEC.md | Architecture stage — tenant config shape lives here |
| auth/SPEC.md | Login, route protection, roles |
| subscriptions/SPEC.md | Adding billing |
| ui-components/SPEC.md | Cards, forms, lists |
| admin/SPEC.md | Any admin surface |
| ai-safety/SPEC.md | Every project — before any AI feature |
| agent-prompts/SPEC.md | Every Cursor session |
| project-management/SPEC.md | Every project — before first session |
| ai-cost-constraints/SPEC.md | Every project — .cursorrules setup |

---

## Build discipline — Mandatory every session

1. Confirm stack with founder before writing any code
2. Check component library before building anything new
3. Check shadcn/ui before building any UI component
4. Agent reads SCOPING.md and PLAN.md before starting
5. **Read schema file (setup.sql) before writing any Supabase queries**
6. **Run pre-flight prompt check in Claude before complex Cursor sessions**
7. Do not proceed to the next feature until the current change compiles, relevant tests pass, and required review is complete
8. **Preview deployment reviewed before any multi-file or infra-touching PR merges**
9. Never switch stacks mid-project without founder approval
10. Explain every technical decision in plain English first
11. Session handover file produced at the end of every session

---

## New project checklist — run before writing any code

### Foundation
- [ ] Stack confirmed by founder
- [ ] GitHub repo created (private)
- [ ] Default branch confirmed (`main` unless project DECISIONS.md overrides)
- [ ] .cursor/rules.md copied from cursor-prompts repo
- [ ] ai-cost-constraints/SPEC.md .cursorrules block added
- [ ] Supabase project created — region Sydney (`ap-southeast-2`) confirmed
- [ ] RLS confirmed enabled on Supabase project
- [ ] **setup.sql written and run before any application code is written**
- [ ] **database.types.ts generated from schema**
- [ ] `tsconfig.json` confirmed: `strict: true` and `noImplicitAny: true`
- [ ] .env.local created with placeholders confirmed in .gitignore
- [ ] Vercel project connected to GitHub repo
- [ ] Environment variables set in Vercel dashboard
- [ ] Vercel AI SDK installed (`npm install ai @ai-sdk/anthropic`)
- [ ] Helicone API key set in Vercel env vars before first production deploy

### Documentation
- [ ] SCOPING.md created and approved by founder
- [ ] PLAN.md created with Foundation Phase tasks
- [ ] ROADMAP.md created with Phase 1 milestones
- [ ] DECISIONS.md created (empty, correct format headers)
- [ ] PROMPTS.md created from agent-prompts/SPEC.md

### Library check
- [ ] Component library checked for relevant modules
- [ ] shadcn/ui checked for relevant components
- [ ] ai-safety/SPEC.md pre-launch checklist noted for later

### Security
- [ ] Security checklist from security/SPEC.md noted
- [ ] AI safety checklist from ai-safety/SPEC.md noted
- [ ] Pre-launch: both checklists completed before go-live

---

## WIP project checklist — run when joining an existing project

- [ ] Read the most recent session handover
- [ ] Read SCOPING.md, PLAN.md, and DECISIONS.md
- [ ] **Read setup.sql before writing or modifying any Supabase queries**
- [ ] Confirm current branch and repo state (`git branch --show-current`)
- [ ] Confirm Supabase project ref and region (must be Sydney `ap-southeast-2`)
- [ ] Confirm RLS is enabled on all tables
- [ ] Confirm .env.local exists and has correct keys
- [ ] Run G03 (Context Refresh prompt) before any work
- [ ] Check component library for anything relevant
- [ ] Do not perform broad discretionary restructures unless explicitly asked
  *(Small structural changes required to safely complete a task are permitted
  and must be documented in the session handover)*
- [ ] Produce session handover at the end

---

## Lessons learned — permanent guardrails

- Stack must be confirmed before any code — always
- Next.js is preferred for primary workflow — confirm first
- Plain HTML for single-session prototypes only
- Component library first — never rebuild what exists
- shadcn/ui first — never rebuild what exists there
- Security and white-label are day one — never phase two
- API keys in Cursor prompts are always placeholders
- Environment variables go in Vercel — not in code
- Branch discipline — confirm default branch before pushing
- .env.local confirmed in .gitignore before first push
- PLAN.md must exist before any multi-file agent task
- DECISIONS.md is append-only — never edit existing entries
- Session handover is non-negotiable — no exceptions
- Tokens are currency — never let the agent read what it does not need
- **Schema file must be read before any application code — column names are never invented**
- **Pre-flight prompt check in Claude before every complex Cursor session — 2 minutes saves a full session of rework**

---

*Version: April 2026 — v4.1a*
*Updated: 13 April 2026*

*v4 additions: schema discipline rule; pre-flight prompt check; both sourced from VIX Trading Journal Session 4 post-mortem*
*v4.1 additions: document role and governance tiers; tenancy model made explicit; Supabase described as typed data-access layer; agent escalation format defined; DECISIONS.md entry format added; session handover and branch convention referenced; tsconfig strict mode added to checklist; Supabase region verification added to WIP checklist; preview deploy check added to build discipline; restructure rule clarified; governance gaps logged*
*v4.1a locked decisions: file-length unified at 300 lines with exemptions; Mandatory tier = no overrides of any kind; branch naming confirmed as feature/issue-[n]-[short-description]; build discipline step 7 explicitly requires tests to pass*

*Reviewed by: Claude (fresh instance) + ChatGPT + third independent review — 13 April 2026*
*Update when stack, tools, rules, or modules change materially*
*This file lives in every Claude project knowledge base*
