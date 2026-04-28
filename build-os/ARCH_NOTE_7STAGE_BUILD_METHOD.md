# Architecture Note — 7-Stage Build Methodology
# claude-knowledge/build-os/ARCH_NOTE_7STAGE_BUILD_METHOD.md
# Version: 1.0 — 27 April 2026
# Status: Reference — not yet adopted as Developer OS standard
# Produced from: External brainstorm session (Google AI, April 2026)
# Reviewed by: Claude (Build OS S2 session, 27 April 2026)
# Decision required before adoption: Review against Developer OS build discipline at Phase 2 scoping

---

## Status of This Document

This is a reference architecture note, not a locked governance standard.
The 7-stage framework below is derived from an external brainstorm session
and has been reviewed for compatibility with the Developer OS build discipline.

It is compatible with and reinforces the Developer OS approach.
It is not adopted wholesale — the Developer OS already has its own build
discipline, approval tier model, and session structure. This note is
preserved for reference because the modular "organ" metaphor and the
staged gating approach both validate and extend existing practices.

**Decision required before adoption as a formal standard:**
Review against Developer OS project standards at Phase 2 Build OS scoping.

---

## The 7-Stage Build Framework

The framework defines seven sequential stages for AI-assisted development.
Each stage has a defined scope and a hard gate before the next stage opens.
No stage is skipped. No stage begins before the previous is approved.

| Stage | Analogy | Technical Name | Scope | Output |
|-------|---------|---------------|-------|--------|
| 1 | The Spine | Schema and Interface Definition | Types, interfaces, database schemas. No logic. | TypeScript interfaces, DB schemas, API types |
| 2 | The Index | System Scaffolding and Routing | Folder structure, empty stub files, navigation | File tree, stubs, routing |
| 3 | The Muscles | Core Logic and Business Rules | Functions, API handlers, algorithms | Working code — no UI |
| 4 | The Nervous System | Observability and Error Handling | Structured logging, try/catch, error boundaries | Error wrappers, logging |
| 5 | The Flesh | Component Assembly and State | UI components connected to logic | React components, state management |
| 6 | The Skin | Design System and UI Polish | CSS, Tailwind, animations, brand assets | Styled, responsive UI |
| 7 | The Immune System | Hardening and Testing | Unit tests, integration tests, security audit | Test suite, security checklist |

---

## Stage Line Limits

These are guidance limits — not hard code-length rules in the current
Developer OS — but they reflect good practice for AI-assisted sessions.

| Stage | Suggested Limit | Reason |
|-------|----------------|--------|
| Spine | 30–50 lines | Interfaces are dense — if longer, the module is too large |
| Index | 20–40 lines | Scaffolding only — logic in Stage 3 |
| Muscles | 100–150 lines per file | Heavy lifting — enforce 30-line function limit |
| Nervous System | 30–50 lines | Error handling should be a wrapper, not a system |
| Flesh | 100–150 lines per component | Break into sub-components if longer |
| Skin | 50–100 lines | Use global themes; avoid per-component CSS sprawl |
| Immune System | 100+ lines | Exception — tests are necessarily longer |

**The 30-line function rule:** No single function exceeds 30 lines.
If trending longer, break into smaller, named helper functions.
This applies to all stages — enforced most strictly in Stage 3.

---

## The Organ Architecture

The framework extends naturally to modular "organ" design.
Each feature module (Auth, Property Listing, Lead Capture) is built
separately through all 7 stages, then integrated via defined interfaces.

### Building separate organs

1. **Define the joint first.** Before building a module, define how it
   connects to the rest of the system. The joint is a TypeScript interface
   or schema that specifies inputs and outputs. This is Stage 1 for the
   joint, not the module itself.

2. **Build the organ in isolation.** Run all 7 stages for the module
   in isolation. The module should be testable independently — without
   the rest of the system connected.

3. **Attach surgically.** Once the organ is complete, import it into
   the main project and connect it to the joint defined in step 1.
   Stage 7 (Immune System) then checks that the body does not reject
   the new organ.

### Organ build order

Build in this sequence to avoid dependency problems:

1. Brain first (core engine — database, auth, shared types)
2. Torso second (global state, routing, layout)
3. Limbs after (features — property listings, lead forms, dashboards)

---

## How This Maps to Build OS

The 7-stage framework is compatible with Build OS in the following ways:

| Build OS concept | 7-stage equivalent |
|-----------------|-------------------|
| Module Readiness Matrix | Verifies the organ's Spine and Muscles exist before assembly |
| Build Plan — modules selected | Identifies which organs are being assembled this session |
| Build Manifest — files to create | Maps to Stage 2 (Index) output |
| Approval tier model | Maps to stage gates — each tier corresponds to a stage |
| Pre-session reads | Corresponds to reading the Spine before any Muscles are written |
| Session boundary rule | One organ (or one stage of an organ) per session |

Build OS does not replace the 7-stage framework. Build OS governs the
intake, selection, and approval process. The 7-stage framework governs
what Cursor does once the Build Plan is approved and execution begins.

---

## Gating Prompt for Cursor Sessions

When a Build Plan is approved and a Cursor session opens, the governed
system prompt should include:

```
We are building [module name] using a staged implementation protocol.

Stage [N] only. Do not proceed to Stage [N+1] until I give sign-off.

Stage [N] scope: [scope description from table above]
Line limit: [limit from table above]
Function limit: 30 lines maximum — break into helpers if longer.

At stage completion, state: "Stage [N] complete — ready for review."
Do not write any code beyond Stage [N] scope.
```

---

## Joints — Defining Connection Points

When building a new organ that connects to an existing system,
define the joint before writing any logic.

Prompt for joint definition:
```
We are building [organ name]. Before any logic, define the joint.
The joint is a TypeScript interface that specifies:
- What this module receives from the rest of the system (inputs)
- What this module returns to the rest of the system (outputs)
Do not write the module's internal logic yet — only the interface.
```

This prevents the "spaghetti" failure mode where a module reaches into
another module to grab what it needs, creating hidden dependencies.

---

## Session Strategy

| Stages | Session approach |
|--------|-----------------|
| 1–3 | Stay in one Cursor session — the conversation context helps the AI understand intent |
| 4–7 | Can refresh to a new session — the Spine, Index, and Muscles exist as files, giving the AI its "long-term memory" |

When a new session opens for Stages 4–7, the governed prompt should
include a reference to the relevant SPEC.md and setup.sql — not the
full conversation history.

---

## What This Is Not

This framework is not a replacement for:

- The Developer OS session structure and handover discipline
- The Build OS approval tier model and Build Plan requirement
- The Module Readiness Matrix gate
- The UNIVERSAL_DECISIONS.md check before every architectural recommendation
- The ChatGPT pre-commit review quality gate

It is a methodology that operates inside those governance structures.

---

## Future Decision Required

Before this framework is adopted as a formal Developer OS standard,
the following questions must be answered at Phase 2 Build OS scoping:

1. Does the 30-line function limit conflict with any existing DECISIONS.md entries?
2. Should the 7-stage language be added to the governed system prompt library?
3. Should the organ architecture be adopted as the standard module design pattern
   in the component library SPEC.md template?

These are not blockers for using this note as a reference. They are
required before any formal adoption.

---

*Version: 1.0 — 27 April 2026*  
*Status: Reference — not yet adopted as formal standard*  
*Source: External brainstorm session — distilled and reviewed*  
*Decision required before formal adoption: Phase 2 Build OS scoping*
