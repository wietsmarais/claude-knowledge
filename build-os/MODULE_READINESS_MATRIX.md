# Build OS — Module Readiness Matrix
# Version: 1.0 — 27 April 2026
# Produced in: Developer OS — Session 5 (Module Readiness Matrix population)
# Status: COMPLETE — all seven Tier 1 modules gate-confirmed
# Location when committed: wietsmarais/docs/architecture/MODULE_READINESS_MATRIX_27042026.md
# Gate rule: A module may be used in a Build OS assembly session only if:
#   - Its matrix row exists
#   - reusable_as_is is YES or reuse_with_adaptation is YES
#   - test_status is VERIFIED or TESTED
#   - last_verified is within the past 90 days
# Next re-verification required before use from: 26 July 2026 onward

---

## Gate Summary

| Module | status | reusable_as_is | test_status | last_verified | Gate |
|--------|--------|---------------|-------------|---------------|------|
| security | ACTIVE | YES | VERIFIED | 27 Apr 2026 | ✅ PASS |
| database | ACTIVE | YES | VERIFIED | 27 Apr 2026 | ✅ PASS |
| white-label | ACTIVE | YES | VERIFIED | 27 Apr 2026 | ✅ PASS |
| auth | ACTIVE | YES | VERIFIED | 27 Apr 2026 | ✅ PASS |
| ui-components | ACTIVE | YES | VERIFIED | 27 Apr 2026 | ✅ PASS |
| project-management | ACTIVE | YES | VERIFIED | 27 Apr 2026 | ✅ PASS |
| ai-safety | ACTIVE | YES | VERIFIED | 27 Apr 2026 | ✅ PASS |

**Build OS first assembly session gate: CONFIRMED — all seven Tier 1 modules pass.**

---

## Structural Flag

Matrix rows were populated from: component library README, AI_BUILD_GUARDRAILS.md,
governance documents, and cross-project build history in Developer OS project knowledge.
All eleven SPEC.md files were reviewed against the matrix on 27 April 2026.

### Cleared items
- shadcn/ui check requirement — confirmed documented in `ui-components/SPEC.md` core principles. ✅ Cleared.

### Outstanding — SPEC.md edits required before first assembly session

These items must be added to the relevant SPEC.md files during Stage 2.
No assembly session opens until they are confirmed.

| Item | File | Required addition |
|------|------|------------------|
| `::uuid` type-cast fix | `security/SPEC.md` | Add note to RLS section: `app_metadata` path requires `::uuid` cast — confirmed fix from NRE-01 / S4 ChatGPT review |
| `setup.sql` canonical reference | `database/SPEC.md` | Add note: `setup.sql` is the canonical schema file — Cursor must read it before writing any query |
| Version number field | All seven Tier 1 SPEC.md files | Add `## Version` field set to `1.0` — currently absent from all SPECs |

### What does not change
Gate assessments are unchanged. All seven modules remain PASS.
The SPEC edits are documentation gaps, not functional failures.
The modules are verified from build evidence — the SPECs document that evidence.

---

## Full Matrix Rows

### security/

| Field | Value |
|-------|-------|
| module_name | security/ |
| version | 1.0 |
| status | ACTIVE |
| reusable_as_is | YES |
| reuse_with_adaptation | YES |
| dependencies | database |
| required_config | Supabase project ref, tenant_id on every table, app_metadata JWT path |
| test_status | VERIFIED |
| known_limits | RLS policy requires `::uuid` cast on app_metadata path — fixed in NRE-01, must carry forward. Anon key never for user-scoped writes. |
| compatible_stack | Both (Next.js 14 App Router / plain HTML) |
| tenant_aware | YES |
| toggle_ready | NO — RLS is always on, non-negotiable |
| last_verified | 27 April 2026 |
| owner | Wiets Marais / Developer OS |
| notes | Used every project, session one. Type-cast fix (::uuid) must be confirmed in SPEC.md. |

---

### database/

| Field | Value |
|-------|-------|
| module_name | database/ |
| version | 1.0 |
| status | ACTIVE |
| reusable_as_is | YES |
| reuse_with_adaptation | YES |
| dependencies | security |
| required_config | Supabase project ref, tenant_id column on every table, subscription tier field on profiles |
| test_status | VERIFIED |
| known_limits | Schema must be read before any query written. No table without tenant_id. No profiles table without subscription tier field from day one. |
| compatible_stack | Both |
| tenant_aware | YES |
| toggle_ready | NO — schema is structural |
| last_verified | 27 April 2026 |
| owner | Wiets Marais / Developer OS |
| notes | setup.sql is the canonical reference. Cursor reads it before writing any query — standing governance rule. |

---

### white-label/

| Field | Value |
|-------|-------|
| module_name | white-label/ |
| version | 1.0 |
| status | ACTIVE |
| reusable_as_is | YES |
| reuse_with_adaptation | YES |
| dependencies | database, security |
| required_config | Supabase project ref, tenant_id, runtime config keys: logo, colours, name, domain |
| test_status | VERIFIED |
| known_limits | No brand assets hardcoded. New tenant onboarded by config change only — no code change. Tailwind tokens driven by tenant config. |
| compatible_stack | Both |
| tenant_aware | YES |
| toggle_ready | YES |
| last_verified | 27 April 2026 |
| owner | Wiets Marais / Developer OS |
| notes | Required at architecture stage for every project. B2B white-label clients get own Supabase instance — separate commercial event. |

---

### auth/

| Field | Value |
|-------|-------|
| module_name | auth/ |
| version | 1.0 |
| status | ACTIVE |
| reusable_as_is | YES |
| reuse_with_adaptation | YES |
| dependencies | database, security, white-label |
| required_config | Supabase project ref, anon key (frontend only), redirect URLs in Supabase dashboard |
| test_status | VERIFIED |
| known_limits | Admin routes protected before content renders. Tokens via Supabase Auth only — never manual. Service role key never in frontend. |
| compatible_stack | Both |
| tenant_aware | YES |
| toggle_ready | YES |
| last_verified | 27 April 2026 |
| owner | Wiets Marais / Developer OS |
| notes | Tier 5 critical-path module. Any auth config change requires second-model review and separate founder approval. |

---

### ui-components/

| Field | Value |
|-------|-------|
| module_name | ui-components/ |
| version | 1.0 |
| status | ACTIVE |
| reusable_as_is | YES |
| reuse_with_adaptation | YES |
| dependencies | white-label, database, shadcn/ui |
| required_config | Tailwind CSS config, shadcn/ui initialised, tenant config for branding tokens |
| test_status | VERIFIED |
| known_limits | shadcn/ui checked before building any component — no exceptions. No hardcoded brand colours. Tailwind tokens only. Plain HTML adaptation requires manual rewrite. |
| compatible_stack | Next.js 14 App Router primary; plain HTML adaptation possible |
| tenant_aware | YES |
| toggle_ready | YES |
| last_verified | 27 April 2026 |
| owner | Wiets Marais / Developer OS |
| notes | Strongly Next.js-native. shadcn/ui check is mandatory for every component addition. |

---

### project-management/

| Field | Value |
|-------|-------|
| module_name | project-management/ |
| version | 1.0 |
| status | ACTIVE (Canonical — applies to all projects) |
| reusable_as_is | YES |
| reuse_with_adaptation | YES |
| dependencies | None |
| required_config | Project name, repo URL, branch naming convention, session counter, GitHub Issues config |
| test_status | VERIFIED |
| known_limits | DECISIONS.md append-only. PLAN.md updated before/after every multi-file task. Session handover is .md file in Claude Web — never pasted inline. No file exceeds 300 lines. |
| compatible_stack | Both — stack-agnostic markdown governance artifacts |
| tenant_aware | NO — per-project, not per-tenant |
| toggle_ready | NO — always required |
| last_verified | 27 April 2026 |
| owner | Wiets Marais / Developer OS |
| notes | Session handover as .md file (not inline) is locked standard. SCOPING.md template in PROJECT_MANAGEMENT_DISCIPLINE.md. |

---

### ai-safety/

| Field | Value |
|-------|-------|
| module_name | ai-safety/ |
| version | 1.0 |
| status | ACTIVE (Canonical — applies to all projects) |
| reusable_as_is | YES |
| reuse_with_adaptation | YES |
| dependencies | security, project-management |
| required_config | AI assistant delivery mode declared (Path A or Path B). Path B requires API cost estimate in SCOPING.md. HITL gate defined. |
| test_status | VERIFIED |
| known_limits | No PII in AI context. No secrets in agent prompts. Auto-publish banned. Custom GPTs excluded (stateless — defeats compounding model). HITL permanent. |
| compatible_stack | Both — architectural constraints, stack-agnostic |
| tenant_aware | YES |
| toggle_ready | YES |
| last_verified | 27 April 2026 |
| owner | Wiets Marais / Developer OS |
| notes | AI delivery mode declared at Stage 1 — never deferred. HITL is permanent. Compounding libraries required from day one. |

---

## Maintenance Rules

| Trigger | Action |
|---------|--------|
| Module used in assembly session | Update last_verified to session date |
| SPEC.md updated | Confirm version increment, update matrix version and last_verified |
| 90 days elapsed since last_verified | Re-verify before using in assembly session |
| New module added to component library | Add matrix row before module is eligible for Build OS selection |
| Module deprecated | Update status to DEPRECATED — module is no longer selectable |

---

## File Destination Label

```
File: MODULE_READINESS_MATRIX_27042026.md
Destination: C:\GitHub\wietsmarais\docs\architecture\ (committed 27 April 2026)
Commit message: governance: add Build OS Module Readiness Matrix v1.0
Action: Already committed
Project knowledge: Yes — upload to Developer OS and to Build OS Claude Project when Stage 2 created
```

---

*Version: 1.0 — 27 April 2026*
*Produced: Developer OS — Session 5*
*Approved by: Wiets Marais — 27 April 2026*
*Next re-verification required before use from: 26 July 2026 onward*
*Committed to: wietsmarais/docs/architecture/MODULE_READINESS_MATRIX_27042026.md*
