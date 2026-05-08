# Founder Endorsed — Advisory Pivot

**Date:** 2026-05-08
**Author:** Yan + Claude
**Status:** Approved

## Goal

Pivot `founderendorsed.co.uk` from a productized £99/£149/£349 AI business plan reviewer to a **bespoke 1:1 advisory** service for UK Innovator Founder Visa applicants. CTA = book a free 30-min discovery call. Engagements quoted per-client after the call, with "from £499" as a single inline anchor.

## Decisions captured

| Decision | Choice |
|---|---|
| Service model | Bespoke advisory engagements, quoted per client |
| Authority/positioning | Rejected-then-endorsed founder |
| Primary CTA | Free 30-min discovery call → Calendly |
| Pricing display | One headline anchor only ("from £499") |
| Brand | Keep "Founder Endorsed". Tagline shifts to "Innovator Founder Visa Advisory" |
| Calendly link | `https://calendly.com/hello-founderendorsed/30min` |

## Services to advertise

1. **Plan review & brainstorming** — pressure-test against the 29-question UKES rubric, rebuild weak sections together.
2. **Endorsing body strategy** — pick the right body (UKES, Envestors, Innovator International) and tailor the plan.
3. **Interview & rejection rebuild** — mock interviews; rejected-applicant rebuild service.
4. **Post-endorsement advisory** — quarterly check-ins for 12/24/36-month visa milestones.

## Page architecture

| # | Section | Background | Purpose |
|---|---|---|---|
| 1 | Nav | Dark | Logo + single "Book a call" button |
| 2 | Hero | Dark | Personal hook + Calendly CTA + price anchor |
| 3 | Founder story | Warm | Rejected→endorsed narrative |
| 4 | Services (4-up) | Warm | The four offerings as cards |
| 5 | How we work | Dark | 3-step: discovery call → scope+quote → delivery |
| 6 | FAQ | Light | Advisory-relevant Qs |
| 7 | From abroad | Warm | Existing 2×2 grid, copy lightly tuned |
| 8 | Final CTA | Dark | Calendly button |
| 9 | Footer | Dark | Standard |

## Copy direction

### Hero
- **H1:** *"I got rejected. Then endorsed."*
- **Sub:** *"Now I help Innovator Founder Visa applicants skip the same traps. Bespoke 1:1 advisory — plan review, endorsing body strategy, interview prep, and post-endorsement support."*
- **Primary CTA:** *"Book a free 30-min call"* → Calendly link
- **Inline anchor (only place pricing appears):** *"Engagements from £499. Scoped after the call."*
- **Trust strip:** UKES rubric specialism · Works with abroad applicants · Built from a rejected-then-endorsed plan

### Services panel — sample copy

- **Plan review & brainstorming** — "You bring a draft. We pressure-test it against the 29-question UKES rubric, rebuild weak sections together, and sharpen the innovation, viability, and scalability story."
- **Endorsing body strategy** — "Pick the right body (UKES, Envestors, Innovator International) for your business and tailor the plan to how *they* score."
- **Interview & rejection rebuild** — "Mock endorsement interviews against likely questions. If you've been rejected, we reverse-engineer the rejection letter and rebuild for resubmission."
- **Post-endorsement advisory** — "Quarterly check-ins for the 12, 24, and 36-month visa milestones — job creation, investment, growth proof."

### How we work — 3 steps
1. **Free 30-min call.** You walk me through your business and stage. No prep needed.
2. **Scope & quote.** Written scope, fixed quote. You decide.
3. **Delivery.** Async work plus working sessions until done.

### FAQ
- Is this a replacement for an immigration lawyer? — *No. We work on your business plan and endorsement strategy, not legal advice.*
- What does an engagement look like? — *Most engagements run 1–4 weeks, mixing async work and 1–2 working sessions.*
- Can you help if I've been rejected? — *Yes — rejected-applicant rebuilds are one of the most common engagements.*
- Do you work with applicants outside the UK? — *Yes. Calls run on Zoom or Google Meet.*
- Is my plan kept confidential? — *Yes. Never shared, never used for marketing.*
- Will you write my plan from scratch? — *No. The plan has to be yours — I help you make yours one that gets endorsed.*
- What does pricing look like? — *Engagements start from £499 for tight-scope reviews. Each engagement is quoted after the call.*

## Removed from current page

- 5-step onboarding wizard (steps 1, consult-branch, 2, 3, 4, tier, 5)
- 3-tier Stripe pricing block (£99 / £149 / £349)
- "What report includes" section
- All Stripe Payment Link logic, thank-you screens, Formspree submission
- AI-report / report-generation language throughout

## Preserved

- Google Ads `gtag` config (`AW-18006245330`) and `trackEvent(...)` calls on every CTA — conversion attribution must keep firing
- Design system tokens (`:root`), font stack, section background classes
- "From abroad" 2×2 grid layout (copy lightly tuned)
- Footer

## SEO updates

- `<title>`: *Founder Endorsed — Innovator Founder Visa Advisory*
- Meta description: bespoke advisory, free 30-min call, from £499
- OG title/description match
- JSON-LD `Service` schema: simplified to single offer, advisory-flavoured description
- JSON-LD `FAQPage`: replaced with new advisory FAQ entries

## Implementation method

1. Surgical edits to `index.html` (preserve diff readability and tracking)
2. Strip wizard markup + JS in dedicated commit-ready blocks
3. Use chrome-devtools MCP to render and screenshot at desktop (1280) and mobile (390) widths
4. Iterate edit → screenshot until layout is clean
5. Devil's advocate review of full diff before declaring done

## Risk flags

- **"Rejected then endorsed"** is a factual claim. Yan must confirm endorsement status is accurate before publishing. If not yet endorsed, soften to "rejected then rebuilt".
- **Tracking removal risk** — wizard removal touches a large `<script>` block. Verify Google Ads `gtag` block at the top of `<head>` and `trackEvent` calls on the new CTAs remain intact.
- **No testimonials / case studies** — credibility rests entirely on the founder story. If conversion suffers, revisit with anonymised case studies (with consent).

## Out of scope

- Worker / Cloudflare backend changes (`worker/` directory remains; not deployed against this site after pivot)
- Domain or DNS changes
- New brand / logo work
- Adding case studies (deferred until consent obtained)

## Pre-publish verification checklist (Yan)

1. **Confirm endorsement status.** Hero H1 says *"I got rejected. Then endorsed."* If endorsement isn't literal, change to *"I got rejected. Then I rebuilt."* before publishing.
2. **Reconfigure Google Ads conversion goals.** Conversion IDs `YXM8CMmF_IUcENL_hYpD` and `yj1iCPKryoYcENL_hYpD` previously fired on payment events. They now fire on discovery-call clicks. Re-define them in Google Ads or expect inflated numbers.
3. **Spot-check mobile hero at ≤320px** (small Android). H1 uses a hard `<br>`; if wrap looks broken, drop the `<br>` from `index.html`.
4. **Verify the Q1 2022 refusal stats** in the abroad section — pre-existing copy, but still load-bearing on a paid-traffic page.

## Tech debt (post-pivot follow-up)

- ~600 lines of dead CSS in `index.html` for the removed wizard (`.tool-section`, `.wizard-progress`, `.radio-card`, `.tier-card`, `.consult-card`, `.glass-input-card`). Harmless but bloats the file. Clean in a separate commit.
- `worker/` directory still contains AI-report generation backend. Not deployed against this site post-pivot — archive or delete.
