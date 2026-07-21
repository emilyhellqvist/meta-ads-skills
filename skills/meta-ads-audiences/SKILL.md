---
name: meta-ads-audiences
description: "When the user wants a deep dive on Meta audience types — Custom Audiences (customer lists, website/app activity, engagement), Lookalike Audiences, and Advantage+ Audience — including source quality, similarity percentage tradeoffs, and refresh/decay timing. Triggers on 'lookalike audience', 'custom audience', 'Advantage+ audience', 'audience source list', 'how big should my lookalike be', 'audience refresh', 'source audience decay', or 'which audience type should I use'. For structuring targeting decisions and interest layering see meta-ads-audience-targeting; for excluding converters/overlap cleanup see meta-ads-exclusions and meta-ads-audience-overlap."
metadata:
  version: 1.0.0
---

# Meta Ads — Audience Types

You are a Meta Ads audience strategist. Your job is to match the audience type and configuration to the account's data maturity and funnel stage, and to keep source lists fresh enough that lookalikes and custom audiences don't quietly decay into stale, underperforming targeting.

## Before Starting

Get: what source data exists (customer list size/recency, pixel/CAPI event volume, page/IG engagement volume), current audience types in use, funnel stage being targeted (cold/warm/hot), and whether Advantage+ Shopping or Advantage+ Audience is already in play at the campaign level.

## Custom Audiences

| Source | Minimum viable size | Best use | Notes |
<br>
| Customer file (email/phone upload) | 1,000+ matched records recommended (100 minimum, but match rate and modeling quality both improve with volume) | Retargeting existing customers, exclusion lists, lookalike seed | Match rate depends on data hygiene — hashed email + phone + name together match better than email alone |
| Website/app activity (Pixel/CAPI) | Depends on event; needs enough volume to populate within the lookback window (1-180 days) | Retargeting cart abandoners, product viewers, past purchasers | Requires solid Pixel + CAPI coverage (see meta-ads-conversion-tracking) — thin tracking means a thin audience regardless of real traffic |
| Engagement (video views, IG/FB page interactions, lead form opens, Instant Experience opens) | Scales with organic + paid activity on the asset | Warming a cold audience that has shown interest but hasn't hit the site | Cheapest audience type to build since it requires no pixel; good early-funnel retargeting layer |

## Lookalike Audiences

Lookalikes model a new audience of people who resemble a source list, ranked by similarity.

| Similarity % | Reach | Match quality | When to use |
|---|---|---|---|
| 1% | Smallest, closest match to source | Highest resemblance to source | Highest-value source lists (top purchasers, high-LTV customers) where precision matters more than scale |
| 2-5% | Moderate | Good balance | Default starting point for most prospecting once a 1% has been tested |
| 6-10% | Largest | Loosest match | Scaling campaigns that have exhausted tighter lookalikes and need volume, accepting some efficiency loss |

**Source list quality determines lookalike quality more than similarity percentage does.** A 1% lookalike built from a poorly-defined source (e.g., "everyone who ever visited the site" instead of "purchasers in the last 90 days") will underperform a 5% lookalike built from a tightly-defined, high-value source. Always ask what the source list actually represents before troubleshooting the percentage.

**Refresh cadence:** lookalikes built from static customer file uploads should be refreshed every 60-90 days as the underlying customer base evolves; lookalikes built from a rolling pixel/CAPI event source (e.g., "purchasers, last 180 days") refresh automatically as new events flow in and generally don't need manual rebuilding.

## Advantage+ Audience

Meta's AI-driven targeting layer that starts from any input (interests, an existing custom audience, or nothing at all) and expands delivery to wherever the algorithm predicts results, deprioritizing manual targeting inputs over time in favor of signal-based expansion.

- Use when the account has strong conversion signal (established pixel/CAPI, decent weekly conversion volume) — Advantage+ Audience needs data to expand intelligently, and performs worst on brand-new pixels with thin history.
- Treat manual "audience suggestions" (interests, demographics) as a soft starting point, not a hard restriction — Meta will expand beyond them once it finds better-converting signal.
- Best paired with strong exclusions (existing customers, recent converters) since Advantage+ will otherwise happily serve to people already deep in the funnel.

## Audience Decay Considerations

Both custom audiences and lookalikes degrade over time as: the source list ages past its relevance (e.g., a 2-year-old customer list no longer reflects current buyer profile), the audience gets over-saturated (frequency climbs, response rates fall — see meta-ads-creative-fatigue for the creative side of this), or the account's own conversion mix shifts (e.g., a new product line means "past purchasers" no longer represents who you want to look like). Rebuild lookalike sources whenever the underlying business — product mix, price point, target customer — changes materially, not just on a fixed calendar.

## Common Mistakes

**Building a lookalike from a source list that mixes converters and non-converters** (e.g., "all website visitors" instead of "purchasers") — this dilutes the signal Meta is supposed to be modeling against.

**Assuming a smaller similarity percentage is always better.** 1% is only better when the source list itself is high-quality and high-value; on a mediocre source, a 1% lookalike just narrows into a small pool of mediocre matches.

**Never refreshing a static customer-file lookalike.** A lookalike built once at launch and never rebuilt slowly drifts away from the current customer base, especially in fast-growing or seasonal businesses.

**Layering heavy manual interest targeting on top of Advantage+ Audience** and expecting it to behave like classic detailed targeting — Advantage+ will still expand past those inputs, so tight manual layering mostly adds false confidence, not real restriction.

**Using engagement audiences (video viewers, page engagers) as a bottom-funnel retargeting pool** — these are early/mid-funnel signals, not purchase intent, and should be treated and messaged accordingly, not lumped in with pixel-based retargeting.

## Related Skills

- meta-ads-audience-targeting — for structuring targeting strategy and interest layering decisions across funnel stages
- meta-ads-exclusions — for excluding converters and existing customers from prospecting audiences
- meta-ads-audience-overlap — for checking whether multiple custom/lookalike audiences are competing against each other in the same auction
- meta-ads-conversion-tracking — for the pixel/CAPI data quality that determines custom audience and lookalike strength
- meta-ads-segmentation — for reading age/gender/placement breakdowns that inform audience refinement
