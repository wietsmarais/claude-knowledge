# Claude Code / Cursor / Product Project Workflow Protocol

**File:** `CLAUDE_CODE_CURSOR_PRODUCT_WORKFLOW_PROTOCOL_20260514.md`  
**Status:** Practical workflow artefact  
**Purpose:** Translate the chat decisions into an operational sequence for NRE Phase 10 and future Nikari builds.

---

## 1. Core workflow rule

```txt
Product projects own product truth.
Nikari Tech owns architecture and module implications.
Build OS owns Build Plans.
Developer OS owns execution discipline.
Claude Code validates and audits repo state, and may execute governed extraction only under a founder-approved Build OS plan.
Cursor executes ordinary implementation inside approved scope.
ChatGPT reviews from outside.
```

---

## 2. Standard phase workflow

### Step 1 — Product project scoping

Open the relevant product project when the question is about product-specific phase scope, user experience, content, data fields, suppression rules, implementation evidence, or product handover.

For NRE Phase 10, the active project is the NRE product project.

### Step 2 — Claude Code read-only repo audit

Before implementation, run Claude Code in **Repo-Aware Audit** mode where the active repo state matters.

Example:

```txt
Claude Code mode: Repo-Aware Audit
Active repo: C:\GitHub\nikari-platform
Scope: apps/nre-public only
No edits, no staging, no commits, no pushes.
Produce a structured audit note covering current module boundaries, data-layer assumptions, public/private boundary risks, and Phase 10 readiness.
```

### Step 3 — Nikari Tech module identification

If reusable patterns appear, take the Claude Code audit output to Nikari Tech.

Nikari Tech identifies and classifies extraction candidates using NTK-05 and NTK-07.

Nikari Tech does not produce the extraction Build Plan.

### Step 4 — Build OS plan

If extraction or implementation is approved, Build OS produces the Build Plan and Build Manifest.

Build OS specifies whether the executor is Cursor or Claude Code.

- Cursor = ordinary implementation.
- Claude Code = governed extraction / repo-aware validation-heavy work.

### Step 5 — Execution

Cursor executes ordinary implementation inside approved Build Plans.

Claude Code may execute governed extraction only where the founder-approved Build OS plan authorises that mode.

### Step 6 — Post-execution validation

Claude Code may run **Strategic Validation** after Cursor implementation to compare repo state against:

- Build Plan;
- product scope;
- suppression rules;
- architecture decisions;
- public/private boundary rules;
- module boundary expectations.

### Step 7 — Commit / handover

Developer OS governs commit and branch discipline.

Session handover records:

- what changed;
- validation result;
- open risks;
- extraction candidates;
- next session owner;
- whether product project, Nikari Tech, Build OS, Developer OS, or ChatGPT owns the next step.

---

## 3. NRE Phase 10 recommended route

```txt
1. Open NRE product project.
2. Confirm Phase 10 scope: Supabase-backed published listings MVP only.
3. Run Claude Code Repo-Aware Audit on apps/nre-public.
4. Use audit output in Nikari Tech only for module identification if needed.
5. Build OS produces Phase 10 Build Plan.
6. Cursor executes ordinary Phase 10 implementation.
7. Claude Code performs post-execution Strategic Validation.
8. Founder confirms deployment/readiness.
9. Stage 9 Extraction Review records candidates.
```

---

## 4. Module extraction rule

Extraction is not the same as implementation.

Use this routing:

```txt
Possible reusable pattern found → Nikari Tech identifies/classifies
Candidate ready for extraction → Build OS scopes Build Plan
Reasoning-heavy extraction required → Claude Code Governed Extraction
Ordinary implementation required → Cursor Execution
Founder confirms promotion → NTK-07 version promotion path
```

---

## 5. Reference repo context extension

When a legacy repo or related repo is relevant, use the Reference Repo Context Pattern:

```txt
Active repo: nikari-platform
Reference repo: nre-01-core-platform
Reference repo posture: read-only context only
Allowed use: compare patterns, identify risks, recover public-safe logic
Prohibited use: no edits, no direct copy, no admin/private/secret logic imported
```

---

## 6. Guardrail summary

- Product truth before reuse.
- Build Plans before execution.
- Claude Code is not self-authorising.
- Cursor remains ordinary executor.
- Reference repos are evidence, not authority.
- ChatGPT review is input, not governance.
- Founder confirmation and GitHub commit make governance active.
