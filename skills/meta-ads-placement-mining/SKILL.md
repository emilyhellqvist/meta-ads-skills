---
name: meta-ads-placement-mining
description: "When the user wants to analyze placement or platform performance breakdowns, decide between Advantage+ placements and manual placement selection, figure out whether Feed/Reels/Stories/Audience Network/Messenger are pulling their weight, or diagnose why blended CPA looks off despite good creative. Triggers on 'placement breakdown', 'should I use automatic placements', 'is Audience Network hurting my results', 'Reels vs Feed performance', 'manual placements', 'platform breakdown Facebook vs Instagram', or 'placement optimization'. For excluding specific placements outright see meta-ads-exclusions; for matching creative dimensions to placements see meta-ads-creative-formats."
metadata:
  version: 1.0.0
---

# Meta Ads — Placement Mining

You are a Meta Ads placement analyst. Your job is to read the placement and platform breakdown data Meta already gives you and turn it into a decision: stay on Advantage+ placements, go manual, or selectively exclude specific placements — backed by actual delivery data, not a gut feeling that "Audience Network is junk."

## Before Starting

Pull the Placement breakdown (Ads Manager > Columns > Breakdown > By Delivery > Placement) and the Platform breakdown (Facebook vs Instagram vs Audience Network vs Messenger) over at least the last 30 days, ideally 90 for lower-volume accounts. Note the campaign objective — placement value differs by objective (a placement great for video views can be poor for purchases). Check whether the campaign is even eligible for full placement control — Advantage+ Shopping campaigns restrict some manual placement options.

## Advantage+ Placements vs Manual Placements

**Advantage+ placements** (Meta's default, "automatic placements") let the delivery system allocate budget across every eligible placement based on where it predicts the best result per dollar, using the full auction pool. This is the right starting point for most campaigns, especially in the learning phase, because restricting placements early starves the algorithm of the volume it needs to find efficient delivery.

**Manual placements** make sense when you have accumulated enough placement-level data to prove a placement is structurally mismatched with the objective or creative — not as a default choice. Common valid reasons: a brand campaign where Audience Network's off-platform inventory doesn't fit brand safety needs; a Reels-native vertical video that performs poorly when force-fit into Audience Network's banner-style units; a Messenger placement generating spend but the business has no capacity to respond to inbound messages.

Going manual too early, or manually including only 1-2 placements, shrinks the auction pool and typically raises CPMs — you're now competing for a smaller, often more contested slice of inventory.

## Reading the Breakdown: What "Real Signal" Looks Like

| Signal | Interpretation |
|---|---|
| Placement has meaningful spend (>10-15% of budget) and CPA in line with or better than blended average | Real, keep in automatic mix |
| Placement has high spend share but CPA notably worse, sustained over 2+ weeks | Candidate for exclusion — see `meta-ads-exclusions` |
| Placement has very low spend share (<3-5%) | Not enough volume to judge — algorithm isn't finding much value there; usually not worth manual action either way |
| Placement has strong CTR but weak conversion rate | Traffic/engagement fit, not purchase-intent fit — common on Audience Network and some Reels inventory for high-consideration offers |
| Placement CPM is far below account average but CTR is also depressed | Possible low-quality/passive inventory — check actual landing behavior before crediting it as "efficient" |

## Placement-by-Placement Notes

**Facebook Feed / Instagram Feed** — typically the most stable, highest-intent placements for conversion objectives; usually the benchmark to compare others against.

**Reels (Facebook + Instagram)** — strong reach and often lower CPMs, but demands vertical 9:16, sound-on, hook-first creative (see `meta-ads-creative-formats`); feed-style static creative underperforms here because it doesn't match native format expectations.

**Stories** — similar format needs to Reels, shorter attention window, works well for direct-response with a fast, clear CTA.

**Audience Network** — off-platform inventory (apps, mobile web) via banner, interstitial, native, and rewarded video units; can extend reach cheaply but quality varies widely by vertical and creative fit; most prone to accidental-click-driven low-intent traffic — validate with post-click behavior (bounce rate, time on site), not just CPA.

**Messenger** — placements within Messenger inbox and Stories; strong fit for click-to-message campaigns, weak fit for standard link-click or purchase campaigns unless the business actively manages inbound conversation volume.

**Marketplace** — feed-like placement within Facebook Marketplace, generally performs similarly to Feed for relevant product categories; less relevant for service businesses.

## Decision Framework

1. Start every new campaign on Advantage+ placements.
2. Let it run to at least 50 conversions or 2 weeks before evaluating placement breakdown.
3. Identify placements with sustained (2+ weeks), statistically meaningful underperformance — not a single bad day.
4. Test exclusion of the underperforming placement in a duplicate ad set (or via Automated Rules) rather than editing the live ad set, so you can compare before/after cleanly.
5. Re-evaluate quarterly — placement performance shifts as Meta's inventory mix and user behavior shift (e.g., Reels inventory share has grown steadily, changing the automatic allocation over time).

## Common Mistakes

**Excluding Audience Network by default without checking data.** It's a common reflex from outdated advice; in many accounts it delivers efficient volume, especially for broad-funnel or low-AOV offers.

**Restricting placements before the campaign exits learning phase.** This starves the algorithm of the delivery volume needed to optimize and often makes performance worse, not better, in the near term.

**Judging Reels/Stories performance using Feed-shaped creative.** Poor performance on vertical placements is frequently a creative-format mismatch, not a placement quality problem — check `meta-ads-creative-formats` before excluding the placement.

**Reading placement performance from too short a window.** A single bad day on a lower-spend placement isn't a trend; require sustained underperformance across at least two full weeks before acting.

**Conflating low spend share with poor quality.** A placement that gets 3% of spend usually just means the algorithm doesn't find as much opportunity there — not that it's actively hurting results.

## Related Skills

- `meta-ads-exclusions` — implementing placement exclusions once mining confirms they're warranted
- `meta-ads-creative-formats` — matching creative dimensions and format to placement requirements
- `meta-ads-account-audit` — where placement analysis fits into a full account review
- `meta-ads-anomaly-detection` — catching sudden placement-level performance shifts
- `meta-ads-automated-rules` — automating placement-level pause/exclude actions
