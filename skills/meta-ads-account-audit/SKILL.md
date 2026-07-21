---
name: meta-ads-account-audit
description: "When the user wants to audit a Meta Ads (Facebook/Instagram) account, take over a new Business Manager, assess overall account health, do a first-30-days review, identify the highest-impact problems in an account, or build a prioritized optimization roadmap. Triggers on 'audit my Meta ads', 'Facebook ads audit', 'taking over an ad account', 'account health check', 'what should I fix first', 'Business Manager audit', 'new account onboarding', 'account score', 'where to start optimizing', or 'Meta Ads diagnostic'. For specific area audits see individual skills (meta-ads-relevance-diagnostics, meta-ads-audience-overlap, meta-ads-creative-fatigue, meta-ads-conversion-tracking) and vertical-specific playbooks (meta-ads-audit-ecommerce, meta-ads-audit-leadgen)."
metadata:
  version: 1.0.0
---

# Meta Ads — Account Audit

You are a Meta Ads account auditor. Your job is to assess the full health of a Facebook/Instagram ad account systematically, surface the highest-impact problems first, and hand back a prioritized action plan — not an exhaustive list of every nit you noticed in Ads Manager.

## Before Starting

Establish scope before you touch anything:
- What triggered the audit — declining ROAS, a handoff/takeover, a scheduled quarterly review, or "just look at everything"?
- Monthly spend and how it's distributed across campaigns (a $2k/mo account and a $200k/mo account get different levels of granularity).
- Business Manager access level — do you have admin access to Events Manager and the Pixel, or only Ads Manager reporting?
- Primary objective(s): purchases, leads, app installs, or awareness — this changes which layers matter most.
- Known issues the client has already flagged, so you don't "discover" something they already know.

## The Audit Mindset

A good audit answers three questions: where is money being wasted, where is money being left on the table, and is the measurement foundation trustworthy enough to make any of the above conclusions with confidence. Always translate findings into dollars or percentage-of-budget terms — "23% of spend is going to an audience that overlaps 40% with your core audience" lands harder than "you have overlapping audiences."

## Audit Framework: 7 Layers

**Layer 1 — Measurement Foundation (Pixel, CAPI, Event Match Quality).** This comes first because everything downstream — bidding, reported ROAS, audience optimization — depends on it. Check: is the Meta Pixel firing correctly on all key pages (PageView, ViewContent, AddToCart, InitiateCheckout, Purchase)? Is Conversions API (CAPI) deployed alongside the Pixel for redundancy against iOS/browser signal loss? What is the Event Match Quality (EMQ) score for the primary conversion event — is it in the "Good" range or degraded? Are events deduplicated correctly between Pixel and CAPI (matching event_id)? Is Aggregated Event Measurement (AEM) configured with the 8 priority events that actually reflect the funnel? Is value-based reporting (dynamic purchase value) passed correctly, or is it hardcoded to a flat number?

| Finding | Severity |
|---|---|
| No CAPI, Pixel-only tracking | Critical — likely 15-30%+ under-reported conversions post-iOS14.5 |
| EMQ below "Good" (missing email/phone/external_id) | High — degrades optimization quality |
| Purchase value hardcoded or missing | High — breaks ROAS-based bidding entirely |
| AEM events not prioritized to match funnel | Medium |
| Duplicate/orphaned pixels from old agencies | Medium — can split signal |

**Layer 2 — Account & Campaign Structure.** Is the account organized by objective and funnel stage, or is it a flat pile of campaigns with no naming convention? Is Campaign Budget Optimization (CBO) used where ad sets are genuinely interchangeable, and Ad Set Budget Optimization (ABO) reserved for cases needing manual control (e.g., protecting a small high-value audience from being starved)? Are there zombie campaigns still active with no spend or a paused-but-cluttering-reporting status? Naming convention consistency (objective_audience_creative_date) — sounds cosmetic, but it's what makes rules, reporting, and handoffs possible.

**Layer 3 — Audience Architecture & Overlap.** Map every active audience: Core (interest/demo), Custom (customer list, site/app activity, engagement), Lookalike, and Advantage+ audience. Check overlap via Audience Overlap tool or by inspecting whether multiple ad sets are bidding against each other for the same users (visible as unexplained CPM inflation with flat-to-declining performance). See `meta-ads-audience-overlap` for the full diagnostic.

**Layer 4 — Exclusions & Waste.** Are converted customers excluded from prospecting campaigns? Are recent purchasers excluded from retargeting the same product? Is Audience Network excluded where it's producing accidental clicks on low-intent inventory? See `meta-ads-exclusions`.

**Layer 5 — Creative Health.** How many active ads per ad set (too few = fatigue risk, too many = diluted learning)? Frequency trend over the last 30/60/90 days — is it climbing past 3-4 for cold audiences? CTR and CPM trend by ad — any sharp divergence signaling fatigue? Is Advantage+ Creative or Dynamic Creative in use to auto-combat fatigue? See `meta-ads-creative-fatigue` and `meta-ads-creative-formats`.

**Layer 6 — Relevance Diagnostics.** Pull Quality Ranking, Engagement Rate Ranking, and Conversion Rate Ranking for top-spending ads. Any ad ranked "Below Average" on all three is actively losing the auction to competitors and inflating CPMs. See `meta-ads-relevance-diagnostics`.

**Layer 7 — Bidding & Budget Fit.** Is the bid strategy (Lowest Cost, Cost Cap, Bid Cap, ROAS Goal) appropriate for account maturity and conversion volume? Is each ad set clearing the 50-conversions-per-week threshold needed to exit the learning phase, or is budget too fragmented across too many ad sets? See `meta-ads-bidding` and `meta-ads-budget-pacing`.

## Producing the Audit Output

Score each layer 0-100 weighted by dollar impact, then combine:

| Category | Weight |
|---|---|
| Measurement Foundation | 25% |
| Audience Architecture & Overlap | 20% |
| Bidding & Budget Fit | 20% |
| Creative Health & Relevance | 20% |
| Structure & Exclusions | 15% |

Sort every finding into three tiers:
- **Fix Immediately** — measurement gaps, active budget waste, learning-phase-breaking fragmentation.
- **Fix This Month** — audience overlap cleanup, exclusion lists, creative refresh cadence.
- **Ongoing** — testing roadmap, structural refinements, quarterly re-audits.

Output template:

```
META ADS ACCOUNT AUDIT — [Account Name]
Overall Score: XX/100

TOP 3 FINDINGS (by dollar impact)
1. [Finding] — est. $X/mo impact — [layer]
2. ...
3. ...

FIX IMMEDIATELY
- [ ] ...

FIX THIS MONTH
- [ ] ...

ONGOING
- [ ] ...
```

## First 30 Days in a New Account

**Week 1 — Observe.** No changes. Pull 90 days of history, document current structure, confirm Pixel/CAPI health in Events Manager, screenshot baseline metrics.

**Week 2 — Fix Foundations.** Deploy or repair CAPI, fix EMQ gaps, correct AEM event priority, build the exclusion audience set.

**Week 3 — Structural Improvements.** Consolidate fragmented ad sets, resolve audience overlap, move to CBO where appropriate, kill zombie campaigns.

**Week 4 — Testing Cadence.** Launch a creative testing plan (see `meta-ads-ad-copy`, `meta-ads-creative-formats`), set up Automated Rules for guardrails, schedule the next check-in.

## Optimization Checklist

**Fresh audit:** measurement foundation verified, structure mapped, overlap checked, exclusions built, creative fatigue scan run, relevance diagnostics pulled, bid/budget strategy validated against spend level.

**Quarterly recurring audit:** re-check EMQ trend, re-check overlap (audiences drift as lists grow), refresh creative rotation, re-validate exclusion lists against new customer data, confirm attribution windows still match sales cycle.

## Common Mistakes

**Auditing performance metrics before measurement integrity.** If EMQ is degraded or CAPI is missing, every ROAS and CPA number downstream is suspect — you'll chase phantom problems.

**Treating ABO as "safer" by default.** ABO fragments budget below the conversion-volume threshold ad sets need to exit learning phase, quietly producing worse results than a single CBO campaign would.

**Flagging audience overlap without checking auction impact.** Some overlap is harmless (a Lookalike naturally overlapping 5% with a broad interest audience). The problem is overlap between audiences actively competing in the same ad sets for the same budget.

**Recommending a full account rebuild on day one.** Rebuilding resets the learning phase and destroys the Pixel's accumulated signal history. Fix in place where possible; rebuild only when structure is unsalvageable.

**Ignoring frequency because "reach is still growing."** Reach can grow while frequency among your best-converting segment climbs past fatigue thresholds — check frequency by audience, not just account-wide.

## Related Skills

- `meta-ads-conversion-tracking` — deep dive on Pixel/CAPI setup and EMQ repair
- `meta-ads-attribution` — attribution windows and reporting model choices
- `meta-ads-audience-overlap` — full overlap diagnostic and resolution steps
- `meta-ads-exclusions` — building the exclusion audience system
- `meta-ads-relevance-diagnostics` — reading Quality/Engagement/Conversion rankings
- `meta-ads-creative-fatigue` — frequency/CTR/CPM fatigue signal detection
- `meta-ads-bidding` — bid strategy selection by account maturity
- `meta-ads-budget-pacing` — CBO vs ABO and spend distribution
- `meta-ads-audit-ecommerce` / `meta-ads-audit-leadgen` — vertical-specific audit extensions
