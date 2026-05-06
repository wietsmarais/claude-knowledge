# Cursor Mode Reference for LLM Projects

**File:** `CURSOR_MODE_REFERENCE_FOR_LLM_PROJECTS.md`  
**Recommended path:** `claude-knowledge/universal/CURSOR_MODE_REFERENCE_FOR_LLM_PROJECTS.md`  
**Status:** Working Standard Reference  
**Owner:** Nikari / Wiets Marais  
**Purpose:** Ensure Claude and ChatGPT projects apply the Nikari Cursor Operating Roles process when brainstorming, scoping, reviewing, or drafting prompts for Cursor execution.

---

## 1. Purpose

This file exists because Cursor operating-mode discipline must be applied **before** work reaches Cursor.

Cursor repo rules and `.mdc` pointer files help Cursor behave correctly inside a repo. However, many important decisions happen earlier, during:

- brainstorming;
- scoping;
- prompt drafting;
- prompt review;
- build planning;
- handover drafting;
- governance-adjacent writing.

Claude and ChatGPT projects must therefore apply the Nikari Cursor Operating Roles process when they produce or review anything that may later be executed in Cursor.

The goal is not to make every session heavy. The goal is to stop generic Cursor prompts from being drafted when a declared Cursor mode, Founder Optimisation Decision Gate, or repo-aware review step is required.

---

## 2. Canonical source files

Primary Cursor operating-role standard:

```txt
https://raw.githubusercontent.com/wietsmarais/wietsmarais/main/docs/process/NIKARI_CURSOR_OPERATING_ROLES.md
```

Reusable Cursor operating-mode starter prompts:

```txt
https://raw.githubusercontent.com/wietsmarais/cursor-prompts/main/prompts/governance/J-cursor-operating-modes.md
```

Structured writing / manuscript addendum, where relevant:

```txt
https://raw.githubusercontent.com/wietsmarais/wietsmarais/main/docs/process/NIKARI_CURSOR_MANUSCRIPT_MODE.md
```

If this file and the canonical source files diverge, the canonical source files govern.

---

## 3. When this reference applies

Apply this reference when an LLM project is asked to:

- draft a Cursor prompt;
- review a Cursor prompt;
- scope a task that Cursor may execute;
- brainstorm a feature, product, build, repo, or workflow that may later go to Cursor;
- prepare a Cursor validation, commit, or handover prompt;
- decide whether Cursor should inspect, edit, validate, or commit files;
- create or review formal handover, closeout, scope-charter, or governance-adjacent content that Cursor may later save or commit.

This applies especially to:

- Developer OS;
- Build OS;
- Nikari Tech;
- Nikari Tech Review;
- NRE / Nikari Platform rebuild sessions;
- prompt-library work;
- structured writing or manuscript projects where Cursor may inspect a writing repo.

---

## 4. Core rule for Claude and ChatGPT

Do not draft Cursor prompts as generic implementation prompts.

Before drafting or reviewing a Cursor prompt, identify:

```txt
Cursor mode:
Task type:
Founder Optimisation Decision Gate required? yes/no/level:
May Cursor inspect?
May Cursor edit?
May Cursor create files?
May Cursor stage?
May Cursor commit?
May Cursor push?
What must Cursor stop and report on?
Which source file or prompt starter is relevant?
```

If the mode is unclear, ask the founder to choose the Cursor mode before finalising the prompt.

---

## 5. Cursor modes to consider

Available Cursor modes:

```txt
Simple / Fast-track
Brainstorm / Context Discovery
Prompt Review
Repo-Aware Optimisation
Execution
Validation / Audit
File Operation / Commit
Manuscript / Structured Writing Repo, where relevant
```

Use the reusable mode starters from:

```txt
https://raw.githubusercontent.com/wietsmarais/cursor-prompts/main/prompts/governance/J-cursor-operating-modes.md
```

Do not duplicate full process text into every prompt. Use only the mode-specific starter and the task-specific instructions needed.

---

## 6. Founder Optimisation Decision Gate

For meaningful non-routine work, the founder decides whether repo-aware optimisation is required before a final Cursor execution prompt is written.

Founder options:

```txt
No optimisation
Light optimisation
Repo-aware optimisation
Risk/security optimisation
Architecture optimisation
```

Only the founder may invoke, waive, reduce, increase, or change the optimisation level.

Claude, ChatGPT, and Cursor may recommend a level, but they may not decide it.

If a task appears simple but becomes more complex, the gate may be re-opened by the founder.

---

## 7. Recommended LLM workflow before Cursor execution

For meaningful build or repo work, use this sequence:

```txt
1. Founder intent
2. Initial scoping
3. Founder Optimisation Decision Gate
4. Cursor repo-aware optimisation or prompt review, if selected
5. Prompt synthesis by Claude or ChatGPT
6. Founder approval
7. Cursor execution in declared mode
8. Cursor validation and factual report
9. Handover drafted or reviewed by Claude/ChatGPT
10. Cursor saves, validates, commits, and pushes approved content if authorised
```

The LLM project should not skip directly from founder idea to Cursor execution unless the task is clearly simple, low-risk, and founder-confirmed as fast-track.

---

## 8. Cursor as repo-aware brainstorm or review partner

Cursor may be used before execution as a repo-aware reviewer or brainstorm/context-discovery partner.

This is not the same as asking Cursor to implement.

Examples:

```txt
Cursor mode: Brainstorm / Context Discovery
Cursor mode: Prompt Review
Cursor mode: Repo-Aware Optimisation
```

In these modes, Cursor may inspect approved files and report repo reality, risks, patterns, overlaps, and options.

Cursor must not edit, commit, or treat its recommendations as approved scope.

Claude or ChatGPT should then synthesise Cursor’s factual findings into a final prompt or recommendation for founder approval.

---

## 9. Handover and governance authorship

Cursor may report factual execution details.

Claude or ChatGPT should draft or review formal:

```txt
handovers
closeouts
scope charters
governance-adjacent summaries
process decisions
```

Cursor may save, validate, commit, and push approved content only after founder approval.

Cursor factual reports are source material. They are not governance by themselves.

---

## 10. File-handling rule

Not every file operation should go through Cursor.

Use direct file placement / GitHub Desktop when:

```txt
the file was drafted and approved outside Cursor
the file is complete and downloaded locally
no rewriting or transformation is needed
the target path is obvious
direct diff review is simpler and safer
```

Use Cursor File Operation / Commit Mode when:

```txt
Cursor generated the session output
repo-aware validation is needed
the file path or repo state is uncertain
new untracked markdown needs git add -N or numbered content verification
exact command/report discipline is needed
```

When Claude or ChatGPT drafts an approved file, it should also recommend the simplest safe file-handling pathway.

---

## 11. New untracked markdown verification

When Cursor creates or saves a new untracked markdown file, do not rely on:

```txt
git diff -- [file]
```

alone.

Use:

```txt
git add -N [file]
git diff -- [file]
git diff --check
```

If markdown fences are present or formatting matters, show numbered lines with fences visible:

```powershell
$i = 1
Get-Content -Path "[file path]" -TotalCount 100 |
  ForEach-Object {
    "{0,3}: {1}" -f $i, ($_.Replace('```', '<FENCE>'))
    $i++
  }
```

---

## 12. Structured writing / manuscript projects

When a Claude or ChatGPT project is working on books, manuscripts, structured writing, courses, or long-form documentation repos, and Cursor may be used to inspect or edit the writing repo, apply:

```txt
https://raw.githubusercontent.com/wietsmarais/wietsmarais/main/docs/process/NIKARI_CURSOR_MANUSCRIPT_MODE.md
```

Cursor may assist with:

- continuity checks;
- theme/rule alignment;
- consistency review;
- approved edit application;
- structured repo inspection.

Cursor must not become the final authorial, theological, editorial, or creative authority.

Use the relevant output labels:

```txt
Writing continuity review — not editorial decision.
Approved edit report.
```

---

## 13. Minimal source rule

Do not fetch or re-read full governance by default.

Use this reference to decide which process source is needed, then read only the relevant canonical file or mode starter.

Use deeper source review only when:

- the task is high-risk;
- repo state is uncertain;
- scope is unclear;
- backend/data/security/form/admin/CRM/analytics/architecture work is involved;
- the founder requests it.

This avoids returning to massive session-opening protocols while preserving source-of-truth discipline.

---

## 14. Standard snippet for LLM project instructions

Add this snippet to Claude or ChatGPT project instructions where the project may draft, review, scope, or improve Cursor-bound work:

```md
## Cursor operating-mode reference

When this project drafts, reviews, scopes, or improves work that will later be executed in Cursor, apply the Nikari Cursor Operating Roles process.

Primary standard:

https://raw.githubusercontent.com/wietsmarais/wietsmarais/main/docs/process/NIKARI_CURSOR_OPERATING_ROLES.md

Reusable Cursor mode starters:

https://raw.githubusercontent.com/wietsmarais/cursor-prompts/main/prompts/governance/J-cursor-operating-modes.md

Structured writing / manuscript addendum, where relevant:

https://raw.githubusercontent.com/wietsmarais/wietsmarais/main/docs/process/NIKARI_CURSOR_MANUSCRIPT_MODE.md

Rule:
Do not draft Cursor prompts as generic implementation prompts. First identify the intended Cursor mode, whether the Founder Optimisation Decision Gate applies, and whether Cursor is being used for brainstorm, prompt review, optimisation, execution, validation, or file operation.

Do not fetch or re-read full governance by default. Use only the relevant mode/process source needed for the task.
```

---

## 15. Final operating rule

```txt
Cursor’s power is repo awareness.
Cursor’s risk is undeclared authority.
Therefore Cursor must operate in declared modes.
```

For LLM projects:

```txt
Claude/ChatGPT shape the prompt before Cursor acts.
Cursor executes, validates, or reports in a declared mode.
Founder approves.
GitHub holds the truth.
```

---

## Version history

| Version | Date | Change |
|---|---|---|
| 1.0 Working Standard Reference | 6 May 2026 | Initial LLM-facing reference for applying Nikari Cursor Operating Roles during Claude/ChatGPT brainstorming, scoping, prompt drafting, and prompt review. |
