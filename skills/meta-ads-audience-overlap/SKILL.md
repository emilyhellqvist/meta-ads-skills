---
name: meta-ads-audience-overlap
description: "When the user suspects their Meta Ads ad sets are competing against each other, wants to check audience overlap, is seeing inflated CPMs across multiple campaigns, or is deciding whether to consolidate ad sets. Triggers on 'check audience overlap', 'my ad sets are competing against each other', 'CPMs are inflated', 'should I consolidate ad sets', 'Advantage+ audience exclusions', or 'is this the Meta equivalent of keyword cannibalization'. This is the direct Meta equivalent of Google Ads keyword cannibalization — the fix mechanics live in meta-ads-exclusions."
metadata:
  version: 1.0.0
---

# Meta Ads — Audience Overlap

You are diagnosing and fixing audience overlap — the direct Meta equivalent of keyword cannibalization in search. When two or more ad sets target audiences that share the same people, those ad sets enter the same auction against each other. Meta's delivery system then suppresses one ad set in favor of the other, inflating CPMs for both, fragmenting the learning phase, and wasting budget on an auction the advertiser is running against itself.

## Before Starting

Get: how many active ad sets/campaigns, whether audiences are reused across campaigns, whether this is a fresh audit or a response to a specific CPM/cost spike, and whether Advantage+ audience or Advantage+ Shopping is in use (overlap works differently and is harder to see directly there).

## Diagnosing Overlap

**The Audience Overlap tool** (found in Ads Manager under Audiences, or historically the Business Manager Custom Audiences tool) compares two saved or custom audiences and reports the percentage of shared membership.

| Overlap % | Read |
|---|---|
| Under 10% | Negligible — no action needed |
| 10–20% | Watch — monitor CPM trend, no urgent fix |
| 20–30% | Moderate — consolidate or exclude |
| Over 30% | Severe — fix immediately, actively wasting budget |

**Limitation:** the overlap tool only compares named/saved audiences directly. It doesn't show overlap between Advantage+ or broad targeting and other active audiences, since those aren't fixed audience definitions. For those, use proxy signals instead: rising frequency across multiple ad sets simultaneously, CPM climbing broadly (not just in one ad set) with no external market cause, or multiple ad sets showing diminishing delivery relative to budget at the same time. These patterns point to implicit self-competition even when the overlap tool has nothing to show.

## Calculating the Cost of Overlap

Compare the CPM of the suspected overlapping ad sets against a comparable, non-overlapping ad set in the same account (same objective, similar audience size, similar timeframe). The delta is a reasonable estimate of the CPM inflation overlap is causing — multiply by impression volume to translate into wasted spend.

| Ad Set | CPM | Comparable non-overlapping CPM | Estimated inflation |
|---|---|---|---|
| A | $ | $ | % |
| B | $ | $ | % |

## Fixing Overlap: Three Paths

1. **Exclusions.** Exclude one custom audience from the other ad set's targeting (e.g., exclude the retargeting audience from the prospecting ad set) so each ad set draws from a distinct pool.
2. **Consolidation.** Merge redundant, overlapping ad sets into fewer, broader ones. Meta's own delivery system rewards concentrated signal — fewer ad sets competing for the same conversions exit the learning phase faster and more stably than many fragmented, overlapping ones.
3. **Advantage+ audience with exclusions.** Let the algorithm find the audience broadly, but still layer in suppression — exclude existing customers, recent purchasers, or a competing campaign's converted audience — so Advantage+ isn't quietly competing against your own retargeting.

## When Overlap Is Actually Fine

- Sequential retargeting funnel stages (e.g., add-to-cart audience vs. purchaser audience) are supposed to have some membership overlap over time — that's the funnel working, not cannibalization, as long as exclusions prevent a person from being served two conflicting messages at once.
- Isolated test cells inside Meta's Experiments tool are deliberately non-overlapping by design (see meta-ads-experiments) — this is not the problem being diagnosed here.
- A deliberate, short-lived Lookalike ladder test (1%/2%/5%) run to compare performance, with the intent to consolidate afterward.

## Output Template
