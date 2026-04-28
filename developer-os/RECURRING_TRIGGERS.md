# Recurring Triggers — Calendar Setup
**Set these up once. They run forever.**
**These are the things Claude cannot remind you about — set them in your calendar now.**

---

## Monthly — first of every month

**Calendar event:** "Dev OS — Monthly Maintenance Check"
**Duration:** 15 minutes
**Recurrence:** Monthly, 1st of every month

**What to do:**
Open Developer OS Claude project and paste prompt I04 from
CURSOR_AGENT_PROMPT_LIBRARY.md Section I.

Claude will check:
- Supabase usage against Pro plan limits
- Whether API key rotation is due
- npm audit on active projects
- Any unfulfilled extraction candidates older than 30 days

**Why it cannot be automated:**
Supabase has no granular alert system. npm audit requires running in the repo.
Key rotation requires your judgment. These four things need a human to trigger them.
15 minutes once a month is the minimum viable maintenance cadence.

---

## Every 90 days — API key rotation

**Calendar event:** "API Key Rotation — All Projects"
**Duration:** 30 minutes
**Recurrence:** Every 90 days from project creation date

**Keys to rotate:**
- Anthropic API key (`ANTHROPIC_API_KEY`)
- Supabase service role keys (one per project)
- Stripe secret key (`STRIPE_SECRET_KEY`)
- Helicone API key (`HELICONE_API_KEY`)
- Any other API keys in active Vercel projects

**Process for each key:**
1. Generate new key in the provider dashboard
2. Update in Vercel → Project → Settings → Environment Variables
3. Trigger a redeploy in Vercel to pick up the new key
4. Confirm the old key is revoked in the provider dashboard
5. Update the rotation date in UNIVERSAL_DECISIONS.md

**Note:** Do not rotate all keys on the same day if avoidable —
stagger them so a rotation failure does not take everything down at once.

---

## Every sprint end — component library review

**Calendar event:** "Component Library — Extraction Review"
**Duration:** 20 minutes
**Recurrence:** Every two weeks (align with sprint cadence)

**What to do:**
1. Open each active project's `docs/decisions/LEARNINGS.md`
2. Check for any entries marked "Extraction candidates"
3. For each candidate older than two weeks — either extract it or explicitly
   decide not to and record why in LEARNINGS.md
4. If extracting: follow the extraction process in TEMPLATE_PROTOCOL.md Section D
5. Update `Component-library_README_final.md` and re-upload to Developer OS

**Why this matters:**
The component library only compounds if patterns are actually extracted.
This review is the forcing function. Without it, LEARNINGS.md fills with
candidates that never become reusable modules and the library stagnates.

---

## Before every production deployment

**Not a calendar event — a gate.**
Run prompt I05 (Pre-Launch Final Gate) from CURSOR_AGENT_PROMPT_LIBRARY.md
before any project goes to production.

This is not optional and not time-based — it fires at the moment of launch.
Paste it into the project Claude session. Every item must be confirmed.
Nothing deploys to production without this gate passing.

---

## On project completion or client handover

**Not a calendar event — an event trigger.**
When a project completes or a client handover occurs:

1. Run the full session close ritual (C11 from AI_BUILD_GUARDRAILS.md)
2. Run I05 (Pre-Launch Final Gate) if not already done
3. Run I02 (Extraction Candidate Check) across the entire project — not just the last session
4. Update active projects in DEVELOPER_PROFILE_09042026.md
5. Re-upload developer profile to Developer OS project knowledge
6. Archive the project's Claude project (do not delete — archive)

---

## Summary — what goes in your calendar right now

| Event | Frequency | Duration |
|-------|-----------|----------|
| Dev OS Monthly Maintenance (I04) | Monthly — 1st of month | 15 min |
| API Key Rotation | Every 90 days | 30 min |
| Component Library Extraction Review | Every 2 weeks | 20 min |

Set these three events now before closing this session.
They are the only recurring commitments the system requires of you.
Everything else is triggered by events (session open, session close, launch, handover).

---

*This file lives in Developer OS project knowledge.*
*It does not need to be in any repo — it is a reminder for the founder, not the agent.*
*Last updated: April 2026*
