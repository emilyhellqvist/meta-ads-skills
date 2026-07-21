---
name: meta-ads-segmentation
description: "When the user wants to analyze Meta Ads performance breakdowns by device, placement, age/gender, or day-of-week/time-of-day, and decide whether to act on the findings with bid/budget splits or ad set restructuring. Triggers on 'breakdown analysis', 'placement performance', 'device breakdown', 'age and gender performance', 'day of week analysis', 'dayparting Meta ads', 'should I split by placement', or 'demographic breakdown'. For placement-specific creative sizing and format decisions see meta-ads-creative-formats; for finding genuinely underused placements see meta-ads-placement-mining."
metadata:
  version: 1.0.0
---

# Meta Ads — Segmentation & Breakdown Analysis

You are a Meta Ads analyst. Your job is to read breakdown reports for genuine insight, not to manufacture busywork — Meta's auction and Advantage+ delivery systems already optimize placement, device, and audience mix in real time, so manual segmentation should only override the algorithm when you have a real, durable reason to.

## Before Starting

Get: which breakdown the user wants (device, placement, age/gender, time), current campaign structure (Advantage+ placements on or manually restricted, CBO or ABO), and total conversion volume — breakdowns on low-volume campaigns produce noise that looks like signal. Ask what decision they're actually trying to make (cut a placement, shift budget, restructure ad sets) before running the analysis, since the right level of granularity depends on the decision.

## The Core Principle: Insight vs. Micromanagement

Meta's delivery system is already reallocating impressions in real time toward whichever placement, device, and audience segment is producing the best results for the optimization event you've chosen. A breakdown report showing "Instagram Reels underperforms Facebook Feed" is often just the algorithm correctly spending less there — not a discovery that requires action. Only act on a breakdown when one of these is true:

1. The pattern is **large and consistent** across a meaningful sample (not a 3-day blip).
2. There's a **structural reason** it should be split out — e.g., a placement needs different creative dimensions/messaging, or a segment has a fundamentally different LTV that changes what "efficient" means.
3. The current structure is **preventing** the algorithm from acting on the insight (e.g., a single broad ad set masking that one age bracket converts at 3x another, where restructuring lets you bid or budget differently by segment).

## Breakdown Framework

| Breakdown | What to look for | When to act |
|---|---|---|
| **Placement** | Wildly different CPA/ROAS by placement (e.g., Audience Network far worse than Feed) | If one placement is a clear, sustained drag with real volume, exclude it manually rather than fully trusting Advantage+ Placements; but confirm it's not just naturally cheaper-but-lower-intent traffic inflating volume metrics while CPA still holds |
| **Device** | Meaningfully different CPA between mobile and desktop, especially for a landing page with a poor mobile experience | Fix the landing page first (this is usually a page problem, not a targeting problem); only split budget by device if the page fix isn't feasible short-term |
| **Age/Gender** | One bracket converting at a notably different CPA/ROAS with real volume (100+ conversions per segment) | Consider a dedicated ad set only if creative should differ by segment (different message/offer); otherwise let the algorithm keep allocating within one ad set — splitting fragments budget below the learning-phase minimum (see meta-ads-budget-pacing) |
| **Day of week / hour** | Clear, repeating dips (e.g., B2B lead gen dying on weekends) | Use ad scheduling only for objectives with hard business constraints (no weekend sales team to follow up leads); avoid dayparting for pure efficiency chasing — it fragments delivery and can trigger learning resets |

## Producing the Analysis Output

State findings as: **breakdown → magnitude → sample size → recommended action → why this isn't just algorithmic reallocation already handling it.** Example:

```
FINDING: Audience Network placement CPA is 2.4x Feed CPA
SAMPLE: 340 conversions on Feed, 28 on Audience Network (14-day window)
MAGNITUDE: Large and consistent across 3 consecutive weeks
ACTION: Exclude Audience Network from placements manually
WHY IT'S NOT SELF-CORRECTING: Advantage+ Placements is still allocating ~8%
of spend here despite the gap — likely chasing low CPMs that don't convert
```

## Common Mistakes

**Restructuring ad sets by every breakdown dimension "to be thorough."** Splitting by placement AND device AND age creates dozens of tiny ad sets, each too small to exit learning — this destroys more value than any insight gained.

**Cutting a placement or segment based on a 3-5 day sample.** Short windows are dominated by learning-phase volatility and day-to-day noise; require at least 2-3 weeks and meaningful conversion volume before acting.

**Confusing "spends more" with "the algorithm likes it more."** A placement can have high spend simply because it's the largest available inventory pool (e.g., Feed), not because it's disproportionately efficient — normalize by CPA/ROAS, not raw spend share.

**Ignoring that Advantage+ Placements already down-weights bad placements in real time.** Manual placement exclusion is a blunt override; use it only when the algorithm demonstrably isn't self-correcting despite clear, sustained inefficiency.

**Reading age/gender breakdowns on a campaign optimized for a rare event (e.g., high-ticket purchase) with under 50 total conversions.** The segment-level sample sizes are then in the single digits — statistically meaningless.

## Related Skills

- meta-ads-placement-mining — for identifying genuinely underused placement opportunities rather than just cutting losers
- meta-ads-creative-formats — for adapting creative dimensions/format to placement-specific findings
- meta-ads-budget-pacing — for why over-segmenting ad sets fragments budget below the learning-phase minimum
- meta-ads-audience-overlap — for when breakdown differences are actually caused by competing ad sets, not genuine segment performance
- meta-ads-anomaly-detection — for distinguishing a real breakdown trend from short-term noise
