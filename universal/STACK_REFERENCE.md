# Stack Reference
# Source: PROJECT_STARTER_PACK_v4.1a — universal stack and tools section
# Extracted to: claude-knowledge/universal/STACK_REFERENCE.md
# Last updated: 27 April 2026
# Update trigger: stack, tools, or accounts change materially

---

## Universal Stack

Every project in the wietsmarais portfolio uses this stack unless a
project-level DECISIONS.md entry explicitly overrides a component.

| Layer | Tool | Version / Notes |
|-------|------|----------------|
| Framework | Next.js App Router | 14 — strict TypeScript |
| Language | TypeScript | Strict mode — no any |
| Styling | Tailwind CSS | v3 — utility-first |
| Components | shadcn/ui | Check ui.shadcn.com before building any UI component |
| Database | Supabase | v2 npm package — org-level Pro plan |
| Auth | Supabase Auth | Session tokens only — never manual |
| Storage | Supabase Storage | For all file uploads |
| Deployment | Vercel Pro | GitHub auto-deploy — every repo |
| Version control | GitHub | wietsmarais org |
| Payments | Stripe | Stripe.js CDN (plain HTML) or npm package (Next.js) |
| Operations | Odoo | Backend workflows — not replicated in frontend |
| Accounting | Xero | All invoicing and financial reporting |
| Email | Loops.so | Marketing and transactional |
| AI monitoring | Helicone | Required in production — all AI call monitoring |

---

## Three-Layer Model

Every project places features in the correct layer before designing a solution.

| Layer | Tool | Responsibility |
|-------|------|----------------|
| Frontend | Vercel + Supabase | UI, listings, enquiries, portals, auth |
| Operations | Odoo | CRM, contracts, pipelines, vendor management |
| Accounting | Xero | Invoicing, billing, financial reporting |

Features that belong in Odoo are never replicated in the frontend stack.
Features that belong in Xero are never built into Supabase.

---

## Tools and Accounts

| Tool | Purpose | Status |
|------|---------|--------|
| Cursor Pro | Primary IDE — Claude agent | Active |
| GitHub | Version control — all repos | Active |
| GitHub CLI (gh) | Admin tasks — label cloning, repo management | Active |
| GitHub Desktop | Commits and pushes — most repos | Active |
| Vercel Pro | Deployment — all projects | Active |
| Supabase | Backend — all projects | Active — org-level Pro |
| Stripe | Payments | Active |
| VentraIP | Domain registration | Active |
| Odoo | Operations | Active |
| Xero | Accounting | Active |
| Loops.so | Email marketing | Active |
| Helicone | AI call monitoring | Active — production requirement |

---

### Cursor declared-mode workflow

Cursor is no longer treated as a generic code executor. For governed Nikari work, Cursor operates in declared modes under the Nikari Cursor Operating Roles standard.

Primary LLM-facing reference:

https://raw.githubusercontent.com/wietsmarais/claude-knowledge/main/universal/CURSOR_MODE_REFERENCE_FOR_LLM_PROJECTS.md

Primary Cursor operating-role standard:

https://raw.githubusercontent.com/wietsmarais/wietsmarais/main/docs/process/NIKARI_CURSOR_OPERATING_ROLES.md

Reusable Cursor operating-mode starters:

https://raw.githubusercontent.com/wietsmarais/cursor-prompts/main/prompts/governance/J-cursor-operating-modes.md

Rule:
Claude/ChatGPT must apply the Cursor operating-mode process when drafting, reviewing, scoping, or improving work that will later go to Cursor.

---

## Workflow Modes

### Primary workflow
For governed platforms, client builds, and any project running more than one session.

- Cursor Pro (Claude agent) inside a GitHub repo
- Vercel Pro — auto-deploy from GitHub
- Next.js App Router — full-stack
- Tailwind CSS — all styling
- shadcn/ui — all UI components (check first before building from scratch)
- Supabase — npm package inside repo
- GitHub Desktop — commits
- No manual terminal inside repos — Cursor agent handles all build commands

### Secondary workflow
For quick prototypes, personal tools, and proof-of-concept builds only.

- Plain HTML + CSS + JavaScript — single self-contained files
- Supabase CDN client (cdn.jsdelivr.net/npm/@supabase/supabase-js@2)
- Vercel drag and drop or GitHub auto-deploy
- No build tools, no terminal, no npm

---

## GitHub Organisation

**Org:** wietsmarais  
**Repos:**

| Repo | Purpose | Visibility |
|------|---------|------------|
| wietsmarais/wietsmarais | Root governance | Private |
| wietsmarais/claude-knowledge | Live Claude reference layer | Public |
| wietsmarais/component-library | Reusable modules | Private |
| wietsmarais/cursor-prompts | Cursor prompt library | Private |
| wietsmarais/nre-01-core-platform | Nikari Real Estate | Private |
| wietsmarais/vix-trading-journal | VIX Trading Journal | Private |

---

## Supabase

- Org-level Pro plan — shared across projects
- Each project gets its own Supabase project instance
- RLS enabled on every table from creation — non-negotiable
- setup.sql is canonical — Cursor reads it before writing any query
- Spend cap is the primary cost protection — monthly usage check cadence
- Service role key never in frontend code

### Active projects

| Project | Ref | Region | Default branch |
|---------|-----|--------|---------------|
| Nikari Real Estate | semkjkssmzpqxdpcqbug | Seoul | main |

---

## Security Non-Negotiables

These apply to every project from session one. No exceptions.

- RLS on every Supabase table from creation
- No anon key for user-scoped writes
- Service role key never in frontend
- No API keys in committed files — environment variables via Vercel
- Input sanitisation on all form fields before DB write
- No user-supplied data rendered as raw HTML
- All admin routes protected before any content renders
- Password gates on every non-public surface
- White-label and subscription-first architecture from day one

---

## Branch Convention

| Branch | Purpose |
|--------|---------|
| main | Production — protected |
| dev/[short-description] | Active development |
| feature/issue-[n]-[short-description] | Feature branches tied to GitHub issues |

**Exception:** vix-trading-journal uses `master` as permanent default.  
This is a locked exception documented in UNIVERSAL_DECISIONS.md.  
Never rename to `main`. Never create a `main` branch in that repo.

---

## Terminal Use Rule

Terminal commands are permitted for one-off system and GitHub admin tasks
run in a plain Command Prompt window outside any repo or Cursor session.

The "no terminal" rule applies only to build commands inside a project repo.
Cursor handles those — not the founder directly.

---

*Last updated: 6 May 2026
*Update reason: Cursor declared-mode workflow and LLM prompt-generation reference added.  
*Source: PROJECT_STARTER_PACK_v4.1a*  
*Update when: stack, tools, accounts, or security standards change*
