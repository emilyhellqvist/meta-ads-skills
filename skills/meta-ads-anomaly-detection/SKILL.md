---
name: meta-ads-anomaly-detection
description: "When the user needs to diagnose a sudden performance drop or spike in a Meta Ads account — CPM jumped, ROAS collapsed, CTR fell off, cost per lead doubled overnight. Triggers on 'why did my CPM spike', 'ROAS dropped', 'CTR collapsed', 'performance dropped overnight', 'something's wrong with my account', 'costs went up suddenly', 'diagnose this drop', or 'set up alerts for anomalies'. For fixing the drop once diagnosed via automation see meta-ads-automated-rules; for tracking-layer root causes see meta-ads-attribution and meta-ads-conversion-tracking."
metadata:
  version: 1.0.0
---

# Meta Ads — Anomaly Detection

You are diagnosing a sudden performance shift in a Meta Ads account. The goal is a systematic, evidence-based root cause — not a guess — delivered fast enough to stop the bleeding. Work outside-in: rule out reporting artifacts first, then platform-side causes, then account-side causes, in that order, because account-side causes are the most common and the most fixable.

## Before Starting

Get: which metric moved, by how much, over what window, and compared to what baseline (day-over-day, week-over-week, or vs. a pre-set benchmark). Get the change history / edit log for the account. Confirm the reporting window isn't crossing a timezone or attribution-window boundary that would make the comparison invalid.

## Step 1: Confirm the Move Is Real

- Meta's reported conversion data can update for up to **7 days** after the fact as delayed attribution events land — a "drop" measured on data from the last 1–2 days is often partially a reporting-lag artifact, not a real performance change. Re-pull the same date range 3–5 days later before panicking.
- Check the account and reporting timezone match. A timezone mismatch alone can make a normal day look like a cliff.
- Check whether the attribution window setting itself changed (e.g., 7-day click moved to 1-day click) — this alone can cut reported conversions by more than half with zero change in actual performance.

## Step 2: Platform-Side Causes

| Cause | How to check | Typical signature |
|---|---|---|
| Auction competition increase (seasonality, new competitor) | Compare CPM trend across the whole ad account, not just one campaign | CPM up broadly, CTR flat |
| iOS/AEM attribution shift | Check Aggregated Event Measurement config, iOS share of audience | Reported conversions down, no real-world revenue change |
| Ad rejection / policy sweep | Check ad status and account quality in Business Manager | Sudden delivery drop, "in review" or "rejected" status |
| Platform outage or bug | Check Meta Business Help Center / status page | Broad, sudden, affects unrelated advertisers too |
| Broad/Advantage+ algorithm shift | Compare delivery mix across placements/audiences week over week | CPM or placement mix changes with no account edits |
| Creative fatigue via frequency | Check frequency trend on the affected ad set | CTR down, frequency up, CPM up |

## Step 3: Account-Side Causes

| Cause | How to check | Typical signature |
|---|---|---|
| Recent edit reset learning phase | Check change history for edits in the last 3–7 days | Volatile cost per result right after the edit |
| Budget change >~20% | Change history | CPA swings, delivery pacing changes |
| Audience edit (targeting, exclusion added/removed) | Change history | Reach/CPM shift, possible overlap introduced |
| Payment/account restriction | Account status in Billing | Delivery stopped entirely |
| New campaign self-competing | Check for newly launched campaigns targeting overlapping audiences | CPM up across multiple campaigns simultaneously |
| CAPI/pixel event firing broken | Events Manager diagnostics | Conversions reported drop but site analytics show orders still happening |
| Catalog feed error (ecommerce) | Commerce Manager diagnostics | Product ads stop delivering or show wrong price/availability |

## The Learning Phase Reset Trap

Any of the following resets an ad set's learning phase, causing 3–7 days of volatile, often worse, delivery: a budget change beyond roughly 20%, adding or removing an ad within the set, changing targeting, placement, or the optimization event, or pausing an ad set for an extended period and reactivating it. If the anomaly started 1–3 days after an edit, the edit is very likely the cause — investigate here before blaming the algorithm or the market.

## Proactive Monitoring Setup

- Set Automated Rules with notify-only conditions on CPA/ROAS/frequency thresholds so you get flagged before a slow drift becomes a crisis (see meta-ads-automated-rules).
- Review the change history log on a fixed weekly cadence, even when nothing looks wrong.
- Monitor Event Match Quality score in Events Manager weekly — a silent CAPI degradation shows up here before it shows up in ROAS.
- Track a rolling CPM/frequency trend line per active audience so creative fatigue and overlap-driven inflation are visible before they tank performance.

## Output Template

```
ANOMALY DIAGNOSTIC REPORT
Metric affected: [ ] Change: [ ] Window: [ ]
Confirmed real? [ ] (reporting lag / timezone / attribution window checked)
Platform-side findings: [ ]
Account-side findings: [ ]
Most likely root cause: [ ]
Recommended fix: [ ]
Expected recovery timeline: [ ]
```

## Common Mistakes

- Blaming "the algorithm" before checking the change history log.
- Reacting to a single bad day that's within normal attribution-lag variance.
- Not checking Events Manager / CAPI health before assuming a real demand-side drop.
- Making a panic edit to "fix" the problem, which resets the learning phase and compounds the volatility.
- Ignoring frequency creep as a slow, silent cause of CTR and CPM erosion.

## Related Skills

- meta-ads-automated-rules — setting up proactive alerts and safeguards
- meta-ads-attribution / meta-ads-conversion-tracking — ruling out tracking-layer causes
- meta-ads-creative-fatigue — diagnosing frequency-driven decay specifically
- meta-ads-budget-pacing — ruling out pacing-driven cost swings
- meta-ads-audience-overlap — diagnosing self-competition as a CPM driver
- meta-ads-account-audit — the broader health check this feeds into
