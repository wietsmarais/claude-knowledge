# claude-knowledge

**Owner:** wietsmarais  
**Visibility:** Public  
**Purpose:** Live governance reference layer for all Claude projects in the Nikari Tech portfolio  
**Status:** Active — updated when source governance files change  
**Last updated:** 27 April 2026

---

## What this repo is

This repo is the permanent, publicly readable reference layer for Claude projects
across the wietsmarais GitHub organisation. Claude projects (Build OS, NRE-01,
VIX, Developer OS) read raw GitHub URLs from this repo rather than relying solely
on uploaded project knowledge files.

This solves a structural problem: uploaded project knowledge goes stale between
sessions. A raw GitHub URL always returns the current committed version of a file.

---

## What this repo is not

This repo is not a build repo. No code is committed here.  
This repo is not a secrets store. No credentials, API keys, or environment variables.  
This repo is not a draft space. Only approved, reviewed governance files are committed.  
This repo is not a replacement for project-specific DECISIONS.md or PLAN.md files.  
Those live in each project repo. This repo holds universal and cross-project governance.

---

## Folder structure

```
claude-knowledge/
├── README.md                           ← this file
├── universal/
│   ├── UNIVERSAL_DECISIONS.md          ← org-wide locked decisions — checked before every recommendation
│   ├── UNIVERSAL_LEARNINGS.md          ← org-wide learnings — updated after each governance session
│   └── STACK_REFERENCE.md              ← stack, tools, and accounts — extracted from PROJECT_STARTER_PACK
├── developer-os/
│   ├── PROJECT_STARTER_PACK_v4_1a.md  ← universal session starter — current version
│   └── RECURRING_TRIGGERS.md           ← trigger and gate prompt reference
├── build-os/
│   ├── BUILD_OS_SCOPING.md             ← governing document for all Build OS decisions
│   ├── MODULE_READINESS_MATRIX.md      ← gate confirmation — updated after every matrix review
│   └── ARCH_NOTE_7STAGE_BUILD_METHOD.md ← build methodology reference — 7-stage organ model
├── nre-01/
│   └── README.md                       ← NRE-01 specific governance docs — populated as needed
└── vix/
    └── README.md                       ← VIX specific governance docs — populated as needed
```

---

## How to reference files in Claude projects

Use raw GitHub URLs. Replace `main` with the correct branch if needed.

```
https://raw.githubusercontent.com/wietsmarais/claude-knowledge/main/universal/UNIVERSAL_DECISIONS.md
https://raw.githubusercontent.com/wietsmarais/claude-knowledge/main/build-os/BUILD_OS_SCOPING.md
https://raw.githubusercontent.com/wietsmarais/claude-knowledge/main/developer-os/PROJECT_STARTER_PACK_v4_1a.md
```

In Claude project instructions, direct Claude to fetch these URLs at session open
rather than relying on project knowledge uploads.

---

## Update discipline

| Trigger | Action |
|---------|--------|
| UNIVERSAL_DECISIONS.md updated in wietsmarais root repo | Copy updated file to universal/ and commit here |
| UNIVERSAL_LEARNINGS.md updated | Same — copy and commit |
| MODULE_READINESS_MATRIX.md updated | Copy to build-os/ and commit here |
| PROJECT_STARTER_PACK version bump | Copy new version to developer-os/ and commit here |
| New governance document approved | Add to correct folder and update this README |

**Commit message format:** `governance: update [filename] — [one-line reason]`

---

## Source of truth hierarchy

1. Individual project DECISIONS.md — project-level locked decisions  
2. `wietsmarais` root repo — source of truth for universal governance files  
3. This repo (`claude-knowledge`) — live mirror of universal governance for Claude project consumption  
4. Claude project knowledge uploads — session-level reference, may lag behind commits  

When files conflict, the wietsmarais root repo is authoritative.  
This repo should reflect the root repo within one session of any change.

---

## Related repos

| Repo | Purpose |
|------|---------|
| wietsmarais/wietsmarais | Root governance — source of truth for universal docs |
| wietsmarais/component-library | Reusable module library — SPEC.md files per module |
| wietsmarais/cursor-prompts | Cursor prompt library — private |
| wietsmarais/nre-01-core-platform | Nikari Real Estate primary platform |
| wietsmarais/vix-trading-journal | VIX Trading Journal |

---

*Repo created: 27 April 2026*  
*Governed by: Developer OS and Build OS project instructions*  
*Questions or corrections: open an issue in wietsmarais/wietsmarais*
