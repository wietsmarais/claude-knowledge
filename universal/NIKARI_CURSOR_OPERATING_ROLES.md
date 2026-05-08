# Nikari Cursor Operating Roles \& AI-Native Workflow

**File:** `NIKARI\_CURSOR\_OPERATING\_ROLES.md`  
**Recommended path:** `wietsmarais/docs/process/NIKARI\_CURSOR\_OPERATING\_ROLES.md`  
**Status:** Working Standard — pending validation across real Cursor sessions before locking  
**Owner:** Nikari / Wiets Marais  
**Date:** 6 May 2026  
**Supersedes:** `NIKARI\_CURSOR\_OPERATING\_ROLES\_AND\_AI\_WORKFLOW\_BLUEPRINT.md` (draft)  
**Related addendum:** `NIKARI\_CURSOR\_MANUSCRIPT\_MODE.md`  
**Purpose:** Define how Nikari uses Cursor as a repo-aware operating agent with declared modes, founder decision gates, prompt-generation discipline, execution boundaries, validation/reporting rules, and GitHub source-of-truth discipline.

\---

## 1\. Executive summary

Nikari's AI workflow is evolving from a simple pattern:

```txt
idea → prompt → Cursor execution
```

into a disciplined AI-native operating model:

```txt
Founder intent
→ scoping
→ Founder Optimisation Decision Gate
→ repo-aware optimisation / review where selected
→ prompt synthesis by ChatGPT or Claude
→ founder approval
→ Cursor execution
→ validation and factual reporting
→ handover drafted/reviewed by ChatGPT or Claude
→ Cursor save / validate / commit / push
→ GitHub truth
```

The core insight is:

```txt
Cursor's power is repo awareness.
Cursor's risk is undeclared authority.
Therefore Cursor must operate in declared modes.
```

Cursor should not be treated as one generic AI code writer. It can be a repo-aware discovery partner, prompt reviewer, optimisation reviewer, executor, validator, or file-operation/commit agent. Each mode has different permissions.

This file defines those modes and the workflow around them.

\---

## 2\. Why this file is needed

Recent Nikari Platform / NRE public rebuild work exposed process lessons that now need to become operational, not merely remembered.

1. **Governance decisions do not automatically change behaviour.**  
A rule committed to `UNIVERSAL\_DECISIONS.md` becomes useful only when the actual prompt templates, Cursor workflows, and session habits apply it.
2. **Long session-opening protocols can create admin overload.**  
Previous raw-GitHub-source approaches ensured current context, but sometimes forced too much reading before simple decisions.
3. **Fast workflows are useful, but need targeted checks.**  
Fast handover-confirmation works when the repo is clean and handovers are committed. New untracked markdown files still require direct content verification or `git add -N` before commit.
4. **Cursor Agent mode is excellent for execution, but should not originate governance-adjacent content by default.**  
Cursor is strong at scoped changes, validation, factual reporting, saving approved content, and commit/push workflow. Formal handovers, closeouts, scope charters, and governance-adjacent content should be drafted or reviewed in ChatGPT or Claude, then saved by Cursor.
5. **Prompt quality determines build quality.**  
Cursor can enforce boundaries, but it will not automatically optimise product quality unless the prompt or process asks it to. Prompt generation must include a deliberate decision about whether repo-aware optimisation is needed before execution.
6. **Cursor can be more than an executor.**  
Cursor can also operate as a repo-aware brainstorm partner, prompt reviewer, optimisation reviewer, validation auditor, and file operator — if the mode is declared and bounded.

\---

## 3\. Core operating rules

These rules govern every Cursor mode and every workflow described in this file.

### Rule 3.1 — GitHub holds the truth

GitHub remains the committed source of truth.

ChatGPT, Claude, Cursor, and memory can support the workflow, but governance becomes authoritative only when founder-confirmed and committed to the correct GitHub location.

### Rule 3.2 — Cursor operates in declared modes

Cursor is not one role.

Every Cursor session must declare its operating mode before work begins. The declared mode determines whether Cursor may:

* inspect files;
* search the repo;
* suggest options;
* review prompts;
* edit files;
* validate;
* save approved content;
* stage;
* commit;
* push.

### Rule 3.3 — Founder authority is preserved

The founder remains the decision authority.

Only the founder may:

* invoke, reduce, waive, or change the Founder Optimisation Decision Gate level;
* approve mode changes;
* approve scope expansion;
* approve execution prompts;
* approve staging, committing, and pushing;
* approve governance, handover, closeout, scope-charter, or process content.

ChatGPT, Claude, and Cursor may recommend. They may not decide.

### Rule 3.4 — Cursor surfaces repo context; it does not decide direction

Cursor may surface facts, patterns, risks, options, and repo context.

Cursor may not treat its findings as approved direction, approved scope, governance, policy, or final strategy.

### Rule 3.5 — Cursor does not originate governance by default

Cursor must not be treated as the default author of governance, canonical documents, formal handovers, scope charters, process decisions, or governance-adjacent summaries.

Cursor may assist with a narrow factual draft only if explicitly authorised by the founder. Even then, the draft must still be reviewed through ChatGPT or Claude and approved by the founder before being treated as formal governance or handover content.

### Rule 3.6 — ChatGPT / Claude synthesise; Cursor executes and reports

Default role split:

```txt
Founder:
  final decision, priority, approval, strategic judgment

ChatGPT / Claude:
  reasoning, synthesis, prompt drafting, governance-adjacent writing, handover drafting/review

Cursor:
  repo-aware discovery, scoped execution, validation, factual reporting, file operations, commits/pushes after approval

GitHub:
  committed source of truth
```

### Rule 3.7 — Prompt length matches risk and uncertainty

Use long prompts when:

* repo state is uncertain;
* a phase closeout has not been committed;
* source files will be modified;
* backend/data/security work is involved;
* legacy/source-mine boundaries require strong protection;
* a new phase or risky capability is being opened.

Use shorter prompts when:

* the handover is committed and tracked;
* the repo is clean and aligned;
* the next task is only next-step scoping;
* the scope is narrow and low-risk.

### Rule 3.8 — Optimisation is explicit, not invisible

Optimisation should not happen accidentally and should not be skipped by accident.

After scoping, the founder decides whether repo-aware optimisation is required before the final prompt is written.

This is the **Founder Optimisation Decision Gate**.

### Rule 3.9 — Output labels are mandatory in non-execution modes

Cursor outputs that may influence decisions must be labelled according to mode.

Examples:

```txt
Context discovery — not decision.
Prompt review — not execution approval.
Optimisation review — not approved scope.
Validation report — not permission to fix.
File operation report — approved content saved/committed only as authorised.
```

This prevents polished Cursor output from being mistaken for founder-approved direction.

\---

## 4\. Preferred Nikari AI-native workflow

The preferred workflow for meaningful build, documentation, governance-adjacent, or structured project work is:

```txt
1. Founder intent
   Capture the business, product, governance, or creative goal.

2. Scoping
   Define the smallest useful bounded slice and exclusions.

3. Founder Optimisation Decision Gate
   Founder decides whether repo-aware optimisation is required and at what level.
   Only the founder may invoke, reduce, waive, or change the gate level.
   ChatGPT, Claude, and Cursor may recommend a level but may not decide it.

4. Repo-aware optimisation / review, if selected
   Cursor inspects approved repo files and reports context, risks, options, reuse, and recommended scope.
   Output label: "Optimisation review — not approved scope."

5. Prompt synthesis
   ChatGPT or Claude turns founder intent, scope, and Cursor review into the final prompt.

6. Founder approval
   Founder approves the final prompt before execution.

7. Cursor execution
   Cursor executes only within the approved prompt and declared mode.

8. Validation and factual reporting
   Cursor runs validation and reports facts: files changed, tests, scans, commits, repo state.

9. Handover drafting/review
   ChatGPT or Claude drafts or reviews the handover using Cursor's factual report.

10. File operation / commit
    Cursor saves approved content, verifies it, stages/commits/pushes after approval.

11. GitHub truth
    Committed files become the operating source of truth.
```

\---

## 5\. Founder Optimisation Decision Gate

### 5.1 Purpose

Before the final Cursor execution prompt is written, the founder decides whether repo-aware optimisation is required.

This prevents two errors:

1. Skipping optimisation when it would materially improve the build.
2. Forcing heavy optimisation onto simple or routine tasks.

### 5.2 Founder authority

Only the founder may invoke, reduce, waive, or change the optimisation gate level.

ChatGPT, Claude, and Cursor may recommend a level, but may not set it.

### 5.3 Mid-session re-entry

If a task proves more complex than expected after a lower optimisation level or “No optimisation” was selected, the founder may re-open the gate at any point in the session.

Cursor must stop and wait for the revised gate decision before continuing.

### 5.4 Gate levels

```txt
A. No optimisation
   Simple/routine task. Proceed directly to prompt/execution.
   See also: Simple-task fast-track.

B. Light optimisation
   Quick check: is this still the right slice, are files bounded, are there obvious risks?

C. Repo-aware optimisation
   Cursor inspects relevant repo files and reports existing patterns, risks, reuse opportunities, and best scoped approach.
   Output label: "Optimisation review — not approved scope."

D. Risk/security optimisation
   Required for forms, data writes, Supabase, auth, CRM, admin, analytics, AI, payments, privacy, security, tenant, or regulated workflows.

E. Architecture optimisation
   Required for contracts, shared packages, module promotion, white-label capability, tenant architecture, cross-product reuse, or strategic platform changes.
```

### 5.5 Default rule

If the task is meaningful and not purely routine, ask the Founder Optimisation Decision Gate question.

Suggested wording:

```txt
Founder Decision Gate:
Should this task go through repo-aware optimisation before the final prompt is written?
Options: No / Light / Repo-aware / Risk-security / Architecture.
Only the founder decides. ChatGPT, Claude, and Cursor may suggest but not set the level.
```

\---

## 6\. Simple-task fast-track

For clearly low-risk, routine tasks, the full mode declaration and optimisation gate may be telescoped into a single short header, provided all of the following are true:

```txt
- No source files are being modified; or the only operation is a previously approved file save/commit.
- No backend, data, security, form, admin, CRM, analytics, architecture, or tenant risk is present.
- The repo is clean and the last handover is committed and tracked.
- The task is a bounded continuation of already-approved work.
```

Example fast-track use case:

```txt
Commit an already-approved handover file that was drafted in ChatGPT/Claude, saved exactly by Cursor, validated with git add -N / diff / diff --check, and confirmed by the founder.
```

Fast-track header:

```txt
Cursor mode: Simple / Fast-track
Repo:
Task:
Optimisation gate: No optimisation — low-risk routine task confirmed by founder.
May inspect: \[list]
May edit: no / approved target file only
May stage/commit/push: only if explicitly approved
```

If any doubt exists about whether a task qualifies, use the full gate.

Fast-track is opt-in by the founder only.

\---

## 7\. Cursor operating modes

Every Cursor session must declare a mode.

Recommended standard header:

```txt
Cursor mode:
Repo:
Task type:
May inspect:
May edit:
May create files:
May stage/commit/push:
Founder approval required before:
Forbidden files/paths:
Expected output:
```

\---

## 8\. Cursor role summary table

|Mode|Primary purpose|May inspect|May edit|May commit/push|Required output label|
|-|-|-|-|-|-|
|Brainstorm / Context Discovery|Surface relevant repo context and missed considerations|Yes, approved files|No|No|`Context discovery — not decision`|
|Prompt Review|Review a proposed prompt against repo reality|Yes, approved files|No|No|`Prompt review — not execution approval`|
|Repo-Aware Optimisation|Recommend best scoped approach before execution|Yes, approved files|No|No|`Optimisation review — not approved scope`|
|Execution|Implement approved prompt|Yes, bounded|Yes, approved files only|Only if separately approved|`Execution report — not handover`|
|Validation / Audit|Validate repo state or implementation|Yes|No by default|No|`Validation report — not permission to fix`|
|File Operation / Commit|Save approved content and commit/push|Only target files|Only approved content|Yes, after approval|`File operation report — approved content only`|

> Manuscript / Structured Writing Repo Mode is defined in the separate addendum: `NIKARI\_CURSOR\_MANUSCRIPT\_MODE.md`.

\---

## 9\. Mode 1 — Brainstorm / Context Discovery

### Purpose

Use Cursor's repo access to discover relevant context before strategy, scoping, or prompt writing.

This mode is not code execution.

### Use when

* Brainstorming a new product, feature, workflow, writing project, or governance idea.
* Checking whether the idea overlaps with existing Nikari work.
* Looking for existing components, docs, patterns, decisions, prompts, or constraints.
* Exploring what has already been built or documented.
* Trying not to miss relevant repo context before prompt synthesis.

### Allowed

* Inspect approved repos/files.
* Search for relevant terms, components, docs, decisions, and prior patterns.
* Identify overlaps, contradictions, opportunities, and risks.
* Suggest questions the founder should answer.
* Recommend whether a deeper optimisation or architecture review is needed.

### Not allowed

* Edit files.
* Generate implementation changes.
* Stage, commit, or push.
* Decide governance.
* Structure or synthesise findings into governance candidates.
* Treat findings as source of truth unless tied to committed files.

### Required output label

```txt
Context discovery — not decision.
This output requires ChatGPT/Claude synthesis and founder approval before any finding becomes direction or governance candidate.
```

### Required output structure

```txt
Cursor mode: Brainstorm / Context Discovery
Output label: Context discovery — not decision.

Files inspected:
Existing relevant context found:
Missed considerations:
Risks / contradictions:
Opportunities / reuse candidates:
Questions for founder:
Recommended next decision:
Boundary note: This is not approved scope or governance.
```

\---

## 10\. Mode 2 — Prompt Review

### Purpose

Review a proposed prompt against actual repo reality before execution.

### Use when

* ChatGPT or Claude has drafted a Cursor prompt.
* The founder wants a repo-aware check before giving Cursor execution authority.
* There is uncertainty around file paths, imports, validation commands, or scope.

### Allowed

* Check whether referenced files exist.
* Check likely imports and related files.
* Identify missing stop conditions.
* Identify unsafe scope or contradictory instructions.
* Recommend tighter allowed/forbidden file lists.
* Recommend validation commands.

### Not allowed

* Execute the prompt.
* Modify files.
* Stage, commit, or push.
* Rewrite the entire strategic intent unless asked.
* Structure prompt review findings into governance candidates.

### Required output label

```txt
Prompt review — not execution approval.
```

### Required output structure

```txt
Cursor mode: Prompt Review
Output label: Prompt review — not execution approval.

Verdict: approved / needs revision / unsafe
Files checked:
Prompt risks:
Missing constraints:
Unsafe scope:
Suggested prompt edits:
Validation requirements:
Founder decision required:
```

> Prompt Review Mode and Repo-Aware Optimisation Mode may be run sequentially in the same session without requiring a full formal mode-switch approval because neither involves editing. The founder should still confirm which mode is active at each step.

\---

## 11\. Mode 3 — Repo-Aware Optimisation

### Purpose

Before implementation, inspect the relevant repo/files and recommend the best, safest, highest-value build approach.

### Use when

* A meaningful feature, page, component, route, package, workflow, or governance-adjacent operation is being planned.
* The founder wants a better app, not merely a compliant implementation.
* The task may affect UX, reuse, security, architecture, data, future extensibility, or operational posture.

### Allowed

* Inspect relevant approved files.
* Identify existing patterns/components.
* Identify risks and constraints.
* Recommend reuse opportunities.
* Recommend a smaller or better slice.
* Suggest what should remain deferred.

### Not allowed

* Implement.
* Modify files.
* Stage, commit, or push.
* Treat optimisation recommendations as approved scope.
* Structure findings into governance candidates.

### Required output label

```txt
Optimisation review — not approved scope.
Recommendations require founder review and approval before becoming execution scope.
```

### Required output structure

```txt
Cursor mode: Repo-Aware Optimisation
Output label: Optimisation review — not approved scope.

Current repo reality:
Files inspected:
Existing patterns to reuse:
Risks and boundary concerns:
Better implementation options:
Suggested smallest safe slice:
Recommended prompt improvements:
Deferred work:
Founder decision required:
Boundary note: This is not approved scope.
```

\---

## 12\. Mode 4 — Execution

### Purpose

Execute a founder-approved prompt inside approved file and capability boundaries.

### Use when

* The final prompt has been approved.
* The task is scoped and bounded.
* Cursor is allowed to edit specific files.

### Allowed

* Inspect and modify approved files only.
* Run specified validation commands.
* Report diffs and results.
* Stop if boundary problems arise.

### Not allowed

* Expand scope without approval.
* Modify unapproved files.
* Originate governance content.
* Stage/commit/push unless separately authorised.

### Required output label

```txt
Execution report — not handover.
```

### Required output structure

```txt
Cursor mode: Execution
Output label: Execution report — not handover.

Files changed:
Summary of changes:
Validation results:
Forbidden-scope scan results:
Scope boundaries observed:
Git status:
Diff check:
Recommended commit message:
Facts for handover:
```

\---

## 13\. Mode 5 — Validation / Audit

### Purpose

Validate repo state, implementation results, or compliance with scope boundaries.

### Use when

* Checking whether a repo is clean/aligned.
* Verifying implementation output.
* Running lint/typecheck/build/scans.
* Reviewing diffs before commit.
* Auditing forbidden-scope drift.

### Allowed

* Run approved commands.
* Inspect diffs.
* Report changed files.
* Identify validation failures or boundary breaches.

### Not allowed

* Fix issues unless a separate execution prompt is approved.
* Stage, commit, or push.

### Required output label

```txt
Validation report — not permission to fix.
```

### Required output structure

```txt
Cursor mode: Validation / Audit
Output label: Validation report — not permission to fix.

Repo state:
Commands run:
Pass/fail results:
Changed files:
Boundary issues:
Recommended next action:
Founder decision required:
```

\---

## 14\. Mode 6 — File Operation / Commit

### Purpose

Save approved content, validate it, stage, commit, push, and report final state.

### Use when

* ChatGPT or Claude has drafted approved handover/scope/governance content.
* Founder has approved the content.
* Cursor is needed to create/save the file and handle Git workflow.

### Allowed

* Create or overwrite target file with approved content exactly.
* Use `git add -N` for untracked markdown files.
* Show diff/content before commit.
* Run `git diff --check`.
* Stage only approved files.
* Commit/push only after explicit founder approval.

### Not allowed

* Rewrite approved content.
* Improve, summarise, or restructure formal handover/governance wording.
* Modify unrelated files.
* Commit without founder approval.

### Required output label

```txt
File operation report — approved content only.
```

### Required untracked markdown workflow

```txt
1. Save approved file.
2. Run git status -sb.
3. Run git add -N \[file].
4. Run git diff -- \[file].
5. Run git diff --check.
6. If needed, show numbered lines with fences visible.
7. Founder confirms.
8. Stage, commit, push.
```

### PowerShell helper for visible fences

```powershell
$i = 1
Get-Content -Path "\[file path]" -TotalCount 100 |
  ForEach-Object {
    "{0,3}: {1}" -f $i, ($\_.Replace('```', '<FENCE>'))
    $i++
  }
```

### Required output structure

```txt
Cursor mode: File Operation / Commit
Output label: File operation report — approved content only.

Approved content source:
Target file(s):
Files changed:
Diff/content verification:
Diff check:
Commit hash:
Push result:
Final repo status:
Latest commits:
```

\---



\## 14b. Approved file-handling pathways



Cursor File Operation / Commit Mode is not mandatory for every approved file.



When formal content has already been drafted or reviewed outside Cursor and founder-approved, the founder may place the file directly into the correct repo path using file explorer or GitHub Desktop, then review the diff, commit, and push through GitHub Desktop.



This is preferred where:

\- the file is already complete and approved;

\- no rewriting, formatting, validation, or repo-aware transformation is needed;

\- the target path is clear;

\- direct diff review is simpler and safer than asking Cursor to recreate the file.



Cursor File Operation / Commit Mode is preferred where:

\- Cursor generated the factual report or file content inside the session;

\- the file must be created from session output;

\- validation commands must be run before commit;

\- the file is new/untracked and needs `git add -N` or numbered content verification;

\- the repo state is uncertain;

\- exact command/report discipline is needed.



Rule:

Do not use Cursor merely because a file needs to be saved. Use Cursor when Cursor adds safety, validation, or repo-aware handling. Use direct placement when the file is already approved and direct diff review is simpler.



\---

## 15\. Mode switching and mode drift



Cursor may not switch modes without founder approval.

Examples:

```txt
Brainstorm Mode → Execution Mode
Requires founder approval and a new execution prompt.

Prompt Review Mode → Execution Mode
Requires founder approval of the revised prompt.

Validation Mode → Fix/Execution Mode
Requires explicit approval to edit.

File Operation Mode → Content Authoring Mode
Not allowed by default.
```

### Mode-drift detection

If Cursor detects that it is approaching a mode boundary it was not authorised to cross — for example, beginning to suggest edits while in Brainstorm Mode, or beginning to implement while in Prompt Review Mode — Cursor must stop immediately, report the boundary approach to the founder, and wait for explicit instruction before proceeding.

Cursor does not self-authorise mode changes. Drift detection is a stop-and-report action, not a self-correction action.

\---

## 16\. Governance authority prohibition

Cursor may surface facts, patterns, risks, options, and repo context in any mode.

Cursor may not:

* structure or synthesise that information into governance candidates;
* frame findings as governance decisions;
* produce documents intended to serve as governance records;
* treat its own output as approved direction or policy.

Governance framing, synthesis, and candidate drafting belong to ChatGPT or Claude, subject to founder review and GitHub commit.

This rule applies in all modes without exception. It is not overridden by a mode declaration.

\---

## 17\. Handover and governance authorship

Formal handovers, closeouts, scope charters, process decisions, and governance-adjacent summaries must be drafted or reviewed in ChatGPT or Claude before being committed.

Cursor's factual reports are source material, not final governance.

Standard flow:

```txt
Cursor reports facts
→ ChatGPT/Claude drafts or reviews handover
→ Founder approves
→ Cursor saves approved file exactly
→ Cursor validates
→ Founder approves commit
→ Cursor commits/pushes
```

\---

## 18\. Fast handover confirmation

After a handover is committed, pushed, tracked, and the repo is clean/aligned, use fast confirmation rather than full forensic re-review.

Minimum check:

```txt
git status -sb
git log --oneline -5
git ls-files \[expected handover file]
```

Proceed directly to the next real scoping decision if checks pass.

Use full review only when:

* repo state is uncertain;
* expected handover is missing;
* commits contradict baseline;
* risky capability is being opened;
* files will be modified;
* founder requests full review.

\---

## 19\. New untracked markdown verification

When a new markdown handover, scope, governance, or documentation file is created and is still untracked, do not rely on `git diff -- \[file]` alone.

Required pattern:

```txt
1. Save approved file.
2. git status -sb
3. git add -N \[file]
4. git diff -- \[file]
5. git diff --check
6. Get-Content numbered output if fences or formatting are important.
7. Founder confirms.
8. Stage, commit, push.
```

This is a small verification step, not a return to heavy forensic review.

\---

## 20\. How this relates to industry standards

This workflow does not reject industry-standard software process. It translates useful industry principles into a founder-led, AI-native operating model.

|Industry principle|Nikari AI-native equivalent|
|-|-|
|Product discovery|Founder intent + repo-aware brainstorm/context discovery|
|Architecture review|Repo-aware optimisation + ChatGPT/Claude synthesis|
|Security review|Risk/security optimisation gate|
|Code review|Cursor prompt review + validation/audit mode|
|Definition of done|Validation gate + handover gate|
|ADR / decision record|Universal decisions, NTK decisions, phase handovers|
|CI discipline|lint/typecheck/build/scans before commit|
|Separation of duties|Declared Cursor modes + founder approval|

The result is not less professional than industry process. It is a tailored process for an AI-assisted, multi-repo, founder-led build system.

\---

## 21\. Standard prompt headers by mode

### Simple / Fast-track

```txt
Cursor mode: Simple / Fast-track
Repo:
Task:
Optimisation gate: No optimisation — low-risk routine task confirmed by founder.
May inspect: \[list]
May edit: no / approved target file only
May stage/commit/push: only if explicitly approved
```

### Brainstorm / Context Discovery

```txt
Cursor mode: Brainstorm / Context Discovery
Repo:
Objective:
Allowed files/repos to inspect:
Do not edit.
Do not stage/commit/push.
Do not structure findings into governance candidates.
Report existing context, missed considerations, risks, opportunities, and founder questions.
Label all output: "Context discovery — not decision."
```

### Prompt Review

```txt
Cursor mode: Prompt Review
Repo:
Prompt to review:
Allowed files to inspect:
Do not execute.
Do not edit.
Report whether the prompt is safe, bounded, and repo-accurate.
Label output: "Prompt review — not execution approval."
```

### Repo-Aware Optimisation

```txt
Cursor mode: Repo-Aware Optimisation
Repo:
Objective:
Allowed files to inspect:
Do not edit.
Do not structure findings into governance candidates.
Recommend the safest, highest-value, smallest useful slice.
Report risks, reuse opportunities, implementation options, and deferred work.
Label all output: "Optimisation review — not approved scope."
```

### Execution

```txt
Cursor mode: Execution
Repo:
Approved task:
Allowed files to inspect/edit:
Forbidden files:
Validation:
Do not stage/commit/push unless separately approved.
Stop on boundary breach.
Label output: "Execution report — not handover."
```

### Validation / Audit

```txt
Cursor mode: Validation / Audit
Repo:
Validation objective:
Commands to run:
Files/diffs to inspect:
Do not edit.
Do not stage/commit/push.
Report pass/fail and boundary issues.
Label output: "Validation report — not permission to fix."
```

### File Operation / Commit

```txt
Cursor mode: File Operation / Commit
Repo:
Approved file(s):
Approved content source:
Commit message:
Do not rewrite approved content.
Validate with git add -N if new markdown.
Stage/commit/push only after founder approval.
Label output: "File operation report — approved content only."
```

\---

## 22\. Manuscript / Structured Writing Repo Mode reference

Cursor may also be used for structured writing repos: books, articles, long-form documentation, courses, or manuscripts.

This mode is defined in a separate addendum:

```txt
wietsmarais/docs/process/NIKARI\_CURSOR\_MANUSCRIPT\_MODE.md
```

The rules in this file — governance authority prohibition, mode-switching, mode-drift detection, output labelling, and founder approval — apply to that mode equally.

\---

## 23\. Governance and template files that should reference this file

This file is an operational process file. It should live under `docs/process/`, not `docs/architecture/`. It is not an NTK architecture document.

|File|Action|
|-|-|
|`UNIVERSAL\_DECISIONS.md`|Confirm or add entry: Cursor must operate in declared modes; mode switching requires founder approval; Cursor may not originate governance candidates in any mode.|
|`UNIVERSAL\_LEARNINGS.md`|Confirm or add entry: Cursor's repo awareness is most useful before execution — discovery, optimisation, prompt review — not only during execution.|
|Developer OS project instructions|Add reference to this file. Add mode declaration as a required session-open step for Cursor sessions. Add Optimisation Decision Gate as a required pre-execution step for meaningful tasks.|
|Build OS project instructions|Add note that Repo-Aware Optimisation Mode and Prompt Review Mode are available before Build OS execution prompts are finalised.|
|Cursor prompt library|Add standard mode headers from this file as named prompt starters.|

\---

## 24\. Final guiding statement

```txt
Cursor's power is repo awareness.
Cursor's risk is undeclared authority.
Therefore Cursor must operate in declared modes.
```

The Nikari AI-native workflow uses Cursor more intelligently than standard code-agent practice, without allowing Cursor to become the default author of governance, strategy, or approved direction.

```txt
Founder intent
→ ChatGPT/Claude reasoning and prompt synthesis
→ Cursor repo-aware review or optimisation where selected
→ founder-approved execution
→ Cursor validation and factual reporting
→ ChatGPT/Claude handover synthesis
→ Cursor file operations and GitHub commit
→ GitHub truth
```

\---

## Version history

|Version|Date|Change|
|-|-|-|
|1.0 Working Standard|6 May 2026|Finalised from blueprint draft and review cycle. Added output labels for all modes, founder gate authority, mid-session re-entry, mode-drift detection, governance authority prohibition, simple-task fast-track, untracked markdown verification, PowerShell helper, operational routing note, and separate manuscript addendum reference.|



