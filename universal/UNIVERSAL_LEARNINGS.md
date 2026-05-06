# Universal Learnings Log
**Repo:** github.com/wietsmarais (root)
**Applies to:** All projects — cross-project learnings only
**Rules:** Append only. Never edit existing entries. Most recent entry at the bottom.
**Maintained by:** Founder + Claude — extracted from project LEARNINGS.md files

Project-specific learnings live in each project's `docs/decisions/LEARNINGS.md`.
A learning moves to this file when it changes how ALL projects are built —
a pattern that failed or succeeded in one project that should be adopted or
avoided across the entire portfolio.

**Extraction trigger:** At the end of every project phase, Claude reads the
project LEARNINGS.md and asks — does anything here change how we build all
projects? If yes, extract it here and update the relevant governance document.

---

## 2026-04-09 — Governance build session

**Source:** Developer OS — April 2026 governance restructure session

**What worked:**
- Treating the Claude project instructions field as an operating manual
  rather than a rules list produced dramatically better session behaviour.
  Claude directed correctly from the first message rather than needing reminding.
- Separating files into three types (Claude reads / Cursor reads / attached on demand)
  resolved the chaos of 13 files with unclear placement. Every file now has
  one clear home and one clear consumer.
- The three-stage project start protocol (Developer OS → Claude project → Cursor)
  gave every project a defined starting sequence. No more reinventing the process
  at the start of each build.
- Writing governance documents to the exact spec of the handover brief produced
  complete, correctly structured outputs in a single pass. Spec-driven production
  is significantly more efficient than open-ended generation.

**What failed / what was missing:**
- The original Developer OS project knowledge accumulated 12 files with no
  clear taxonomy. Seven individual SPEC files were being permanently loaded
  when they should be attached on demand. This inflated context and reduced
  Claude's focus on the files that actually mattered.
- The session close ritual did not exist as a formal step. Sessions ended
  without consistent handovers, without extraction candidate checks, and
  without a clear boundary signal. This was the single biggest process gap.
- Free tier monitoring thresholds in PROJECT_STANDARDS.md were documented
  for Supabase free tier. The organisation is on Pro. The thresholds were
  wrong by an order of magnitude and would not have triggered alerts at
  relevant levels.
- Universal learnings and decisions had no home. Project-level files captured
  everything but insights that applied across projects had nowhere to go.

**What changes across all projects:**
- Session close is now a seven-step mandatory ritual ending with an explicit
  boundary phrase. One chat per session is a structural rule, not a preference.
- Developer OS project knowledge is capped at 7 files. SPEC files attach on demand.
- PROJECT_STANDARDS.md now reflects actual Pro plan limits, not free tier limits.
- Universal DECISIONS.md and LEARNINGS.md now exist in the wietsmarais root repo.
  Project-phase reviews include an extraction check to this level.
- The component library is formally the long-term knowledge base. Extraction
  is a closing-ritual step, not an afterthought.

**Component library candidates identified this session:**
- Session close ritual pattern — could become a reusable SPEC for any project
- Three-stage project start protocol — documented in Developer OS instructions,
  candidate for component-library/project-management/SPEC.md update
- Scope deviation detection — added to AI_BUILD_GUARDRAILS C12, candidate for
  component-library/ai-safety/SPEC.md update

**Governance documents updated this session:**
- AI_BUILD_GUARDRAILS.md — added C11 (mandatory session close) and C12 (scope deviation)
- PROJECT_MANAGEMENT_DISCIPLINE.md — updated Section B with one-chat rule,
  seven-step close ritual, extraction candidate step, scope deviation detection
- PROJECT_STANDARDS.md — updated Supabase section to Pro plan limits,
  added spend cap rule and revenue trigger rule
- DEVELOPER_OS_PROJECT_INSTRUCTIONS_v2.md — added session boundary rule at top

---

*Append new entries below this line.*
*Format: ## [YYYY-MM-DD] — [Session or sprint description]*
*Never edit entries above this line.*

## 2026-04-22 — Cursor command approval discipline
**What worked:** Separating read-only commands (run freely) from write commands
(show and wait) eliminated silent errors in git commits and file edits. Encoding
this as a standing instructions block in A01 makes it a consistent manual habit
rather than relying on memory each session.

**What failed:**
- Em-dash and smart quote corruption in commit messages when special characters
  were interpolated directly in the -m flag.
- PowerShell echo and Set-Content write BOM characters into commit message files —
  use [System.IO.File]::WriteAllText with [System.Text.Encoding]::UTF8 instead.
- Cursor automatically appends --trailer "Made-with: Cursor" to all commit commands —
  this is accepted behaviour, cannot be disabled via settings UI. It affects commit
  metadata only, not file content.
- Cursor modified guardrail file content without authorisation — inserted --trailer
  into C13/C14 text. Required explicit instruction to separate commit command
  behaviour from file content.
- Guardrails planned as C11/C12 landed as C13/C14 because those numbers were already
  taken. UNIVERSAL_DECISIONS.md entry from Change 1 references C11/C12 incorrectly —
  correction entry appended separately.
- cursor-prompts remote was misconfigured — pointed at wietsmarais.git instead of
  cursor-prompts.git. Fixed via git remote set-url in Command Prompt.

**What changes next time:** All commit messages via WriteAllText with UTF8 no-BOM.
Cursor trailer is accepted but must never appear in governed file content. Always
grep for existing C-series numbers before drafting guardrail content. Verify remote
URLs for all repos before first push of any session.

**Component library candidates:** None.
**Prompt library candidates:** A01 Universal Session Opener — updated version
committed to cursor-prompts in Change 3.

---

27 April 2026 — Build OS Session 1
Learning 1 — Prose carry-forward lists are not an accountability system
Open actions listed as "Topics Carrying Forward" in session handovers
have no enforcement mechanism. Eight items drifted across six consecutive
sessions (25 April → 27 April 2026) without being actioned. The items
existed in handover files but were never visible, never prioritised,
and never created any obligation to act.
The fix: Every open action becomes a GitHub issue before the handover
closes. Issues are visible, searchable, and persistent across session
boundaries. They do not depend on the next Claude session reading the
right handover file in the right order.
Locked as: UNIVERSAL_DECISIONS.md — 27 April 2026 — session handover
open actions must become GitHub issues.

Learning 2 — Static uploaded project knowledge creates its own drift problem
Uploading governance files to Claude project knowledge solves the
"Claude needs to read this" problem but creates a new one: every time
the source file is updated, every Claude project that has a copy needs
a re-upload. With multiple active Claude projects and frequently updated
governance documents, this becomes a recurring manual overhead that is
easy to skip and hard to track.
The result is Claude projects reading stale governance documents without
knowing they are stale. A session might proceed against an outdated
UNIVERSAL_DECISIONS.md and produce recommendations that have already
been superseded.
The fix: Universal and project-level reference files live in a public
GitHub repo (wietsmarais/claude-knowledge). Claude fetches them via
raw URL at session open. One update to GitHub propagates to every Claude
project automatically. No re-upload required.
Locked as: UNIVERSAL_DECISIONS.md — 27 April 2026 — claude-knowledge
public repo as live Claude reference layer.

Learning 3 — Command Prompt file path errors are avoidable
gh CLI --body-file commands fail silently with "cannot find file" when
run from the wrong directory. The error message does not tell you where
it looked — only that it failed. This wastes time diagnosing a trivial
problem.
The fix: Always cd to the folder containing the body files before
running any gh CLI command. State the working directory explicitly in
any Claude-produced gh CLI instructions.
Pattern:
cd C:\Temp\issues
gh issue create --repo wietsmarais/wietsmarais --title "..." --body-file "issueNN.txt" ...

Learning 4 — Public repo for Claude knowledge layer is architecturally cleaner than uploads
The instinct to extend a governance public repo beyond universal decisions
to a full Claude knowledge layer (one folder per project, all reference
files fetchable by raw URL) is correct. It treats the knowledge layer as
infrastructure — maintained in one place, consumed everywhere — rather
than as a per-project upload task.
The distinction between what is public-safe (governance, reference,
architecture notes) and what stays private (session handovers, prompt
library, SPEC files, client data) is clear and enforceable. The public
repo does not become a security risk if the classification rule is
followed.

---
## Learning: Prompt length should match risk and uncertainty
Date: 6 May 2026
Context: Nikari Platform / NRE public rebuild — Phase 6 to Phase 7 workflow

Long, highly constrained prompts are useful when:
- repo state is uncertain;
- a closeout has not been committed;
- implementation may touch source files;
- the next step could introduce risky product capability;
- backend, forms, data writes, CRM, admin, analytics, Supabase, or security are involved;
- legacy/source-mine boundaries need strong protection.

Shorter confirmation prompts are better when:
- the handover is already committed and pushed;
- the repo is clean and aligned;
- the expected handover file is tracked;
- the next task is only to make the next scoping decision.

The improved pattern is:
1. Confirm repo clean/aligned.
2. Confirm expected handover file is tracked.
3. Move directly to the next real decision.

This reduces administrative friction while preserving governance discipline.

---
## Learning: Cursor Agent mode is superior for most governed execution
Date: 6 May 2026
Context: Nikari Platform / NRE public rebuild

Using Cursor Agent mode for routine governed repo work has proven better than manual terminal-first execution in most cases.

Benefits observed:
- fewer command-construction mistakes;
- clearer stop/report behaviour;
- better context retention;
- easier validation reporting;
- cleaner commit preparation;
- stronger file-boundary discipline;
- lower founder cognitive load.

Manual terminal remains useful for direct commands and troubleshooting, but Agent mode should be the default for scoped Nikari repo workflows unless there is a specific reason not to use it.

---
## Learning: Cursor factual reports should feed handovers, not replace handover authorship
Date: 6 May 2026
Context: Nikari Platform / NRE public rebuild

Cursor Agent is effective at reporting factual execution details:
- repo status;
- changed files;
- validation results;
- forbidden-scope scan results;
- commit hashes;
- latest commits;
- boundary conditions observed.

Those reports are excellent source material for handovers. However, formal handovers, closeouts, scope charters, and governance-adjacent summaries should be drafted or reviewed in ChatGPT or Claude before being committed.

This keeps Cursor in the execution role and keeps synthesis, judgment, and governance-adjacent wording in the review/authoring layer.

---
## Learning: New untracked documentation files need direct content display or intent-to-add before commit
Date: 6 May 2026
Context: Nikari Platform / NRE public rebuild — Phase 7 closeout handover

When a markdown file is new and untracked, `git diff -- [file]` may show no content. This can make a file appear unreviewed even though it exists locally.

For new markdown handover or scope files, use one of these before commit:
- `git add -N [file]` followed by `git diff -- [file]`; or
- direct content display with numbered lines, especially where markdown fences are present.

Recommended pattern:

    git status -sb
    git add -N [file]
    git diff -- [file]
    git diff --check
    Get-Content [file] -TotalCount 60-100 with numbered lines and visible fences, if needed

This is a small verification step, not a return to long forensic review.

---
