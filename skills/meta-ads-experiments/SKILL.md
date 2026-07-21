---
name: meta-ads-experiments
description: "When the user wants to A/B test something in Meta Ads, run a controlled experiment, compare creative or audience or placement performance, or decide whether a result is statistically real. Triggers on 'A/B test', 'split test', 'run an experiment', 'test creative vs creative', 'which audience performs better', 'test placements', 'statistical significance', 'how long should I run this test', 'is this result real or noise', or 'Meta Experiments tool'. For diagnosing why performance moved outside a controlled test see meta-ads-anomaly-detection; for the underlying audience mechanics being tested see meta-ads-audience-targeting and meta-ads-audience-overlap."
metadata:
  version: 1.0.0
---

# Meta Ads — Experiments (A/B Testing)

You are running controlled tests inside a Meta Ads account. Your job is to isolate one variable, hold everything else constant, and produce a defensible answer — not a hunch dressed up as a result. Meta's built-in Experiments tool (formerly "Split Testing") exists specifically to solve the problem that duplicating ad sets manually creates: overlapping audiences that compete against each other in the same auction and invalidate the comparison.

## Before Starting

Confirm: what decision does this test inform (creative direction, audience strategy, budget allocation)? What's the one variable changing? What's the primary metric (must be chosen at setup — it cannot be changed retroactively once the test is reading results)? What budget and timeframe are available? Is this test even necessary, or is the answer already obvious from existing data?

## Why the Experiments Tool, Not Manual Duplication

If you duplicate an ad set to test Variant B against Variant A, both ad sets draw from the same audience pool and enter the same auction — they compete against each other, inflate each other's CPMs, and Meta's delivery system may favor one arbitrarily based on early signal, contaminating the result. The Experiments tool instead performs a **population split**: it randomly and permanently assigns each person in the eligible audience to exactly one test cell before the campaign runs, so no user ever sees ads from more than one cell. This is the only setup inside Meta where a true head-to-head comparison is possible without audience overlap distorting it.

## What to Test

| Variable | What it tells you | Notes |
|---|---|---|
| Creative | Highest-leverage lever in the account | Test concept/hook, not just color swaps |
| Audience | Core vs. Lookalike vs. Custom vs. Advantage+ | Biggest structural decision, slow to read |
| Placement | Advantage+ placements vs. manual placement set | Watch CPM differences by surface |
| Delivery optimization | Optimization event (e.g., landing page view vs. purchase) | Needs conversion volume to read cleanly |
| Bid strategy | Lowest cost vs. Cost cap vs. Bid cap vs. ROAS goal | Test cost control tolerance, not raw cost |

Test **one variable per experiment**. Multivariate changes (new creative *and* new audience in the same cell) make it impossible to attribute the result to a cause, which defeats the purpose of using the tool at all.

## Sizing the Test: Duration and Budget

- Minimum runtime is 4 days; Meta caps experiments at 30 days. In practice, run 7–14 days minimum to absorb day-of-week variance (B2B and B2C both show weekday/weekend swings in CPM and CVR).
- Rule of thumb for statistical usefulness: aim for at least **50–100 conversions per cell** before trusting a CPA/ROAS-based read. Below that, treat results as directional only.
- Budget the test using: `budget per cell ≈ (target conversions per cell ÷ expected conversion rate) × expected CPA`, then multiply by the number of cells. Under-resourcing a test is the single most common reason experiments come back "inconclusive."
- If the primary metric is upper-funnel (CTR, hook rate, engagement), you can call results with less spend since sample sizes are impression/click-based, not conversion-based.

## Reading the Results Panel

- Meta's panel shows a confidence percentage on your chosen primary metric. Meta's own UI may flag a "winner" at a lower threshold than you should act on — treat anything under 90% confidence as *lean*, not *decided*, unless the gap is enormous and the loser is clearly broken.
- The confidence score is tied to the single primary metric selected at launch. A creative that "wins" on CTR but loses on ROAS is not a clean win — check secondary metrics before declaring victory.
- Don't call a test early because one cell looks good on day 2–3. Early spend often reflects auction noise and initial delivery skew, not a stable signal.

## Output Template

```
EXPERIMENT BRIEF
Hypothesis: [what we expect and why]
Variable tested: [creative | audience | placement | optimization | bid strategy]
Cells: [A vs B vs ...]
Budget / Duration: [$ per cell, days]
Primary metric: [metric + target]
Result: [winner, confidence %, secondary metric check]
Decision: [scale / kill / retest]
Next test: [follow-up hypothesis]
```

## Common Mistakes

- **Manually duplicating ad sets instead of using the Experiments tool** — audience overlap poisons the comparison before it starts.
- **Testing multiple variables at once** — you get a result with no attributable cause.
- **Calling a winner during the learning phase** — early volatility isn't signal.
- **Underpowered budget** — ending a test with 8 conversions per cell and treating the outcome as fact.
- **Generalizing a result learned during a seasonal spike** (e.g., Black Friday) to normal-period strategy.

## Related Skills

- meta-ads-audience-overlap — why manual ad set duplication produces invalid test results
- meta-ads-audience-targeting / meta-ads-audiences — the targeting options being tested
- meta-ads-creative-fatigue — distinguishing a real creative winner from one that just hasn't fatigued yet
- meta-ads-bidding — testing bid strategies specifically
- meta-ads-anomaly-detection — diagnosing performance shifts that happen *outside* a controlled test
- meta-ads-account-audit — where experiment findings should feed into broader account strategy
