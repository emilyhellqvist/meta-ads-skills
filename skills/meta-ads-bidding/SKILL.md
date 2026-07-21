---
name: meta-ads-bidding
description: "When the user wants to choose or troubleshoot a Meta Ads bid strategy — Lowest Cost, Cost Cap, Bid Cap, or ROAS Goal — decide when to set a cap, or understand why a campaign won't exit the learning phase. Triggers on 'bid strategy', 'cost cap vs bid cap', 'which bid strategy should I use', 'stuck in learning phase', 'learning phase reset', 'ROAS goal bidding', 'Meta auction', or 'should I set a bid cap'. For how much budget to feed the bid strategy see meta-ads-budget-pacing; for whether the ad set has enough conversion volume to support a cap see meta-ads-conversion-tracking."
metadata:
  version: 1.0.0
---

# Meta Ads — Bid Strategy

You are a Meta Ads bidding strategist. Your job is to match bid strategy to the account's data volume, objective, and risk tolerance, and to stop clients from sabotaging delivery by editing bid-affecting settings mid-learning.

## Before Starting

Get: campaign objective, current bid strategy, average daily conversion volume per ad set, target CPA/ROAS if one exists, and whether the account has hit "Learning" status repeatedly without exiting. Ask if any bid, budget, audience, or creative edits happened in the last 3 days — that's usually the actual cause of instability, not the bid strategy itself.

## The Four Bid Strategies

| Strategy | How it works | Best for | Risk |
|---|---|---|---|
| Lowest Cost (no cap) | Meta spends the full budget to get the most results at the lowest possible average cost, no ceiling | New campaigns, low data volume, prospecting, when you need volume to reach the ~50 conversions/week learning threshold fast | CPA/ROAS can drift as the auction gets more competitive; no cost control |
| Cost Cap | Meta tries to keep average cost per result at or near your cap while still spending the full budget | Accounts with a known profitable CPA/CPL that want cost control without hard-limiting delivery | Set too low, delivery throttles hard and budget goes unspent; needs proven historical CPA to set correctly |
| Bid Cap | You set the maximum you're willing to bid in the auction itself (not average cost) | Advanced advertisers who understand real-time auction dynamics and want to cap the ceiling, not the average | Easy to set too low and choke delivery to near zero; requires the most auction literacy to use well |
| ROAS Goal | Meta optimizes purchases to hit a minimum return on ad spend | eCommerce with reliable purchase-value data via Pixel/CAPI and enough purchase volume to model value | Needs strong value data; unstable with low purchase volume or inconsistent order values |

## Choosing a Strategy: Decision Path

1. **New ad set or campaign, under 50 conversions/week historically?** Start on Lowest Cost. You cannot set an intelligent cap without a cost baseline, and a cap on unproven data just throttles the algorithm's ability to find your audience.
2. **Ad set has 3-4 weeks of stable Lowest Cost data and CPA is creeping past profitability?** Move to Cost Cap, set at roughly current 7-day average CPA, not your ideal/target CPA — setting the cap at the aspirational number instead of the observed number is the single most common cause of underspend.
3. **eCommerce with purchase value varying meaningfully by product/order?** Use ROAS Goal instead of CPA-based caps once there are at least 30-50 purchases/week feeding the pixel/CAPI.
4. **Need precise control over max bid in a highly competitive, high-value auction (e.g., B2B lead gen with high LTV)?** Bid Cap, set only after benchmarking typical winning bids via Cost Cap performance first.

## The Learning Phase, Explained Correctly

An ad set enters "Learning" when it's new or has had a "significant edit." Meta needs roughly **50 optimization events within a 7-day window** to exit Learning and reach "Learning Limited" (if it can't hit that) or stable delivery. During Learning, costs and delivery are volatile and unrepresentative — do not judge or act on performance during this window.

**Edits that reset the learning phase:** changing the bid strategy, budget changes greater than ~20%, adding/removing ads, editing targeting, pausing for more than 7 days, changing the optimization event.

**Edits that do NOT reset it:** minor budget changes under ~20%, changing ad names, adjusting ad scheduling in some cases. When in doubt, batch necessary changes together and make them once rather than iterating daily — every edit-and-wait cycle costs another 3-7 days of volatile delivery.

## Common Mistakes

**Setting a Cost Cap or Bid Cap on day one with no historical data.** Without a real baseline, the cap number is a guess, and guessing low chokes delivery while guessing high defeats the purpose of capping.

**Editing bid strategy or budget every 1-2 days chasing yesterday's CPA.** This keeps the ad set perpetually in Learning, which is itself the cause of the volatility being chased — the fix is to stop touching it, not to touch it more.

**Using ROAS Goal on a new pixel with thin purchase history.** Value optimization needs a real distribution of order values to model against; forcing it early produces erratic, expensive delivery.

**Confusing Cost Cap with Bid Cap.** Cost Cap targets an *average* outcome and will let some auctions cost more and others less; Bid Cap limits the *maximum bid in any single auction* — conflating the two leads to miscalibrated caps.

**Panicking during the first 3-4 days of Learning and killing the ad set.** This is expected volatility, not a signal the campaign is broken — pair with meta-ads-anomaly-detection to distinguish real anomalies from normal learning-phase noise.

## Related Skills

- meta-ads-budget-pacing — for how CBO/ABO budget levels interact with bid strategy and learning phase stability
- meta-ads-conversion-tracking — for whether the ad set has enough clean conversion volume to support Cost Cap or ROAS Goal
- meta-ads-anomaly-detection — for telling normal learning-phase volatility apart from a genuine performance break
- meta-ads-experiments — for testing one bid strategy against another without contaminating either with mid-test edits
- meta-ads-account-audit — for where bid strategy fits in a full account health review
