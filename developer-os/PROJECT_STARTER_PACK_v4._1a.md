# Component Library — wietsmarais

Private module library for all platform builds.
Check here before building anything from scratch.

---

## How to use this library

### In a Claude session
Attach the relevant SPEC.md file(s) from this repo to your chat.
Tell Claude: "Use the spec in [folder]/SPEC.md as the basis for this module."

### In a Cursor session
Open this repo alongside your project repo in Cursor.
Reference the SPEC.md in your prompt:
"Build this following the pattern in component-library/[folder]/SPEC.md"

---

## Module index — UI and backend patterns

| Module | Folder | Status | First used in |
|--------|--------|--------|---------------|
| Supabase Auth / Password Gate | auth/ | ✅ Proven | Nikari |
| Stripe Subscription Gate | subscriptions/ | 🔲 To be extracted | — |
| White-label Tenant Config | white-label/ | ✅ Proven | Nikari |
| Row Level Security Patterns | security/ | ✅ Proven | Nikari |
| Supabase Schema Starter | database/ | ✅ Proven | Nikari |
| Property / Product Card | ui-components/ | ✅ Proven | Nikari |
| Admin Dashboard Shell | admin/ | ✅ Proven | Nikari |

## Module index — AI-native build governance

| Module | Folder | Status | Applies to |
|--------|--------|--------|------------|
| AI Safety & Guardrails | ai-safety/ | ✅ Canonical | All projects |
| Agent Mode Prompts | agent-prompts/ | ✅ Canonical | All projects |
| Project Management | project-management/ | ✅ Canonical | All projects |
| AI Cost & Token Constraints | ai-cost-constraints/ | ✅ Canonical | All projects |

---

## Governance documents index

These documents live in `docs/architecture/` in the NRE-01 repo and apply universally.

| Document | Where it lives | What it governs |
|----------|---------------|-----------------|
| `AI_BUILD_GUARDRAILS.md` | NRE-01 `docs/architecture/` | Safety, token cost, build execution guardrails |
| `CURSOR_AGENT_PROMPT_LIBRARY.md` | cursor-prompts repo `prompts/` | 40+ prompts across 8 phases — for Cursor and Claude |
| `PROJECT_MANAGEMENT_DISCIPLINE.md` | NRE-01 `docs/architecture/` | Living files, session discipline, GitHub Issues, roadmap |
| `TEMPLATE_PROTOCOL.md` | NRE-01 `docs/architecture/` | Template evaluation, adaptation, component extraction |
| `PROJECT_STANDARDS.md` | NRE-01 `docs/architecture/` | GitHub, Vercel, Supabase, domain, credential standards |
| `CLIENT_BUILD_PROTOCOL.md` | NRE-01 `docs/architecture/` | Owned vs client builds, IP, disclosure, handover |

---

## Status key

| Symbol | Meaning |
|--------|---------|
| ✅ Proven | Extracted from a live project, tested, ready to reuse |
| ✅ Canonical | Applies to all projects — not project-specific |
| 🔧 Draft | Written but not yet tested in a real project |
| 🔲 To be extracted | Exists in a project, not yet written up as a module |
| ❌ Deprecated | Do not use — superseded by newer module |

---

## When to use each module

| Module | Use when |
|--------|----------|
| security/ | Every project — session one, non-negotiable |
| database/ | Schema design stage |
| white-label/ | Architecture stage — every project |
| auth/ | Adding login or route protection |
| subscriptions/ | Adding billing — design in from day one |
| ui-components/ | Building cards, forms, or lists |
| admin/ | Building any admin surface |
| ai-safety/ | Every project — before any AI feature is built |
| agent-prompts/ | Every Cursor session — adapt to docs/PROMPTS.md in each project |
| project-management/ | Every project — SCOPING.md and PLAN.md before first session |
| ai-cost-constraints/ | Every project — add .cursorrules block before first agent session |

---

## The check hierarchy — always in this order

1. **DECISIONS.md** — is there a past decision that constrains this?
2. **shadcn/ui** (ui.shadcn.com) — does it exist here? Use it.
3. **Component library** — does a proven module exist? Use it.
4. **Governance documents** — are there relevant guardrails? Follow them.
5. **Build from scratch** — only if none of the above apply.

Never build from scratch without checking steps 1–4 first.

---

## Non-negotiable rules for all builds

### Stack and process
- Stack confirmed by founder before any code is written — every session, every project
- No code until explicit founder approval of the approach
- Never switch stacks mid-project without founder approval
- Component library and shadcn/ui checked before building anything

### Architecture
- RLS enabled on every Supabase table from creation — never disabled
- No API keys or secrets in any frontend file or any committed file
- Subscription tier field on every user/profiles table from day one
- White-label tenant config loaded at runtime — nothing brand-related hardcoded
- Security checklist completed before any project goes live
- Odoo handles complex backend workflows — not the frontend
- Xero handles all accounting integration

### AI-native build rules
- Agent reads SCOPING.md, PLAN.md, and DECISIONS.md before starting work
- PLAN.md updated before and after every multi-file task
- DECISIONS.md is append-only — every architectural decision recorded
- Session handover produced at the end of every session — no exceptions
- No agent reads all files in a directory — tree or ls first
- No file exceeds 300 lines — refactor before adding to it
- No empty catch blocks — every catch logs error with context
- No `any` types in TypeScript — ever
- Diffs only for small changes — no full file rewrites

### AI safety
- No PII in any prompt sent to an external AI API
- No secrets in any agent prompt or session
- Rate limits set for all AI-powered features
- Tenant data isolated in white-label AI builds
- Human review required for auth, payments, RLS, and data migrations
- Auto-publish ban — nothing goes live without human approval

### Client builds
- Client informed of AI-assisted build before engagement starts
- Client's own Vercel and Supabase accounts — never share with owned products
- Nikari IP, rules, and internal tools never included in client deliverables
- Handover document produced for every client delivery

---

## Adding a new module

1. Create a folder with a short lowercase name
2. Add a SPEC.md using the template in any existing folder
3. Update both module index tables above
4. Commit: `add: [module-name] spec`
5. Re-upload updated README.md to Developer OS project knowledge

---

## Maintaining the library

| Trigger | Action |
|---------|--------|
| New module proven in a project | Create folder + SPEC.md, update README, push, re-upload |
| Existing SPEC updated | Edit in repo, commit, re-upload to project knowledge |
| Governance document updated | Update in NRE-01 repo, push, re-upload to Claude project knowledge |
| New project starts | Add to active projects in developer profile |
| Project goes live or status changes | Update developer profile, re-upload |
| .cursorrules block updated | Update ai-cost-constraints/SPEC.md starter block |

GitHub is always the source of truth.
Project knowledge always reflects GitHub.
Never the other way around.

---

*Last updated: April 2026*