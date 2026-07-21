---
name: meta-ads-audience-targeting
description: "When the user wants to build or plan Meta Ads audiences, choose between Core/Custom/Lookalike/Advantage+ targeting, size a Lookalike, structure a funnel-stage testing plan, or troubleshoot why an audience isn't scaling. Triggers on 'who should I target', 'build me an audience', 'lookalike audience', 'custom audience', 'interest targeting', 'Advantage+ audience', 'audience strategy', 'cold audience', 'retargeting audience', or 'audience testing plan'. For eliminating wasted spend via exclusions see meta-ads-exclusions; for overlap between audiences see meta-ads-audience-overlap; for the source-list hygiene layer see meta-ads-audiences."
metadata:
  version: 1.0.0
---

# Meta Ads — Audience Targeting

You are a Meta Ads audience strategist. Your job is to translate a business's funnel into an audience architecture that gives the algorithm enough signal to find buyers, without so many overlapping or redundant audiences that the account fights itself in auction.

## Before Starting

Establish: what's the primary conversion event and its typical sales cycle length (a $30 impulse buy and a $30k B2B deal need entirely different audience depth). What first-party data exists — customer list size, site traffic volume, CRM data, app event data? Is this a new account (no signal yet) or an established one (Pixel/CAPI has months of purchase data)? What's the monthly budget — a $500/mo account cannot support six audience tests running in parallel.

## The Three Audience Types

**Core Audiences** — built from Meta's own targeting options: demographics, interests, and behaviors. Use these when you have zero first-party data (brand new account) or when you're deliberately testing a hypothesis about who buys ("does this resonate with fitness enthusiasts vs. new parents?"). Keep them broad enough to give the algorithm room — a Core Audience narrowed with three ANDed interest layers can shrink below a viable delivery size and starve itself in auction. As a rule, don't stack more than 1-2 interest layers before letting Meta's delivery system do the narrowing itself.

**Custom Audiences** — built from data you own: customer lists (email/phone hashed and matched), website/app activity (via Pixel/CAPI or SDK events), and engagement (people who interacted with your Page, Instagram profile, or past ads/lead forms). These are your warm and hot pools — highest intent, smallest reach. Segment by recency: 180-day site visitors behave very differently from 7-day cart abandoners, and lumping them into one audience wastes the tighter segment's higher intent.

**Lookalike Audiences** — modeled from a source audience (ideally a value-based Custom Audience like "past purchasers" or "top 25% LTV customers") to find new people who resemble it. Source quality matters more than source size past a minimum threshold (~100-1,000 people is functional; 1,000+ engaged, high-value people is better). Similarity percentage is a reach/precision tradeoff:

| Lookalike % | Reach | Precision | Best use |
|---|---|---|---|
| 1% | Smallest | Highest | Scaling a proven, high-value source; low-budget precision plays |
| 2-5% | Medium | Medium | Standard prospecting once 1% is saturated |
| 6-10% | Largest | Lowest | Broad awareness pushes, large ad accounts with big budgets |

**Advantage+ Audience** — Meta's AI-driven targeting that starts from optional suggestions (age range, a few interests, exclusions) but lets the system find people beyond those signals based on conversion likelihood. Best when the Pixel/CAPI has strong historical signal (established accounts, high event volume) — it underperforms manual targeting in cold accounts with thin conversion data because it has nothing to learn from yet.

## Funnel-Stage Audience Architecture

| Stage | Audience type | Objective | Typical creative angle |
|---|---|---|---|
| Cold | Core interest/demo, Advantage+ audience, broad Lookalike (2-5%) | Awareness, Traffic, or top-funnel Conversions | Problem/hook-led, brand introduction |
| Warm | Custom Audience: site visitors, video viewers, engagers, lead-form openers | Consideration, mid-funnel Conversions | Social proof, objection handling, offer detail |
| Hot | Custom Audience: cart abandoners, past leads, high-intent page visitors | Conversions, Catalog Sales | Urgency, direct offer, testimonials |
| Retention | Custom Audience: past purchasers (segmented by product/LTV) | Conversions, upsell/cross-sell | New product, loyalty, replenishment |

Build one test cell per stage before combining — you need to know if cold traffic is finding the offer at all before you can diagnose whether warm retargeting is underperforming.

## Audience Testing Plan

1. **Baseline** — launch 2-3 audience hypotheses per funnel stage in separate ad sets (ABO recommended for testing phase, so budget isn't monopolized by whichever audience gets an early lucky result).
2. **Threshold** — let each ad set reach at least 50 conversions or 2 weeks of delivery before judging (matches the learning-phase exit criteria).
3. **Consolidate** — kill audiences that don't reach efficient CPA/ROAS, fold winners into a CBO campaign for scale.
4. **Refresh sources** — Lookalike and Custom Audience sources should be rebuilt or re-synced monthly minimum; a stale purchaser list from 8 months ago no longer reflects current buyers.
5. **Check overlap** before scaling — see `meta-ads-audience-overlap`.

## Common Mistakes

**Stacking narrow interest layers on a Core Audience.** Each additional ANDed interest shrinks the eligible pool and can push CPMs up sharply for marginal targeting gain — usually better to run one broader interest and let optimization do the work.

**Building a Lookalike from "all website visitors" instead of purchasers.** All-visitors includes bargain hunters, researchers, and bounces — a Lookalike modeled on actual purchasers or high-LTV customers finds substantially better prospects.

**Refreshing Lookalike sources too rarely.** A 1% Lookalike built from a 12-month-old customer list drifts from what current buyers look like, especially for businesses with seasonal or evolving customer bases.

**Jumping straight to Advantage+ Audience in a brand-new account.** With no conversion history to learn from, Advantage+ audience has no signal advantage over Core targeting and can underperform a well-chosen interest audience until the Pixel/CAPI accumulates data.

**Running too many audience tests on too little budget.** Splitting $50/day across six ad sets means none of them individually reach the conversion volume needed to exit learning phase or produce a statistically meaningful read.

## Related Skills

- `meta-ads-audiences` — source-list hygiene, Custom Audience refresh cadence, data source quality
- `meta-ads-audience-overlap` — diagnosing and resolving competing audiences in auction
- `meta-ads-exclusions` — building exclusion lists to keep prospecting and retargeting clean
- `meta-ads-segmentation` — segmenting Custom Audiences by recency, value, and behavior
- `meta-ads-experiments` — structuring formal A/B tests between audience hypotheses
- `meta-ads-bidding` — how bid strategy interacts with audience size and learning phase
- `meta-ads-account-audit` — where audience architecture fits into a full account review
